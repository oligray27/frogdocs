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
| `completionActivity` | Games completed per month (`type: "monthly"`, with `year`) or per year (`type: "yearly"`). Each entry: `{ label, count, titles }`. |
| `lsStats` | The same kind of figures for live service games, plus `sessionActivity` and `sessionHeatmap` |
| `combinedStats` | Totals and top lists for games and live service together |

Each top-list entry looks like:

```json
{ "id": 1, "title": "PC (Steam)", "count": 128, "status": "128 Games (54%)", "hours": 2310 }
```

Sessions over 24 hours are left out of the day-based figures (`sessionHeatmap`, `thisMonth`, `thisYear`) but included in totals. See [how hours are counted](/stats).

## Someone else's stats

`GET /users/:username/stats` takes the same `year` and `lsYear` queries and returns the same shape, counting only their public games and sessions.
