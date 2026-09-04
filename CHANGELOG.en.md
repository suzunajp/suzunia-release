[日本語](CHANGELOG.md) | **English**

# Changelog

[Back to README](README.en.md)

### 2026.09.05.

- **"Next book" and "Previous book" now work for image folders too.** The destination is the neighboring folder at the same level, sorted in the same natural order as archives ("1 / 2 / … / 10"). While an archive is open you still move only among archive files; folders and archives are never counted together. Hidden folders are skipped.
  - **Moving to a folder that has no images leaves you in that folder.** The title bar shows "full path of the folder (no images)" and the picture goes away, but the folder becomes your current location, so you can keep going to the next or previous folder from there. Previously the viewer stayed on the earlier book, so an empty folder in the middle of a series was a dead end. Dropping an empty folder, or choosing one in the Open dialog, puts you in the same state (an empty archive still just reports the error and keeps showing the current book).

- **Fixed folders with no images directly inside them opening as "no images".** Even with "Read subfolders" turned on in the settings app's Display tab, opening a series folder (no images of its own, just one folder per chapter) gave up without reading the subfolders. This only happened when the folder was opened together with startup, because the folder was scanned before the settings had been read; the viewer now waits for the settings and rescans with subfolders before giving up.

- **The settings app now runs as a single instance** (**Windows only**). Launching a second copy brings the existing settings window to the front and exits. The "always on top" flag used when the viewer is set to stay on top, and the requested tab, are handed over to that window. This prevents two windows from editing the same settings file separately, where the one saved last would silently overwrite the other's changes.

- **Reworked prefetching for heavy pages.** Books whose pages take a long time to decode (such as 3000×5000 lossless scans) now have the next page ready sooner.
  - Prefetching used to decode the upcoming pages side by side, one thread per page across all workers. That is fastest for light pages, but in a book where a single page takes a second or more, **the adjacent page was finished no earlier than the page eight positions ahead**, so turning the page hit an "decode it now" wait. The viewer now estimates each page's cost from its file size and, only for pages that look heavy, decodes them one after another with **half the workers' threads × 2 decoders**, nearest page first. Total CPU use (the number of threads) is unchanged.
  - Measured on large lossless jxl, two-page display, turning every 0.5–1 s: the next spread is ready in **0.7 s instead of 1.9 s** (Apple M4). When a page turn still outruns the prefetch, the viewer now waits for the partly decoded page instead of starting over, cutting that wait from **215 ms to 130 ms** (Ryzen 9 9900X) / **387 ms to 161 ms** (M4). Page turns that were already prefetched, and light books in general, are as fast as before.
  - Added **"Heavy page threshold (ms)"** to the Performance tab of the settings app (default 200). A page estimated to take longer than this on a single thread counts as heavy. **Set it to 0 for the previous behavior.**
  - The System section of the info panel gained a **"Heavy tier"** line showing the decoder configuration in use and the measured value the estimate is based on.
  - The Image section of the info panel gained a **"Decode"** line: how long the page being shown took to decode, who decoded it (prefetch / prefetch, heavy tier / on demand, meaning the prefetch did not make it and the page was decoded when you turned to it), and how many threads were used. A run of "on demand" lines in a heavy book is a hint to revisit the prefetch settings. The time includes extracting the page from the archive.
  - Applies to jxl and avif (webp and the OS decoders cannot decode a single page in parallel).
- The diagnostic `--log <path>` option is now accepted by a normal launch and by `--selftest`, not only by `--bench` / `--shot`.

### 2026.09.03.

- **Added the floating display.** A short message appears over the image on a translucent strip and fades away after a moment. There are three kinds, and the new **Floating display tab** of the settings app switches the feature and each kind on and off (all on by default).
  - **The opened file name** — shown whenever a book is opened (at startup, on drop, when moving to the previous or next book, and so on). It takes one of the same four forms as "Copy file name to clipboard" on the File menu — file name, full file path, folder name, full folder path — chosen separately for **archives** and for **image files / folders** (defaults: "file name" for archives, "full folder path" for image files and folders; for the latter, "file name" means the image being displayed when the book opens).
  - **Warnings** — when a move stops at an edge, such as "Last page" when you try to go past the last page or "No next book" when there is no neighboring book. Errors that used to appear only in the title bar (failed to open, could not delete, and so on) are shown with the same wording.
  - **Mouse-gesture progress** — while you hold the right button and draw, the arrows drawn so far and the command that will run if you release now stay on screen, like "→  Previous page", updating with every stroke; a sequence with no assignment reads "(not assigned)". When you release and the command runs, **"[done]"** is appended and the message stays for the display duration; if nothing runs it disappears.
  - The Floating display tab sets the position (a share of the image area from its top-left corner, X / Y 0–100%, 2% by default), the font and size (system default font, 14 pt), the text color (white), the background color and opacity (black, 75%), the duration (0.5–10 s, 2 s by default) and the **fade-out time** — how long the text and background take to fade together once the duration has passed (0–2 s, 0.3 s by default; 0 makes it vanish at once).
  - **Speed is unaffected.** Nothing is added to page turns while no message is showing, and the font is loaded in the background the first time a message appears (so the very first one right after startup may show up slightly late).

