---
leafwiki_id: fl-api-ref-notifications
leafwiki_title: Notifications
leafwiki_created_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_updated_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# Notifications

Your [notifications](/social/notifications).

## The notification object

| Field | Notes |
|---|---|
| `id` | |
| `type` | `follow`, `like`, `crown_earned`, `crown_lost`, `badge_earned` or `changelog` |
| `data` | Details for the type, for example the liked item's `target_type`, `game_title` and IDs, or a badge's `name` and `tier_name` |
| `read_at` | Timestamp, or `null` if unread |
| `created_at` | |
| `actor_username`, `actor_display_username`, `actor_nickname`, `actor_avatar_url` | Who did it, for follows and likes |

## GET /notifications

Newest first.

| Query | Default | Notes |
|---|---|---|
| `page` | `1` | |
| `limit` | `30` | Up to 100 |

Returns `{ "notifications": [...], "total": 58, "page": 1, "totalPages": 2 }`.

## GET /notifications/unread-count

```json
{ "unreadCount": 3 }
```

## PUT /notifications/:id/read

Marks one as read.

## PUT /notifications/read-all

Marks them all as read.

## DELETE /notifications/:id

Deletes one.

## DELETE /notifications

Deletes them all.

## GET /notifications/stream

A live stream of new notifications, using [server-sent events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events). Browsers can't send headers on these, so pass your key as a query parameter instead:

```
GET /notifications/stream?token=flk_your_key_here
```

Each event's `data` is a notification object as JSON. The stream also sends comment lines every so often to keep the connection open; ignore them.

```js
const stream = new EventSource('https://api.froglog.co.uk/api/notifications/stream?token=flk_your_key_here');
stream.onmessage = (e) => console.log(JSON.parse(e.data));
```

Putting the key in a URL means it can end up in logs, so only do this from code you control.
