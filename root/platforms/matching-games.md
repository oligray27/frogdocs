---
leafwiki_id: fl-platforms-matching-games
---
# Matching Games

When an import or automatic tracking finds a game on Steam, PlayStation, Xbox or Switch, FrogLog has to work out which game in your library it is. This page explains how it decides, and how to fix it when it gets one wrong.

## Platform links

Each game in your library can be linked to one or more platforms. The details card shows a platform badge, and the edit form's **Platforms** field shows every link as a coloured chip.

A link to a real platform (Steam, PSN, Xbox or Switch) is how FrogLog recognises the game next time. Anything else you type, such as `Epic Games` or `PS5`, is a label for your own reference.

> **[Screenshot]** The Platforms field in the edit form, showing a Steam chip and a free-text chip.

## How FrogLog picks a game

When FrogLog sees you playing something, or imports a game, it looks in this order:

1. **A game already linked to that exact platform game.** If more than one matches, it prefers one that's In Progress, then Dormant, then Imported.
2. **An unfinished game with the same title** that isn't linked to a different platform yet, such as a game you added by hand. The new platform link is added to it.
3. **A game on your Up Next list**, which is moved to Games.
4. If nothing matches, **a new game** is added, with its details and cover art.

If the best match is already **Completed** or **DNF**, FrogLog doesn't reopen it. It starts a new playthrough linked to it as a [replay](/library/replays-and-dnf), and the platform link moves to the new playthrough.

FrogLog never quietly merges two different platforms onto one game by title alone. If you're playing the same playthrough on two platforms, choose **Add hours from [platform] to the latest entry** when importing (see [Importing](/platforms)) to combine them deliberately.

## Steam links when adding a game

When you add a game from Search that's on Steam, the Add New Game form offers a Steam chip, faded until you click it to confirm you're playing on Steam. That stops PC versions being linked when you're actually playing on console.

If you'd rather have Steam linked automatically, set **Profile > Settings > Library Defaults > Confirm Steam Links** to **Auto-link**.

## Fixing a wrong match

If sessions are landing on the wrong game, or a game shows a platform it shouldn't:

1. Open the game that has the wrong link and click **Edit**.
2. In **Platforms**, remove the chip for the platform that's wrong. The change saves straight away.

Next time that platform game is played or imported, FrogLog looks for a match again, following the order above. To steer it to the right game, make sure that game is unfinished and has exactly the same title.

If tracking created a duplicate game you don't want, delete it from its edit form. Its sessions are deleted with it, so note down anything you want to keep first. See [Editing Games](/library/editing-games).
