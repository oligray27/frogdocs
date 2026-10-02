---
leafwiki_id: fl-api
leafwiki_title: API & Integrations
leafwiki_created_at: "2026-10-02T11:47:09.405032296Z"
leafwiki_updated_at: "2026-10-02T11:47:09.405032296Z"
leafwiki_creator_id: system
leafwiki_last_author_id: system
---
# API & Integrations

FrogLog has a REST API, the same one the website and LilyPad use. You can use it to build your own tools: a Stream Deck button that starts a Quick Session, an iPhone Shortcut that logs a session, a dashboard widget, a script that backs up your library, and so on.

This section covers:

- **API keys** (this page): how to get one and keep it safe
- [Conventions](/api-and-integrations/conventions): base URL, request format, errors and rate limits
- [Homepage Widget](/api-and-integrations/homepage-widget): showing FrogLog on a gethomepage.dev dashboard
- [API Reference](/api-and-integrations/reference): every endpoint, grouped by what it does

## Creating an API key

1. Open **Profile > Settings > API Keys**.
2. Enter a **New Key Name** that tells you where it's used, for example "iPhone Shortcuts".
3. Click **Generate**.
4. Copy the key from the **New API Key** window. It starts with `flk_`.

**The key is only shown once.** If you lose it, revoke it and generate a new one.

> **[Screenshot]** The API Keys settings, with one key listed and the New API Key window open.

## Using a key

Send the key in the `Authorization` header of every request:

```
Authorization: Bearer flk_your_key_here
```

For example, to list your games:

```bash
curl https://api.froglog.co.uk/api/games \
  -H "Authorization: Bearer flk_your_key_here"
```

## Keeping keys safe

**An API key can do everything you can do when logged in.** It can read and change your library, post sessions, change your settings, and even delete your account. The only thing a key can't do is create more API keys.

- Treat a key like a password. Don't share it, post it, or commit it to a public repository.
- Use a separate key for each tool, so you can revoke one without breaking the others.
- Revoke keys you no longer use.

## Managing keys

Your keys are listed in **Profile > Settings > API Keys**, each with the date it was last used (or **Never used**).

To stop a key working, click **Revoke**, then **Confirm?**. Anything using that key stops working straight away.
