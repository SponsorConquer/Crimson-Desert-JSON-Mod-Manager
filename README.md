
# Crimson Desert — JSON Mod Manager

## ![⬇️ Download Latest Release](https://github.com/SponsorConquer/Crimson-Desert-JSON-Mod-Manager/releases/download/ModManager/JSON.ModManager.V10.0.zip)


<img width="1483" height="789" alt="2" src="https://github.com/user-attachments/assets/8a4c3240-fc2d-4cf3-9a47-5939c2ca8c6b" />


A standalone mod manager for Crimson Desert that applies byte-level patches to game files using a safe overlay system. No game files are permanently modified — all changes go into a separate overlay directory that the game loads on top of the originals.

## Features

- Single MSI — just double-click `mod_manager.msi`, no Python or other dependencies required
- Dark-themed 3-panel GUI: Available Mods → Active Mods → Per-Patch Toggles
- Per-patch control — enable or disable individual changes within a mod
- Color-coded categories
- Automatic Steam game directory detection
- One-click Apply / Uninstall
- Automatic backup of original `0.papgt` before any changes
- One-click Restore from backup
- Safe overlay system — original game files are never touched

## How It Works

The mod manager uses an overlay system. Instead of modifying the game's original PAZ archives, it:

1. Reads the original compressed game files from `0008/`
2. Decompresses them (LZ4), applies your chosen byte patches, and recompresses
3. Writes the patched files into a new overlay directory (`0036/`)
4. Registers the overlay in `meta/0.papgt` so the game loads patched files on top of originals
5. Uninstalling simply removes the overlay and restores the original `0.papgt` from backup.

## Installation

1. Download and extract the archive anywhere on your PC
2. Double-click `mod_manager.msi`
3. The GUI will auto-detect your Crimson Desert install (Steam). If not found, click **Browse** to set it manually
4. Select the mods you want from the left panel, activate them with the arrow button
5. Toggle individual patches on/off in the right panel if desired
6. Click **APPLY**
7. Launch the game

## Uninstalling Mods

Click **UNINSTALL** in the mod manager — this removes the overlay directory and restores your original `0.papgt`. Your game is back to 100% vanilla.

Alternatively, click **RESTORE** to restore the backed-up `0.papgt` directly.


## Requirements

- Crimson Desert (Steam)
- No Python, no .NET, no other dependencies — everything is bundled in the MSI

---

## ⚠️ Important Notes

> **Before using:** Create a manual backup of your `0.papgt` file. While extensively tested, unexpected issues may occur.

### Understanding Overlap

Overlap is **informational only** — it visually shows which files are targeted by multiple mods. Overlap does **not** automatically mean one mod overwrites another. When multiple mods target the same file **and** the same entries, the mod with the higher ID (lower in load order) takes precedence. JSON mods are entry-based, not file-based.

### Troubleshooting

#### If JSON Mod Manager is not working:

1. Remove all numeric folders `>0036` (including `0036`) from your game directory — keep `0035` as the last original folder. Do **not** delete `bin64`
2. Go to Steam and verify game files
3. Copy your mods folder to another location as backup
4. Remove everything from the manager folder, leaving only the `.msi` file
5. Run the JSON mod manager — it will generate fresh config files
6. Drag and drop your mods into the mod folder (folders starting with `_` will be ignored)

#### "Failed: Access problem"

Your game is likely on your system drive. Run the manager with **Administrator privileges**.

#### RAW mods causing crashes

Test the mod alone first. Try turning **off** "Encrypt Overlay output" in the patches field (enabled by default).

---

## Changelog

### Update 10.0

- Added Language mods support — there is now new tab "Language mods" (do not install language mods to Data mods tab). Drop your language mod there, select your current language in game — manager will target the specific language folder you selected
- Added experimental value change for JSON mods — on the right side of the JSON mod is a new icon that allows changing values. Be careful with this; wrong values can cause crashes or unexpected behavior (like division by zero)
- Added remove button for available tab — it will remove the mod from the mod folder

### Update 9.01

- Data in changelog

### Update 7.5

- Added support for Crimson Browser mods (Experimental)
- Fixed PAZ replacement — experimental, be careful as it replaces entire files. Manager makes a copy, but in some cases issues may occur requiring verification
- Added Load order control
- Added compiled file merging — when multiple files target the same file, manager extracts data from the original file, compares, and merges into one. Load order should work but needs more feedback

### Update 7

- UI improvements:
    - Added Start Game button
    - Added folding categories for better JSON management
    - Added search field
- Now clicking "Apply mods" scans game directory, removes all old mod folders, and reinstalls clean with new IDs (fixes common issue where multiple folders with different JSON versions were both being applied)

### Update 6

- Overall improvements
- MAJOR: Now you can mix JSON mods and precompiled ones (those with `0036` and `meta`). Make sure to put them into one folder — example: in `mods` folder create `MODNAME` folder and put `0036` and `meta` there
- Not tested: Should now work with raw data if paths are correct

Instead of pushing everything to `0036`, manager now scans where original game folders end and creates new ones — better for future official DLCs and resolves conflicts between mods as each mod now has its own folder (JSONs are compiled and put into one folder)

### Update 4.1

- Improved Stability
- Added JSON detection — previously only targeting `0008` folder, now detects which archive to patch
- Added experimental folder support with the following structure:

