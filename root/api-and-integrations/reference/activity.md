---
leafwiki_id: fl-api-ref-activity
---
# Activity

The data behind the [Activity](/social/activity) page. Everything covers you and the people you follow, respecting their privacy settings.

## GET /activity

The activity feed, newest first.

| Query | Default | Notes |
|---|---|---|
| `page` | `1` | |
| `limit` | `30` | Up to 100 |
| `usernames` | all | Comma-separated usernames to include |
| `types` | all | Comma-separated activity types to include (see below) |

Activity types: `game_started`, `game_completed`, `game_dnf`, `review_added`, `session_logged`, `wishlist_added`, `list_created`.

```json
{
  "activity": [
    {
      "id": 9012,
      "type": "session_logged",
      "game_type": "game",
      "game_id": 12,
      "game_title": "Hades II",
      "parent_title": null,
      "session_id": 501,
      "session_hours": "2.5",
      "created_at": "2026-10-01T21:14:00.000Z",
      "username": "alex",
      "display_username": "Alex",
      "nickname": null,
      "avatar_url": "/uploads/avatars/…",
      "like_count": 2,
      "liked_by_me": false
    }
  ],
  "total": 340,
  "page": 1,
  "totalPages": 12
}
```

`nickname` is the nickname you've given that person, if any. `avatar_url` is a path on `https://api.froglog.co.uk`.

## GET /activity/online

Online Now: the people you follow, and who's playing what.

```json
[
  { "username": "alex", "displayUsername": "Alex", "avatarUrl": null, "online": true, "title": "Balatro", "platform": "steam", "lastSeenAt": null },
  { "username": "sam", "displayUsername": "Sam", "avatarUrl": null, "online": false, "title": null, "platform": null, "lastSeenAt": "2026-10-01T22:40:00.000Z" }
]
```

## GET /activity/trending

New From Friends: up to 9 games the people you follow have started or played in the last 7 days.

```json
[
  { "title": "Hades II", "img": "https://…", "playerCount": 2, "players": [{ "username": "alex", "displayUsername": "Alex", "avatarUrl": null }] }
]
```

## GET /activity/highlights

The Highlights leaderboards and totals for the last 7 days, the last 30 days and all time. The response is an object with one entry per tile. Field names follow the tiles described in [Activity](/social/activity).
