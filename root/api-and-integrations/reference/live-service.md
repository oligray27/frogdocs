---
leafwiki_id: fl-api-ref-live-service
leafwiki_title: Live Service
leafwiki_created_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_updated_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# Live Service

Your [live service games](/library/live-service-games). These work like [Games](/api-and-integrations/reference/games), with a few differences:

- They have no end date, DNF, replay or status override. Hours always come from sessions.
- Their status is `"active"` or `"dormant"`, set with `live_service_status`.
- You can only have one live service game with each title.

## The live service game object

The same as the [game object](/api-and-integrations/reference/games), without `end_date`, `hours_played`, `dnf`, `status_override`, `session_tracking`, `no_achievements` and the replay fields, plus:

| Field | Notes |
|---|---|
| `status` | `"active"` or `"dormant"` |
| `start_date` | When you started playing |

`GET /live-service` also includes `platform_links`, `total_hours`, `session_count`, `last_session_date`, `last_session_logged_at` (when the most recent session was logged, as a full timestamp), the like fields and `screenshot_count`.

---

## GET /live-service

Lists your live service games, most recently played first.

## POST /live-service

Adds a live service game. Send the same fields as for a game, plus `live_service_status` (`"active"` or `"dormant"`, default `"active"`). `409` if you already have a live service game with that title.

## PUT /live-service/:id

Updates a live service game. **Replaces the whole game**, like `PUT /games/:id`: send every field, not just the ones you're changing.

## DELETE /live-service/:id

Deletes the game and its sessions. Returns `{ "success": true }`.

## POST /live-service/bulk-move-to-games

```json
{ "ids": [3, 7] }
```

Moves live service games into your regular games, keeping their sessions (with session tracking on) and screenshots. Returns `{ "moved": [...], "skipped": [...] }`. Games are skipped if you already have a regular game with the same title.

## Sessions

Session objects and fields are the same as for [games](/api-and-integrations/reference/games).

| Endpoint | Does |
|---|---|
| `GET /live-service/:id/sessions` | Lists the game's sessions, newest first |
| `POST /live-service/:id/sessions` | Logs a session: `date`, `hours`, `notes`, `is_public`, `spoiler`, `sync_ref` |
| `PUT /live-service/:id/sessions/:sessionId` | Replaces a session's `date`, `hours`, `notes`, `is_public` and `spoiler` |
| `DELETE /live-service/:id/sessions/:sessionId` | Deletes a session |

## Platforms

`POST /live-service/:id/platform-links` and `DELETE /live-service/:id/platform-links/:linkId` work the same as for [games](/api-and-integrations/reference/games).

## Trophies

`GET /live-service/:id/achievements` returns the game's trophies. See [Trophies](/api-and-integrations/reference/trophies).
