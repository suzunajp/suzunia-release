[日本語](操作リファレンス.md) | **English**

# Operation Reference

[Back to README](../README.en.md)

The default key and mouse assignments, the complete list of assignable commands, and the menu layout.
**Identical on Windows and macOS** (anything absent on macOS is noted in the relevant table).

- [Changing assignments](#changing-assignments)
- [Default key assignments](#default-key-assignments)
- [Default mouse assignments](#default-mouse-assignments)
- [Assignable mouse actions](#assignable-mouse-actions)
- [Command list](#command-list)
- [Menu layout](#menu-layout)
- [Settings window](#settings-window)
- [Per-book options via the filename](#per-book-options-via-the-filename)
- [Editing the settings file directly](#editing-the-settings-file-directly)

## Changing assignments

Use the "Input" tab of the settings window. Open it in any of these ways:

- Menu → Options → "Settings..."
- The default key <kbd>F2</kbd>
- **Windows** — run `suzunia-settings.exe` directly (it is a separate app)
- **macOS** — from the Options menu (it is built into the app)

A single command can have several keys assigned to it. By default, "Next page" already has
two: <kbd>PageDown</kbd> and <kbd>Space</kbd>.

## Default key assignments

| Key | Command |
|---|---|
| <kbd>←</kbd> | Page to the left |
| <kbd>→</kbd> | Page to the right |
| <kbd>PageDown</kbd> / <kbd>Space</kbd> | Next page |
| <kbd>PageUp</kbd> / <kbd>Backspace</kbd> | Previous page |
| <kbd>Ctrl</kbd>+<kbd>→</kbd> | Forward one page |
| <kbd>Ctrl</kbd>+<kbd>←</kbd> | Back one page |
| <kbd>Shift</kbd>+<kbd>PageDown</kbd> | Forward by step A |
| <kbd>Shift</kbd>+<kbd>PageUp</kbd> | Back by step A |
| <kbd>Ctrl</kbd>+<kbd>PageDown</kbd> | Forward by step B |
| <kbd>Ctrl</kbd>+<kbd>PageUp</kbd> | Back by step B |
| <kbd>Home</kbd> | First page |
| <kbd>End</kbd> | Last page |
| <kbd>Ctrl</kbd>+<kbd>G</kbd> | Go to page |
| <kbd>Ctrl</kbd>+<kbd>C</kbd> | Copy page |
| <kbd>Ctrl</kbd>+<kbd>S</kbd> | Save page |
| <kbd>Delete</kbd> | Delete file |
| <kbd>1</kbd> | Single page |
| <kbd>2</kbd> | Two pages |
| <kbd>D</kbd> | Toggle single / two pages |
| <kbd>R</kbd> | Toggle reading direction |
| <kbd>S</kbd> | Shift spread by one page |
| <kbd>W</kbd> | Toggle single view for wide pages |
| <kbd>T</kbd> | Toggle auto-crop margins |
| <kbd>F</kbd> | Cycle display size |
| <kbd>B</kbd> | Cycle background |
| <kbd>G</kbd> | Cycle interpolation |
| <kbd>U</kbd> | Toggle unsharp mask |
| <kbd>I</kbd> | Toggle info panel |
| <kbd>F11</kbd> / <kbd>Alt</kbd>+<kbd>Enter</kbd> | Full screen |
| <kbd>F5</kbd> | Reload settings |
| <kbd>F2</kbd> | Open settings |
| <kbd>Esc</kbd> | Exit |

The same names are used on macOS. Note that <kbd>Ctrl</kbd> means the <kbd>control</kbd> key,
not <kbd>command</kbd>.

## Default mouse assignments

| Action | Command |
|---|---|
| Left click | Next page |
| Right click | Previous page |
| Wheel down | Next page |
| Wheel up | Previous page |
| Middle click | Full screen |
| Side button 1 | Forward one page |
| Side button 2 | Next page |

**A left click only fires if you release the button without moving.**
Left-dragging doubles as panning (sliding the view), so moving beyond a small threshold
cancels the click and starts a pan. Because of this, page turning by left click happens
on button release.

Right, middle, and side buttons fire on press. The exception is the right button when you
have assigned a long press or a wheel-while-held gesture to it — then it waits for release
so the two can be told apart.

## Assignable mouse actions

Any command can be assigned to any of these actions.

| Group | Actions |
|---|---|
| Click | left / right / middle / side button 1 / side button 2 |
| Double click | left |
| Wheel | up / down |
| Wheel while held | left button + up / down, right button + up / down |
| Long press | left / right |
| Right-drag gesture | any combination of up / down / left / right, up to 3 strokes (`↑`, `↑↓`, `←↓→`, ... — 84 in total) |

For a right-drag gesture, hold the right button, draw the strokes in sequence,
and the command runs **when you release the button**.

## Command list

There are **151 assignable commands** (not counting "(unassigned)"). They appear in this
order in the settings dropdown.

### Page navigation

| Command | Notes |
|---|---|
| Next page / Previous page | Moves in reading order |
| Page to the left / Page to the right | Moves by on-screen direction, resolved to next/previous by the binding direction |
| First page / Last page | |
| Go to page | Opens a small input window |
| Forward one page / Back one page | Always moves exactly one page, even in two-page view |
| Forward by step A / Back by step A | The step size is set in the settings window |
| Forward by step B / Back by step B | Same, giving you two different step sizes |
| Shift spread by one page | Shifts the spread pairing by one page. Use it when a cover throws the pairing off |
| Random page | |

### Book navigation

| Command | Notes |
|---|---|
| Next book / Previous book | Moves within the sort order of the same folder |
| Random book | |
| At end of book: stay / loop / next book | What happens when you page past the end (or start) of a book |

### Display mode

| Command | Notes |
|---|---|
| Single page / Two pages / Toggle single / two pages | |
| Toggle reading direction | Right-to-left or left-to-right |
| Toggle single view for wide pages | Wide pages are shown alone instead of paired |
| Toggle single view for the first page | For covers |
| Toggle single view for the last page | For back covers and colophons |
| Toggle size matching in two-page view | Evens out left and right when the two pages differ in size |
| Reset page settings | Returns this book to the state it had when freshly opened |

### Display size

| Command | Notes |
|---|---|
| Cycle display size | |
| Display size: original size | |
| Display size: fit to window | |
| Display size: shrink large images only | |
| Display size: enlarge small images only | |
| Display size: fill window | |
| Display size: fit height | |
| Display size: fit width | |
| Display size: switch between A and B | Assign two favorites and flip between them with one action |

### Background

| Command | Notes |
|---|---|
| Cycle background | |
| Background: solid color | The color is set in the settings window |
| Background: match image | Samples the color from the page border (default) |
| Background: checkerboard | For inspecting transparent images |

### Page processing and effects

| Command | Notes |
|---|---|
| Toggle auto-crop margins | Detects the white paper border and trims it |
| Toggle splitting of wide pages | Splits a scanned spread into two pages |
| Rotate 90° right / Rotate 90° left | |
| Rotation: reset / 90° right / 180° / 90° left | |
| Cycle interpolation | Nearest neighbor / area average / linear / Catmull-Rom / Mitchell / spline / Lanczos3 |
| Toggle unsharp mask | |
| Toggle auto levels | Finds the black and white points per page and stretches the range |
| Toggle pseudo-color | Paints monochrome pages in the colors you configure |
| Toggle ICC profile handling | |
| Toggle zoom | |
| Effect preset 1–9, 0 | Ten complete sets of effect settings |
| Effect: switch between A and B | |
| Cycle effect presets | |

**Auto levels and pseudo-color are not applied to color pages or transparent pages.**
The former because a 1-D tone mapping would ruin the hue, the latter because a transparent
page already has the background composited into it and would clash with the surrounding fill.
In two-page view the decision is made **per page**, so a monochrome body page paired with a
color cover still gets the effect.

### Channel picker

| Command | Notes |
|---|---|
| Channel: normal (RGBA) / R only / G only / B only / A only | Shows a single channel in grayscale |
| Cycle channel | |

This is a temporary setting that is not written to the settings file (reopening a book resets it).

### Page sort order

| Command | Notes |
|---|---|
| Sort order: file name, ascending / descending | Numbers sort naturally (`9` before `10`) |
| Sort order: file date, ascending / descending | |
| Sort order: file size, ascending / descending | |
| Sort order: archive entry, ascending / descending | The order stored in the archive |
| Sort order: random | |
| Toggle reading of subfolders | Applies when opening a folder as a book |

### Window and panels

| Command | Notes |
|---|---|
| Full screen | |
| Maximize / restore window | |
| Minimize window | |
| Always on top | |
| Toggle info panel | Shows book / page / image / display / EXIF information in a separate window |
| Toggle page slider | **Windows only** (the macOS version has no page slider) |

### File operations

| Command | Notes |
|---|---|
| Copy page | Puts a full-resolution bitmap on the clipboard; a spread is joined into one image |
| Save page | Writes the original data untouched, so it is lossless |
| Delete file | Trash or permanent deletion, selectable in the settings |
| Reload file | |
| Show in Explorer | Reveals the file in Finder on macOS |
| Copy current file name | Puts just the file name on the clipboard (as text) |
| Copy current file full path | |
| Copy current folder name | Puts just the folder name on the clipboard (as text) |
| Copy current folder full path | |
| Open install folder | Opens the folder the suzunia executable sits in |
| Open settings folder | Opens the folder `suzunia.json` sits in (see [the settings file](#editing-the-settings-file-directly) below) |
| Open with another app 1–9 | Hands the file to a configured external program (**Windows only**; see [Open with another app](#open-with-another-app) below) |

"The current file" is the same file as "Show in Explorer": **the archive itself for
archives, PDF and EPUB**, and **the page being displayed when an image file or an image
folder is open**. "The current folder" is the folder that file sits in.
On the menu these four are grouped under File → "Copy file name to clipboard".

### Automatic page turning

| Command | Notes |
|---|---|
| Start auto page turn (A) / (B) | Two configurable intervals. Run it again to stop |

### Bookmarks

| Command | Notes |
|---|---|
| Save bookmark 1–16 | Records the current book and page |
| Load bookmark 1–16 | Opens the recorded book and jumps to that page |

Also available from File → "Save bookmark" / "Load bookmark".

### Application

| Command | Notes |
|---|---|
| Open settings | |
| Reload settings | Use this after editing the settings file by hand |
| Switch the UI language | Japanese / English |
| Exit | |

## Menu layout

There are six menu headings, and the **layout and order are the same on Windows and macOS**.

| Heading | Main items |
|---|---|
| File | Open / Reload file / Recent files / Save bookmark / Load bookmark / Copy page / Copy file name to clipboard / Save page / Delete file / Show in Explorer (Finder) / Open with another app (Windows only) / Open install folder / Open settings folder / About / Exit |
| View | Display size / Background / Channel picker / Apply ICC profile / Full screen / Info panel / Page slider / Always on top |
| Effects | Choose one of ten effect presets (modified ones are marked "(modified)") |
| Navigate | Next/previous page / by one page / by step A and B / first and last / go to page / random / previous, next, and random book / start auto page turn / behavior at end of book |
| Page | Single and two pages / split wide pages / the various single-view options / size matching / auto-crop margins / reading direction / sort order / rotation / read subfolders / reset page settings |
| Options | Settings / Reload settings |

Only four things differ on macOS:

- An application menu comes first, and "About" and "Quit" live there
- There is no page slider item
- There is no "Open with another app" (Finder already has "Open With")
- "Maximize" and "Minimize" are at the end of the View menu (they are window buttons on Windows)

**Items in the Page menu are temporary changes that last only while that book is open.**
Reopening the book restores the values from the settings file, and then any
[filename options](#per-book-options-via-the-filename) are applied on top.

## Settings window

There are 9 tabs on Windows and 7 on macOS (which has neither the other-apps tab nor
shell integration). The order of items is the same on both.

| Tab | Groups |
|---|---|
| View | Pages / display size / background / color management / zoom / pan / page step sizes |
| Effects | Presets / resize filter / unsharp mask / auto levels / pseudo-color / upscaling (Windows only) / shared settings |
| General | Startup / auto page turning / page navigation / image folders / archives / file operations / page slider (Windows only) |
| Input | Key assignments / mouse assignments |
| Other apps | The nine "Open with another app" entries (**Windows only**) |
| Performance | Presets / prefetch and cache / PDF (Windows only) / EPUB (Windows only) / archives (rar / 7z) |
| History | History / sound effects / logging |
| Bookmarks | The contents of the 16 slots |
| Shell integration | Context menu / file associations (**Windows only**) |

- **Apart from "Shared settings" at the bottom, the Effects tab holds the settings of the
  single preset chosen in "Preset being edited".** The settings window opens on whichever
  preset the viewer is currently using. Which preset is in use is chosen from the Effects
  menu or a key binding, not from the settings window.
- **"Shared settings" are not switched by the preset.** Two groups live there:
  - **Setting A / Setting B** — the two presets the "Effects: switch between A and B"
    command alternates between
  - **Monochrome vs. color detection** — thresholds shared by auto levels and pseudo-color;
    changing them changes how both behave. They describe how your scans look rather than
    how a page should be shown, so there is a single pair for all presets
- Raising **prefetch and cache** makes page turning faster but uses more memory. Be careful
  with large-format books (100 MB or more per page).

## Open with another app

**Windows only.** Hands the file you are viewing to an image editor or any other program.
Up to **nine** entries can be registered on the Other apps tab, each with these four fields.

| Field | Meaning |
|---|---|
| Menu name | The name shown under File → "Open with another app". Empty by default |
| Full path to the executable | Pick it with "Choose…". Besides .exe, a .bat or a shortcut (.lnk) works. Empty by default |
| Argument | See the table below. "Current file path" by default |
| After launch | Do nothing (default) / Minimize / Maximize / Exit |

| Argument | What is passed |
|---|---|
| Current file path | The same file as "Show in Explorer" (the archive itself for archives, the page being displayed for image folders) |
| Current folder path | The folder that file sits in |
| Copy the image to the clipboard | Puts the page being displayed on the clipboard at full size, then starts the app with no argument (paste it in the app yourself) |
| Send nothing | Starts the app with no argument |

- **Only entries that have both a menu name and an executable appear in the menu.**
  With none registered, the submenu shows just "(not configured)".
- They can be bound to keys and mouse actions as "Open with another app 1" – "9"
  (the number is the row number on the Other apps tab).

## Per-book options via the filename

If the filename (or folder name) contains one of these tags, the display settings are
overridden while that book is open.

| Tag | Effect |
|---|---|
| `[左開き]` | Left-to-right binding (page 1 on the left) |
| `[単ページ]` | Force single-page mode |
| `[1ページ目単独]` | Show the first page alone even in two-page mode |
| `[最終ページ単独]` | Show the last page alone even in two-page mode |

Example: `Title Vol.1 [左開き][1ページ目単独].zip`

Changing an option from the menu after opening takes precedence.

## Editing the settings file directly

You may edit `suzunia.json` by hand. Apply the changes with "Reload settings"
(<kbd>F5</kbd>) or by restarting. Key and mouse assignments are stored like this:

```json
{
  "keys":  { "Ctrl+Right": "NextPageSingle", "F11": "ToggleFullScreen" },
  "mouse": { "LeftClick": "NextPage", "RightGestureUp": "FirstPage",
             "RightGestureUpDown": "LastPage" }
}
```

A mouse-gesture key is `RightGesture` followed by up to 3 directions
(`Up` / `Down` / `Left` / `Right`) in drawing order, e.g. `RightGestureLeftDownRight`.

The value is the internal command name from the [command list](#command-list), not the label
shown in the Input tab. **A misspelled line is silently ignored**, so if an assignment does
nothing, check the spelling first.

The file lives next to the executable on Windows, and in
`~/Library/Application Support/suzunia/` on macOS.
