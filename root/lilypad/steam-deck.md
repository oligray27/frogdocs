---
leafwiki_id: fl-lilypad-steam-deck
leafwiki_title: LilyPad on Steam Deck
leafwiki_created_at: "2026-10-02T10:52:08.230591981Z"
leafwiki_updated_at: "2026-10-02T10:52:08.230591981Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# LilyPad on Steam Deck

On a Steam Deck, Bazzite, or another system running Steam's Gaming Mode, LilyPad runs as a plugin for [Decky Loader](https://decky.xyz). It tracks your games in the background and lives in the Quick Access Menu.

It works on its own. You don't need the Linux desktop app, though it works alongside it if you have it.

## Installing

1. Install [Decky Loader](https://decky.xyz) if you haven't already.
2. Download `LilyPad-<version>.zip` from the [latest release](https://github.com/oligray27/lilypad/releases/latest).
3. In Decky's settings, turn on developer mode.
4. Go to **Decky settings > Developer > Install Plugin from ZIP** and choose the zip.

LilyPad now appears in the Quick Access Menu (the **...** button).

## Logging in

Open LilyPad in the Quick Access Menu and use **Log in to FrogLog** with your FrogLog username and password.

## The LilyPad panel

> **[Screenshot]** The LilyPad panel in the Quick Access Menu while a game is being tracked.

| Section | What's there |
|---|---|
| **Now Tracking** | The game being tracked and how long the session has run. **Stop tracking this session** ends a session tracked against the wrong game. |
| **Sessions to submit** | Sessions waiting for you to submit, when auto-submit is off |
| **Pending Submissions** | Sessions that couldn't be sent. **Retry** or **Delete**. |
| **New Games** | Games you've played that aren't in your FrogLog yet. See [New Games](/lilypad/new-games). |
| **Settings** | **Auto-submit sessions**, **Session message**, **Mirror online presence to FrogLog** and **Record games not in FrogLog** |
| **Account** | Log out |

Toasts tell you when tracking starts, when a session has been submitted, and when you're playing a game that isn't in your FrogLog yet.

## Auto-submit

- **On** (the default): every session is submitted as soon as the game closes, with your **Session message** as its note. Leave the message blank for no note.
- **Off**: when a game closes, a **Session Ended** dialog lets you add notes, tick **Contains spoilers** or **Hide from public**, then **Submit to FrogLog** or **Do not record session**. If you close the dialog, the session waits under **Sessions to submit**.

The desktop app's auto-submit settings don't apply in Gaming Mode.

## Linking games

Steam games already in your FrogLog are linked automatically the first time you play them. Anything else appears under New Games.

Linking a program to a game by hand needs the [Linux desktop app](/lilypad/linux) in Desktop Mode. Links you make there are used in Gaming Mode too.

## Using it with the desktop app

If you also have the Linux desktop app, both share one login, one set of game links and one history. Only one tracks at a time: the desktop app while it's running in Desktop Mode, and the plugin in Gaming Mode. While the desktop app is tracking, the panel says so. A game that's running when you switch modes carries on as the same session.

## Updating

When a new version is out, you get a one-off toast, and an **Update available** section appears at the top of the panel. Click **Update now**, and Decky asks you to confirm before installing it. Your login and history are kept, and a game in progress keeps being tracked.

If your version of Decky can't update this way, **Open release page** has the zip to install the same way as before.
