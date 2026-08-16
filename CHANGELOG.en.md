[日本語](CHANGELOG.md) | **English**

# Changelog

[Back to README](README.en.md)

### 2026.08.17.

- bug fix.

### 2026.08.16.

- Added **"Copy file name to clipboard"** to the File menu. It puts one of four strings on the clipboard: the current file name, its full path, the current folder name, or the folder's full path. "The current file" here means the same file as "Show in Explorer": the archive itself for archives, PDF and EPUB, or the page being displayed when an image file or an image folder is open.
- Added **"Open install folder"** and **"Open settings folder"** to the File menu. The settings folder is normally the folder the exe sits in on Windows, but becomes `%APPDATA%\suzunia` when suzunia is installed somewhere it cannot write (under Program Files, for example); on macOS it is `~/Library/Application Support/suzunia`.
- Added **"Open with another app"** to the File menu (**Windows only**). It hands the file you are viewing to an image editor or any other program. Up to nine entries can be registered on the new **Other apps tab** of the settings app, each with a menu name, the full path to the executable, an argument and what suzunia should do after launching.
  - **Argument** — "Current file path" (default) / "Current folder path" / "Copy the image to the clipboard" / "Send nothing". The clipboard option puts the page being displayed on the clipboard at full size and then starts the app with no argument (paste it in the app yourself).
  - **After launch** — "Do nothing" (default) / "Minimize" / "Maximize" / "Exit".
  - Only entries that have **both a menu name and an executable** appear in the menu. Besides .exe, the executable may be a .bat or a shortcut (.lnk).
- All of the above can also be **assigned to keys and mouse actions** (Input tab of the settings app). The command list grew by 15, to 151.

### 2026.08.15.

- **Faster page turns (look-ahead pre-rendering).** The next spread is now prepared in the background — resampled to display size and sharpened — so turning the page becomes just a transfer to the screen. The larger the window or the page, the bigger the win (measured: 5.9 ms → 2.4 ms per turn at 4K, two-page view). The picture is exactly the same as before. It can be turned off with "Prepare the next page's display image ahead of time" on the Performance tab of the settings app (on by default).
- Added **"Trade drawing quality for speed while page turns are rapid-fired"** (off by default). Only while page turns keep coming faster than the chosen threshold (slider: 0.05–0.5 s, 0.2 s by default) — such as holding a key down — pages are drawn with lighter interpolation and without the unsharp mask; once you stop, the usual quality is redrawn.
- The title bar is no longer redrawn on every single page turn, shaving a little off each turn (the text catches up within 0.05 s).
- Added **"Forward / back by percentage"** to page navigation. It moves by a share of the total page count, so the same command jumps the same amount of *progress* no matter how long the book is. The share is set with a **slider (1–100%, 5% by default)** under "Page step" on the Display tab of the settings app. It is also on the Move menu (assign a key on the Input tab).
- Added the **"Confirm before sending to the Recycle Bin"** setting (off by default). Until now only direct deletion asked for confirmation.
- **Image files and folders can now be shown two pages at a time.** Opening an image file or a folder directly used to be locked to one-page view; you can now **switch to two-page view** from the Page menu or a key assignment. Turning on **"Use two-page view for image files and folders too"** — added to the Behavior tab of the settings app (off by default) — makes them open that way from the start, following "Page layout" on the Display tab. Archives and PDFs are unaffected.
- Added the **"Bring suzunia to the front when a file is dropped"** setting (on by default). Dropping a file onto the window brings suzunia to the front; with it off the book still opens, but whatever you dragged from (Explorer, for example) stays in front. Opening by file association, and the hand-off used when multiple instances are not allowed, come to the front regardless of this setting.
- **The window buttons are now shown in full screen too.** Until now, revealing the title bar by moving the cursor to the top of the screen gave you no minimize or close button. The middle button acts as **leave full screen**.
- The page slider is now **one step thicker and brighter**.
- **Fixed the error beep on "Alt + key" assignments such as Alt+1.** The assigned command was actually running, but Windows then decided the combination was not on any menu and played its error sound. Assigning a menu's first letter (Alt+F, for example) also **opened that menu on top of running the command**; that is fixed too (in exchange, such a menu can no longer be opened with Alt — clicking still works).

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
