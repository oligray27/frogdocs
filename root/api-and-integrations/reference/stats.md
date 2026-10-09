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
| `topPlatforms`, `topDevelopers`, `topCountries`, `topGenres` | Top lists (see below) |
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

## Someone else's stats

`GET /users/:username/stats` takes the same `year` and `lsYear` queries and returns the same shape, counting only their public games and sessions. `weekSummary` is left out if they've made you unable to see when they play, and `weekLeaderboard` is never included.
