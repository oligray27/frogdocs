---
leafwiki_id: fl-android-app
leafwiki_title: Android App
leafwiki_created_at: "2026-11-10T12:15:25.374183392Z"
leafwiki_updated_at: "2026-11-10T12:15:25.374183392Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# Android App

The FrogLog Android app is the FrogLog website in its own app, with a few extras you can't get in a browser: home screen widgets, push notifications that work like they do on a computer, and **Play on PC**, which starts a game on your PC from your phone.

[Download the Android app](https://github.com/oligray27/froglog-android/releases/latest)

## Installing

1. Open the link above on your phone and download the latest `.apk` file.
2. Open it. Android will ask you to allow installs from the app you downloaded it with (your browser or file manager). Allow it, then install.
3. Open **FrogLog** and sign in as you would on the website.

To get updates without checking back, add the app's [GitHub page](https://github.com/oligray27/froglog-android) to [Obtainium](https://obtainium.imranr.dev/). It watches the releases and offers each new version.

The app is free and open source.

## What's different from the website

- **It matches your theme.** The bars at the top and bottom of the screen take on the colour of your FrogLog theme.
- **Back goes back.** The system back button steps back through the pages you've visited. From the Games page it closes the app.
- **Notifications.** Turn them on in **Profile > Settings > Notifications**, exactly as on the website. See [Notifications](/social/notifications).

## Widgets

Press and hold your home screen, choose **Widgets**, and look for **FrogLog**. There are four:

| Widget | What it shows |
|---|---|
| **Current Activity** | The game you're playing now, or the last one you played, with the session timer and buttons to pause, resume or stop it |
| **Online Now** | Which of the people you follow are online, what they're playing and for how long, and when the rest were last seen |
| **Last 7 Days** | Your hours and sessions this week, how that compares with last week, and a chart of each day |
| **Remote Start** | Games you played recently that your PC can start, with a button to start each one (see below) |

When you add a widget, you pick its theme from the same list as the website. Each widget keeps its own theme, and on Android 12 and later you can change it later from the widget's settings option. On a Samsung Galaxy Z Flip, the widgets are also available for the cover screen: turn them on in **Settings > Cover screen > Widgets** on the phone.

## Starting games on your PC

With **LilyPad** running on your PC, the app can start a game there from your phone, over your home network. Nothing goes through the FrogLog website, and nothing on your account can start a game on your PC: the phone and the PC have to be linked to each other first, on your PC.

You'll need LilyPad **0.6.7 or later** on your PC, signed in to the same FrogLog account, and your phone on the same Wi-Fi as your PC. See [LilyPad](/lilypad).

### Linking a PC

1. In LilyPad on your PC, open **Manage Remote Devices** and turn on **Allow connections from remote devices**.
2. In the app, open **Profile > Settings > Remote Start** and tap **Find PCs on this network**.
3. Tap **Link** next to your PC. The app shows a four-digit code.
4. Type that code into the **Manage Remote Devices** window on your PC.

The app and the PC are now linked. You can give a PC a name of your own with **Rename**. To remove a link, remove the device in LilyPad's **Manage Remote Devices** window (or use **Unlink all**), or tap **Unlink** in the app. A PC that has removed your phone disappears from the app's list.

### Play on PC

Once a PC is linked, games it can start get a **Play on PC** button on their details card. It starts the game on your PC through Steam, or through the program you've set LilyPad up to run for it. For a game Steam doesn't sell, see [Steam](/platforms/steam).

A few things to know:

- The button is dimmed while you already have a session running, or when the PC can't be reached. Tap it to see why.
- LilyPad can be set to **ask on the PC before launching a game**, so someone has to confirm each start there. It's off by default.
- LilyPad only starts the game. Your session is logged the usual way once the game is running.
- If you link more than one PC, **Play on PC** asks which to use each time. To skip that, pick one under **Primary PC** in **Profile > Settings > Remote Start** and it will start games there straight away.

### The Remote Start widget

The **Remote Start** widget lists your recently played games that your PC can start, with a play button beside each. Tap one to start it. If you have more than one PC linked, choose which one the widget uses when you add it, so you can put one on your home screen for each. When the PC can't be reached, the badge at the top turns red and says **Unavailable**.
