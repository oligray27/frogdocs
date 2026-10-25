---
tags: []
leafwiki_id: fl-library-sessions
leafwiki_title: Sessions
leafwiki_created_at: "2026-10-02T10:38:03.21649587Z"
leafwiki_updated_at: "2026-10-02T14:10:44.02997098Z"
leafwiki_creator_id: system
leafwiki_last_author_id: 6AZN8grDR
---
# Sessions

A **session** is one sitting with a game: a date, how many hours you played, and optional notes. Sessions give you a play-by-play history of a game instead of one running total.

Every [live service game](/library/live-service-games) uses sessions. For regular games, sessions are optional. Turn them on with **Enable Session Tracking** when adding or editing the game. Games with session tracking show a notebook icon in your library.

With session tracking on, the game's hours are the total of all its sessions. You can't type in **Hours Played** directly.

## Adding a session by hand

1. Select the game and click **Add Session** on its details card.
2. Pick the **Date**, enter the **Hours** (for example `2.5`), and add any **Notes**.
3. Save.

![The Add Session form](/assets/fl-library-sessions/addsessionform.webp){width=40%}

## Tagging people in notes

Type **@** followed by someone's username in a session's notes, for example "Played with @Reayon". Typing **@** lists the people you follow, and as you carry on typing, FrogLog suggests matching users. Use the arrow keys and **Enter**, or click a name, to fill it in.

Each person you tag gets a [notification](/social/notifications) linking to the session. They're only notified if they can see it, so a session that's hidden from public, or in a game without **Public Sessions**, doesn't notify anyone. If you make it public later and save it, they're notified then. Editing a session never notifies the same person twice.

Tag people by the name you see for them, including a nickname you've given them. Everyone reading the note sees each tagged person under the name they know them by, and tagged names link to that person's profile.

### Mirroring a session you're tagged in

If someone tags you, you can copy their session into your own FrogLog. Open the session from the notification (or find it in their sessions), and click the **Mirror to my FrogLog** button next to the heart.

The session form opens with their date and hours, and the notes "Played with @their name", which tags them back. Change anything you like, then save, and FrogLog takes you to your copy.

**Game** at the top shows which of your games the session goes on. FrogLog picks your matching game for you, even if it's in Live Service for you and Games for them. Search there for a different game of yours, or choose **Add … as a new game** at the top of the list to add a separate entry. The box then shows the game with a **+** in front; click the **✕** to search again.

- If the game's session tracking is off, the hours are added to its **Hours Played** instead.
- If you haven't started the game yet (for example it's **Imported**), it moves to In Progress, starting on the session's date.
- If you've finished the game (Completed or DNF), it moves back to In Progress. To keep a finished playthrough as it is, choose **Add … as a new game** instead.

The line under the title tells you which of these will happen before you save.
- If you don't have the game, or choose to add it as new, it's added to your FrogLog as In Progress, with session tracking on.

You can mirror each session once. Afterwards the button shows a tick.

A mirrored session can't be mirrored back. When someone mirrors your session, their copy tags you, and you'll get a notification for it, but there's no mirror button on it. The same goes for any other copy of a session you've already mirrored.

## Viewing and editing sessions

Click **View Sessions** on the details card to see every session for the game, with its date, hours and notes. On a wide screen, the sessions show under the details card instead.

Each session has buttons to:

- **Show to public / Hide from public**: whether other users can see this session. Other users only see sessions at all if the game has **Public Sessions** turned on.
- **Mark as spoiler**: hides the notes behind "Note may contain spoilers. Click to reveal anyway." ("Spoilers inside. Tap to reveal." on a phone).
- **Edit** or **Delete** the session.

![The sessions table, showing the visibility, spoiler, edit and delete buttons on a row](/assets/fl-library-sessions/sessiontable.webp)

## Quick Session

Quick Session is a stopwatch for when you're about to play.

1. Select a game and click the **Quick Session** button (the timer icon) on its details card. You can also right-click a game in your Games list, or press and hold it, and choose **Quick Session**.
2. A bar with the game's name and a running timer appears at the top of the page. It keeps running if you close the tab or switch devices, so you can start it on your phone and stop it on your computer.
3. To take a break, click **Pause** in the bar. The timer stops until you click **Resume**, and paused time doesn't count towards the session's hours.
4. When you're done, click **Stop** and choose:
   - **Auto Save** saves the session straight away with the note "Session auto submitted with Quick Session".
   - **Manual** lets you add notes, tick **Contains spoilers** or **Hide from public**, then click **Save Session**.
   - **Discard** throws the session away. Click it twice to confirm.

![The Quick Session bar at the top of the page](/assets/fl-library-sessions/quicksessiontoolbar.webp)

You can only run one Quick Session at a time.

Quick Session also works for games without session tracking: the time is simply added to the game's **Hours Played**. **Manual** isn't available for those games, since there's no session to attach notes to.

While a Quick Session is running, you show as playing that game in Online Now on the [Activity](/social/activity) page. You drop off Online Now while it's paused.

### Without a connection

Quick Session keeps working if you lose your connection. You can start, pause, resume, stop and discard a session as usual, and a **No connection** bar shows at the bottom of the screen.

FrogLog keeps those changes on your device, even if you close the app, and sends them once you're back online. Each one keeps the time it really happened, so a session played entirely offline logs the same hours as one played online. It's dated by the day you stopped it, even if it's sent the next day. A message confirms once your sessions have gone through.

If a change can't be saved when it's sent, for example because a different session was started on another device in the meantime, a notice appears in the Quick Session bar.

## Sessions recorded automatically

You don't have to log every session yourself. FrogLog can record them for you:

- **Automatic tracking** for Steam, PlayStation, Xbox and Nintendo Switch, turned on per platform in **Profile > Settings > Autonomous Tracking**. See [Platforms & Automatic Tracking](/platforms).
- **[LilyPad](/lilypad)**, FrogLog's desktop app, which detects games you launch on your PC.

Use only one of these for any given game. Running two at once can log the same session twice.
