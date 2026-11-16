# Project Midas: Xbox Series X|S (UWP)

An Xbox Series X|S port of [Project Midas](https://github.com/murkantor/Project-Midas), the PC port of GE built from the N64 decompilation. It runs as a UWP app in the console's Developer Mode and reads its game data from your own copy of the US cart.

This is a **beta**. It is based on Project Midas 1.0.2b.

## What works

- Every solo mission, the attract demos, saving, and full sound and music.
- Midas's controller system: layouts, rebinding, dead zones, rumble, hot-plugging.
- All of Midas's Video options: resolution, display mode, MSAA, texture filtering, mipmaps, anisotropy, VSync, Max FPS, Classic Mode / N64 AA, composite.
- The 1.0.2b options, including FPS Counter, Mute in Background and Background Input (the Guide overlay counts as "in the background").
- Loading the cart image from the app's `Data` folder or from a USB drive.

## Requirements

- An Xbox Series X or Series S in **Developer Mode** (needs a Microsoft Partner Center developer account; see Microsoft's [Xbox Developer Mode](https://learn.microsoft.com/windows/uwp/xbox-apps/devkit-activation) guide).
- Your own GE (USA) cart image (`.z64`, `.n64` or `.v64`). The app checks it and names it in the log as `stock GoldenEye 007 (U)`.
- A PC on the same network, to install the package through the Xbox Device Portal.


## Installing

### On Xbox

1. On the console, open **Dev Home**, turn on **Remote Access**, and note the Device Portal address.
3. In a browser on your PC, open the Device Portal and go to **Home > My games & apps > Add**.
4. Choose `MidasUwpShell_<version>_x64.msix`. When asked for dependencies, add `Dependencies\x64\Microsoft.VCLibs.x64.14.00.appx`.
5. Start **Project Midas UWP Shell** from Dev Home or **My games & apps**.

## Your cart image

On the start screen, pick one of:

| Option | What it does |
| --- | --- |
| **SELECT ROM FOLDER** | In-app browser for internal and USB drives. |
| **USE THE DATA FOLDER** | Uses the image in the app's `LocalState\Data` folder. Copy it there with the Device Portal's File Explorer. |
| **WINDOWS FOLDER PICKER** | The system folder picker. |

The app remembers your choice, and later starts go straight into the game.

USB drives: the folder must be readable by the app. If the in-app browser lists your `.z64` but says it is not an N64 cart, check the folder's permissions on the console, or use **WINDOWS FOLDER PICKER**.

Browser controls: **A** select, **B** back, **X** allow drive access, **Y** parent folder, **LB/RB** page, **D-pad** move.

## Files

Everything lives in the app's `LocalState` folder. On Xbox, reach it through the Device Portal's **File Explorer**, under the app's folder.

| Path | What it is |
| --- | --- |
| `midas.ini` | Settings, the same format as PC Midas. Delete it to restore the defaults. |
| `Data/` | Your cart image, if you use the Data folder. |
| `Data/Saves/eeprom.bin` | Save file. A Project64 `.eep` save renamed to `eeprom.bin` is converted on load. |
| `Data/Logs/engine.log` | The game's log. **Attach this to bug reports.** |
| `Data/Logs/shell.log` | The start screen's log (cart image selection). |


No cart image or game data is needed to build. The game reads everything from your cart image at runtime.

## Known issues

- Bullet holes near a wall's edge can overhang into the air.
- A few guards don't spawn in some levels (for example one each in Facility and Silo). The original game skips the same guards.
- The 007 intro runs at 30 fps and the attract demos at 17 to 40 fps. PC Midas does the same.
- VSync off can't go above the TV's refresh rate (a UWP limit).
- The Line Mode cheat hasn't been tested yet.

Planned: a Direct3D 12 renderer, with Direct3D 11 kept as a fallback.

## Reporting bugs

Please open an issue with:

- the package version (bottom right of the start screen);
- the level and what you were doing;
- a clip or screenshot if you can;
- `Data/Logs/engine.log`.

Check whether PC Midas 1.0.2b does the same; if it does, report it to the PC port instead.

## Credits

- [Project Midas](https://github.com/murkantor/Project-Midas) by murkantor and contributors: the PC port this is built on, and everything listed in its readme.
- [GoldenEye decompilation](https://github.com/n64decomp/007) by KholdFuzion and contributors.
- [Fast3D renderer](https://github.com/Emill/n64-fast3d-engine) by Emill and MaikelChan (MIT); this port adds a Direct3D 11 backend.

## License

The port code follows Project Midas's license (MIT, see [LICENSE](LICENSE)). The license does not cover the decompiled game code, GE itself or its assets.

GE is owned by Rare, Nintendo and the Bond rights holders. This project contains no game assets.
