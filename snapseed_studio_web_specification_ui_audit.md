# Snapseed Studio Web — Complete Specification, Architecture & UI Audit

A desktop-grade, non-destructive web photo editor modeled after **Snapseed v4.x**, engineered for full-resolution workflows, multi-layer compositing, precision numeric controls, and lossless multi-format export.

---

## 1. Desktop UI Layout & Workspace Architecture

### A. Top Action Ribbon
* **New (`Ctrl+N`)**: Opens a fresh, independent workspace tab ready for a new photo.
* **Open (`Ctrl+O`)**: Loads standard web images (`JPG`, `PNG`, `WEBP`, `SVG`) and camera RAW formats (`.DNG`, `.NEF`, `.CR2`, `.ARW`, `.ORF`, `.RW2`) at 100% native resolution.
* **Save (`Ctrl+S`) / Save As (`Ctrl+Shift+S`)**: Writes lossless master PNG files directly to disk via the File System Access API (with automatic browser download fallback) and updates tab save state.
* **Export (`Ctrl+E`)**: Opens a modal export dialog supporting **JPG**, **PNG**, **WEBP**, **SVG**, and binary **PDF** with quality and resolution scaling controls, automatically closing upon download.
* **Multi-Document Workspace Tabs**: Displays open files on the right of the top ribbon, each with an unsaved change indicator dot (`•`) and a close cross (`×`) that prompts **Save**, **Don't Save**, or **Cancel** if edits are unsaved.

### B. Sub-Top Info & Quick-Action Ribbon
* **File Name & Native Dimensions**: Displays the active file name (e.g., `2B1A6344.JPG`) and native pixel dimensions (`5472 × 3648`).
* **Meta Data Inspector**: Opens a modal displaying extracted binary EXIF camera tags (Make, Model, Exposure, Aperture, ISO, Focal Length, Date Taken) paired with an interactive **Leaflet / OpenStreetMap** view pinned to embedded GPS coordinates.
* **Zoom Controls (`−`, `%`, `+`, `Fit`)**: Supports smooth scroll-wheel zoom (`25%` to `800%`) and click-drag panning.
* **Revert to Original**: Positioned directly to the left of the *Original* button; discards all active edits and adjustment layers to restore the pristine uploaded photo.
* **Original Compare**: Hold-to-compare toggle that bypasses the edit pipeline to display the unedited source image.
* **Quick Export Button**: Highlighted primary action button on the far right mirroring the top *Export* workflow.

### C. Left Vertical Tool Panel
* Minimalist dark outline-icon navigation housing **all 41 Snapseed v4.x tools**, complete with live keyword search (`Filter 41 tools...`) and category filter pills (`All`, `Tone`, `Color`, `Detail`, `Lens`, `Film`, `Portrait`, `Geo`, `Pro`).
* Clicking any tool header loads its dedicated sliders, wheels, curves, or presets into the bottom control dock.

### D. Center Working Viewport & Zoom Navigator
* **Lossless Working Canvas**: Displays real-time non-destructive edits while preserving the original full-resolution bitmap in memory for export.
* **Picture-in-Picture Zoom Navigator**: Automatically appears in the top-right corner when zoomed above `100%`, displaying the **original unedited image** with a live viewport bounding box.
* **Interactive Canvas Overlays**: Renders draggable rule-of-thirds crop brackets, Selective U-Point pins, Brush/Healing strokes, and draggable Text handles.

### E. Bottom Dynamic Control Dock
* Dynamically renders controls for the active tool alongside **Undo (`Ctrl+Z`)**, **Redo (`Ctrl+Y`)**, and **Reset Tool**.
* **Precision Slider Cards**:
  * **Center-Zero Bipolar Tracks**: Sliders with negative-to-positive ranges (e.g., `-100` to `+100`) fill outward from the center `0` point.
  * **Click-to-Edit Numeric Readouts**: Clicking any numeric value opens an inline text cursor; pressing `Enter` or clicking outside applies and clamps the typed number.
  * **Individual Reset (`↺`)**: Every slider includes a dedicated reset button immediately to the right of its numeric box.

### F. Right Vertical Panel
* **Real-Time Multi-Mode Histogram**: Updates live as edits are applied, supporting **RGB Overlay**, **Luminance**, **RGB Parade**, **Red**, **Green**, and **Blue** channels, a **Clip** warning toggle (blue crushed blacks / red blown highlights), and live **Shadows / Midtones / Highlights** percentage readouts.
* **Non-Destructive Layer Stack**:
  * Header controls: **`+`** (add adjustment layer), **`−`** (delete selected layer), and **`Total Layers`** live counter.
  * Per-layer **Blend Mode** (`Normal`, `Multiply`, `Screen`, `Overlay`, `Soft Light`, `Darken`, `Lighten`), **Opacity (`0–100%`)**, and visibility eye toggle.

