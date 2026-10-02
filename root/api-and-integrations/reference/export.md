---
leafwiki_id: fl-api-ref-export
leafwiki_title: Export
leafwiki_created_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_updated_at: "2026-10-02T11:47:09.406032319Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# Export

## GET /export

Downloads everything you've logged as a zip file, the same as **Export Data** in [Account](/profile-settings/account). Limited to 10 an hour.

```bash
curl https://api.froglog.co.uk/api/export \
  -H "Authorization: Bearer flk_your_key_here" \
  -o froglog-export.zip
```

The zip contains:

| File | Contains |
|---|---|
| `games.csv` | Your games |
| `game_sessions.csv` | Sessions for your games |
| `live_service_games.csv` | Your live service games |
| `live_service_sessions.csv` | Sessions for your live service games |
| `wishlist.csv` | Your Up Next list |
| `profile.csv` | Your profile details |
| `froglog-backup.json` | All of the above as JSON |

Handy for scheduled backups.
