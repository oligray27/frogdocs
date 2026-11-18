---
leafwiki_id: fl-android-app
leafwiki_title: Android App
leafwiki_created_at: "2026-11-10T12:15:25.374183392Z"
leafwiki_updated_at: "2026-11-10T12:15:25.374183392Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# Android App

The FrogLog Android app is the FrogLog website in its own app, with a few extras you can't get in a browser: home screen widgets, push notifications that work like they do on a computer, **Play on Phone**, which opens a game on your phone and times it, and **Play on PC**, which starts a game on your PC from your phone.

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

## Playing games on your phone

### Play on Phone

Link a game to its Android app and it gets a **Play on Phone** button on its details card. Tapping it starts a [Quick Session](/library/sessions#quick-session) and opens the game.

To link a game, open its details card, tap **Edit**, then **Link Android App**. You'll see the apps on your phone, with the closest matches to the game's name first, then your other games, then everything else. Tap the right one and it's linked straight away. The link is saved to your account, so it works on any phone you sign in on that has the app installed. To change or remove it, tap the same button (it now shows the app's name).

The button only shows when the linked app is installed on the phone you're using, and it's dimmed while you already have a session running. If the game can also be started on your PC, the two buttons are combined: **Play on**, then a PC button and a phone button.

The first time you play a game this way, it gets a green **Mobile** tag in its platforms. If you remove the tag, it isn't added again.

### The running session notification

A Quick Session you start on your phone, whether from a game's card, **Play on Phone** or the **Current Activity** widget, shows in your notifications with buttons to **Pause**, **Resume** and **Stop**. It shows the game's app icon if the game is linked for **Play on Phone**, and otherwise its cover. **Stop** opens the app at the usual stop menu, so you can save it, add notes or discard it. Sessions started anywhere else (the website on a computer, LilyPad, or a platform like Steam) don't get the notification.

The notification goes by itself when the session ends, including when you stop it somewhere else. It isn't cleared by **Clear all**, but you can swipe it away, and then it stays away for that session unless you pause or resume it.

Turn it off in **Profile > Settings > Notifications > Running Session**. That setting only applies to the phone you change it on. The first time it's needed, Android asks whether FrogLog can show notifications. If you refuse, it can't appear until you allow notifications for FrogLog in your phone's settings.

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
