---
leafwiki_id: fl-lilypad-linux
---
# LilyPad for Linux

The Linux version of LilyPad is a native GTK app. It does everything the [Windows version](/lilypad/windows) does, with the same menus and settings, so this page only covers what's different.

## Installing

Download the package for your system from the [latest release](https://github.com/oligray27/lilypad/releases/latest):

| Package | For | Install with |
|---|---|---|
| `lilypad-gtk_<version>-1_amd64.deb` | Ubuntu 24.04+, Debian 13+ and derivatives | `sudo apt install ./lilypad-gtk_*.deb` |
| `lilypad-gtk-<version>-1.x86_64.rpm` | Fedora 40+ and derivatives | `sudo dnf install ./lilypad-gtk-*.rpm` |
| `LilyPad-x86_64.AppImage` | Any other distribution with glibc 2.39 or newer | `chmod +x LilyPad-x86_64.AppImage`, then run it |

LilyPad needs GTK 4.12+ and libadwaita 1.5+. The `.deb` and `.rpm` install these for you, and the AppImage includes them.

LilyPad adds itself to your login items the first time it runs.

## The tray icon

- **KDE Plasma** shows the tray icon straight away.
- **GNOME** needs the [AppIndicator and KStatusNotifierItem Support](https://extensions.gnome.org/extension/615/appindicator-support/) extension for any tray icon. Without it, LilyPad opens its window every time it starts instead, and the **⋮** menu in the window has everything the tray menu would.

## Proton games

Windows games running through Proton are recognised by their `.exe`, the same as on Windows.

## Updating

When a new version is out, you get a notification with a **Download** button, and the tray menu shows **Update to (x.y.z)…**. Both open the release page, where you download the package for your system and install it over the top.

## Using it with Steam Deck Gaming Mode

On a Steam Deck or Bazzite, you can use the Linux app in Desktop Mode and the [Decky plugin](/lilypad/steam-deck) in Gaming Mode. They share one login, one set of game links and one history, and only one tracks at a time. A game that's running when you switch modes carries on as the same session.

## Known limitations

- **Flatpak Steam:** only games you've already linked in Configure are tracked. Unlinked games aren't picked up as New Games.
- **Window title filters** only work for games running under X11 or XWayland.
- **No notification service:** sessions are submitted automatically without the chance to add notes. You can add notes afterwards on the FrogLog website.

## Upgrading from LilyPad 0.5

The first time a newer version starts, it brings across your pending sessions and New Games. Older versions didn't record which account a session belonged to, so those sessions appear in **Pending Submissions** under *From an earlier LilyPad version*. Choose **Assign to me** or **Discard** for each.

You can't go back to 0.5 after upgrading.

## Where LilyPad keeps its data

`~/.local/share/froglog-lilypad/`. It holds your login, game links, and any sessions not yet sent.
