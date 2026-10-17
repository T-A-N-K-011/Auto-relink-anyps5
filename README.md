# Relinker Runner

A single double-click `.bat` file that converts a game's `eboot.bin.esbak` into a Windows executable (`app.exe`) using `relinker`.

When you open `relink.bat` it looks for a `source` folder next to it:

- **No `source` folder found** → prints an error and stops.
- **`source` folder found** → it does *not* enter the folder; it runs the commands from the parent folder:

```powershell
Copy-Item ".\source\eboot.bin.esbak" ".\source\input.elf"
.\relinker-v0.1.2.exe --windows source\input.elf app.exe
```

(The `.bat` uses the equivalent `copy` command, so no PowerShell or execution-policy setup is needed.)

---

## ⚠️ Legal notice

**You must legally own the game.** This project does not include, distribute, or help you obtain any game files. Use it only with a copy of a game that you personally own. You are responsible for complying with the laws in your country and with the license terms of the game and of any tools you use.

---

## Requirements

You **must** download all of the following:

1. **exFAT Image Builder**: https://github.com/kerrdec97/ps5-exfat-builder
2. **AnyPS5 PRX package (Windows)**: [prx-windows-v0.1.2.zip](https://github.com/boykopovar/AnyPS5/releases/download/v0.1.2/prx-windows-v0.1.2.zip) (release page: https://github.com/boykopovar/AnyPS5/releases/tag/v0.1.2)
3. **relinker**: [relinker-v0.1.2.exe](https://github.com/boykopovar/AnyPS5/releases/download/v0.1.2/relinker-v0.1.2.exe)
4. **A game you own**, in **exFAT** format.
5. **Windows**.

## 🎬 Video Tutorial

Watch the full tutorial for this tool here: **https://gofile.io/d/kVDY6oyP**

## Setup

### Step 1: Extract the game with exFAT Image Builder

1. Open **exFAT Image Builder**.
2. Go to the **Extract** tab.
3. Select your game's **exFAT image** and **extract** it.
4. Extract the output **into a folder named `source`** (create it first if needed). When it finishes, `source` should contain the game files, including `eboot.bin.esbak`.

### Step 2: Download the AnyPS5 PRX package

5. Download [`prx-windows-v0.1.2.zip`](https://github.com/boykopovar/AnyPS5/releases/download/v0.1.2/prx-windows-v0.1.2.zip) and **extract it next to the `source` folder** (same parent folder, not inside `source`).

### Step 3: Create `app0`

6. Create a new folder named **`app0`** next to the `source` folder.
7. **Copy** (don't move) everything that is inside `source` into `app0`.

### Step 4: Add relinker and the runner

8. Download [`relinker-v0.1.2.exe`](https://github.com/boykopovar/AnyPS5/releases/download/v0.1.2/relinker-v0.1.2.exe) and put it next to the `source` folder.
9. Put `relink.bat` next to the `source` folder as well.

## 🎮 Game Testing / Compatibility

Results from testing games with this tool. Only games the tester legally owns should be reported.

| Game | Version | Status | Notes | Tested by |
|---|---|---|---|---|
| Dreaming Sarah | - | ✅ Works | Tested by the author with `relink.bat` | Maintainer |
| The King is Watching | - | ✅ Works | Tested by the author with `relink.bat` | Maintainer |

**Status legend:** ✅ Works · ⚠️ Partial (runs with problems) · ❌ Doesn't work

### Tested a game?
[Open a game test report](../../issues/new?template=game-test-report.md) and include the game name, version, result, and the text from the `relink.bat` window. Confirmed results get added to the table above.

## Expected folder layout

```
MyGame/
├── source/
│   └── eboot.bin.esbak          (+ the rest of the game files)
├── app0/
│   └── ...                      (a copy of everything inside source)
├── (extracted contents of prx-windows-v0.1.2.zip)
├── relinker-v0.1.2.exe
└── relink.bat
```

## Usage

Double-click **`relink.bat`**. The window stays open at the end so you can read the result.

To run it on a different folder, open `cmd` and pass the path:

```bat
relink.bat "D:\Games\MyGame"
```

## What it does

1. Checks that the folder exists.
2. Looks for a `source` folder. If it is missing, it shows an error and stops.
3. Looks for `source\eboot.bin.esbak`. If it's missing, it looks for `source\eboot.bin` instead. If neither exists, it shows an error and stops.
4. Checks that `relinker-v0.1.2.exe` exists.
5. Copies the file it found (`eboot.bin.esbak` or `eboot.bin`) to `source\input.elf`.
6. Runs `relinker-v0.1.2.exe --windows source\input.elf app.exe`.
7. `app.exe` is created in the same folder.

## Troubleshooting

| Problem | Fix |
|---|---|
| `No "source" folder found` | Put `relink.bat` in the folder that *contains* `source`, not inside `source`. |
| `Neither eboot.bin.esbak nor eboot.bin was found` | Re-check that you used the **Extract** tab in exFAT Image Builder and extracted the image *into* the `source` folder. |
| `relinker-v0.1.2.exe was not found` | Download it from the Requirements section and put it next to the `source` folder. |
| Missing PRX files / `app0` problems | Re-check Setup: the zip must be extracted next to `source`, and `app0` must contain a copy of the files from `source`. |

## Credits

- [exFAT Image Builder](https://github.com/kerrdec97/ps5-exfat-builder) by kerrdec97
- [AnyPS5](https://github.com/boykopovar/AnyPS5) by boykopovar (PRX package and relinker, v0.1.2)
