# OPBR Skin Mods Installer

A Windows desktop app for installing, repairing and removing skin mods for
**ONE PIECE Bounty Rush**. Built by **MedoIQ** with Python + PySide6.

> **Safety first:** download this tool only from MedoIQ's Discord server.
> Reuploads can contain malware. Mods are unofficial and you use them at your
> own risk — keep backups of your game data.

- Discord: [discord.gg/s42FR9pabQ](https://discord.gg/s42FR9pabQ) (`@medoiq`)
- Donate (Binance Pay): **1273526111** (`MedoIQ-OPBR`)

## Features

- **Browse** — live mod feed with thumbnails, search, character filter and sorting.
  Install, Fix or Uninstall any mod in one click.
- **Installed Mods** — manifest-backed library that verifies every installed file
  (size, SHA-256 and modification date). Corrupted or manually edited mods get a
  yellow ring and a one-click **Fix**.
- **Manual Install** — drag & drop (or pick) a `.zip`. The app detects `.unity3d`
  payloads with or without a `mod/` folder, reads a bundled preview image, and
  supports `original/` archives that restore vanilla assets. Files that do not
  exist in your game version are skipped with a warning instead of failing the
  whole install.
- **Settings** — six languages (English, Japanese, Spanish, French, Thai, Arabic
  with RTL), automatic game-folder detection (global/JP), a custom folder option,
  Steam launch, temp/cache cleanup, animations toggle and About/credits.
- **Safety** — every install is recorded in a persistent manifest and a dated
  change log. Uninstall removes only the files the app installed and lets the game
  re-download the originals. **Force Purge** is available when a mod was corrupted.

## Run from source

```powershell
cd "mods installer"
python -m pip install -r requirements.txt
python run.py
```

Requires Python 3.11+ (developed on 3.14) and Windows 10/11.

## Build the .exe

```powershell
cd "mods installer"
.\build.ps1 -InstallDeps
```

The packaged app is written to `dist\OPBR Skin Mods Installer.exe`. It is a
single-file, windowed build (no console) and bundles `assets\app.ico` plus the
Binance QR image.

- `.\build.ps1` — rebuild with the current environment.
- `.\build.ps1 -Console` — keep a console window for troubleshooting.

## Project layout

```
opbr_mods/
  config.py        config, user-data paths, temp/cache helpers
  constants.py     app identity, feed URL, Steam App ID, donation info
  feed.py          live feed download + parsing + thumbnail caching
  install.py       archive mapping, manifests, install/verify/uninstall/restore
  i18n.py          six bundled languages
  main.py          application bootstrap
  main_window.py   frameless shell, sidebar, first-run wizard
  paths.py         game-folder detection
  steam.py         Steam launch helper
  ui/              theme, widgets, pages and dialogs
assets/            app icon and Binance QR
tools/             smoke tests, screenshot renderer, asset builder
```

## Data locations

| What | Where |
| --- | --- |
| Config, manifests, logs | `%APPDATA%\MedoIQ\OPBRModsInstaller\` |
| Temp downloads / extracts | `%TEMP%\OPBRModsInstaller\` |
| Game assets (global) | `%USERPROFILE%\AppData\LocalLow\Bandai Namco Entertainment Inc_\ONE PIECE BountyRush\StreamingAssets\assets` |
| Game assets (JP) | `%USERPROFILE%\AppData\LocalLow\Bandai Namco Entertainment Inc_\ONE PIECE BountyRush JP\StreamingAssets\assets` |

Use **Settings → Game Folder** to auto-detect the installation or pick the
`StreamingAssets\assets` folder manually.

## Tests

```powershell
$env:QT_QPA_PLATFORM = "offscreen"
python tools\smoke_test.py
python tools\render_shots.py screenshots
```

The smoke test exercises archive mapping, install/verify/tamper/missing,
uninstall, restore archives, feed parsing, every page, search and Arabic RTL.

## Credits

- **Author:** MedoIQ — Discord `@medoiq`
- Unofficial fan tool. Not affiliated with Bandai Namco Entertainment or Steam.
- ONE PIECE and its characters belong to Eiichiro Oda / Shueisha / Toei Animation.
