---
leafwiki_id: fl-api-ref-up-next
---
# Up Next

Your [Up Next](/library/up-next) wishlist. In the API it's called the **wishlist**.

## The wishlist item object

| Field | Notes |
|---|---|
| `id` | |
| `title`, `description`, `img`, `cover_image` | |
| `genre`, `dev`, `studio_country` | |
| `rel_date`, `rel_date_category` | See [release date precision](/api/conventions) |
| `steam_app_id`, `igdb_slug`, `igdb_id` | |
| `sort_order` | Position in your list |
| `is_public` | |
| `created_at` | |

---

## GET /wishlist

Your list, in your order.

## POST /wishlist

Adds a game to the top of the list. Send `title` and any other fields above. Returns the new item.

```bash
curl -X POST https://api.froglog.co.uk/api/wishlist \
  -H "Authorization: Bearer flk_your_key_here" \
  -H "Content-Type: application/json" \
  -d '{"title": "Hollow Knight: Silksong", "steam_app_id": 1030300}'
```

Tip: use [`GET /search/fetch`](/api/reference/search) to fill in a game's details from its title first.

## PUT /wishlist/:id

Updates an item. **Replaces the whole item**: send every field. `cover_image` is only changed if you send it.

## DELETE /wishlist/:id

Removes an item. Returns `{ "success": true }`.

## POST /wishlist/reorder

```json
{ "ids": [9, 4, 12] }
```

Sets the order of your list, first to last. Returns `{ "success": true }`.

## POST /wishlist/:id/move-to-games

Moves an item into your games, as when you click **Add to Games**. Send the new game's fields, as for [`POST /games`](/api/reference/games): for example `start_date`, `hours_played`, `rating`, `session_tracking`. Returns `{ "success": true }`.

## POST /wishlist/:id/move-to-live-service

Moves an item into your live service games. Send `title` and any other fields. Returns the new live service game. `409` if you already have one with that title.

## POST /wishlist/sync-steam

**Deletes your whole list** and replaces it with your Steam wishlist. Needs Steam linked and your Steam wishlist public. Limited to 5 an hour.

Returns `{ "synced": 42, "total": 45 }`: how many games were added, out of how many on your Steam wishlist (duplicates are skipped).
