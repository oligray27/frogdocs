---
leafwiki_id: fl-api-ref-badges
---
# Badges

Your [badges](/badges) and progress.

## GET /badges

Every badge, with your progress.

```json
{
  "tiers": [{ "key": "bronze", "name": "Bronze" }, "…"],
  "ladders": [
    {
      "slug": "library",
      "section": "ladders",
      "name": "Library",
      "description": "Games you've added to your log.",
      "tier": 2,
      "tier_key": "silver",
      "earned": [
        { "tier": 1, "tier_key": "bronze", "earned_at": "2026-09-28T…", "criteria": "Awarded for logging 50 games." },
        { "tier": 2, "tier_key": "silver", "earned_at": "2026-09-30T…", "criteria": "Awarded for logging 100 games." }
      ],
      "value": 173,
      "thresholds": [50, 100, 250, 500, 1000],
      "next": { "tier": 3, "tier_key": "gold", "threshold": 250, "text": "Log 250 games." }
    }
  ],
  "badges": [
    { "slug": "masterpiece", "group": "moments", "name": "Masterpiece", "description": "Rate a game 5 stars.", "earned": true, "earned_at": "2026-09-28T…" }
  ],
  "secrets_remaining": 2
}
```

- `ladders` are tiered badges. `tier` is your current tier (`0` for none yet), `value` is your current count, and `next` is `null` once you reach Platinum. `section` is `"ladders"` or `"genres"`.
- `badges` are the one-offs, grouped by `group`: `moments`, `connections`, `commemorative` and `secrets`. Secret badges only appear once you've earned them.
- `secrets_remaining` is how many secret badges you haven't found yet.

## GET /badges/user/:username

Someone else's earned badges, in the same shape but without progress (`value`, `thresholds` and `next`), and only including badges they've earned.

## GET /badges/leaderboard

The [leaderboard](/badges): you and the people you follow, by points.

```json
[
  { "rank": 1, "username": "alex", "displayUsername": "Alex", "avatarUrl": null, "points": 34, "badgeCount": 21, "isSelf": false }
]
```

Equal points share a rank.

## Pinned badges

| Endpoint | Does |
|---|---|
| `GET /badges/pinned` | Your pinned badges |
| `PUT /badges/pinned` | Replaces your pinned badges: `{ "pins": [{ "slug": "library", "tier": 2 }] }`. Up to 5, each one you've earned. Use `"tier": 0` for one-off badges. |
| `GET /badges/user/:username/pinned` | Someone else's pinned badges |
