---
leafwiki_id: fl-lilypad
leafwiki_title: LilyPad
leafwiki_created_at: "2026-10-02T10:52:08.230591981Z"
leafwiki_updated_at: "2026-10-02T10:52:08.230591981Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# LilyPad

LilyPad is FrogLog's companion app for PC and Steam Deck. It notices when you start a game, times the session, and logs it to FrogLog when you stop. It works for any game on your computer, not just Steam: launchers, emulators, DRM-free games and so on.

[Download LilyPad](https://github.com/oligray27/lilypad/releases/latest)

## Which version do I need?

| You're playing on | Use | Guide |
|---|---|---|
| Windows | The Windows app (`LilyPad_<version>_x64-setup.exe`) | [Windows](/lilypad/windows) |
| Linux desktop | The Linux app (`.deb`, `.rpm` or AppImage) | [Linux](/lilypad/linux) |
| Steam Deck or Bazzite in Gaming Mode | The Decky plugin (`LilyPad-<version>.zip`) | [Steam Deck](/lilypad/steam-deck) |

All three work the same way and log into the same FrogLog account.

## How it works

1. **Log in** with your FrogLog username and password. LilyPad then sits in your system tray.
2. **Link your games.** Tell LilyPad which program belongs to which game in your FrogLog. Steam games already in your library are linked automatically the first time you play them.
3. **Play.** LilyPad shows "Tracking Started", and the tray shows "Now Tracking" with the time so far.
4. **Stop playing.** LilyPad logs the session, either automatically or after asking you.

If you start a game that isn't in your FrogLog yet, LilyPad still records it, and you decide what to do with it later. See [New Games](/lilypad/new-games).

## What gets logged

What LilyPad sends depends on the game:

- **Games with session tracking** and **live service games** get a new [session](/library/sessions), with the date, the hours, and any notes you add.
- **Games without session tracking** have the time added to their **Hours Played**.

## LilyPad or automatic tracking?

FrogLog can also track Steam, PlayStation, Xbox and Switch on its own (see [Platforms & Automatic Tracking](/platforms)). The difference:

- **Automatic tracking** needs nothing installed, but only works for those platforms.
- **LilyPad** works for any PC game, and times sessions more precisely, because it watches the game on your PC directly instead of checking every couple of minutes.

Use one or the other for any given game, not both, or sessions will be logged twice. For example, if you use LilyPad for your Steam games, leave **Automatic Steam Session Tracking** off.

## If something goes wrong

- **No internet, or logged out?** Sessions that can't be sent wait under **Pending Submissions**, and **Retry** sends them later. Nothing is lost.
- **LilyPad or your PC crashed mid-game?** Sessions are saved as they happen. Next time LilyPad starts, it recovers the session, counted up to the last moment it knew the game was running.
- **Wrong game being tracked?** Choose **Stop Tracking Current Session** from the tray (or **Stop tracking this session** on Steam Deck), then choose what to do with the time.
- **Nothing is ever sent twice**, even if you retry after a dropped connection.

## Updates

LilyPad checks for a new version shortly after it starts and then once a day, and tells you when one is out. It never downloads or installs anything without asking. Turn this off with **Check for LilyPad updates automatically** in Configure.
