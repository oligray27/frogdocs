---
leafwiki_id: fl-api-ref-users
leafwiki_title: Users
leafwiki_created_at: "2026-10-02T11:47:34.852622128Z"
leafwiki_updated_at: "2026-10-02T11:47:34.852622128Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# Users

Your own account, other people's profiles, following, and your presence.

Everything about other people respects their privacy: private games, sessions and lists are never returned, and someone who has made themselves invisible to you looks like they don't exist (`404`).

## Your account

### GET /users/me

Your account and all your settings, in one object. Includes `id`, `username`, `created_at`, `avatar_url`, your linked platform names, and every setting (as `snake_case` fields like `rating_mode`, `merged_view` and `default_sort_games`).

### PUT /users/bio

```json
{ "bio": "Mostly RPGs." }
```

### PUT /users/top-games

Sets your favourite games (up to 4; extra ones are dropped). Returns `{ "top_games": [...] }`.

```json
{ "top_games": [{ "title": "Hades", "img": "https://…", "igdb_id": 26193 }] }
```

Most other settings have their own endpoints, which aren't covered here. Change them in **Profile > Settings**.

## Presence

Tell FrogLog what you're playing from your own tracker, so you show in Online Now. This is what LilyPad uses.

### PUT /users/me/now-playing

```json
{ "game_id": 12, "game_type": "game", "title": "Hades II", "started_at": "2026-10-02T18:00:00Z", "platform": "my-tracker" }
```

| Field | Notes |
|---|---|
| `game_id`, `game_type` | Required. `game_type` is `"game"` or `"live_service"`. |
| `title` | Shown to others |
| `started_at` | When the session began, shown in Online Now as how long you've been playing. If you leave it out, it's kept from your previous heartbeat for the same game, or set to now for a new one. |
| `platform` | A short name for your tracker: lowercase letters, numbers, `-` and `_`, up to 32 characters. `steam`, `psn`, `xbox`, `switch` and `quicksession` are reserved. Anything invalid is shown as `lilypad`. |

**Send it again at least every few minutes while playing.** Presence that hasn't been updated for 12 minutes is treated as stale and hidden.

**Stop sending it when the session ends.** A heartbeat is ignored, with `{ "success": true, "ignored": "…" }` sent back, when:

- you've already logged a session for that game with a `sync_ref` since `started_at` (`session_already_logged`). Your presence is cleared.
- its `started_at` is more than 12 hours ago (`session_too_old`). Your presence goes stale as above.

This only sets presence. It doesn't log a session. To log one, use [Quick Session](/api-and-integrations/reference/sessions) or post a session yourself.

### DELETE /users/me/now-playing

Clears your presence, unless a Quick Session or automatic tracking session is running.

## Other people

| Endpoint | Returns |
|---|---|
| `GET /users` | Everyone you can see, with `username`, `display_username`, `avatar_url`, `game_count`, `total_hours`, `ls_game_count`, `ls_total_hours`, `hours_last_7_days`, `latest_game`, `now_playing` and `last_seen_at` |
| `GET /users/:username` | Their profile: `bio`, `top_games`, `display_username`, `following_count`, `follower_count`, `like_count`, `public_list_count`, `now_playing`, `last_seen_at`, and their profile card's look |
| `GET /users/:username/games` | Their public games |
| `GET /users/:username/games/:id/sessions` | A game's public sessions |
| `GET /users/:username/live-service` | Their public live service games |
| `GET /users/:username/live-service/:id/sessions` | A live service game's public sessions |
| `GET /users/:username/stats` | Their [stats](/api-and-integrations/reference/stats) |
| `GET /users/:username/lists` | Their public lists |
| `GET /users/:username/lists/:id` | One public list, with `members` |

If someone has hidden their online status and sessions from you, their session fields come back empty.

## Following

| Endpoint | Does |
|---|---|
| `GET /users/me/following` | The people you follow |
| `PUT /users/me/following/:username` | Follow someone. They get a notification. |
| `DELETE /users/me/following/:username` | Unfollow |

## Nicknames, hiding and invisibility

| Endpoint | Does |
|---|---|
| `GET /users/me/nicknames` | Nicknames you've set: `[{ target_username, nickname }]` |
| `PUT /users/me/nicknames/:username` | Set a nickname: `{ "nickname": "Al" }` |
| `DELETE /users/me/nicknames/:username` | Remove a nickname |
| `GET /users/me/hidden` | People you've hidden from your Social page |
| `PUT /users/me/hidden/:username` | Hide someone |
| `DELETE /users/me/hidden/:username` | Unhide |
| `GET /users/me/invisibility` | Your [Invisible To](/social/privacy) list |
| `PUT /users/me/invisibility/:username` | Add or change someone: `{ "mode": "presence" }` (Online & Sessions) or `{ "mode": "full" }` (Whole Account) |
| `DELETE /users/me/invisibility/:username` | Remove someone |

## Deleting your account

`DELETE /users/me` permanently deletes your account and everything in it. There's no confirmation step in the API, so be careful with anything that holds your key.
