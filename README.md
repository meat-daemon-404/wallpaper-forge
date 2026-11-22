# Wallpaper Forge (v0.10.0)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python Desktop](https://img.shields.io/badge/Desktop_Tests-635_Passing_(98.91%25_Cov)-3776AB?logo=python&logoColor=white)](https://github.com/meat-daemon-404/wallpaper-forge)
[![Web PWA](https://img.shields.io/badge/Web_Tests-422_Passing_(98.81%25_Cov)-2ea44f?logo=javascript)](https://github.com/meat-daemon-404/wallpaper-forge/tree/main/web)

> **Dual-Runtime (Python Desktop GUI + Offline-Capable Web PWA) Wallpaper Format Converter, Timeline Video/GIF Editor & Wallpaper Engine `.pkg`/`.tex`/`.mpkg` Unpacker**

## Core Capabilities (v0.10.0)

1. **Wallpaper Engine `.pkg` / `.tex` / `.mpkg` Unpacker & Texture Decoder**
   - Parses PKGV0001–PKGV0022 archive headers and decodes TEXV0001–TEXV0004 textures (RGBA8888, DXT1/BC1, DXT5/BC3, RG88, R8, raw MP4/WebM/PNG streams, and LZ4-compressed mipmaps) in both Python (`src/wallpaper_forge/pkg_unpacker.py`) and pure browser Web Workers (`web/lib/pkg.js` + `web/process_worker.js`).
2. **Batch Wallpaper Converter & Smart Aspect-Ratio Crop**
   - Converts and resizes static/animated wallpapers across `PNG`, `JPEG`, `WebP`, `AVIF`, `GIF`, `MP4`, and `WebM` with presets for 16:9 (1080p/2K/4K), 21:9 Ultrawide, 32:9 Super-Ultrawide, and mobile portrait ratios.
3. **Non-Linear Timeline Video & GIF Wallpaper Editor**
   - Frame-accurate trim, loop crossfade, speed ramp, FPS resample, color grading (brightness/contrast/saturation), and live preview.
4. **Hardened Web Worker Concurrency & Offline PWA (`web/`)**
   - **2-Way Bounded Worker Pool (`runLimited` & `poolConcurrency()`)**: Prevents browser OOM during large 4K batch jobs by clamping Web Worker concurrency to `[1, 2]` with automatic main-thread fallback if a worker crashes.
   - **Strict CSP, SRI & Service Worker Offline Shell**: Works 100% locally in the browser with zero server upload required.

## Quick Start

### 1. Python Desktop Application

```bash
git clone https://github.com/meat-daemon-404/wallpaper-forge.git
cd wallpaper-forge
python -m pip install -e ".[dev]"

# Launch the desktop GUI
python -m wallpaper_forge

# Or run CLI batch conversion / PKG extraction
python -m wallpaper_forge unpack scene.pkg -o ./extracted
```

### 2. Web PWA (`web/`)

```bash
# Serve the zero-build static Web PWA locally
python -m http.server 8080 --directory web
```

## Verification Suite (1,057 Total Automated Tests)

```bash
# 1. Run all 635 Python desktop tests (98.91% coverage)
pytest -q

# 2. Run all 422 Node.js Web PWA & Worker tests (98.81% web/lib coverage)
node --test web/tests/*.test.mjs
```

## License

Released under the [MIT License](LICENSE).
