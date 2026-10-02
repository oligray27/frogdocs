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
| **Platforms** | Add or remove platforms. Changes save straight away. |
| **Fetch Missing Data** | Fills in any empty fields (description, genre, developer, release date and artwork) from the game's database entry. Fields you've already filled in are left alone. Click **Save Changes** afterwards to keep them. |

## Turning session tracking on or off

**Enable Session Tracking** switches a game between one total of hours and a log of individual [sessions](/library/sessions).

- **Turning it on** creates a first session called "Pre-tracked hours" holding the game's current hours, so your total doesn't drop to zero.
- **Turning it off** deletes every session. Their combined total is copied into **Hours Played** first, so you keep the hours but lose the individual entries.

The form warns you before either happens.

## Privacy

Untick **Public** to hide a game from other users. Private games show a padlock in your library. A private game's sessions are always private too.

## Deleting a game

Click **Delete** at the bottom of the form, then **Confirm?**. This removes the game and all its sessions, and can't be undone.
