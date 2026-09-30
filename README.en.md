# NeoCD SD Manager

**[Português](README.md)**

**Windows app that gets the SD card of your Neo Geo CD (Neo CD SD Loader — BR Edition) ready in a few clicks: it installs the menu, gives every game its proper name and makes the cover of each one.**

A project of the **[Maniaco Game Room](https://www.maniacogameroom.com.br/)** blog.

![Game list with the cover next to it](imagens/menu-lista-capa.png)

## How it works

Put the SD card in the PC with the games already on it, open the app and click **Prepare card**. It:

1. **installs the BR Edition menu** on the card (copies the update file and verifies the copy);
2. **organizes the game names:** identifies each folder by name (and, if you want, by disc content, against the Redump database) and renames it with the proper title, e.g. `metal_slug_2 [!]` → `Metal Slug 2`;
3. **makes the cover of each game** (`bg.bmp`), ready for the console, using your own images or downloading them.

![App](imagens/app-preparar-en.png)

| | |
|---|---|
| ![Games and covers](imagens/app-jogos-en.png) | ![Cover on the console](imagens/menu-capa.png) |

- **Nothing is deleted:** old names can be restored (**Undo last** button) and whatever is replaced on the card goes to the `_neocd-manager` folder.
- **Faithful preview:** click a game to see its cover as the console will show it (reduced colors, same palettes).
- **Portuguese or English:** **Idioma / Language** menu, plus window color themes.

## How to use

1. Download **`NeoCD-SD-Manager.exe`** from the **[Releases](../../releases)** page.
2. Put the card in the PC (formatted as **FAT32**), with each game in its own folder containing the `.cue` file.
3. Open the app, choose the card and click **Prepare card**.
4. Put the card in the console and power it on.

Full walkthrough with every option: **[App manual](MANUAL.en.md)**.

## Requirements

- Neo Geo CD with the **Neo CD SD Loader** installed (Furrtek's mod kit).
- Windows 10 or 11.
- **FAT32** SD card, with up to **200 games** (a menu limit).
- Internet the first time (name and cover databases are downloaded and kept on the PC).

## Notice

This project **does not provide games or BIOS files**. The bundled menu update file (`NSDL0014.WAD`) is free software (GPL) based on Furrtek's Neo CD SD Loader and only holds the loader's patches, not the console BIOS; the source code is at [NeoCDSDLoader-BR-Edition](https://github.com/maniaco007/NeoCDSDLoader-BR-Edition). This project is not affiliated with SNK or Furrtek. Use at your own risk.

## Credits

- Neo CD SD Loader (original hardware, firmware and menu): **Furrtek** — [furrtek.org/sdloader](http://www.furrtek.org/sdloader/)
- Box art: [libretro-thumbnails](https://github.com/libretro-thumbnails)
- Game databases (Redump): [libretro-database](https://github.com/libretro/libretro-database)

## License

**Freeware — free to use. © 2026 Maniaco Game Room. All rights reserved** (except the menu update file, which is GPL). See the [license](LICENCA.md) and the [third-party components](TERCEIROS.md).

Found a problem? Open an [Issue](../../issues).
