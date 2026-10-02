---
leafwiki_id: fl-api-homepage-widget
leafwiki_title: Homepage Widget
leafwiki_created_at: "2026-10-02T11:47:09.405032296Z"
leafwiki_updated_at: "2026-10-02T11:47:09.405032296Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# Homepage Widget

Show what you're playing, and which of the people you follow are playing right now, on a [Homepage](https://gethomepage.dev/) dashboard, using its built-in [Custom API widget](https://gethomepage.dev/widgets/services/customapi/).

![The FrogLog widget on a Homepage dashboard](/assets/fl-api-homepage-widget/homepageexample.png)

## Setting it up

1. In FrogLog, create an [API key](/api-and-integrations) named `Homepage` and copy it.
2. Add this to Homepage's `services.yaml`, replacing the key:

```yaml
- Gaming:
    - FrogLog:
        href: https://froglog.co.uk
        description: Current session and following
        widget:
          type: customapi
          url: https://api.froglog.co.uk/api/integrations/homepage
          headers:
            Authorization: "Bearer flk_REPLACE_WITH_YOUR_KEY"
          refreshInterval: 30000
          display: dynamic-list
          mappings:
            items: items
            name: name
            label: value
            limit: 12
```

3. Reload Homepage. The widget refreshes every 30 seconds.

## What it shows

- **Playing**: your current game and how long you've been playing, or "No active session".
- **Following**: how many of the people you follow are playing, or "Nobody playing".
- One row for each of them, with what they're playing.

`limit: 12` shows the two summary rows plus up to ten people. Raise it to show more. The "Following" count is always the full number, whatever the limit.

## Good to know

- "Playing" means FrogLog's play tracking (Quick Session, LilyPad or automatic tracking), not just having the website open.
- Your own game always shows, even if you've hidden it from other people.
- The people listed respect privacy settings, hidden users and nicknames. You're never listed yourself.
- Anyone who can see your Homepage dashboard can see the widget. Your key has [full access to your account](/api-and-integrations), so keep it in Homepage's server-side configuration and revoke it when you stop using it.

## The endpoint

### GET /integrations/homepage

Returns your current session and who you follow that's playing, already formatted for Homepage. You can use it for other dashboards too.

```json
{
  "currentSession": {
    "title": "Hades II",
    "startedAt": "2026-09-24T18:00:00.000Z",
    "elapsedSeconds": 2520,
    "tracked": true
  },
  "followingOnlineCount": 1,
  "followingOnline": [
    {
      "username": "alex",
      "displayUsername": "Alex",
      "avatarUrl": null,
      "online": true,
      "title": "Balatro",
      "platform": "steam",
      "lastSeenAt": null
    }
  ],
  "session": "Hades II · 42m",
  "items": [
    { "name": "Playing", "value": "Hades II · 42m" },
    { "name": "Following", "value": "1 playing" },
    { "name": "Alex", "value": "Balatro" }
  ]
}
```

- `currentSession` is `null` when you're not playing anything. `tracked` is `true` when FrogLog itself is timing the session (a Quick Session or automatic tracking), and `false` when it comes from LilyPad or presence mirroring.
- `startedAt` and `elapsedSeconds` are `null` if the start time isn't known.
- `items` always has the two summary rows first.
