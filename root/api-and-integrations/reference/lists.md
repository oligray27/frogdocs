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
| `hero_img`, `title_img` | The list's banner image and logo (image URLs), or `null`. Returned by `GET /collections/lists/:id`, and by create and update. |
| `title_img_scale` | How large the logo is drawn, from `0.5` to `2`; `null` is the default size (`1`). Returned alongside the images. |
| `hero_pos_x`, `hero_pos_y` | Which part of the hero image the banner shows, as CSS `object-position` percentages (`0` to `100`); `null` is centred. Returned alongside the images. |
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
| `rel_date` | The game's release date (`YYYY-MM-DD`), when it's known. Only when you get a single list. |
| `resolved_igdb_id` | The game's IGDB id: `igdb_game_id`, else the linked library game's. Only when you get a single list. |
| `hltb_main_seconds` | HowLongToBeat's main-story time in seconds, when FrogLog has it, else `null`. Only when you get a single list. |
| `hltb_cached` | `false` while FrogLog hasn't looked the game up on HowLongToBeat yet. Getting the list starts those lookups, a few at a time, so ask again later for the rest. |
| `froglog_players` | How many people on FrogLog have the game (public entries you can see). Only when you get a single list. |

---

## Your lists

| Endpoint | Does |
|---|---|
| `GET /collections/lists` | Your lists, in your order |
| `GET /collections/lists/public` | Other people's public lists, with `owner_username`, `owner_avatar_url` and `owner_label` |
| `GET /collections/lists/explore` | No key needed. Public lists with games in, from profiles shared outside FrogLog, most liked first (up to 200). Each has `owner_username`, `owner_avatar_url`, `owner_label`, `member_count`, `like_count` and its first five covers as `thumbnails`. |
| `GET /collections/lists/:id` | One of your lists, with `like_count` and a `members` array. Each member also has `owner_status`, its status in your library. Add `?compareAs=<username>` to include someone you follow's status too (`compare_status`). |
| `POST /collections/lists` | Creates a list: `{ "name": "Kingdom Hearts", "description": "…", "is_public": true }`. `name` is required. `hero_img` and `title_img` are optional http(s) image URLs. |
| `PUT /collections/lists/:id` | Updates a list's `name`, `description` and `is_public`. Send all three. Include `hero_img`, `title_img`, `title_img_scale`, `hero_pos_x` or `hero_pos_y` to change them (`null` removes an image or resets the scale or position); left out, they stay as they are. |
| `DELETE /collections/lists/:id` | Deletes a list |
| `POST /collections/lists/reorder` | Sets the order of your lists: `{ "ids": [3, 1, 2] }` |

Other people's lists are under [Users](/api-and-integrations/reference/users-and-profiles).

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
