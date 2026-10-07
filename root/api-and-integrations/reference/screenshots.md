---
leafwiki_id: fl-api-ref-screenshots
leafwiki_title: Screenshots
leafwiki_created_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_updated_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# Screenshots

Screenshots on your games. Each game can have up to 10, and you can pin up to 10 items in total, screenshots and clips together, to your profile's Media Showcase.

## The screenshot object

| Field | Notes |
|---|---|
| `id` | |
| `game_id` | The game's ID, which may be a regular or a live service game (see below) |
| `game_title` | |
| `file_url` | Path to the image. Add it to `https://api.froglog.co.uk`, for example `https://api.froglog.co.uk/uploads/screenshots/…`. |
| `caption` | |
| `spoiler`, `nsfw` | |
| `pinned`, `pin_order` | Whether it's in your Media Showcase, and where |
| `display_order` | Position among the game's screenshots |
| `created_at` | |
| `like_count`, `liked_by_me` | In list responses |

Screenshot endpoints take a game ID without saying which kind of game it is. FrogLog checks your regular games first, then your live service games. Because the two have separate IDs, a regular game and a live service game can share a number, and in that case the regular game is used.

---

## GET /screenshots/game/:gameId

The game's screenshots, in order.

## POST /screenshots/game/:gameId

Uploads a screenshot. Send `multipart/form-data` with:

| Field | Notes |
|---|---|
| `screenshot` | The image file: JPG, PNG, GIF or WebP, up to 10 MB |
| `caption` | Optional |
| `spoiler`, `nsfw` | Optional, `"true"` or `"false"` |

```bash
curl -X POST https://api.froglog.co.uk/api/screenshots/game/12 \
  -H "Authorization: Bearer flk_your_key_here" \
  -F "screenshot=@boss-fight.png" \
  -F "caption=Finally beat him" \
  -F "spoiler=true"
```

Returns the new screenshot. `400` if the game already has 10.

## GET /screenshots/:id

One of your screenshots.

## PATCH /screenshots/:id/details

Changes any of `caption`, `spoiler` and `nsfw`. Only send what you're changing. Returns the updated screenshot.

## PATCH /screenshots/:id/pin

Pins the screenshot to your Media Showcase, or unpins it if it's already pinned. A new pin goes at the end. Returns the updated screenshot. `400` if you already have 10 items pinned, counting clips.

## DELETE /screenshots/:id

Deletes a screenshot.

## Media Showcase

The showcase holds pinned screenshots and clips in one order. Each item has a `kind`, `"screenshot"` or `"clip"`, and IDs are only unique within a kind. Screenshots have `file_url`; clips have `video_url`, `poster_url` and `name`. Both have `game_title`, `parent_title`, `caption`, `spoiler`, `nsfw`, `pin_order`, `like_count` and `liked_by_me`.

| Endpoint | Does |
|---|---|
| `GET /showcase/me` | Your showcase, in order |
| `GET /showcase/user/:username` | Someone else's showcase |
| `PUT /showcase/me/reorder` | Sets the order: `{ "items": [{ "kind": "clip", "id": 4 }, { "kind": "screenshot", "id": 12 }] }`, up to 10 |

The older screenshot-only endpoints below still work, but only see the screenshots in the showcase.

| Endpoint | Does |
|---|---|
| `GET /screenshots/me/pinned` | Your pinned screenshots, in showcase order |
| `PUT /screenshots/me/pinned/reorder` | Sets the order of your pinned screenshots: `{ "ids": [up to 10 screenshot IDs] }` |

## Other people's screenshots

Only screenshots on their public games are returned.

| Endpoint | Does |
|---|---|
| `GET /screenshots/user/:username/all` | All their screenshots. Each also has `is_live_service` and `parent_title`. |
| `GET /screenshots/user/:username/game/:gameId` | Their screenshots for one game |
| `GET /screenshots/user/:username/pinned` | The screenshots in their Media Showcase |
