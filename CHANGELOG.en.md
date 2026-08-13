[日本語](CHANGELOG.md) | **English**

# Changelog

[Back to README](README.en.md)

### 2026.08.14.

- **Released the macOS version (Apple Silicon).**

- The settings window now opens the Effects tab on **whichever preset the viewer is currently using**, instead of always starting at preset 1.
- "Monochrome / color detection" on the Effects tab is now **shared by all presets** instead of being stored per preset. It moved to the new **"Shared settings"** group at the bottom of the tab, together with "Setting A / Setting B".
- Added the **"Tone coloring"** false-color pattern (5 colors). Pure black and pure white stay put, so only the midtones (screentones) shift toward a skin tone.
- Effect preset **9 now defaults to "Tone coloring (pseudo-color)"**, and **"Effect: toggle A / B" now defaults to preset 9 for B** (defaults only — settings you have already saved are untouched).

### 2026.08.13

- Added **English / Japanese UI switching**.
- Added support for the **TGA** and **PSD** formats.
- Added the "channel picker" — display only one of the R, G, B, or A channels.
- Reorganized the false-color patterns and effect presets.
- Fixed several bugs around false color, auto level correction, and background color.
- Tuned the upscaling parameters.

### 2026.08.12

- Added the "auto level correction" effect.
- Added the "false color" effect.
- Added "adjust size in two-page mode".

### 2026.08.11

- Added upscaling. It is lightweight, at the cost of quality.
- Added ICC profile support.
- Consolidated the effects and made them manageable as presets.

### 2026.08.10

- Added "auto-crop margins".
- Added "split wide pages".
- Added rotation in 90-degree steps.
- Added navigation to a random page / book.
- Added deletion of archive files.
- Adjusted title bar rendering.
- Fixed a problem with file association settings.

### 2026.08.09

- Added epub support.
- Added a shell integration tab (context menu, file associations) to the settings app.

### 2026.08.08

- Added bookmarks.
- Added automatic page turning (slideshow), with two configurable speeds.
- Added mouse gestures.
- Added support for archives nested inside archives.
- Made prefetch status visible — while an asterisk ("＊") is shown next to the page number at the top left of the title bar, prefetching is still running.
- Added file deletion (move to trash / delete directly).
- Added file reloading.
