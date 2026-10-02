---
leafwiki_id: fl-platforms-playstation
---
# PlayStation

Linking your PlayStation Network (PSN) account lets FrogLog import your PlayStation history, track your PS4 and PS5 sessions automatically, and show your trophies.

## Linking

Sony doesn't offer a "sign in with PlayStation" button for other sites, so linking uses a token from your PlayStation login called an **NPSSO token**.

1. Open your **Profile** and click **Link PSN**.
2. In the same browser, sign in at [playstation.com](https://www.playstation.com).
3. Then open [ca.account.sony.com/api/v1/ssocookie](https://ca.account.sony.com/api/v1/ssocookie). The page shows a short piece of text containing `"npsso"` followed by a long code.
4. Copy the code and paste it into the **NPSSO token** box in FrogLog. You can paste the whole page's text instead and FrogLog picks out the code for you.
5. Click **Link**.

The button now shows your PSN name and avatar.

> **[Screenshot]** The Link PSN Account dialog with its three steps.

Treat the NPSSO token like a password. FrogLog stores the access it grants encrypted, and only uses it to read your games, trophies and what you're playing.

## Re-linking

PlayStation's access expires after about two months. When that happens:

- The button on your profile changes to **Relink PSN**, and **Import** is unavailable.
- Automatic tracking and presence pause for PlayStation.

Click **Relink PSN** and repeat the steps above with a fresh token. Your settings carry on where they left off.

## Importing

1. Click the **Import** button next to your PSN name.
2. Optionally, set **Only import games played for at least** a number of hours.
3. Start the import, then choose what to do with any games you already have. See [Importing](/platforms).

## Automatic tracking

Turn on **Automatic PSN Session Tracking** in **Profile > Settings > Autonomous Tracking > PSN**. Games you play that aren't in your library are added automatically. See [How it works](/platforms).

This only works for console play on PS4 and PS5. PlayStation doesn't report what you're playing on PC, even for PlayStation games on PC linked to your account.

To show what you're playing without logging sessions, use **Mirror PSN In-Game Presence to FrogLog** instead.

## Trophies

Games linked to PlayStation show their trophies, including which you've earned. See [Trophies](/library/trophies).

## Unlinking

Click the **Unlink** button next to your PSN name. Games and sessions already in your library are kept.
