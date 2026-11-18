**English** | [简体中文](README.md)

# DOT — Directly Optimized TactileDots

Turns Chinese text into braille G-code that can go straight to a 3D printer. Built for Klipper and Bambu Lab platforms, with 214 printer profiles included.

Type text → preview the dots live → export G-code → send it to the printer.

---

## Download

**Get the latest build from [Releases](https://github.com/raymondzoufangzhen/DOT/releases/latest)**

| File | Notes |
|---|---|
| `DOTv1.2.exe` | Windows 10 / 11 (64-bit), about 17 MB |

Single-file portable build. No installer, no Python, no runtime libraries. Copy it anywhere and double-click.

> If Windows SmartScreen blocks the first launch, click *More info* → *Run anyway*. The executable is not code-signed, which is the normal prompt for unsigned binaries.

---

## Features

- **Chinese Braille conversion**: dot patterns follow the current Chinese national braille standard, with tones applied by rule; Latin letters, digits and punctuation map directly. Polyphonic characters use their most common reading.
- **Dome-shaped dots**: each dot is a dome rather than a cylinder, which forms reliably under a 0.4 mm nozzle, gives a crisp tactile feel and does not slip under the finger.
- **Two size presets**: the standard preset for everyday reading; a *jumbo* preset with roughly 1.4× larger dot spacing and dot diameter for teaching, demonstrations, or wherever a larger cell is needed.
- **Base plate and nozzle wipe included**: the base plate, inter-layer wipe path and object-exclusion commands are generated together, so the export is already a complete printable file.
- **G-code export, STL optional**: print the G-code directly; export STL when you need further processing.
- **"6 processes" test coupon**: a built-in calibration part for comparing forming quality on your own machine and dialling in its parameters.
- **GUI**: live dot preview, character limit computed from the current machine's printable width, Chinese/English interface, light/dark theme following the system.

---

## Supported printers

**214 machines across 47 brands**, including Creality, Elegoo, Voron, Sovol, Anycubic, Flashforge, Snapmaker, Bambu Lab, QIDI, RatRig, TwoTrees, FLSun, Cubicon and Vivedino.

Prerequisites:

| Item | Requirement |
|---|---|
| Firmware | Klipper dialect (relies on `SET_VELOCITY_LIMIT`, `EXCLUDE_OBJECT`, G2/G3 arcs, M83 relative extrusion) |
| Build volume | Printable width and depth both ≥ 150 mm |
| Nozzle | 0.4 mm |

Bambu Lab P1P / X1 / A1 / A1 mini / H2D go through the vendor's own channel: raw G-code can be submitted via Bambu Connect or LAN developer mode.

Marlin, RepRapFirmware and Repetier dialect machines are not supported.

---

## Usage

1. Double-click `DOTv1.2.exe`
2. **Settings → Printer** → pick your machine in the dialog that opens (brands on the left, models on the right, with search)
3. Type your text and check the dot layout and line count in the preview
4. Export, then copy the G-code to the printer

**For a first run, print the "6 processes" test coupon first** and confirm Z-offset and flow before printing real content; braille dots are far more sensitive to first-layer height than ordinary models.

---

## Default temperatures

The program ships with **240 °C nozzle / 75 °C bed**, and those values are set up **for PETG**.

| Material | Nozzle | Bed |
|---|---|---|
| **PETG** (default) | 240 °C | 75 °C |
| PLA | 200–210 °C | 55–60 °C |

**Lower the temperature before printing PLA.** At 240 °C PLA strings and oozes, and a 75 °C bed makes it elephant-foot and cling to the plate. Both values are editable in the settings window; the accepted range is 180–260 °C nozzle and 0–100 °C bed.

Other materials (ABS, TPU, wood-fill, carbon-fill and so on) are not tuned by this program — it only exposes the temperature fields, so set them to whatever that material normally needs.

---

## Caveats

1. `printer.cfg` must enable `[gcode_arcs]` and `[exclude_object]`. This is a hard prerequisite — the program can only warn, it cannot set this for you.
2. Only 7 of the machine profiles have their start/end macros cross-checked against vendor presets; the rest are converted automatically. **Check the macro names and parameters against your actual `printer.cfg` before the first print** — macro signatures differ between firmware versions.
3. The nozzle is fixed at 0.4 mm. Switching to 0.6 / 0.8 mm would ruin the dot shape, so the option is not offered.
4. The built-in self-check only guarantees internal consistency of structure, temperature, coordinates and extrusion budget. **It does not replace calibration on the machine.**
5. Bambu's `.gcode.3mf` packaging has not been tested on hardware. Confirm with the vendor slicer that the file channel accepts raw G-code before relying on it.

---

## Version

**V1.2** (current)

- Printer pool expanded to 214 machines across 47 brands, covering Klipper and Bambu Lab models with width and depth both ≥ 150 mm
- Character limit now derived from each machine's printable width instead of a fixed 220 mm rule
- Printer selection moved into its own window: brands on the left, models on the right, each scrolling independently, with search by brand or model
- Interface switches between Chinese and English, following the system language by default
- Version number shown in the main window title; settings window holds the printer button and language option

---

## Feedback

If something fails, a machine profile doesn't fit, or a macro doesn't match, please open an [issue](https://github.com/raymondzoufangzhen/DOT/issues) and include the machine name plus the corresponding `START_PRINT` / `PRINT_END` macro definitions from your `printer.cfg` so it can be traced.

---

## License

Closed source, all rights reserved. Free to use for personal, teaching and other non-commercial purposes; unmodified copies may be shared free of charge; redistributing modified versions, decompilation, reverse engineering and any commercial use are not permitted.

See [LICENSE](LICENSE) for the full terms, which govern.

Dot positions follow the current Chinese national braille standard; the dot geometry and its parameters are this project's own implementation.
