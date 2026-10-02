---
leafwiki_id: fl-api-ref-likes
leafwiki_title: Likes
leafwiki_created_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_updated_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# Likes

Like other people's things. See [Likes](/social/likes).

All three endpoints take a **target type** and the target's ID:

| Target type | Likes a… |
|---|---|
| `game` | Regular game |
| `live_service_game` | Live service game |
| `game_review` | Regular game's review (use the game's ID) |
| `live_service_review` | Live service game's review (use the game's ID) |
| `game_session` | Session on a regular game |
| `live_service_session` | Session on a live service game |
| `screenshot` | Screenshot |
| `list` | List |

## PUT /likes/:targetType/:targetId

Likes something. Liking it again does nothing. Returns `{ "success": true }`.

```bash
curl -X PUT https://api.froglog.co.uk/api/likes/game_session/501 \
  -H "Authorization: Bearer flk_your_key_here"
```

`400` if you try to like your own content. `404` if it doesn't exist or you can't see it.

## DELETE /likes/:targetType/:targetId

Takes your like back. Returns `{ "success": true }`.

## GET /likes/:targetType/:targetId

Who has liked something, newest first (up to 100):

```json
{ "likers": [{ "username": "alex", "display_name": "Alex", "avatar_url": null }] }
```

Like counts themselves come with the things being liked, as `like_count` and `liked_by_me`.