- **Fixed the settings app window overflowing the screen on short monitors** (**Windows only**).
  - The window now shrinks on opening so it fits the monitor's work area (the space left over by the taskbar). The default height used to be taller than 1366×768-class monitors, which could push the OK / Cancel / Apply row at the bottom off the screen. Restoring the previous size on opening is kept within the work area the same way.
  - On the Input tab, a short window used to cut off the "Restore defaults" button to the right of "Key assignments", leaving it out of reach. Each section now keeps a usable minimum height, and the tab shows a scroll bar when it still does not fit.

### 2026.08.31.

- **Added scrolling.** When the image overflows the window, keys and the mouse wheel can now move the view. There are six commands, assigned on the Input tab of the settings app.
  - **"Scroll up / down / left / right"** — moves a fixed amount toward the overflowing side, and stops at the edge (it never turns the page).
  - **"Scroll down / next page"** and **"Scroll up / previous page"** — scroll first, and turn the page once the edge is reached. The new page opens where the reading flow continues: **at the top when moving forward, at the bottom when moving back.** Bind these to the wheel and pages taller than the window scroll under the wheel, advancing to the next page once you have seen the bottom.
  - The distance of one step is the new **"Scroll amount"** on the Display tab of the settings app (a share of the window's edge, 5–100%, 25% by default).
- Added **"Align the view to the reading start on every page move (top edge when moving forward)"** (off by default). With overflowing layouts such as "fit to width", turning the page used to land on the middle of the new page; with this on, it always opens at the reading start (top edge plus the leading side for the reading direction when moving forward, bottom edge when moving back). Pages that fit the window behave as before.
- Added **scroll bars** (off by default). Turn them on from "Scroll bars" on the View menu, or on the Display tab of the settings app: a position marker (thumb) is overlaid along the right and bottom edges, only on the axes that overflow. It shows at a glance where panning, scrolling or zooming has taken you.
- Added **stepwise zoom ("Zoom in", "Zoom out", "Reset zoom")**. The view is enlarged or reduced one step at a time — by the new **"Step factor"** (Display tab of the settings app, 1.1–4.0, 1.25 by default) — keeping the point under the cursor in place. "Reset zoom", like switching "Toggle zoom" off, restores the pre-zoom view including its pan position. The View menu gained a **Zoom submenu** (toggle / in / out / reset).
- All of the above can also be **assigned to keys and mouse actions** (Input tab of the settings app). The command list grew by 10, to **173**.
- **With default settings and assignments, nothing behaves differently from before.**

### 2026.08.18.

- Mouse gestures (right-click + direction) now take **any combination of up / down / left / right, up to 3 strokes** (`↑`, `↑↓`, `←↓→`, ... — 84 in total). Hold the right button, draw the strokes in sequence, and the assigned command runs **when you release the button**.
  - The Input tab of the settings app has a new **"Mouse gestures"** section: pick up to three directions and press "Add" to create a sequence, then assign a command to each row or remove it. **Existing single-stroke assignments carry over as they are.**
  - Drawing four or more strokes is treated as a slip of the hand: nothing runs, and it does not fall back to a right click either.
  - When editing `suzunia.json` by hand, the key is `RightGesture` followed by the directions (`Up` / `Down` / `Left` / `Right`) in drawing order, e.g. `RightGestureUpDown`.
  - As part of this, single-stroke gestures now fire **when the button is released** instead of the moment the stroke is drawn (so that pairs like `↑` and `↑↓` can coexist).
- The Effects menu is now split into two sections, **"Presets"** and **"Quick customization"**, each marked with a greyed-out heading. The lower section changes an effect **on the spot without rewriting the preset**: Interpolation / Interpolate in linear light / Unsharp mask / Auto levels / Pseudo-color / Upscaling (Upscaling is **Windows only**).
  - **Interpolation** — pick one of the seven filters (in the same order as "Cycle interpolation", most used first).
  - **Pseudo-color** — "none" plus "Preset colors" plus the **32 built-in patterns**. The same lineup as "Pattern" on the Effects tab of the settings app; picking one replaces only the colors (the stops), leaving the strength as the preset has it. The check mark is decided by the stop values, so a preset whose stops were hand-edited in the settings app shows the mark on "Preset colors".
  - **Upscaling** — Off / Line-art restore / Line-art restore CNN. The strength and the "only above this scale" threshold belong to the settings app, so a preset with strength 0 stays unaffected whichever method you pick.
  - While a quick customization is in effect, the preset name shows **" (modified)"** in the menu and in the info panel. Selecting a preset again (the same number is fine), reloading the settings, or **"Discard quick customization"** at the bottom of the menu puts everything back. **It survives opening another book.** Make a preset in the settings app for combinations you want to keep.
- All of the above can also be **assigned to keys and mouse actions** (Input tab of the settings app). The command list grew by 12, to 163. **Only the 32 pseudo-color patterns are menu-only**, as they would swamp the list (use the existing "Toggle pseudo-color" to switch it on and off from a key).
- The page slider now **shows its click area** (**Windows only**, on by default). When the cursor enters the area where a click / drag jumps to a page (the slider strip at the bottom of the title bar plus the hit area over the top of the image below it), the whole area appears as a translucent slider with the same track / fill split. It makes it obvious that a click will now turn pages, so clicks meant for the image are no longer taken by surprise. Turn it off with **"Show the click area when hovering over it"** on the General tab of the settings app.
- While **dragging the page slider, the cursor is now confined to the click area**. Moving left and right with the button held still follows to that page, as before; releasing the button (or leaving the window with Alt+Tab and the like) lifts the confinement.

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
