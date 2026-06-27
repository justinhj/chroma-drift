# Chroma Drift // Generative Soundscape

> A self-contained, interactive audiovisual soundscape combining tranquil generative music with fluid WebGL metaballs, wrapped in a retro-futuristic terminal UI.

---

## 🌌 Overview

**Chroma Drift** is a browser-based generative instrument and visualizer. Click, drag, and interact with the screen to release glowing liquid blobs of color that float, merge, and trigger harmonic chimes upon colliding. A slow generative engine breathes life into the background with ambient stardust notes, accompanied by a togglable deep cosmic drone.

Everything is packed into a single, offline-capable file ([index.html](file:///Users/justinhj/projects/highplay/index.html)). No servers, compilers, or installation required.

---

## 🎨 Key Features

- **Fluid Visual Metaballs:** Real-time WebGL fragment shader rendering glowing blobs of color that dynamically warp and merge when they collide.
- **Generative Music Engine:** Beautiful pentatonic melodies powered by **Tone.js**. A note's pitch is determined by its vertical coordinate on screen, and its spatial panning follows its horizontal position.
- **Merge Chimes:** When two or more blobs collide and fuse, a chime chord triggers, producing rich harmonic intervals.
- **Ambient Drone:** A slow, LFO-modulated background polyphonic drone that adds depth (enabled via the Control Center).
- **Stardust Sequencer:** Auto-spawns random background droplets to keep the audio and visuals drifting infinitely.
- **Retro-Futuristic Terminal UI:** Collapsible control drawers, scrolling event logs, subtle scanlines, and a CRT-inspired visual grain.

---

## 🚀 Quick Start

1. Open [index.html](file:///Users/justinhj/projects/highplay/index.html) directly in any modern web browser (Chrome, Firefox, Safari, Edge).
2. Click **LET'S GO!** on the splash screen to initialize the audio context.
3. Interact! Click/tap or drag your cursor across the dark space.

---

## ⌨️ Controls & Shortcuts

Interact with the soundscape using your mouse, touch screen, or keyboard:

| Control | Action |
| :--- | :--- |
| **Click / Tap** | Spawn a large metaball and play a primary synth note. |
| **Click + Drag** | Stream small, fast-decaying "stardust" droplets that create gentle high-pitched tones. |
| **`C` / `c`** | Open or close the **Control Center** (left panel). |
| **`L` / `l`** | Open or close the **System Monitor Logs** (right panel). |
| **`R` / `r`** | Reset / Clear all active blobs on screen. |
| **`Spacebar`** | Toggle Pause / Resume (freezes the soundscape logic). |

---

## ⚙️ Configuration & Presets

Open the **Control Center** (`C`) to customize the soundscape parameters:

- **Musical Scale Selector:** Shift the mood between 5 distinct pentatonic profiles:
  - `Celestial` • `Melancholic` • `Peaceful` • `Mystical` • `Bright`
- **Evaporation Rate:** Control how fast blobs shrink and disappear (from permanent/slow-decay to rapid evaporation).
- **Tempo (BPM):** Speeds up or slows down the automatic stardust node sequencer.
- **Ambient Drone:** Turn on/off the slow-pulsing background synth pad.
- **Soundscape Presets:** Quick-launch pre-configured states:
  - 🌌 **Deep Space:** Slow, long-decaying cyan/magenta blobs with a heavy drone.
  - ✨ **Starlight:** Fast, sparkly high-frequency stardust droplets with rapid decay.
  - 🚀 **ETH Drone:** A continuous mystical drone focus with a slow, relaxed bubble pace.

---

## 🛠️ Built With

- **HTML5 & Vanilla CSS3** (utilizing CSS custom properties, backdrop filters, and CSS Grid)
- **WebGL** (custom fragment shader for metaball arithmetic, glows, rims, and CRT scanlines)
- **Tone.js 14.8.49** (CDNs) for audio generation, effects processing (Delay, Reverb, Panning), and synthesis (Triangle/Sine synths)
- **Native Web Audio API Fallback** (in case Tone.js fails to load or is blocked)
- **Google Fonts** (JetBrains Mono & Outfit)
