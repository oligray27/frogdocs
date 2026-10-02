---
leafwiki_id: fl-api-ref-search
---
# Search

Look up games in FrogLog's game index, which is built from IGDB.

## GET /search

| Query | Notes |
|---|---|
| `q` | Search text, or `appid:<number>` to look up a Steam app ID |

```bash
curl "https://api.froglog.co.uk/api/search?q=hades" \
  -H "Authorization: Bearer flk_your_key_here"
```

Returns an array of results, best match first. An empty `q` returns `[]`.

```json
[
  {
    "id": 26193,
    "name": "Hades",
    "background_image": "https://…",
    "cover_image": "https://…",
    "description_raw": "Defy the god of the dead…",
    "developers": [{ "id": null, "name": "Supergiant Games" }],
    "dev_country": "United States",
    "steam_app_id": 1145360,
    "igdb_slug": "hades--1",
    "genres": [{ "id": 12, "name": "Role-playing (RPG)" }],
    "platforms": [{ "platform": { "id": 6, "name": "PC (Microsoft Windows)" } }],
    "released": "2020-09-17",
    "rel_date_category": 0
  }
]
```

`id` is the game's IGDB ID.

## GET /search/fetch

| Query | Notes |
|---|---|
| `title` | Required. The game's title. |

Returns the best match's details, in the same field names as a [game](/api/reference/games), ready to send to `POST /games` or `POST /wishlist`:

```json
{
  "title": "Hades",
  "description": "Defy the god of the dead…",
  "img": "https://…",
  "genre": "Role-playing (RPG), Indie",
  "dev": "Supergiant Games",
  "dev_country": "United States",
  "rel_date": "2020-09-17",
  "rel_date_category": 0,
  "steam_app_id": 1145360,
  "igdb_slug": "hades--1",
  "igdb_id": 26193
}
```

`404` if nothing matches. Note that the country field is `dev_country` here, but `studio_country` when you add a game.
