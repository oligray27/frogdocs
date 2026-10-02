---
leafwiki_id: fl-platforms-nintendo-switch
leafwiki_title: Nintendo Switch
leafwiki_created_at: "2026-10-02T10:46:51.402757666Z"
leafwiki_updated_at: "2026-10-02T10:46:51.402757666Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# Nintendo Switch

Linking your Nintendo Switch account lets FrogLog see what you're playing, so it can track your sessions automatically or show friends what you're playing.

Nintendo doesn't share play history or achievements with other services, so Switch has **no import** and **no trophies**. It only knows what you're playing right now.

## How it works

Nintendo has no official way for other sites to see what you're playing. FrogLog uses **nxapi-auth**, a free community service run by a third party (not FrogLog or Nintendo), which reads your Switch's online status and passes it on.

Because it's a third-party service, Switch tracking depends on it being up. If it's down, FrogLog can't see your Switch activity until it's back.

## Linking

1. Open your **Profile** and click **Link Switch**.
2. Go to [nxapi-auth.fancy.org.uk](https://nxapi-auth.fancy.org.uk) and register.
3. Link your Switch user account on that site.
4. Follow its instructions to turn on the presence API.
5. At the end, the site gives you a URL ending in a 16-character code, made of the numbers 0–9 and the letters a–f. Copy that code.
6. Paste it into the **Nintendo Switch Account ID** box in FrogLog and click **Link**.

The button now shows your Switch name and avatar.

![The Link Nintendo Switch Account dialog](/assets/fl-platforms-nintendo-switch/linknintendo.png)

## Automatic tracking

Turn on **Automatic Nintendo Switch Session Tracking** in **Profile > Settings > Autonomous Tracking > Switch**. Games you play that aren't in your library are added automatically. See [How it works](/platforms).

Your Switch must be connected to the internet for FrogLog to see what you're playing.

To show what you're playing without logging sessions, use **Mirror Switch In-Game Presence to FrogLog** instead.

## Unlinking

Click the **Unlink** button next to your Switch name. Games and sessions already in your library are kept.
