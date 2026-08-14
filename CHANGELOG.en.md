[日本語](CHANGELOG.md) | **English**

# Changelog

[Back to README](README.en.md)

### 2026.08.15.

- **Faster page turns (look-ahead pre-rendering).** The next spread is now prepared in the background — resampled to display size and sharpened — so turning the page becomes just a transfer to the screen. The larger the window or the page, the bigger the win (measured: 5.9 ms → 2.4 ms per turn at 4K, two-page view). The picture is exactly the same as before. It can be turned off with "Prepare the next page's display image ahead of time" on the Performance tab of the settings app (on by default).
- Added **"Trade drawing quality for speed while page turns are rapid-fired"** (off by default). Only while page turns keep coming faster than the chosen threshold (slider: 0.05–0.5 s, 0.2 s by default) — such as holding a key down — pages are drawn with lighter interpolation and without the unsharp mask; once you stop, the usual quality is redrawn.
- The title bar is no longer redrawn on every single page turn, shaving a little off each turn (the text catches up within 0.05 s).
- Added **"Forward / back by percentage"** to page navigation. It moves by a share of the total page count, so the same command jumps the same amount of *progress* no matter how long the book is. The share is set with a **slider (1–100%, 5% by default)** under "Page step" on the Display tab of the settings app. It is also on the Move menu (assign a key on the Input tab).
- Added the **"Confirm before sending to the Recycle Bin"** setting (off by default). Until now only direct deletion asked for confirmation.

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
