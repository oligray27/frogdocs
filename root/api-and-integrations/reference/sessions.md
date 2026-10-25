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

## Tags in notes

Session notes can tag people with `@`. Send a tag as the name you see for that person (their username, or the display name or nickname you see), and FrogLog stores it so it keeps pointing at them. Wherever notes come back, each tag shows as the name that you know the person by, and every session object also has:

| Field | Notes |
|---|---|
| `mentions` | `[{ "label": "Reayon", "username": "reayon" }]`, one per person tagged, where `label` is how the tag reads in `notes` |
| `tagged_me` | `true` if you're one of the people tagged |

## Mirroring a session you're tagged in

Copies someone else's session that tags you into your own FrogLog. `:type` is the session's kind, `game` or `live_service`, and `:id` is its ID. Both endpoints return `404` if you can't see the session or aren't tagged in it.

A session and every copy made from it count as one session for this. You can't mirror one if the original is yours, or if you've already mirrored any copy of it: the GET returns `404` and the POST `409`.

### GET /sessions/mirror/:type/:id

What mirroring would do:

```json
{
  "target": { "game_type": "game", "game_id": 12, "title": "Hades II", "session_tracking": true },
  "library": [{ "game_type": "game", "game_id": 12, "title": "Hades II", "session_tracking": true }],
  "title": "Hades II",
  "prefill": { "date": "2026-10-01", "hours": "2.5", "notes": "Played with @Ollie", "spoiler": false }
}
```

`target` is the game in your library it goes on by default, or `null` if you don't have that game, in which case it's added to your library first. `library` lists all your games, regular and live service, for choosing a different one.

### POST /sessions/mirror/:type/:id

| Field | Notes |
|---|---|
| `date` | |
| `hours` | Required if the target game doesn't track sessions |
| `notes` | |
| `spoiler` | Default `false` |
| `is_public` | Default `true` |
| `target` | Optional. `{ "game_type", "game_id" }` for one of your games, or `"new"` to add the game as a new entry. Left out, it goes on the default `target` from the GET. `400` if the game isn't yours. |


A regular target game ends up In Progress: one you haven't started yet (no start date) starts on the session's `date`, and a completed or DNF one is reopened (its end date and DNF flag are cleared).

Returns where it went: `{ "game_type", "game_id", "title", "session_id", "created_game" }`. If the target game doesn't track sessions, the hours are added to its `hours_played` and `session_id` is `null`. `409` if you've already mirrored that session.

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
| `paused_at` | Timestamp the session was paused, or `null` while it's running |
| `paused_seconds` | Total time spent in earlier pauses, in seconds. Paused time isn't counted in the hours that are saved. |

### GET /live-session/active

Your running session, or `{ "active": null }`.

```json
{ "active": { "game_type": "game", "game_id": 12, "title": "Hades II", "session_tracking": true, "started_at": "2026-10-02T18:00:00.000Z", "source": "manual", "paused_at": null, "paused_seconds": 0 } }
```

### GET /live-session/last-played

The game you played most recently, as `{ "game": { "game_type", "game_id", "title" } }`, or `{ "game": null }`. Useful for a one-tap "carry on where I left off" button.

### POST /live-session/start

```json
{ "game_type": "game", "game_id": 12 }
```

| Field | Notes |
|---|---|
| `game_type` | `"game"` or `"live_service"` |
| `game_id` | |
| `started_at` | Optional. Timestamp the session began, if earlier than now. A time in the future counts as now. |
| `notify_followers` | Optional, default `true`. `false` skips telling your followers you've started playing, for a session you're logging after the fact. |

Starts a session and returns `201` with `{ "active": {...} }`.

- `409` with `{ "error": "A session is already active", "active": {...} }` if one is already running. Only one can run at a time.
- `404` if the game isn't yours.

```bash
curl -X POST https://api.froglog.co.uk/api/live-session/start \
  -H "Authorization: Bearer flk_your_key_here" \
  -H "Content-Type: application/json" \
  -d '{"game_type": "game", "game_id": 12}'
```

### POST /live-session/pause

Pauses the running Quick Session. The timer stops, the paused time isn't counted in the hours that are saved, and you don't show as playing in Online Now until you resume. Returns `{ "active": {...} }`, with `paused_at` set.

The body is optional:

| Field | Notes |
|---|---|
| `at` | Timestamp the pause happened, if not now. It can't be earlier than the session's start or later than now. |

- Pausing a session that's already paused changes nothing and returns it as it is.
- `404` if nothing is running.
- `409` with `{ "error": "Only Quick Sessions can be paused", "active": {...} }` if the running session came from automatic tracking.

### POST /live-session/resume

Resumes a paused Quick Session. The time spent paused is added to `paused_seconds` and `paused_at` goes back to `null`. Takes the same optional `at` field (it can't be earlier than the pause), and returns and fails the same way as `/pause`. Resuming a session that isn't paused changes nothing.

### POST /live-session/submit

Stops the running session and saves it. All fields are optional:

| Field | Notes |
|---|---|
| `notes` | |
| `spoiler` | Default `false` |
| `is_public` | Default `true` |
| `stopped_at` | Timestamp to stop at, if not now. It can't be earlier than the session's start or later than now. |

```json
{ "hours": 1.25, "game_type": "game", "game_id": 12, "title": "Hades II", "session": { "id": 502, "...": "..." } }
```

`hours` runs from `started_at` to the stop time, minus any time spent paused. A session that's still paused when you submit it ends when it was paused. The saved session is dated by the day it stopped, and shows in followers' Activity feed from the time it stopped.

If the game doesn't log sessions, the hours are added to its `hours_played` instead. `404` if nothing is running.

### DELETE /live-session/active

Stops the running session without saving it. Returns `{ "success": true }`, or `404` if nothing is running.
