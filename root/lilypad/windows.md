---
leafwiki_id: fl-lilypad-windows
leafwiki_title: LilyPad for Windows
leafwiki_created_at: "2026-10-02T10:52:08.230591981Z"
leafwiki_updated_at: "2026-10-02T10:52:08.230591981Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# LilyPad for Windows

## Installing

1. Download `LilyPad_<version>_x64-setup.exe` from the [latest release](https://github.com/oligray27/lilypad/releases/latest).
2. Run it. The installer asks whether LilyPad should check for updates automatically.
3. LilyPad opens its login window.

## Logging in

Enter your FrogLog **Username** and **Password** and click **Log in**. Leave **Remember me** ticked to stay logged in.

LilyPad then runs in the system tray. If you can't see its icon, check the hidden-icons arrow at the end of the taskbar.

![The LilyPad login window](/assets/fl-lilypad-windows/lilypadlogin.webp){width=70%}

## The tray menu

Right-click the tray icon for:

| Item | What it does |
|---|---|
| **Now Tracking: [game] ([time])** | Shown while a game is being tracked |
| **Stop Tracking Current Session** | Ends a session tracked against the wrong game. You then choose what to do with the time. |
| **New Games (N)** | Games LilyPad noticed that aren't in your FrogLog. See [New Games](/lilypad/new-games). |
| **Pending Submissions (N)** | Sessions waiting to be sent |
| **Configure...** | Link games and change settings |
| **Update to (x.y.z)...** | Shown when a new version is out |
| **About**, **Logout**, **Quit** | |

![The LilyPad tray menu while a game is being tracked](/assets/fl-lilypad-windows/lilypadtracking.webp){width=25%}

## Linking games

LilyPad recognises a game by its program file (its `.exe`). Steam games already in your FrogLog are linked automatically the first time you play them. For anything else:

1. Choose **Configure...** from the tray.
2. The table lists every game in your FrogLog. Use **Games** and **Live service** to switch between them, and **Search…** to find one.
3. In the game's **exe** column, type the program's file name (for example `hl2.exe`), or click **Browse…** to pick it.
4. Click **Apply**.

![The Configuration window with a game's exe filled in](/assets/fl-lilypad-windows/lilypadexemapping.webp){width=80%}

### Games that share a program

Some games run through the same program, such as Java games (`javaw.exe`) or several games in one emulator. Give each one a **Window title filter**: a piece of text from that game's window title. LilyPad then tells them apart by their window. If two links clash, they're highlighted in red until you add filters.

## Settings

The checkboxes at the top of **Configure...**:

| Setting | What it does |
|---|---|
| **Auto-submit play time to games without session tracking** | Adds the time to the game's hours without asking |
| **Auto-submit sessions to games with session tracking** | Logs sessions without asking |
| **Auto-submit live service sessions** | Logs live service sessions without asking |
| **Enable online presence on FrogLog** | Shows what you're playing in Online Now on the [Activity](/social/activity) page |
| **Detect games not in your FrogLog library** | Records Steam and watched-folder games you haven't added yet, under [New Games](/lilypad/new-games) |
| **Check for LilyPad updates automatically** | Checks for new versions on start and once a day |

### Non-Steam Games

**Non-Steam Games…** lets you add folders for LilyPad to watch, such as a folder of DRM-free or emulated games. Each subfolder counts as one game, and new ones appear under New Games.

### Excluded Games

Some Steam apps install like games but aren't, such as Wallpaper Engine. Add them under **Excluded Games…** and LilyPad never tracks them.

## When you stop playing

**With auto-submit on**, the session is logged straight away. For games with session tracking and live service games, a notification first offers **Add Notes** for a few seconds.

**With auto-submit off**, a **Session Ended** window shows the game, date and session length. Add **Session Notes** if you like, tick **Contains spoilers** or **Hide from public**, then click **Submit to FrogLog** or **Do not record session**.

![The Session Ended window](/assets/fl-lilypad-windows/sessionended.webp){width=55%}

## Pending Submissions

If a session can't be sent, for example because you're offline or your login has expired, it's saved under **Pending Submissions** in the tray. Log out and back in from the tray if your login has expired, then click **Retry** on each session. **Delete** discards one.

## Updating

When a new version is out, you get a notification and the tray shows **Update to (x.y.z)...**. Click it to download the installer, then run it over the top of your current version. Your login, links and history are kept.

## Where LilyPad keeps its data

`%LOCALAPPDATA%\froglog-lilypad\`. It holds your login, game links, and any sessions not yet sent.