---

## 2. Complete Reference of All 41 Snapseed v4.x Tools

| # | Tool Name | Category | Controls, Presets & Parameters |
| :- | :--- | :--- | :--- |
| 1 | **Tune Image** | Tone | Brightness, Contrast, Saturation, Ambiance, Highlights, Shadows, Warmth (`-100` to `+100`) |
| 2 | **Color HSL** | Color | 8 Channels (Red, Orange, Yellow, Green, Aqua, Blue, Purple, Magenta) + Hue, Saturation, Luminance, Color Spread |
| 3 | **Color Grade** | Color | Interactive 360° HSL Spectrum Color Wheel for Global, Shadows, Midtones, Highlights + Luminance & Tonal Balance |
| 4 | **Curves** | Tone | RGB, Red, Green, Blue channels; Monotone Cubic Hermite Spline multi-point graph; Linear, Soft/Hard Contrast, Faded Film, Brighten presets |
| 5 | **White Balance** | Color | Auto White Balance button, Temperature, Tint |
| 6 | **Dehaze** | Tone | Dehaze Strength (`-100` mist/fog to `+100` atmospheric haze removal) |
| 7 | **Details** | Detail | Local micro-contrast Structure (`-100` to `+100`), Sharpening (`0` to `100`) |
| 8 | **Tonal Contrast** | Tone | High Tones, Mid Tones, Low Tones, Protect Shadows, Protect Highlights |
| 9 | **HDR Scape** | Tone | Presets (Nature, People, Fine, Strong) + Filter Strength, Brightness, Saturation |
| 10 | **RAW Develop** | Pro | Linear Exposure, Highlights, Shadows, Contrast, Structure, Temperature, Tint |
| 11 | **Smart Masking** | Pro | All Image, Subject Select, Sky Select, Background Select, Invert Mask, Mask Edge Feathering |
| 12 | **Selective** | Pro | Interactive U-Point control pins on canvas + Radius, Brightness, Contrast, Saturation, Structure |
| 13 | **Brush** | Pro | Dodge & Burn, Exposure, Temperature, Saturation, Eraser + Brush Strength (`-10` to `+10`), Brush Radius |
| 14 | **Healing** | Pro | Interactive blemish & object patch-clone brush + Undo Patch & Healing Brush Size |
| 15 | **Lens Blur** | Lens | Presets (Object Depth, Elliptical, Linear) + Blur Strength, Transition, Vignette |
| 16 | **Motion Blur** | Lens | Presets (All, Background, Subject) + Blur Strength, Angle (`-180°` to `+180°`), Acceleration |
| 17 | **Bloom** | Lens | Luminance-isolated Strength, Dispersion Size, Highlight Range threshold |
| 18 | **Halation** | Lens | Specular Threshold, Red-Orange Fringe Strength, Softness |
| 19 | **Chromatic Aberration** | Lens | Fringe Shift, Edge Fall-off, Anamorphic dispersion |
| 20 | **Glamour Glow** | Film | Styles 1–5 + Glow, Saturation, Warmth |
| 21 | **Film** | Film | 11 Film Stocks (`KP1 Portra 400`, `KP2`, `KG1`, `KE1`, `FS1`, `FS2`, `FP1`, `AG1`, `AS1`, `PD1`, `TC1`) + Style Strength, Film Grain |
| 22 | **Grainy Film** | Film | Presets (`A01`–`X02`) + Style Strength, Grain |
| 23 | **LUTs** | Color | Built-in cinematic LUTs + `.cube` / `.3dl` 3D LUT file importer with trilinear interpolation & LUT Intensity |
| 24 | **Black & White** | Film | Presets (Neutral, Contrast, Bright, Dark, Film, Dark Sky) + B&W Mix, Brightness, Contrast, Grain |
| 25 | **Noir** | Film | Presets `S01`–`S14` + Filter Strength, Brightness, Wash, Grain |
| 26 | **Vintage** | Film | Styles `1`–`12` + Style Strength, Brightness, Saturation, Vignette |
| 27 | **Retrolux** | Film | Styles `1`–`13` + Shuffle button, Style Strength, Brightness, Saturation, Contrast, Scratches, Light Leaks |
| 28 | **Drama** | Film | Presets (Drama 1–2, Bright 1–2, Dark 1–2) + Filter Strength, Saturation |
| 29 | **Grunge** | Film | Styles `1`–`15` + Shuffle button, Style Strength, Brightness, Contrast, Texture, Saturation |
| 30 | **Portrait** | Portrait | Face Spotlight, Skin Smoothing, Eye Clarity, Teeth Whitening, Lip Color Pop |
| 31 | **Head Pose** | Portrait | 3D Tilt, 3D Turn, Pupil Size, Smile, Focal Length |
| 32 | **Crop** | Geo | Freeform & Aspect Ratios (`Free`, `Original`, `1:1`, `3:2`, `4:3`, `5:4`, `16:9`), draggable canvas corner/edge brackets, numeric bounds, Apply Crop |
| 33 | **Rotate** | Geo | 90° Left/Right, Horizontal/Vertical Flip, Straighten Angle (`-45°` to `+45°`) |
| 34 | **Perspective** | Geo | Presets (Smart Edge Fill, White Fill, Black Fill) + Vertical Tilt, Horizontal Tilt, Rotate, Scale |
| 35 | **Expand** | Geo | Presets (Smart Edge Fill, White, Black) + Top, Bottom, Left, Right border expansion (`0–50%`) |
| 36 | **Double Exposure** | Pro | Second photo overlay loader + Blend Modes (`screen`, `lighten`, `darken`, `overlay`, `multiply`) & Opacity |
| 37 | **Vignette** | Lens | Outer Brightness, Inner Brightness, Radius |
| 38 | **Text** | Pro | 7 Typography Styles (`Modern Badge`, `Editorial Serif`, `Cinema Poster`, `Typewriter Mono`, `Script Signature`, `Gallery Stamp`, `Retro Box`), Color swatches, Font Size, Opacity, direct canvas drag |
| 39 | **Frames** | Film | 8 Border Styles (`Clean White`, `Clean Black`, `Polaroid`, `Film 35mm`, `Medium Format`, `Darkroom Rough`, `Instant Slide`, `Gallery Mat`) + Frame Width |
| 40 | **Snapseed Camera** | Pro | Live `getUserMedia` viewfinder with automatic stream cleanup and one-click capture into workspace |
| 41 | **Edit Stack, Batch & Looks** | Pro | Copy and paste complete non-destructive parameter stacks across open workspace tabs |

