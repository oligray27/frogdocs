---
leafwiki_id: fl-api-ref-stats
leafwiki_title: Stats
leafwiki_created_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_updated_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# Stats

The numbers behind your [Stats](/stats) page.

## GET /stats

| Query | Notes |
|---|---|
| `year` | Optional. Limits the games stats to one year. |
| `lsYear` | Optional. Limits the live service stats to one year. |

The response is large. The main parts:

| Field | Contains |
|---|---|
| `totalGames`, `completed`, `completionRate` | Games started and finished |
| `totalHours` | Hours across your games |
| `avgRating`, `ratedCount` | Average rating (0–100) and how many games are rated |
| `statusCounts` | `{ completed, inProgress, dnf, dormant, notStarted }` |
| `topPlatforms`, `topDevelopers`, `topCountries`, `topGenres`, `topTags` | Top lists (see below). `topTags` counts each game under its top ten descriptive Steam tags, up to 100 tags. |
| `availableYears` | Years you can pass as `year` |
| `thisMonth`, `thisYear` | `{ total, completed, hours }` for games started recently. Only without `year`. |
| `sessionHeatmap` | One entry per day with play: `{ day, hours, sessions }` |
| `weekSummary` | The Last 7 Days summary (see below). Ignores `year`. |
| `weekLeaderboard` | Hours in the last 7 days for you and who you follow (see below). Ignores `year`. |
| `completionActivity` | Games completed per month (`type: "monthly"`, with `year`) or per year (`type: "yearly"`). Each entry: `{ label, count, titles }`. |
| `lsStats` | The same kind of figures for live service games, plus `sessionActivity`, `sessionHeatmap` and `weekSummary` |
| `combinedStats` | Totals, top lists and `weekSummary` for games and live service together |

Each top-list entry looks like:

```json
{ "id": 1, "title": "PC (Steam)", "count": 128, "status": "128 Games (54%)", "hours": 2310 }
```

`weekSummary` covers today and the six days before, compared with the seven days before that:

```json
{
  "days": [{ "day": "2026-10-03", "hours": 2.5, "sessions": 1, "games": { "game-412": 2.5 } }],
  "hours": 14.5, "prevHours": 11,
  "sessions": 9, "prevSessions": 7,
  "gamesPlayed": 3, "daysPlayed": 5, "longestSession": 4,
  "topGame": { "title": "Hades II", "type": "game", "hours": 8.5 },
  "games": [{ "key": "game-412", "id": 412, "type": "game", "title": "Hades II", "cover": "https://…", "hours": 8.5, "sessions": 4, "lastPlayed": "2026-10-08" }]
}
```

`days` always has seven entries, oldest first; each day's `games` gives the hours per game, keyed by the game's `key`. `games` lists every game played in those seven days, most hours first (`type` is `game` or `ls`). `topGame` is `null` if nothing was played.

`weekLeaderboard` ranks you and the people you follow by hours in the last 7 days, the same figure as the [weekly crown](/social):

```json
{
  "followsAnyone": true,
  "entries": [{ "username": "frogfan", "label": "frogfan", "avatarUrl": "/uploads/…", "hours": 21.5, "isYou": false, "crown": true }]
}
```

Sessions over 24 hours are left out of the day-based figures (`sessionHeatmap`, `weekSummary`, `thisMonth`, `thisYear`) but included in totals. See [how hours are counted](/stats).

## GET /stats/year-in-review

The years of your [Year in Review](/stats/year-in-review) you can open, newest first: `{ "years": [2026, 2025, 2024] }`. Each year opens once FrogLog releases it, usually on 1 January after it, and 2024 and 2025 come out with 2026.

## GET /stats/year-in-review/:year

Your Year in Review for one year. A year answers `403` with `{ "error": "…", "unlocks_at": "2027-01-01" }` until it's released (`unlocks_at` is when it's expected), and `404` if it's before 2024 or hasn't begun.

| Field | Contains |
|---|---|
| `year`, `shared` | The year, and whether you've shared it |
| `has_previous_year` | Whether you had an account before that year (when the "than last year" comparisons apply) |
| `summary` | `{ played, previous_played, new_games, hours, sessions, active_days, completed }` |
| `trophies` | `{ unlocked, previous, games, has_platforms, best_month }`: achievements unlocked that year and the year before, across how many games, and the busiest month (`{ month, count }`, or `null`) |
| `tracking` | One entry per source, most sessions first: `{ source, sessions, hours, share }`. `source` is one of the session `source` values (see [Games](/api-and-integrations/reference/games)), or `other` |
| `top_games` | Your five most played games by hours (see below) |
| `platforms` | One entry per platform label, most hours first: `{ name, label, hours, share, games, sessions, top_games }`. `name` is the stored label (`Steam`, `PSN`, `PC (Non-Steam)`, `Unknown`…), `label` how it reads. `top_games` are its five most played, each with `share` of that platform's hours |
| `months` | Twelve entries: `{ month, hours, games }`, where `games` gives the hours of each top game played that month, keyed by its `key` |
| `release_mix` | `{ new, recent, classic, unknown }`: games released that year, in the five years before, earlier, or with no date |
| `release_hours` | The same groups, as hours played |
| `tags` | `{ axes, coverage }`: up to six Steam tags `{ id, name, hours }`, and the share of your hours they cover |
| `genres` | `{ axes }`: up to six genres `{ name, hours }`, most hours first |
| `streak` | Your longest run of days in a row with a session: `{ days, from, to, timeline, games }`, or `null` |
| `games` | Every game you played that year, most hours first: `{ key, id, type, title, parent_title, img, cover_image, igdb_id, hours, share, new_this_year, completed, private }` (`parent_title` is the main game of a DLC or expansion, or `null`) |
| `community` | How you compare: `{ users, games_played, streak, trophies }`, each `{ you, median, max, percentile, users }`, where `percentile` is the share of the other players with a lower figure (so the top player is 100) (`trophies` is `null` without a linked account). `null` when fewer than 10 people logged a session that year. |

Each `top_games` entry has the `games` fields plus `rank`, `sessions`, `months` (hours in each month), `streak_days`, `first_played`, `playing_since`, `status`, `end_date`, `replay` and `achievements`: `{ unlocked, items }`, with up to 60 `{ platform, name, icon, unlocktime }`, newest first.

Shares are percentages of the year's hours. Only dated sessions of up to 24 hours count towards hours.

## PUT /stats/year-in-review/:year/share

Shares or stops sharing your Year in Review for that year. Send `{ "shared": true }` or `{ "shared": false }`. Returns `{ year, shared }`.

## Someone else's Year in Review

`GET /users/:username/year-in-review` returns `{ "years": [2026] }`: the years they've shared that have unlocked, newest first.

`GET /users/:username/year-in-review/:year` returns a shared Year in Review in the same shape, without `shared`, plus `hidden_games`. Their private games count in every total, share and chart, but are left out of each platform's `top_games`, `top_games` (the rest are renumbered), each month's `games`, `games` (`hidden_games` says how many) and `streak`, where they're one entry with the `key` `private`. It answers `404` unless they've shared that year and you can see their profile and when they play.

## Someone else's stats

`GET /users/:username/stats` takes the same `year` and `lsYear` queries and returns the same shape, counting only their public games and sessions. `weekSummary` is left out if they've made you unable to see when they play, and `weekLeaderboard` is never included.
