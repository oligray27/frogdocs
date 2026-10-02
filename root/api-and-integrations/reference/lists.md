---
leafwiki_id: fl-api-ref-lists
leafwiki_title: Lists
leafwiki_created_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_updated_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# Lists

Your [lists](/library/lists). In the API they live under `/collections/lists`. Games in a list are called **members**.

## The list object

| Field | Notes |
|---|---|
| `id`, `name`, `description` | |
| `is_public` | |
| `created_at` | |
| `member_count`, `played_count` | How many games, and how many of them you've played |
| `like_count`, `liked_by_me` | |
| `thumbnails` | A few member covers for previews |

## The member object

| Field | Notes |
|---|---|
| `id` | The member's own ID, used to edit or remove it |
| `title`, `img` | |
| `game_id` | Set if it's one of your games |
| `live_service_game_id` | Set if it's one of your live service games |
| `igdb_game_id`, `igdb_slug` | For games that aren't in your library |
| `sort_order`, `added_at` | |

---

## Your lists

| Endpoint | Does |
|---|---|
| `GET /collections/lists` | Your lists, in your order |
| `GET /collections/lists/public` | Other people's public lists, with `owner_username`, `owner_avatar_url` and `owner_label` |
| `GET /collections/lists/:id` | One of your lists, with a `members` array. Each member also has `owner_status`, its status in your library. Add `?compareAs=<username>` to include someone you follow's status too (`compare_status`). |
| `POST /collections/lists` | Creates a list: `{ "name": "Kingdom Hearts", "description": "…", "is_public": true }`. `name` is required. |
| `PUT /collections/lists/:id` | Updates a list's `name`, `description` and `is_public`. Send all three. |
| `DELETE /collections/lists/:id` | Deletes a list |
| `POST /collections/lists/reorder` | Sets the order of your lists: `{ "ids": [3, 1, 2] }` |

Other people's lists are under [Users](/api-and-integrations/reference/users).

## Members

### GET /collections/lists/:id/members

The list's members, in order.

### POST /collections/lists/:id/members

Adds a game. `title` is required.

```json
{ "title": "Kingdom Hearts II", "game_id": 44 }
```

Use `game_id` or `live_service_game_id` for a game in your library (`403` if it isn't yours), or `igdb_game_id` and `igdb_slug` for any other game. `img` sets the cover. `409` if the game is already in the list.

### PUT /collections/lists/:id/members/:memberId

Changes a member's `title` and `img` for this list only. Send `img` every time, or the cover is cleared.

### DELETE /collections/lists/:id/members/:memberId

Removes a game from the list.

### POST /collections/lists/:id/members/reorder

Sets the order of the list: `{ "ids": [member IDs, first to last] }`.
