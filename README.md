# C3.AVcompressorMenu

```text
░█▀▀░▀▀█░█▀█░█▀▀░▀█▀
░█░░░░▀▄░█░█░█▀▀░░█░
░▀▀▀░▀▀░░▀░▀░▀▀▀░░▀░

C3.AVcompressorMenu
--------------------------------------------------------
```

**Interaktive Terminal-CLI-Menü-Anwendung für [C3.AVcompressor](https://github.com/c0d3d-net/C3.AVcompressor/)**  
**Entwickler-Team:** C3net Development (C0D3D-NET)  
**Binary-Schnittstelle:** `c3avcompressor`  
**Zielplattformen:** macOS (Apple Silicon M1–M4 & Intel) & Linux (x86_64, aarch64)

---

## ⚡ Übersicht & Highlights

`C3.AVcompressorMenu` ist ein interaktives Terminal-Kontrollzentrum für den hochoptimierten, KI/NPU-beschleunigten Medien-Transcoder `C3.AVcompressor`. Es bietet eine intuitive Menüsteuerung mit farbigen ANSI-Verläufen, Echtzeit-Konfigurationsübersicht, Drag-and-Drop-Unterstützung für Pfade und vollständiger Kontrolle über alle Transcoding- und Medienbearbeitungsfunktionen.

- **Einzeldatei-Modus (Single File):** Schnelle Transcodierung einer einzelnen Datei mit automatischer Zielpfad-Berechnung (`ReadyConv/`).
- **Ordner-Stapelverarbeitung (Batch Folder Mode):**
  - Scannt einen ausgewählten Ordner nach allen vorhandenen Videodateien (`.mp4`, `.mkv`, `.mov`, `.avi`, `.webm`, `.m4v`, `.ts`, `.flv`, `.wmv`, `.vob`, `.mpg`, `.mpeg`, `.m2ts`).
  - **Kein Scannen von Unterordnern:** Verarbeitet strikt nur die oberste Ebene des ausgewählten Ordners.
  - **Automatischer Zielordner `ReadyConv`:** Erstellt im selben Ordner wie die Quelle einen Unterordner `ReadyConv` und speichert dort alle konvertierten Videos.
  - Fortschrittsanzeige mit Dateizähler `[1/N]`, Vorher-Nachher-Größenvergleich und berechneter Speicherersparnis in Prozent.
  - Erkennung bereits existierender Zieldateien mit Überspringen/Überschreiben-Option (ideal zum Wiederaufnehmen unterbrochener Batches).
- **Vollständige Einstellbarkeit aller Parameter:**
  - **Video-Codecs:** `hevc` (H.265 / Apple VideoToolbox / NPU), `h264`, `av1` (SVT-AV1), `vp9`, `prores`, `copy` (Lossless Passthrough).
  - **Videogröße & Skalierung:**
    - Originalgröße beibehalten (100%)
    - Zielbreite festlegen (`-w`, Höhe wird automatisch proportional berechnet)
    - Zielhöhe festlegen (`--height`, Breite wird automatisch proportional berechnet)
    - Breite und Höhe festlegen (`--resolution WxH`, z. B. `1920x1080`)
    - Preset-Auflösungen (`1080p`, `720p`, `4k`, `480p`)
  - **Bitrate- & Qualitätskontrolle:**
    - Dynamischer AI-CRF-Modus (CRF 16–38, adaptive Quantisierung durch NPU-Saliency)
    - Feste Video-Bitrate (z. B. `2000k`, `4500k`, `5M`)
  - **Audio-Codecs & Bitraten:** `aac`, `ac3`, `dts`, `wav`, `mp3`, `flac`, `opus`, `copy` mit Bitraten von `128k` bis `320k` oder benutzerdefiniert.
  - **Container-Typen:** `.mp4`, `.mkv`, `.webm`, `.mov` oder Quell-Endung beibehalten.
  - **Framerate (FPS):** Frei konfigurierbar (24, 25, 30, 60, etc.) oder Original.
  - **NPU/AI-Steuerung & Hardware-Beschleuniger:** Umschaltbar zwischen VideoToolbox, VA-API, NVENC oder CPU.
  - **Transcoding-Presets:** Schnellauswahl aus vordefinierten Profilen (`enc_hevc_balanced`, `enc_hevc_ultrafast`, `enc_hevc_hq_1080p`, `enc_hevc_extreme`, `enc_h264_compat`, `enc_prores`, `enc_stream_copy`, etc.).
- **Zusätzliche Medien-Werkzeuge:**
  - **Split Mode:** Schneiden nach Start/End-Zeitstempel, Dauer, gleich langen Segmenten oder **AI Scene Cut Detection**.
  - **Extract Mode:** Extrahieren von Audiospuren (MP3, AAC, AC3, WAV, FLAC, Opus) oder reinen Videospuren (ohne Ton).
  - **Mux Mode:** Zusammenführen separater Video- und Audio-Dateien.
  - **Probe Mode:** Medienanalyse (Streams, Codecs, Bitraten, Kanäle) mit formatiertem Text oder JSON.
  - **NPU Status:** Anzeige der erkannten Neural Processing Units (Apple M-Series ANE, TOPS, UMA) und Encoder.
  - **Benchmark:** NPU-Durchsatz-Test gegen klassische Encoder (1080p / 4K).
- **Konfigurations-Persistenz:** Benutzereinstellungen werden automatisch in `~/.config/c3avcompressormenu/config.env` gespeichert und beim nächsten Start wieder geladen.

---

## 📦 Multi-Plattform Installationspakete (`dist/`)

Wie auch bei `C3.AVcompressor` stehen fertige Installationspakete zur Verfügung.

### 🍏 macOS Installer Package (.pkg)
Installiert `c3avcompressormenu` systemweit nach `/usr/local/bin`, inklusive Man-Page und Shell-Completions:

### 🐧 Debian / Ubuntu Packages (.deb)
Installiert das Menü systemweit via `dpkg` oder `apt`:
```bash
# Für x86_64 / amd64:
sudo dpkg -i c3avcompressormenu_0.1.0_amd64.deb

# Für ARM64 / aarch64:
sudo dpkg -i c3avcompressormenu_0.1.0_arm64.deb
```

---

## 📂 Ordnerstruktur & Speicherort `ReadyConv`
Wenn Sie im Menü den **Batch Folder Mode** (Option `2`) oder den **Single File Mode** (Option `1`) verwenden:

```text
/MeinVideoOrdner/
├── Clip1.mov
├── Urlaub.mkv
├── Video.mp4
├── Unterordner/                <-- Wird NICHT gescannt
│   └── ignored.mp4
└── ReadyConv/                  <-- Automatisch vom Menü erstellt
    ├── Clip1.mp4
    ├── Urlaub.mp4
    └── Video.mp4
```

- Alle Zieldateien landen sicher im Unterordner `ReadyConv` im selben Ordner wie die Quelldateien.
- Ihre Originaldateien bleiben zu 100 % unangetastet.

---

## 🖥️ Hauptmenü-Übersicht

```text
╔══════════════════════════════════════════════════════════════════════════╗
║  AKTUELLE TRANSCODING- & KOMPRESSIONS-KONFIGURATION                      ║
╠══════════════════════════════════════════════════════════════════════════╣
║  • Profil/Preset:      [Benutzerdefiniert]
║  • Video-Codec:        HEVC | Preset: balanced
║  • Bitrate-Modus:      Dynamischer CRF: 23 (AI Dynamic Rate Control)
║  • Videogröße:         Originalgröße beibehalten (100%)
║  • Ziel-Videotyp:      .mp4
║  • Audio:              AAC (256k)
║  • Hardware / NPU:     HW: auto | NPU-AI: Aktiviert
╚══════════════════════════════════════════════════════════════════════════╝

[HAUPTMENÜ]
  1) 🎬 Einzelne Video-Datei komprimieren / konvertieren
  2) 📁 Ganzen Ordner scannen & stapelverarbeiten (Batch -> 'ReadyConv')
  3) ⚙️  Video- & Transcoding-Optionen konfigurieren (Codec, Bitrate, Größe...)
  4) ⚡ Transcoding-Preset laden / auswählen (Apple HEVC, ProRes, Web...)
  5) ✂️  Video schneiden & teilen (Split Mode: Zeitbereich, Segmente, AI-Scene)
  6) 🎵 Tonspur / Videospur extrahieren (Extract Mode: MP3, AAC, AC3, WAV...)
  7) 🔀 Video & Audio zusammenfügen (Mux Mode)
  8) 🔍 Mediendatei analysieren (Probe File)
  9) 🧠 NPU & Hardware-Status anzeigen (NPU-Status / TOPS)
 10) 🚀 NPU Durchsatz-Benchmark ausführen (1080p / 4K)
 11) 📜 Alle System-Presets auflisten (Presets List)
 12) 🔄 Konfiguration auf Standard zurücksetzen
  0) 🚪 Beenden
```

---
