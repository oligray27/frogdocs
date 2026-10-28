---
tags: []
leafwiki_id: fl-library-editing-games
leafwiki_title: Editing Games
leafwiki_created_at: "2026-10-02T10:38:03.215495847Z"
leafwiki_updated_at: "2026-10-02T14:10:25.949715347Z"
leafwiki_creator_id: system
leafwiki_last_author_id: 6AZN8grDR
---
# Editing Games

To change anything about a game, select it and click **Edit** on its details card. The **Edit Game Details** form has the same fields as when you [added it](/library/adding-games), plus a few more.

![The Edit Game Details form](/assets/fl-library-editing-games/editgamedetailsform.webp){width=50%}

## Status

A game's status is worked out from its dates, unless you set it yourself:

| Status | When a game has it |
|---|---|
| **Not Started** | No start date and no end date |
| **In Progress** | A start date but no end date |
| **Completed** | An end date, or the status is set to Completed |
| **DNF** | The **DNF** box is ticked |
| **Dormant** | The status is set to Dormant |
| **Imported** | Imported from a platform with no dates yet |

For a game with session tracking, the **End Date** picker has a **Set to last session date** button, which fills in the date of your most recent session.

### Setting the status yourself

**Game Status (Override)** has three options:

- **Auto** (the default) works the status out from the dates, as in the table above.
- **Completed** marks the game as finished without needing an end date. Useful for games you finished long ago and don't remember when.
- **Dormant** marks a game you've put down but might come back to. It stops counting as In Progress.

The override and **DNF** can't both be on. Ticking one greys out the other.

## Rating

Ratings are one to five stars, in half-star steps. If you prefer a 0–100 percentage, switch **Profile > Settings > Display & Layout > Default Rating Mode** to **%**. The edit form then shows a number box and a **Clear** button.

Both modes store the same rating, so switching back and forth doesn't change anything.

## Review

Write your review in **Your Review**. It appears on the **Your Review** tab of the details card, and other users can read and [like](/social/likes) it if the game is public.

To hide a spoiler, wrap it in double pipes: `||Aerith dies||`. Readers see a blurred block until they click it.

## Fields only in the edit form

| Field | What it's for |
|---|---|
| **Cover Image URL** | The cover art used in grid view, lists and elsewhere |
| **Launch via Steam** | Adds a **Play** button to the details card that opens the game in Steam. Paste the `steam://rungameid/…` link from a Steam desktop shortcut (in Steam, right-click the game and choose **Manage > Add desktop shortcut**, then copy the shortcut's URL), or just its number. This works for non-Steam games you've added to Steam too. For a game you own on Steam, it's already filled in with that version. See [Steam](/platforms/steam). |
| **Platforms** | Add or remove platforms. Changes save straight away. |
| **Fix Match** | Tells FrogLog which game this entry really is, for example when you move from a demo to the full game or a game was added as the wrong title. Pick the right game from the search and its details replace the entry's (your hours, sessions, dates, rating and review stay). If its Steam version is different, you can choose whether to switch the entry's Steam link too. Click **Save Changes** to keep it. |
| **Merge Into…** | Folds this entry into another game in your library and deletes it, for example a beta into the full game. Its sessions move across as they are (dates, notes and likes included), along with its hours, screenshots, clips, pinned trophies and list places. The game you merge into keeps its own details and fills any blanks from the merged one, and the earlier start date wins. If LilyPad was tracking the merged entry, it lists that game under [New Games](/lilypad/new-games) the next time you play it, so you can map it to the kept one. |
| **Fetch Missing Data** | Fills in any empty fields (description, genre, developer, release date and artwork) from the game's database entry. Fields you've already filled in are left alone. Click **Save Changes** afterwards to keep them. |
| **Hide HLTB** | Hides the HowLongToBeat badge on this game's details card, for example if it shows the wrong game's times |
| **Hide Metacritic** | Hides the Metacritic badge on this game's details card |

## Turning session tracking on or off

**Enable Session Tracking** switches a game between one total of hours and a log of individual [sessions](/library/sessions).

- **Turning it on** creates a first session called "Pre-tracked hours" holding the game's current hours, so your total doesn't drop to zero.
- **Turning it off** deletes every session. Their combined total is copied into **Hours Played** first, so you keep the hours but lose the individual entries.

The form warns you before either happens.

## Syncing missed playtime

If you played somewhere FrogLog couldn't see, such as Steam in offline mode, **Sync Playtime** compares your total playtime from somewhere else with what FrogLog has, and adds the difference.

Click **Sync Playtime** next to **Hours Played** in the edit form. If there's more than one place to sync from, it opens a menu:

- **via Steam**, **via PlayStation** or **via Xbox**: for a game with one of these platforms, fetches that platform's total. A game with more than one of them shows one option for them all (such as **via Steam & PlayStation**), because their totals are added together.
- **via Custom Source**: for any game. Type in your total from anywhere else, such as the game's own stats screen. Only include hours for the playthrough you're editing, because it's compared with that playthrough's hours alone.

A Sync Playtime section opens below Hours Played. If the other total is higher, click **Add ... and Save** to add the extra time and save your changes, the same as **Save Changes**:

- For a game with session tracking (and live service games), it's logged as one "Playtime sync" session with no date, since the time could have been played on any number of days. It counts towards your hours but not the session heatmap or per-day stats.
- For other games, it's added to **Hours Played**.

When syncing via Steam, PlayStation or Xbox for a replay, FrogLog's side counts every playthrough of the game by default, because those platforms only keep one total across all of them. If your other playthroughs were somewhere else, untick **Include my other playthroughs** to compare with this playthrough only.

A platform's total only covers play on that platform. PlayStation counts PS4 and PS5 only, and Steam needs your game details set to public. If FrogLog already has as much time as the platforms (or more), there's nothing to add.

## Privacy

Untick **Public** to hide a game from other users. Private games show a padlock in your library. A private game's sessions are always private too.

## Deleting a game

Click **Delete** at the bottom of the form, then **Confirm?**. This removes the game and all its sessions, and can't be undone.
