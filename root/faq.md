---
leafwiki_id: fl-faq
leafwiki_title: FAQ & Troubleshooting
leafwiki_created_at: "2026-10-02T12:21:50.75429424Z"
leafwiki_updated_at: "2026-10-02T12:21:50.75429424Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# FAQ & Troubleshooting

Answers to common questions, and fixes for common problems.

## Tracking and sessions

### My sessions are being logged twice

You probably have two trackers running for the same game, for example LilyPad and automatic Steam tracking, or automatic tracking plus Quick Sessions you start yourself. Use only one for each game. If you use LilyPad for your PC games, turn off automatic tracking for that platform in **Profile > Settings > Autonomous Tracking**. See [Platforms & Automatic Tracking](/platforms).

To clean up, delete the duplicate sessions from the game's sessions list. See [Sessions](/library/sessions).

### Automatic Steam tracking isn't picking up my games

- Check your Steam profile's **Game details** are set to **Public**. See [Steam](/platforms/steam).
- If you appear **Offline** or **Invisible** on Steam, FrogLog can't see what you're playing.
- Check **Automatic Steam Session Tracking** is **On** in **Profile > Settings > Autonomous Tracking > Steam**.
- FrogLog checks about every two minutes, so a session can take a few minutes to start and end.

### PlayStation tracking or importing has stopped working

PlayStation's access expires after about two months. If your profile shows **Relink PSN**, click it and link again with a fresh NPSSO token. See [PlayStation](/platforms/playstation).

Remember that PlayStation only reports console play, not PlayStation games on PC.

### Nintendo Switch tracking has stopped working

Switch tracking relies on a third-party community service. If it's down, FrogLog can't see your Switch activity until it's back. Nothing on your side needs changing. See [Nintendo Switch](/platforms/nintendo-switch).

### Sessions are going to the wrong game

FrogLog matched the platform's game to the wrong entry in your library. Remove the wrong platform from that game's edit form, and FrogLog will match it again next time. See [Matching Games](/platforms/matching-games).

### Tracking added a game I already had

FrogLog only joins a tracked game to one you already have if it's unfinished and has the same title, or is already linked to that platform. Otherwise it adds a new entry. A finished game gets a new playthrough as a [replay](/library/replays-and-dnf), which is on purpose. See [Matching Games](/platforms/matching-games) for how it decides.

### LilyPad didn't track my game

- Check the game is linked in **Configure...**, with the right `.exe`. See [LilyPad for Windows](/lilypad/windows).
- If it's a game that isn't in your FrogLog yet, look under [New Games](/lilypad/new-games).
- On Linux with Flatpak Steam, only games you've linked by hand are tracked. See [LilyPad for Linux](/lilypad/linux).

### LilyPad says a session couldn't be sent

It's waiting under **Pending Submissions** in the tray menu. Check your internet connection, or log out and back in from the tray if your login has expired, then click **Retry**. Nothing is lost.

## Your library

### I can't find a game in Search

Try a shorter or alternative title, or search by Steam app ID (for example `appid:524220`). If it really isn't there, use **Add Custom Game (Mod/Fork)**. See [Adding Games](/library/adding-games).

### What does the "Imported" status mean?

The game came from an import, which only knows your total hours, not when you played. Edit the game to add dates, or just play it with automatic tracking on, and it becomes a normal game. Imported games don't count towards [badges](/badges) until you've done one of those.

### What's the difference between DNF and Dormant?

**DNF** means you've given up on a game. **Dormant** means you've put it down but might come back. See [Replays and DNF](/library/replays-and-dnf).

### Syncing my Steam wishlist wiped my Up Next list

The Steam wishlist sync replaces your whole Up Next list with your Steam wishlist. It warns you first, but it can't be undone. See [Up Next](/library/up-next).

### Turning off session tracking deleted my sessions

Turning session tracking off deletes a game's sessions, but copies their total into **Hours Played** first, so your hours are kept. The form warns you before saving. See [Editing Games](/library/editing-games).

## Stats

### My hours for a year look wrong

Games without session tracking count all their hours towards the year you started them, because FrogLog doesn't know when you played them. Games with session tracking split their hours across the years you played. See [how hours are counted](/stats).

### Trends is empty

Time charts on Trends only use games with session tracking. Turn on session tracking for your games, or use a **Bar** chart, which uses all-time hours for every game. See [Trends](/stats/trends).

### My friend sees lower stats for me than I do

Other people only see your public games and sessions. If you've made some private, your numbers look lower to them. See [Comparing Stats](/stats/comparing).

## Profile and privacy

### Who can see my FrogLog?

By default, everyone on FrogLog. You can make individual games, sessions and lists private, and hide your account or your activity from particular people. See [Privacy](/social/privacy).

### I can't change my background on my phone

Custom backgrounds only show on desktop, so the button is greyed out on phones. See [Appearance](/profile-settings/appearance).

### How do I get a copy of my data?

Use **Export Data** in **Profile > Settings > Logout & Other**. See [Account](/profile-settings/account).

### I've lost my API key

Keys are only shown once. Revoke the old one and generate a new one in **Profile > Settings > API Keys**. See [API & Integrations](/api-and-integrations).