---

## 3. UI & Rendering Audit (Current Build Review)

Based on the visual inspection of the active workspace (`2B1A6344.JPG`, `5472 × 3648`), three specific UI and rendering items require attention:

### 1. Bottom Control Dock Clipping & Dual Scrollbars *(Selected Area)*
* **Observation**: Under **TUNE IMAGE**, the 3-column slider grid displays Row 1 (*Brightness*, *Contrast*, *Saturation*) and Row 2 (*Ambiance*, *Highlights*, *Shadows*), while Row 3 (*Warmth*) is vertically clipped at the bottom edge. Both a vertical scrollbar (right) and a horizontal scrollbar (bottom) appear inside the dock.
* **Root Cause**: Fixed height constraints on `#bottomControlsDock` combined with `overflow-x: auto` / `overflow-y: auto` and tall card vertical padding prevent all 3 rows from fitting simultaneously.
* **Recommended Fix**:
  * Set `#bottomControlsDock` to `height: auto; overflow: visible;` (or compact card padding to `py-1.5 px-2.5` with `gap-1.5`) so all 3 slider rows render cleanly in full view with zero scrollbars.

### 2. Main Canvas & Histogram Blank Display on High-Resolution Photos
* **Observation**: Although `2B1A6344.JPG` (`5472 × 3648`) is loaded and tonal percentages (`Shad: 43%`, `Mid: 47%`, `High: 11%`) are populated, both the center `#mainCanvas` and the `#histogramCanvas` appear blank.
* **Root Cause**: A container sizing / `ResizeObserver` race condition where `fitAndDrawMainCanvas()` or `updateHistogram()` executes before flex layout dimensions stabilize, or CSS `max-w-full max-h-full` conflicts with explicit inline pixel dimensions on `#mainCanvas`.
* **Recommended Fix**:
  * Remove conflicting `max-w-full max-h-full` classes from `#mainCanvas` when setting explicit `style.width` and `style.height`, and trigger a deferred `requestAnimationFrame` redraw immediately after `syncWorkspaceUI()` unhides `#mainCanvas`.

### 3. Native Light-Theme Scrollbars on Dark Panels
* **Observation**: Bright system-default scrollbars appear on the left category strip (`All (41)`, `Tone`, `Color`, `Detail`), the left tool list, and the bottom adjustment dock.
* **Recommended Fix**:
  * Add `color-scheme: dark;` to `:root`, wrap the left category buttons cleanly with `flex-wrap` so no horizontal scrollbar is needed, and apply dark `::-webkit-scrollbar` styling across all scrollable containers.