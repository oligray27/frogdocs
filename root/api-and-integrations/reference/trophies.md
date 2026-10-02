---
leafwiki_id: fl-api-ref-trophies
---
# Trophies

A game's [trophies](/library/trophies) (achievements) from Steam, PlayStation and Xbox.

| Endpoint | Returns |
|---|---|
| `GET /games/:id/achievements` | One of your games' trophies |
| `GET /live-service/:id/achievements` | One of your live service games' trophies |
| `GET /users/:username/games/:id/achievements` | Someone else's game's trophies |
| `GET /users/:username/live-service/:id/achievements` | Someone else's live service game's trophies |

All return `404` if the game isn't linked to Steam, PlayStation or Xbox. Mods and forks use their parent game's trophies.

## Response

```json
{
  "primaryPlatform": "steam",
  "total": 49,
  "unlocked": 31,
  "hasSteamId": true,
  "hasPsnId": false,
  "hasXboxId": false,
  "achievements": [
    {
      "apiname": "ACH_BEAT_HADES",
      "name": "Is There No Escape?",
      "description": "Clear an escape attempt.",
      "icon": "https://…",
      "iconGray": "https://…",
      "hidden": false,
      "unlocked": true,
      "unlocktime": 1601234567,
      "platform": "steam"
    }
  ],
  "platforms": {
    "steam": { "total": 49, "unlocked": 31, "hasAccountLink": true, "achievements": ["…"] }
  }
}
```

- `achievements`, `total` and `unlocked` are for the `primaryPlatform`, which is the platform with the most recent unlock.
- `platforms` has the same for every platform the game is linked to.
- `unlocktime` is a Unix timestamp in seconds, or `null`.
- `hasAccountLink` is `false` if the player hasn't linked that platform, in which case every trophy shows as locked.
- Hidden trophies are returned in full, including their name and description. Hide them yourself if you're showing them to someone.

## Pinned trophies

| Endpoint | Does |
|---|---|
| `GET /users/me/pinned-achievements` | Your Trophy Cabinet, in order |
| `GET /users/:username/pinned-achievements` | Someone else's Trophy Cabinet |
| `PUT /users/me/pinned-achievements` | Replaces your whole Trophy Cabinet |

### PUT /users/me/pinned-achievements

Send the complete list of up to 12 trophies, in display order. Anything not in the list is unpinned.

```json
{
  "pins": [
    {
      "game_id": 12,
      "game_type": "game",
      "game_title": "Hades II",
      "achievement_apiname": "ACH_BEAT_HADES",
      "achievement_name": "Is There No Escape?",
      "achievement_description": "Clear an escape attempt.",
      "achievement_icon": "https://…",
      "achievement_icon_gray": "https://…",
      "achievement_hidden": false
    }
  ]
}
```

Copy the trophy details from the trophies response above. `game_type` is `"game"` or `"live_service"`. `403` if any game isn't yours.
