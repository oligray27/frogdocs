---
leafwiki_id: fl-platforms
leafwiki_title: Platforms & Automatic Tracking
leafwiki_created_at: "2026-10-02T10:46:51.402757666Z"
leafwiki_updated_at: "2026-10-02T10:46:51.402757666Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# Platforms & Automatic Tracking

Link your gaming accounts to FrogLog, and it can fill in your library and keep it up to date without you logging everything by hand.

FrogLog supports:

- [Steam](/platforms/steam)
- [PlayStation](/platforms/playstation)
- [Xbox](/platforms/xbox)
- [Nintendo Switch](/platforms/nintendo-switch)

For games on PC outside these platforms, use [LilyPad](/lilypad), FrogLog's desktop app.

## Linking a platform

Link platforms from your **Profile**. Under your profile card there's a button for each one: **Link Steam**, **Link PSN**, **Link Switch** and **Link Xbox**. Each platform's page explains the steps.

> **[Screenshot]** The profile card's platform buttons, with Steam linked (showing the Steam name, Import and Unlink buttons) and the others not yet linked.

Once linked, the button shows your name on that platform, with two smaller buttons beside it:

- **Import** brings in your play history (not available for Switch).
- **Unlink** disconnects the account.

## Three things a linked platform can do

| | What it does | Where to turn it on |
|---|---|---|
| **Import** | A one-off copy of your history on that platform: every game you've played, with its hours | The **Import** button on your profile |
| **Automatic session tracking** | Watches what you're playing and logs a session for you when you stop, adding new games to your library as needed | **Profile > Settings > Autonomous Tracking** |
| **Presence mirroring** | Shows other FrogLog users what you're playing right now, without logging anything | **Profile > Settings > Autonomous Tracking** |

You can use any combination. Most people import once, then turn on automatic tracking.

## Importing

Importing adds every game you've played on that platform to your library, with the hours the platform has on record. It's a quick way to get started when you've been playing for years.

Before importing, you can set **Only import games played for at least** a number of hours, to skip games you only tried briefly.

Imported games start with the status **Imported** and no dates, because the platform only knows your total hours, not when you played. Edit a game to add dates, a rating or a review.

### Games you already have

If a game being imported is already in your library, the import asks what to do with each one. It shows the hours on your FrogLog entry next to the hours on the platform, and offers:

- **Add hours from [platform] to the latest entry**: count the platform's hours towards the game you already have.
- **Create new entry with hours from [platform]**: add it as a separate playthrough.
- **Do nothing**: leave it for now. You'll be asked again next time you import.

**Skip All** sets every game to "Do nothing". Click **Confirm Choices** when you're done.

> **[Screenshot]** The import conflict step, with one game showing the three choices.

You can import again whenever you like. Games already in your library are recognised rather than duplicated.

## Automatic session tracking

Open **Profile > Settings > Autonomous Tracking** and pick a platform's tab. Each tab has:

| Setting | What it does |
|---|---|
| **Automatic [platform] Session Tracking** | **On** to have FrogLog log your sessions on that platform |
| **Auto-Submit Note** | The note saved on each session it logs. The default is "Session auto submitted via [platform]". Click **Save** after changing it. |
| **Mirror [platform] In-Game Presence to FrogLog** | **On** to show what you're playing, without logging sessions |
| **Public Sessions** | Whether the games and sessions automatic tracking creates are **Public** or **Private** by default |

The settings are greyed out until that platform is linked.

> **[Screenshot]** The Autonomous Tracking settings, showing the platform tabs and the four settings.

### How it works

FrogLog checks each linked platform about every two minutes.

1. When it sees you playing something, it starts a session, just like a Quick Session. You show as playing in Online Now on the Activity page.
2. It finds the game in your library (see [Matching Games](/platforms/matching-games)). If it isn't there, it adds it for you, with its details and cover art. If it's on your Up Next list, it's moved to Games.
3. When you stop playing, FrogLog waits for a couple more checks to be sure, then saves the session with the hours played and your Auto-Submit Note.

Because of those checks, sessions are accurate to within a few minutes.

The first time FrogLog tracks a game, it turns on session tracking for it. Any hours the game already had become a first session called "Pre-tracked hours", and if the game had no start date, it gets today's. So an imported game moves from **Imported** to **In Progress** as soon as you play it.

If the game in your library is already Completed or DNF, FrogLog starts a new playthrough as a [replay](/library/replays-and-dnf) rather than reopening the finished one.

### Don't double up

Use only one tracker for any game. If you use LilyPad, or start Quick Sessions yourself, for games on a platform, leave automatic tracking off for that platform. Running two at once can log the same session twice and double your hours.

FrogLog shows a reminder of this when you turn automatic tracking on.

## Presence mirroring

**Mirror [platform] In-Game Presence to FrogLog** shows what you're playing in Online Now on the Activity page, so friends can see you're in a game.

It only works for games already in your library. It never creates games, logs sessions or changes your hours. If automatic tracking is on, you'll show as playing anyway, so you don't need both.
