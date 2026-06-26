# AGENTS.md

## Project Overview

**Chroma Drift** (originally known as **AGY-SOUNDSCAPE** or **Antigravity**) is a self-contained, single-page web application that combines tranquil generative music with interactive visual metaballs.

It was created in response to this prompt:

> "can you make a single page app in index.html i can load in my browser. it should pull in any libraries needed.
> i want something with some tranquil auto generated music and the user can click on the screen and generate big blobs of
> random color that grow and merge with each others
> make the color theme similar to the antigravity cli one"

The app features:
- Click (or drag) to spawn glowing, colorful metaballs that grow, drift, and merge.
- Ambient generative music using pentatonic scales with an optional slow background drone (disabled by default, togglable in UI).
- Musical chimes triggered when blobs collide and merge.
- Auto-generated "stardust" notes that periodically spawn new blobs.
- Rich retro-futuristic terminal-style UI layout.

Everything is contained in a single `index.html` file that works offline after initial CDN loads.

## How to Run

1. Open `index.html` directly in any modern browser (Chrome, Firefox, Safari, Edge).
2. No build step or local server is required.
3. Click **LET'S GO!** on the splash screen to start the audio context.

The app gracefully falls back to the native Web Audio API if Tone.js fails to load.

## Technology Stack

- **HTML/CSS/JS**: Everything in one file.
- **WebGL** (fragment shader): Real-time metaball rendering with soft glows, borders, scanlines, and noise.
- **Tone.js 14.8.49** (CDN): Primary audio engine for synths, reverb, delay, panning, and drone.
- **Web Audio API fallback**: Pure `AudioContext` implementation when Tone.js is unavailable.
- **Google Fonts**: JetBrains Mono + Outfit (loaded via CDN).

## Architecture & Key Components

### Visuals (`#webgl-canvas`)
- Fullscreen WebGL canvas using a simple quad + metaball fragment shader.
- Blobs are represented as position + radius + color uniforms (up to 64).
- Classic metaball formula: `sum(r² / d²)`.
- Blobs have soft auroral glows outside the main threshold and bright rims.

### Blob System (`BlobParticle` class)
- User blobs and "droplet" (stardust) blobs.
- Growth animation, gentle random drift, wall bouncing.
- Configurable evaporation rate (decay of `targetRadius`).
- Merging logic conserves approximate area and momentum, blends colors.

### Audio
- **Scales** (`SCALES`): 5 musical modes (Celestial, Melancholic, Peaceful, Mystical, Bright).
- **Main voices**: 6 triangle synths routed through panners + delay/reverb.
- **Chime voices**: 4 fast sine synths for merge events.
- **Drone**: Slow polyphonic sine drone with LFO-filtered lowpass (optional, controlled by the "AMBIENT BACKGROUND DRONE" UI toggle).
- Spatial panning based on horizontal position.
- Note selection biased by vertical click position in the current scale.

### Interaction
- `mousedown` / `touchstart` → large blob + note.
- Drag → streams of small fast-decaying "stardust" droplets.
- Collisions → harmonic chime chords.
- Autoplay sequencer (when enabled) spawns background blobs + notes.
- **Keyboard shortcuts**:
  - `R` / `r` → Reset / clear all blobs.
  - `C` / `c` → Open or close the Control Center (left panel).
  - `L` / `l` → Open or close the System Monitor Logs (right panel).

### UI
- Left panel: Master controls, scale selector, tempo, evaporation rate, presets.
- Right panel: Scrolling terminal-style event log.
- Collapsible side panels and pause/resume button.
- Three soundscape presets (Deep Space, Starlight, ETH Drone).

### Color Theme ("antigravity cli")
```css
--bg-color: #06080f;          /* Deep space blue-black */
--accent-cyan: #00f2fe;
--accent-magenta: #ff007f;
--accent-violet: #8b5cf6;
--accent-green: #10b981;
--accent-yellow: #f59e0b;
```

Mono font for headers/logs, subtle scanlines and grain for terminal feel.

## Important Implementation Details

- Maximum of 60 active blobs (oldest is dropped when exceeded).
- Blob data is packed into `Float32Array`s and uploaded to uniforms each frame.
- Audio must be started via a user gesture (`Tone.start()` or `AudioContext`).
- Decay rate is applied live to all existing blobs when changed.
- Merges calculate an aspect-corrected distance for correct collision on non-square screens.
- The app seeds the scene with 5 initial blobs after initialization.

## Guidelines for AI Agents & Contributors

- **Single-file discipline**: Keep the entire experience in `index.html`. Do not introduce separate JS/CSS files unless the user explicitly asks.
- **CDN policy**: Only add libraries via CDN (e.g., `cdnjs`, unpkg). Do not assume npm or build tooling.
- **Audio safety**:
  - Always respect the user gesture requirement.
  - Maintain the Tone.js + native fallback pattern.
  - Do not block the main thread with audio work.
- **Visual fidelity**:
  - The WebGL shader is the heart of the visual identity — edit carefully.
  - Preserve the cyan/magenta/violet "antigravity" (deep space) palette and dark space background.
- **Performance**:
  - Blob loop is O(n²) for merges — fine at current limit of 60.
  - Keep shader simple and avoid dynamic loops beyond the current 64-slot design.
- **Logging**: Use `logToTerminal(category, message, colorClass)` for user-visible events.
- **Mobile**: Touch support exists; be cautious when changing layout or adding heavy UI.
- **Testing**: Open the file locally and exercise click/drag, merges, scale changes, presets, pause, and long sessions.

## File Structure

```
/Users/justinhj/projects/highplay/
├── index.html     ← The entire application
└── AGENTS.md      ← This file
```

No other files exist in the project.

## Future Directions (Optional Ideas)

These are not implemented:
- Exporting recordings (audio + video)
- More scales / microtonal options
- Particle trails or background starfield
- MIDI output or Web MIDI input
- Saving/loading user scenes

Only implement if requested.

---

This document exists to help future agents (and humans) quickly understand the intent, constraints, and structure of the Chroma Drift soundscape.