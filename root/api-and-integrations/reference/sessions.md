---
leafwiki_id: fl-api-ref-sessions
leafwiki_title: Sessions & Quick Session
leafwiki_created_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_updated_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# Sessions & Quick Session

Endpoints for listing all your sessions at once, and for running a [Quick Session](/library/sessions): a timer that FrogLog keeps on its side, so you can start and stop it from anywhere. They're handy for Stream Deck buttons, phone shortcuts or your own tracker.

To add, change or delete a single session, use the game's own endpoints in [Games](/api-and-integrations/reference/games) or [Live Service](/api-and-integrations/reference/live-service).

## All sessions

### GET /sessions/games

Every session across your regular games, newest first, a page at a time.

| Query | Default | Notes |
|---|---|---|
| `page` | `1` | |
| `limit` | `20` | Up to 100 |

```json
{
  "sessions": [
    {
      "id": 501, "date": "2026-10-01", "hours": "2.5", "notes": null, "is_public": true, "spoiler": false,
      "game_id": 12, "title": "Hades II", "img": "https://…", "status": "", "dnf": false,
      "start_date": "2026-09-24", "end_date": null
    }
  ],
  "total": 214,
  "page": 1,
  "totalPages": 11
}
```

### GET /sessions/live-service

The same for your live service games.

## Quick Session

### The active session object

| Field | Notes |
|---|---|
| `game_type` | `"game"` or `"live_service"` |
| `game_id` | |
| `title` | |
| `session_tracking` | Whether the game logs sessions (otherwise the time is added to its hours) |
| `started_at` | Timestamp |
| `source` | What started it, for example `"manual"` for a Quick Session, or a platform for automatic tracking |

### GET /live-session/active

Your running session, or `{ "active": null }`.

```json
{ "active": { "game_type": "game", "game_id": 12, "title": "Hades II", "session_tracking": true, "started_at": "2026-10-02T18:00:00.000Z", "source": "manual" } }
```

### GET /live-session/last-played

The game you played most recently, as `{ "game": { "game_type", "game_id", "title" } }`, or `{ "game": null }`. Useful for a one-tap "carry on where I left off" button.

### POST /live-session/start

```json
{ "game_type": "game", "game_id": 12 }
```

Starts a session and returns `201` with `{ "active": {...} }`.

- `409` with `{ "error": "A session is already active", "active": {...} }` if one is already running. Only one can run at a time.
- `404` if the game isn't yours.

```bash
curl -X POST https://api.froglog.co.uk/api/live-session/start \
  -H "Authorization: Bearer flk_your_key_here" \
  -H "Content-Type: application/json" \
  -d '{"game_type": "game", "game_id": 12}'
```

### POST /live-session/submit

Stops the running session and saves it. All fields are optional:

| Field | Notes |
|---|---|
| `notes` | |
| `spoiler` | Default `false` |
| `is_public` | Default `true` |
| `stopped_at` | Timestamp to stop at, if not now |

```json
{ "hours": 1.25, "game_type": "game", "game_id": 12, "title": "Hades II", "session": { "id": 502, "...": "..." } }
```

If the game doesn't log sessions, the hours are added to its `hours_played` instead. `404` if nothing is running.

### DELETE /live-session/active

Stops the running session without saving it. Returns `{ "success": true }`, or `404` if nothing is running.
