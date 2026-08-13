[日本語](README.md) | **English**

# suzunia

A manga / image viewer for **Windows and macOS**.
It is designed with **overall speed — startup and page turning above all** — as the top priority.

It is primarily a book viewer for **zip (cbz), pdf, and epub**, but it also works as a plain viewer for individual image files such as **JPEG XL, AVIF, WebP, PNG, JPG, GIF, and more**.

![suzunia-picture](suzunia.png)

## Download

| Platform | File | Requirements |
|---|---|---|
| Windows | `suzunia-*.zip` | Windows 10 / 11 (64-bit) |
| macOS | `suzunia-*-macos-arm64.zip` (recommended) or `.dmg` | macOS 13 or later / Apple Silicon only |

Get them from [Releases](../../releases).

The macOS zip and dmg have identical contents. **The zip is recommended** — the one-time
security confirmation described under [Installation](#macos) takes one round with the zip
and two with the dmg.

**Latest update** — [Changelog](CHANGELOG.en.md).

## Requirements

### Windows

| Item | Requirement |
|---|---|
| OS | Windows 10 / 11 (**64-bit only**). Windows on ARM is not supported |
| CPU | An x64 CPU with AVX2 (Intel 4th-generation Core〈2013〉or later, AMD Ryzen, etc.) |
| Main app `suzunia.exe` | **No** additional runtime (all required DLLs are bundled) |
| Settings app `suzunia-settings.exe` | Requires the [.NET Desktop Runtime 10.0 (x64)](https://dotnet.microsoft.com/download/dotnet/10.0) |

- The main app is a self-contained executable built with NativeAOT; installing .NET is not necessary.
- Every viewing feature works without the .NET runtime. The only thing you cannot open is the settings window (settings can also be changed by editing `suzunia.json` directly).

### macOS

| Item | Requirement |
|---|---|
| OS | macOS 13 (Ventura) or later |
| CPU | **Apple Silicon (M1 or later) only. It does not run on Intel Macs** |
| Runtime | **None** required. The settings window is built into the app |

## Installation

### Windows

1. Download the zip from [Releases](../../releases).
2. Extract it anywhere you like.
3. Run `suzunia.exe`.

The zip contains the main app (`suzunia.exe`), the settings app (`suzunia-settings.exe` and friends), the image and archive decoder DLLs, and the license documents for the bundled libraries (`license/`).

**If SmartScreen warns you** — the executable is not code-signed, so Windows SmartScreen may show "Windows protected your PC" on first launch. **Click "More info" → "Run anyway" and ignore it.**

**It does not touch your registry or any other folder**

- There is no installer. suzunia never writes to the registry, and all settings and history files are created **in the same folder as the executable**.
- **To uninstall, just delete the folder.**
- Exception: only when extracted somewhere unwritable such as `C:\Program Files`, settings are stored in `%APPDATA%\suzunia` instead. If you want to keep it portable, put it somewhere writable.

### macOS

1. Download the zip (or dmg) from [Releases](../../releases).
2. Put `suzunia.app` into your `Applications` folder.
3. The first launch needs the confirmation steps below.

**macOS will block this app once.** It is not signed through Apple's paid Developer Program
(US$99/year); this does not mean anything is wrong with the app.

When you try to open the downloaded file, you will see:

> **"suzunia-…" Not Opened**
> Apple could not verify "suzunia-…" is free of malware that may harm your Mac or compromise your privacy.
> 　[ Move to Trash ]　[ Done ]

**⚠️ Click "Done", not "Move to Trash".**

### The easy way (terminal)

**Before** opening the downloaded file, run this one line:

```
xattr -dr com.apple.quarantine ~/Downloads/suzunia-*-macos-arm64.*
```

No dialog will appear after that. Put `suzunia.app` into `Applications` and launch it
normally with a double-click.

### Without the terminal

1. Click **"Done"** in the dialog
2. Open **Apple menu → System Settings → Privacy & Security**
3. Scroll down and click **"Open Anyway"** next to the blocked item
4. Click **"Open"** once more in the confirmation dialog

**With the zip, that is all** — put `suzunia.app` into `Applications` and go through
steps 1–4 once.

**With the dmg you need one more round**, because both the dmg itself and the app are
checked. Once the dmg opens, drag `suzunia.app` into `Applications`, then repeat steps 1–4
for the dialog that appears when you double-click it.

From the second launch onward it opens normally with a double-click.

**To uninstall**, just delete `suzunia.app`. To remove settings and history as well, also delete `~/Library/Application Support/suzunia/`.

### Updating

- **Windows** — copy the contents of the new zip over the folder containing the old one.
- **macOS** — replace `suzunia.app` in your Applications folder.

Settings, history, and bookmarks are carried over on both platforms.

### It never connects to the network

**suzunia has no networking features at all.** It never sends anything over the internet, including update checks, telemetry, and crash reports.

### Ways to open a book

| Method | Windows | macOS |
|---|---|---|
| Drag and drop onto the window | Yes | Yes |
| Drop onto the app icon / Dock icon | Yes | Yes |
| "Open" from the menu | Yes | Yes |
| File association (double-click) | Yes | Yes |
| "Open with" | Yes | Yes |
| Command line | `suzunia.exe <path>` | `open -a suzunia <path>` |

## Features

### Everything is built for speed

- Win32 API directly on Windows, AppKit directly on macOS. Both are NativeAOT, and neither uses a GUI framework (WPF / WinForms).
- At startup, the only work on the critical path is "open the archive → decode page 1 → resize → display". Everything else (creating the window, loading settings, preparing the prefetcher) runs in parallel.
- Neighboring pages are prefetched and cached, so turning a page completes in a few milliseconds.
- CPU usage is 0% while a still image is displayed (there is no background timer and no render loop).

### zip (cbz) is the fastest

- zip files are read by a custom reader (memory mapping plus central directory parsing; stored entries are handed to the decoder without being copied). **If you want speed, use uncompressed (stored) zip / cbz archives.**
- rar and 7z are also supported, but solid archives must be decompressed sequentially from the beginning by nature of the format, so they cannot match zip.
- **Recovery of broken zips**: even when the end-of-central-directory record or the central directory is damaged, suzunia scans the local headers and reads everything it can. Pages whose data is truncated are displayed up to the point that could be decompressed.
- Japanese filenames inside zips (CP932 / Shift_JIS) are decoded correctly.

### Supported formats

**Still images** — the format is detected from the file contents rather than the extension, so files display correctly even when the extension does not match.

| Format | Windows | macOS | Notes |
|---|---|---|---|
| JPEG (.jpg .jpeg .jpe .jfi .jfif) | Yes | Yes | |
| PNG (.png .apng) | Yes | Yes | Only the first frame of an APNG is shown |
| GIF (.gif) | Yes | Yes | |
| WebP (.webp) | Yes | Yes | |
| AVIF (.avif) | Yes | Yes | |
| JPEG XL (.jxl) | Yes | Yes | |
| TIFF (.tif .tiff) | Yes | Yes | |
| BMP (.bmp .dib) | Yes | Yes | |
| TGA (.tga) | Yes | Yes | |
| ICO (.ico) | Yes | Yes | |
| HEIC / HEIF (.heic .heif) | Partial | Yes | On Windows, only if the OS codec is installed |
| Others | Partial | — | Windows only. Anything for which an extra WIC codec is installed |

**Animated images** — GIF, WebP, AVIF, and JPEG XL are supported. Transparency (alpha) is composited against the background.

**Archives and other containers**

| Format | Windows | macOS | Notes |
|---|---|---|---|
| zip / cbz | Yes | Yes | Fastest. Includes broken-zip recovery |
| rar / cbr | Yes | Yes | rar5 and solid archives supported |
| 7z / cb7 | Yes | Yes | Solid archives supported |
| PDF | Yes | No | Rasterized at a configurable DPI |
| epub | Yes | No | The first open takes a while because page counts must be measured |
| PSD | Yes | Yes | |
| Folder | Yes | Yes | Treats a folder as one book. Including subfolders is configurable |
| A single image file | Yes | Yes | Displays that image immediately and treats the rest of the folder as one book |

### The settings window

- **Windows** — putting a settings GUI in the main process would make startup roughly ten times slower just from loading the GUI framework (measured: 24–29 ms to show an empty window with Win32, versus 266–324 ms with WPF). To keep the app as fast as possible, the settings window `suzunia-settings.exe` is a separate process. Changes made there are applied to the running app immediately.
- **macOS** — AppKit does not carry that loading cost, so the settings window is built into the app. No extra runtime is needed.

### The feature set is deliberately small

Because performance comes first, the feature set is limited to what is needed to read manga and images. There is no library/bookshelf, no thumbnail grid, no tag management, and no image editing.

### Per-book display options via the filename

If the filename (or folder name) contains one of the following tags, the display settings are overridden while that book is open.

| Tag | Effect |
|---|---|
| `[左開き]` | Left-to-right binding (page 1 on the left) |
| `[単ページ]` | Force single-page mode |
| `[1ページ目単独]` | Show the first page alone even in two-page mode (for covers) |
| `[最終ページ単独]` | Show the last page alone even in two-page mode (for back covers and colophons) |

Example: `Title Vol.1 [左開き][1ページ目単独].zip`

Anything not listed follows your normal settings. Changing an option from the menu after opening takes precedence.

## Feature list (overview)

This is just an overview of what is available. For the default key assignments and the
meaning of each setting, see the **[Operation Reference](docs/operation-reference.en.md)**.
**Everything here works on both platforms** except as noted under "Not available on macOS" below.

- **Page navigation** — next/previous, left/right on screen (resolved automatically by binding direction), by single page, by spread, jumps of a configurable A / B page count, first/last, go to a page number, shift the spread pairing by one page
- **Book navigation** — move to the previous/next book in the same folder. Behavior at the end of a book is selectable: stay / loop / go to the next book
- **Display modes** — one-page / two-page (spread), right-to-left / left-to-right binding, automatic single display of wide pages, single display of the first and last pages
- **Sizing** — 7 modes (original size / fit to window / shrink large images only / enlarge small images only / fill window / fit height / fit width). Two favorites can be assigned to A / B and toggled with a single action
- **Image quality** — 7 interpolation filters (nearest neighbor / area average / linear / Catmull-Rom / Mitchell / spline / Lanczos3), unsharp mask, interpolation in linear light, upscaling (line-art restoration when enlarged; Windows only)
- **Effect presets** — ten complete sets of the image-quality settings. Switch with a single key (or the Effects menu). By default 1-4 are image quality, 5-9 are pseudo-color samples and 0 is for pixel art (nearest neighbor, no unsharp mask)
- **Effects** — auto level correction, false color, auto-crop margins, splitting wide pages, rotation in 90-degree steps, channel picker (show only one of R/G/B/A)
- **Color management** — ICC profile support
- **Pan and zoom** — drag with the left button to slide the view, zoom to a configurable factor centered on the cursor
- **Background** — solid color / match the image / checkerboard (for transparent images)
- **Page ordering** — filename / date / size / archive entry order (each ascending or descending), random
- **Window** — full screen, always on top
- **Info panel** — a separate window showing book, page, image, display, and EXIF information
- **Copy and save a page** — copy gives a full-resolution bitmap (a spread is joined into one image); save writes out the original data untouched, so it is lossless
- **History** — up to 50 entries. "Recent files" reopens at the page you left off
- **Bookmarks** — 16 slots
- **Automatic page turning** — slideshow, with two configurable speeds
- **Customizable input** — assign 130+ commands freely to keys and mouse actions (click / double-click / long press / wheel / wheel-while-held / X buttons / mouse gestures)
- **UI language** — Japanese / English
- **Sound effects** — play a .wav when page or book navigation stops at an edge (off by default)
- **Other** — single-instance enforcement (multiple instances can be allowed), window position and full-screen state restored, reveal in Explorer / Finder, file deletion (trash or direct), reload the settings file

### Not available on macOS

These are either out of scope for the port or absent for platform reasons.

| Feature | Reason |
|---|---|
| PDF / epub | Out of scope (the Windows version uses pdfium / WebView2) |
| Upscaling | Out of scope (the Windows version uses Direct3D 11) |
| Custom-drawn title bar | macOS uses the standard system title bar |
| Page slider | Same reason as above |
| Shell integration tab (context menu, file associations) | Not needed — Finder handles this from the `.app` bundle automatically |
| Archives nested inside archives | Not verified |

Everything else matches the Windows version, down to the menu layout and the order of items in the settings window.

## Settings files

You may edit these by hand (use the "reload settings" command or restart to apply).

| File | Contents |
|---|---|
| `suzunia.json` | Display and behavior settings, key and mouse assignments |
| `suzunia-history.json` | Reading history (up to 50 entries) |
| `suzunia-window.json` | Main window position and state |
| `suzunia-settings-window.json` | Settings window position (Windows only) |

Their location differs by platform.

| OS | Location |
|---|---|
| Windows | **The same folder as the executable** (only `%APPDATA%\suzunia` when placed somewhere unwritable) |
| macOS | `~/Library/Application Support/suzunia/` (preserved when you replace the app) |

## License

- **suzunia itself is freeware.** You may use it free of charge. Apparently the author holds the copyright — though it is a bit odd to claim copyright on something an AI wrote all of, isn't it?
- You are free to share the distributed zip / dmg as-is, but this is the only official distribution page. Redistributing modified builds, or decompiling / disassembling the executable — do whatever you want, I guess. Just don't expect me to take responsibility for it.
- The bundled third-party libraries are covered by their own licenses. Full texts are in the `license/` folder inside the Windows zip, and in "ライセンス表記.txt" inside the macOS dmg as well as `Contents/Resources/THIRD-PARTY-NOTICES.txt` inside the app.

**Bundled with the Windows version**

| DLL | Library | License |
|---|---|---|
| jxl.dll | libjxl (includes brotli, highway, and others) | BSD-3-Clause and others |
| libwebp.dll / libwebpdemux.dll / libsharpyuv.dll | libwebp | BSD-3-Clause |
| avif.dll | libavif | BSD-2-Clause |
| dav1d.dll | dav1d | BSD-2-Clause |
| pdfium.dll | PDFium (includes freetype, libjpeg-turbo, and others) | BSD-3-Clause / Apache-2.0 and others |
| 7z.dll | 7-Zip | LGPL-2.1 (with the unRAR restriction) |
| vcruntime140.dll | Visual C++ Runtime | Microsoft redistributable license |

7z.dll is used unmodified via dynamic loading (as required by the LGPL, the full license text is bundled in `license/`).

**Bundled with the macOS version**

| dylib | Library | License |
|---|---|---|
| libjxl.dylib / libjxl_cms.dylib | libjxl (includes highway and skcms) | BSD-3-Clause / Apache-2.0 |
| libbrotlicommon / libbrotlidec / libbrotlienc.dylib | Brotli | MIT |
| libwebp.dylib / libwebpdemux.dylib / libsharpyuv.dylib | libwebp | BSD-3-Clause |
| libavif.dylib | libavif (includes dav1d) | BSD-2-Clause |
| (statically linked into the app) | .NET runtime | MIT |

rar and 7z extraction uses the libarchive that ships with macOS, so it is not bundled with the app.

## Disclaimer

- This software is provided "AS IS", without warranty of any kind, express or implied, as to its operation, quality, or fitness for a particular purpose.
- The author accepts no liability whatsoever for any damage (including data loss) arising from the use of, or inability to use, this software.
- Use it at your own risk.

## Bug reports and requests

Please use [Issues](../../issues). Pull requests are not accepted, since the source is not public.

The following information helps a lot with bug reports:

- The symptom and how to reproduce it
- The type of file you had open (zip / rar / 7z / PDF / folder) and, if you know, the image format and size inside
- Your OS version (Windows 10 / 11, or your macOS version)

## Acknowledgements

The feature set and control scheme take after earlier viewers of this kind, MangaMeeya in particular.
I intend to use this as my own MangaMeeya successor.

The original icon was drawn by [yosshin](https://yosshin4004.github.io/) in lieu of covering their share of a drinking party.
