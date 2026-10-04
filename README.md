# C3.AVcompressorMenu

```text
░█▀▀░▀▀█░█▀█░█▀▀░▀█▀
░█░░░░▀▄░█░█░█▀▀░░█░
░▀▀▀░▀▀░░▀░▀░▀▀▀░░▀░

C3.AVcompressorMenu
--------------------------------------------------------
```

**Interactive Terminal CLI Menu Application for [C3.AVcompressor](https://github.com/c0d3d-net/C3.AVcompressor/)**  
**Development Team:** C3net Development (C0D3D-NET)  
**Binary Interface:** `c3avcompressor`  
**Target Platforms:** macOS (Apple Silicon M1–M4 & Intel) & Linux (x86_64, aarch64)

---

## ⚡ Overview & Highlights

`C3.AVcompressorMenu` is an interactive terminal control center for the highly optimized, AI/NPU-accelerated media transcoder `C3.AVcompressor`. It offers intuitive menu navigation with ANSI color gradients, a real-time configuration summary, drag-and-drop path support, and complete control over all transcoding and media processing features.

- **Single File Mode:** Quick transcoding of an individual file with automated destination path calculation (`ReadyConv/`).
- **Batch Folder Processing (Batch Folder Mode):**
  - Scans a selected directory for all supported video files (`.mp4`, `.mkv`, `.mov`, `.avi`, `.webm`, `.m4v`, `.ts`, `.flv`, `.wmv`, `.vob`, `.mpg`, `.mpeg`, `.m2ts`).
  - **No Subfolder Scanning:** Strictly processes only the top level of the selected folder.
  - **Automatic Destination Folder `ReadyConv`:** Creates a `ReadyConv` subfolder in the same directory as the source and saves all converted videos there.
  - Progress display with file counter `[1/N]`, before/after file size comparison, and calculated percentage of space saved.
  - Detection of already existing destination files with skip/overwrite options (ideal for resuming interrupted batch jobs).
- **Complete Configurability of All Parameters:**
  - **Video Codecs:** `hevc` (H.265 / Apple VideoToolbox / NPU), `h264`, `av1` (SVT-AV1), `vp9`, `prores`, `copy` (lossless passthrough).
  - **Video Sizing & Scaling:**
    - Keep original size (100%)
    - Set target width (`-w`, height is calculated proportionally)
    - Set target height (`--height`, width is calculated proportionally)
    - Set width and height (`--resolution WxH`, e.g., `1920x1080`)
    - Preset resolutions (`1080p`, `720p`, `4k`, `480p`)
  - **Bitrate & Quality Control:**
    - Dynamic AI-CRF mode (CRF 16–38, adaptive quantization via NPU saliency)
    - Fixed video bitrate (e.g., `2000k`, `4500k`, `5M`)
  - **Audio Codecs & Bitrates:** `aac`, `ac3`, `dts`, `wav`, `mp3`, `flac`, `opus`, `copy` with bitrates from `128k` to `320k` or custom values.
  - **Container Types:** `.mp4`, `.mkv`, `.webm`, `.mov`, or retain source extension.
  - **Framerate (FPS):** Freely configurable (24, 25, 30, 60, etc.) or original.
  - **NPU/AI Control & Hardware Accelerators:** Switchable between VideoToolbox, VA-API, NVENC, or CPU.
  - **Transcoding Presets:** Quick selection from predefined profiles (`enc_hevc_balanced`, `enc_hevc_ultrafast`, `enc_hevc_hq_1080p`, `enc_hevc_extreme`, `enc_h264_compat`, `enc_prores`, `enc_stream_copy`, etc.).
- **Additional Media Utilities:**
  - **Split Mode:** Split by start/end timestamp, duration, fixed-length segments, or **AI Scene Cut Detection**.
  - **Extract Mode:** Extract audio tracks (MP3, AAC, AC3, WAV, FLAC, Opus) or pure video tracks (without audio).
  - **Mux Mode:** Merge separate video and audio files into a single container.
  - **Probe Mode:** Media analysis (streams, codecs, bitrates, channels) with formatted text or JSON output.
  - **NPU Status:** Displays detected Neural Processing Units (Apple M-Series ANE, TOPS, UMA) and available hardware encoders.
  - **Benchmark:** NPU throughput benchmark vs. conventional encoders (1080p / 4K).
- **Configuration Persistence:** User settings are automatically saved to `~/.config/c3avcompressormenu/config.env` and reloaded on next startup.

---

## 📦 Multi-Platform Installation Packages (`dist/`)

Just like with `C3.AVcompressor`, pre-built installation packages are available.

### 🍏 macOS Installer Package (.pkg)
Installs `c3avcompressormenu` system-wide to `/usr/local/bin`, including man pages and shell completions:

### 🐧 Debian / Ubuntu Packages (.deb)
Installs the menu system-wide via `dpkg` or `apt`:
```bash
# For x86_64 / amd64:
sudo dpkg -i c3avcompressormenu_0.1.0_amd64.deb

# For ARM64 / aarch64:
sudo dpkg -i c3avcompressormenu_0.1.0_arm64.deb
```

---

## 📂 Directory Structure & `ReadyConv` Destination
When using **Batch Folder Mode** (Option `2`) or **Single File Mode** (Option `1`) from the menu:

```text
/MyVideoFolder/
├── Clip1.mov
├── Vacation.mkv
├── Video.mp4
├── Subfolder/                  <-- Will NOT be scanned
│   └── ignored.mp4
└── ReadyConv/                  <-- Automatically created by the menu
    ├── Clip1.mp4
    ├── Vacation.mp4
    └── Video.mp4
```

- All converted files are safely saved to the `ReadyConv` subfolder within the source folder.
- Your original files remain 100% untouched.

---

## 🖥️ Main Menu Overview

```text
╔══════════════════════════════════════════════════════════════════════════╗
║  CURRENT TRANSCODING & COMPRESSION CONFIGURATION                         ║
╠══════════════════════════════════════════════════════════════════════════╣
║  • Profile/Preset:      [Custom]
║  • Video Codec:         HEVC | Preset: balanced
║  • Bitrate Mode:        Dynamic CRF: 23 (AI Dynamic Rate Control)
║  • Video Size:          Keep original size (100%)
║  • Target Video Type:   .mp4
║  • Audio:               AAC (256k)
║  • Hardware / NPU:      HW: auto | NPU-AI: Enabled
╚══════════════════════════════════════════════════════════════════════════╝

[MAIN MENU]
  1) 🎬 Compress / convert single video file
  2) 📁 Scan & batch process whole folder (Batch -> 'ReadyConv')
  3) ⚙️  Configure video & transcoding options (codec, bitrate, size...)
  4) ⚡ Load / select transcoding preset (Apple HEVC, ProRes, Web...)
  5) ✂️  Cut & split video (Split Mode: time range, segments, AI scene)
  6) 🎵 Extract audio / video track (Extract Mode: MP3, AAC, AC3, WAV...)
  7) 🔀 Merge video & audio (Mux Mode)
  8) 🔍 Analyze media file (Probe File)
  9) 🧠 View NPU & hardware status (NPU status / TOPS)
 10) 🚀 Run NPU throughput benchmark (1080p / 4K)
 11) 📜 List all system presets (Presets List)
 12) 🔄 Reset configuration to defaults
  0) 🚪 Exit
```

---
