---
leafwiki_id: fl-api-conventions
leafwiki_title: Conventions
leafwiki_created_at: "2026-10-02T11:47:09.405032296Z"
leafwiki_updated_at: "2026-10-02T11:47:09.405032296Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# Conventions

How requests and responses work across the whole API.

## Base URL

```
https://api.froglog.co.uk/api
```

Every endpoint in the [reference](/api-and-integrations/reference) is relative to this. For example, `GET /games` means `GET https://api.froglog.co.uk/api/games`.

## Authentication

Every endpoint needs your [API key](/api-and-integrations) in the `Authorization` header:

```
Authorization: Bearer flk_your_key_here
```

## Requests

- Send request bodies as JSON, with `Content-Type: application/json`.
- The only exception is uploading a screenshot, which uses `multipart/form-data`.
- IDs in paths are numbers, for example `/games/42`.

## Responses

Responses are JSON. Fields use `snake_case` (for example `hours_played`, `start_date`), except a few newer endpoints that use `camelCase`. Each endpoint's reference shows which.

Actions that don't return anything else respond with:

```json
{ "success": true }
```

## Data types

| Type | Format | Example |
|---|---|---|
| Date | `YYYY-MM-DD` | `"2026-09-28"` |
| Timestamp | ISO 8601, UTC | `"2026-09-28T18:04:11.000Z"` |
| Hours | Number, decimals allowed, under 10,000 | `2.5` |
| Rating | Whole number from 0 to 100, where each star is 20. `0` or `null` means unrated. | `80` (4 stars) |
| Numbers from the database | Sometimes returned as strings, for example `"12.5"`. Convert them before doing maths. | |

### Release date precision

Games have a `rel_date` and a `rel_date_category` that says how precise it is:

| `rel_date_category` | Means |
|---|---|
| `0` or `null` | Exact date |
| `1` | Month only |
| `2` | Year only |
| `3`, `4`, `5`, `6` | Quarter: Q1, Q2, Q3, Q4 |
| `7` | To be decided |

### Validation

- Session dates can't be in the future.
- Hours must be a positive number under 10,000. `0` is treated as no hours.

## Errors

Errors return an HTTP status code and a JSON body with a message:

```json
{ "error": "Not found" }
```

| Status | Means |
|---|---|
| `400` | Something in the request is missing or invalid. The message says what. |
| `401` | No API key was sent (`"No token"`), or it isn't valid (`"Invalid token"`) |
| `403` | You're not allowed to do this, for example adding someone else's game to your list |
| `404` | The thing doesn't exist, or isn't yours |
| `409` | Conflict: it already exists, or something needs confirming first |
| `429` | You've hit a rate limit. Wait and try again. |
| `500` | Something went wrong on FrogLog's side |

## Rate limits

| Limit | Applies to |
|---|---|
| 300 requests an hour | Every request that changes something (`POST`, `PUT`, `PATCH`, `DELETE`) |
| 60 an hour | Adding games (`POST /games`) |
| 10 an hour | Data exports (`GET /export`) |
| 5 an hour | Steam wishlist sync (`POST /wishlist/sync-steam`) |

Reading data (`GET`) has no general limit. When you hit a limit, you get a `429` with an error message. The `RateLimit` response headers show how many requests you have left and when the limit resets.

## Games and live service games

Regular games and [live service games](/library/live-service-games) are stored separately and have **separate ID numbers**, so game `12` and live service game `12` are different games. Endpoints that work with either take a `game_type` of `"game"` or `"live_service"` to say which.
