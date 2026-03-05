# BO3 Mod Merger

Merge multiple Call of Duty: Black Ops III mods into one. BO3 only loads a single mod at a time—this tool combines 2+ mods so you can run them together (e.g. whitelist + HUD + custom map).

---

## Features

| Feature | Description |
|---------|-------------|
| **Merge mods** | Combine 2+ mod folders into one output mod. Zone files and scripts are merged automatically. |
| **Decompile Workshop mods** | Extract scripts from compiled `.ff` files using Cerberus or HydraX + gsc-tool. |
| **Asset extraction** | Open Greyhound or GDTExtractor from the GUI to extract models, sounds, and GDT assets. |
| **Conflict handling** | When both mods override `_clientids.gsc`, callbacks are merged so both run. |
| **Copy stock _clientids.gsc** | Copy the game's base script to any folder. |

---

## Requirements

### To run the software

- **Windows** (tested on Windows 10/11)
- **Black Ops III** installed (Steam)
- **Black Ops III Mod Tools** (to build the merged mod in-game)
- **Mods with source files** (`scripts/`, `zone_source/`) — Workshop mods that only have compiled `.ff` files must be decompiled first

### To decompile Workshop mods

Place one of these **next to `BO3 Mod Merger.exe`**:

I dont take any credit for these tools that down here.
| Tool | Purpose | Download |
|------|---------|----------|
| **Cerberus** | Easiest — extracts and decompiles `.ff` in one step | [Releases](https://github.com/withmorten/Cerberus/releases) |
| **HydraX + gsc-tool** | Alternative — build HydraX from [source](https://github.com/Scobalula/HydraX-Original), get [gsc-tool](https://github.com/xensik/gsc-tool/releases) | — |

### To extract assets (models, sounds)

| Tool | Use | Download |
|------|-----|----------|
| **Greyhound** | Load mod's `.xpak` → export models, images, sounds | [Releases](https://github.com/Scobalula/Greyhound/releases) |
| **GDTExtractor** | Drag `.gdt` files onto it | [Repo](https://github.com/Scobalula/GDTExtractor) |

---

## Installation

### Option A: Download the .exe (no Python needed)

1. Download `BO3 Mod Merger.exe` from the [Releases](releases) page (or build it yourself).
2. Copy it to your BO3 `mods` folder (or any folder).
3. Place `DECOMPILED_MOD_MERGE_GUIDE.md` next to the exe if you want the "Open guide" button to work.
4. Double-click to run.

### Option B: Run from source (Python)

```bash
# Clone or download the repo
cd bo3_mod_merger

# Run the GUI (Python 3.8+ required)
python merge_gui.py
```

### Option C: Build the .exe yourself

```bash
cd bo3_mod_merger
pip install pyinstaller
build_exe.bat
```

The exe is created at `dist\BO3 Mod Merger.exe`.

---

## How to use

### Merge mods

1. Set **Mods folder** to your BO3 `mods` path (e.g. `C:\...\Steam\steamapps\common\Call of Duty Black Ops III\mods`).
2. Check 2+ mods.
3. Enter **Output mod name** (e.g. `zm_combined`).
4. Click **Merge Mods**.
5. Open **Mod Tools Launcher** → select the merged mod → **Build**.

### Decompile Workshop mod

1. Click **Decompile Workshop Mod** → read the disclaimer → Continue.
2. Select the Workshop mod folder (e.g. `mods\1234567890`).
3. Select files (check `.ff` for scripts; `.xpak`, `.mvk`, etc. are copied).
4. Choose **Decompile method:** Auto / Cerberus / HydraX+gsc-tool.
5. Set **Output folder**.
6. Click **Decompile / Copy selected**.

**Note:** Decompilation is not 100% reliable. Script-only mods work best. For full asset mods, use Greyhound to extract from `.xpak`.

### Copy stock _clientids.gsc

Use this to copy the game's base `_clientids.gsc` to a folder (e.g. your mod's `scripts/zm/gametypes/`).

---

## CLI usage

```bash
python merge_mods.py --mods zm_whitelist my_hud_mod --output zm_combined
```

Requires mod source folders. Works from the project directory.

---

## Project structure

```
bo3_mod_merger/
├── merge_gui.py          # GUI entry point
├── merge_mods.py         # Merge logic + CLI
├── gsc_merge.py          # GSC script conflict resolution
├── DECOMPILED_MOD_MERGE_GUIDE.md
├── build_exe.bat         # Build standalone .exe
├── BO3 Mod Merger.spec   # PyInstaller spec
└── requirements.txt      # Python deps (PyInstaller only for build)
```

---

## Limitations

- **Mods need source** — Workshop mods with only `.ff` must be decompiled first.
- **Decompile ≠ 100% reliable** — Can fail or produce broken scripts.
- **Script conflicts** — Only `_clientids.gsc` is auto-merged. Other conflicts use "first mod wins."
- **Don't re-upload** — Decompiled content is for personal use/learning only.

---

## References

- [Steam: How to load Multiple Mods?](https://steamcommunity.com/app/311210/discussions/0/343787920120382321/)
- [BO3 callbacks support multiple handlers](https://bo3explorer.zeroy.com/mp_2__callbacks_8gsc_source.html)
- [modme.co wiki – Zone structure](https://wiki.modme.co/wiki/Game-Support-_-Black-Ops-3.html)


