---
leafwiki_id: fl-api-ref-games
leafwiki_title: Games
leafwiki_created_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_updated_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# Games

Your library of regular games. For live service games, see [Live Service](/api-and-integrations/reference/live-service).

## The game object

| Field | Type | Notes |
|---|---|---|
| `id` | number | |
| `title`, `description`, `review` | string | `review` supports `||spoiler||` markup |
| `genre`, `dev`, `studio_country` | string | `genre` can be a comma-separated list |
| `img` | string | Hero artwork URL |
| `cover_image` | string | Cover art URL |
| `title_img` | string | Logo URL |
| `rel_date`, `rel_date_category` | date, number | See [release date precision](/api-and-integrations/conventions) |
| `start_date`, `end_date` | date | |
| `hours_played` | number | The game's hours, for games without session tracking |
| `rating` | number | 0–100, each star is 20 |
| `dnf` | boolean | |
| `status_override` | string | `null` (Auto), `"completed"` or `"dormant"` |
| `status` | string | Stored status. Usually blank; `"Imported"` for untouched imports. Work out the shown status from the dates, `dnf` and `status_override`, as described in [Editing Games](/library/editing-games). |
| `is_public` | boolean | |
| `session_tracking`, `sessions_public` | boolean | |
| `no_achievements` | boolean | Hides trophies |
| `replay`, `replay_of_id` | boolean, number | `replay_of_id` is the earlier playthrough's ID |
| `parent_igdb_slug`, `parent_title`, `parent_img` | string | Set for mods and forks |
| `igdb_id`, `igdb_slug` | number, string | The game's IGDB entry |
| `created_at` | timestamp | |

`GET /games` also includes:

| Field | Notes |
|---|---|
| `platform_links` | Array of `{ id, platform_key, external_id, label }`. `platform_key` is `steam`, `psn`, `xbox`, `switch` or `other` (free text in `label`). |
| `total_hours`, `session_count`, `last_session_date` | Totals from the game's sessions |
| `like_count`, `liked_by_me`, `review_like_count`, `review_liked_by_me` | Likes on the game and its review |
| `screenshot_count` | |

---

## GET /games

Lists every game in your library, most recently started first.

```bash
curl https://api.froglog.co.uk/api/games \
  -H "Authorization: Bearer flk_your_key_here"
```

Returns an array of game objects.

## POST /games

Adds a game. Limited to 60 an hour.

Send any of the game fields above. Most useful:

| Field | Required | Notes |
|---|---|---|
| `title` | yes | |
| `platform_chips` | | Array of platform names, for example `["PS5"]` |
| `steam_app_id` | | Links the game to Steam |
| `start_date`, `end_date`, `hours_played`, `rating`, `dnf`, `review` | | |
| `session_tracking` | | `true` to log hours as sessions |
| `is_public` | | Defaults to public |
| `replay` | | `true` if you've played it before |
| `client_ref` | | Your own unique ID for this add, up to 200 characters. Sending the same `client_ref` again returns the existing game instead of adding a duplicate, so retries are safe. |

```bash
curl -X POST https://api.froglog.co.uk/api/games \
  -H "Authorization: Bearer flk_your_key_here" \
  -H "Content-Type: application/json" \
  -d '{"title": "Hades II", "platform_chips": ["PC"], "start_date": "2026-09-24", "session_tracking": true}'
```

Returns the new game object.

**If you already have this game**, either unfinished (`"action": "continue_playthrough"`) or linked to the same platform ID (`"action": "attach_platform_link"`), the response is `409` with:

```json
{ "needs_confirmation": true, "action": "continue_playthrough", "existing_game": { "id": 12, "title": "Hades II", "status": "" } }
```

Send the same request again with `confirm_action` set to:

- `"attach"` to add the platform to the existing game instead. The response is that game, with `"attached": true`.
- `"new"` to add it as a separate playthrough, linked as a replay.

## PUT /games/:id

Updates a game.

**This replaces the whole game.** Any field you leave out is cleared, except `cover_image`, which is only changed if you send it. To change one field, `GET /games` first, change what you need, and send the whole object back.

Turning `session_tracking` off deletes the game's sessions. Turning it on creates a "Pre-tracked hours" session; send `initial_session_hours` to set how many hours it holds.

Returns the updated game object.

## DELETE /games/:id

Deletes a game and its sessions. Returns `{ "success": true }`.

## Moving to Live Service

### POST /games/:id/move-to-live-service

Turns one game into a live service game. Send the game's fields (as for `PUT`); its hours become a single session. Returns the new live service game. `409` if you already have a live service game with that title.

### POST /games/bulk-move-to-live-service

```json
{ "ids": [12, 15, 31] }
```

Moves several games, keeping their sessions and screenshots. Returns `{ "moved": [...], "skipped": [...] }`: `moved` holds the new live service games, and `skipped` holds the IDs that weren't moved, because the game wasn't found or you already have a live service game with the same title.

## Sessions

Sessions for one game. For all your sessions at once, see [Sessions](/api-and-integrations/reference/sessions).

### The session object

| Field | Type | Notes |
|---|---|---|
| `id`, `game_id` | number | |
| `date` | date | `null` for "Pre-tracked hours" |
| `hours` | number | |
| `notes` | string | |
| `is_public`, `spoiler` | boolean | |
| `sync_ref` | string | Your own ID, if you sent one |
| `created_at` | timestamp | |
| `like_count`, `liked_by_me` | | Only in `GET` |

### GET /games/:id/sessions

The game's sessions, newest first.

### POST /games/:id/sessions

| Field | Notes |
|---|---|
| `date` | `YYYY-MM-DD`, not in the future |
| `hours` | Under 10,000 |
| `notes` | |
| `is_public` | Defaults to `true` |
| `spoiler` | Defaults to `false` |
| `sync_ref` | Your own unique ID. Sending the same one again returns the existing session instead of logging it twice. |

```bash
curl -X POST https://api.froglog.co.uk/api/games/12/sessions \
  -H "Authorization: Bearer flk_your_key_here" \
  -H "Content-Type: application/json" \
  -d '{"date": "2026-10-01", "hours": 2.5, "notes": "Beat the second boss"}'
```

Returns the new session. The game needs session tracking on for its sessions to count towards its hours.

### PUT /games/:id/sessions/:sessionId

Replaces a session's `date`, `hours`, `notes`, `is_public` and `spoiler`. Send all five. Returns the updated session.

### DELETE /games/:id/sessions/:sessionId

Returns `{ "success": true }`.

## Platforms

### POST /games/:id/platform-links

Links a game to a platform. Either:

- a real platform: `{ "platform_key": "steam", "external_id": "1145350" }`. `platform_key` is `steam`, `psn`, `xbox` or `switch`, and `external_id` is that platform's ID for the game. `409` if the game already has a different link for that platform, or another game has this ID.
- a free-text label: `{ "label": "Epic Games" }`.

Returns the link `{ id, platform_key, external_id, label, ... }`.

### DELETE /games/:id/platform-links/:linkId

Removes a link. Returns `{ "success": true }`.

## Trophies

### GET /games/:id/achievements

The game's trophies. See [Trophies](/api-and-integrations/reference/trophies).
