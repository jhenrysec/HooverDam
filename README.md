# 🏗️ Hoover Dam — 3D Structural Schematic

> **Interactive Three.js wireframe model of Hoover Dam — an engineering-briefing visualization built for authorized cybersecurity training and OT/ICS demonstration.**

[![License: MIT](https://img.shields.io/badge/License-MIT-cyan.svg)](#license)
[![Three.js: r128](https://img.shields.io/badge/Three.js-r128-blue.svg)](#requirements)
[![Self-Hosted](https://img.shields.io/badge/Dependencies-Self--Hosted-brightgreen.svg)](#requirements)
[![Offline: 100%](https://img.shields.io/badge/Offline-100%25-orange.svg)](#offline--deployment)
[![CSP: Compatible](https://img.shields.io/badge/CSP-Compatible-green.svg)](#content-security-policy)

---

## Overview

A Three.js-based interactive 3D wireframe model of Hoover Dam with a cinematic intelligence-briefing aesthetic. The whole experience is a single HTML file (~1,150 lines) plus a self-hosted copy of the Three.js library — no build step, no CDN, no external network calls at runtime.

It was originally built as the OT-target visualization component of an ICS/SCADA training lab and now stands on its own as a self-contained demonstration piece: a rotatable, labeled, spec-annotated 3D schematic of an arch-gravity dam and its power-generation systems.

---

## Features

- **Procedurally generated geometry** — arch-gravity dam body built from 32 curved segments with accurate taper (660 ft base → 45 ft crest)
- **10 major structural components modeled:**
  - Dam body (curved arch-gravity wall with ghost-fill transparency)
  - 4 intake towers (cylindrical, upstream face)
  - 2 powerhouse wings (downstream base, curved alignment)
  - 4 penstocks (curved tube geometry, 30 ft diameter)
  - 2 spillways with drum gate cylinders
  - 2 diversion tunnels (56 ft diameter)
  - Canyon walls (tapered rock geometry)
  - Lake Mead water surface (translucent disc)
  - Crest highway (US-93 road line)
- **10 projected 3D labels** with leader lines — anchored in 3D space, projected to screen coordinates, fade with camera distance, hide when behind camera
- **Interactive orbit controls** (hand-implemented, no external addon): left-drag rotate, scroll zoom, right-drag pan, full touch support
- **6 preset camera views**: Front, Side, Aerial, Downstream, Closeup, Top Down
- **Toggle controls**: Auto-rotate, X-ray mode (boosted transparency), Labels on/off, Grid on/off
- **HUD overlay**: real-time rotation/zoom readout, coordinate display, engineering specs in side panels
- **Zoomed-out default view** — the camera opens at a distance that frames the entire structure (dam body, towers, spillways, and canyon walls) on load, rather than starting in close

### Engineering Data Displayed

| Category | Data Points |
|---|---|
| Structure | 726 ft height, 1,244 ft crest, 660 ft base / 45 ft crest width |
| Power | 2,080 MW capacity, 17 Francis turbines, ~4.2 TWh annual output |
| Reservoir | 26.1M acre-ft capacity, 157,900 acres, 532 ft max depth |
| Construction | 1931–1936, 3.25M cubic yards concrete, ~21,000 workers |
| Penstocks | 30 ft diameter, steel-lined |
| Spillways | 50 ft wide, drum gates, 200,000 CFS capacity, 400 ft tunnels |
| Diversion Tunnels | 56 ft diameter, 4 tunnels, concrete-lined |

---

## Requirements

- A modern browser with **WebGL** support
- **Three.js r128** — included in the project as a self-hosted file (`three.min.js`); no CDN or internet access required

---

## Project Structure

```
hoover-dam/
├── index.html        ← The 3D schematic (single-file app)
└── three.min.js      ← Three.js r128, self-hosted (must sit beside index.html)
```

> **Both files must live in the same directory.** `index.html` loads Three.js with a relative `<script src="three.min.js"></script>` tag.

| File | Lines / Size | Description |
|---|---|---|
| `index.html` | ~1,150 lines | The full 3D wireframe model, HUD, controls, and labels |
| `three.min.js` | ~590 KB | Three.js r128 minified UMD build, self-hosted |

---

## Deployment

Drop both files into a directory served over HTTP(S) and open `index.html`:

```
your-site/
└── projects/
    └── dam/
        ├── index.html
        └── three.min.js
```

No build, no install, no package manager. Because the model is rendered entirely client-side and Three.js is self-hosted, the page works on a fully air-gapped host.

### Content Security Policy

This project is **CSP-friendly**. Three.js is loaded locally rather than from a CDN, so a strict `script-src 'self'` policy will run it without modification — there is no `cdnjs`/external-script dependency to allow-list.

> The page also references Google Fonts for its display typography. If the host enforces a CSP that blocks external stylesheets, the fonts simply fall back to the system stack (the model and HUD render correctly regardless). To keep the exact display fonts under a strict CSP, either allow `fonts.googleapis.com` / `fonts.gstatic.com` in `style-src`/`font-src`, or self-host the font files the same way Three.js is self-hosted.

### Offline / Air-Gapped Use

100% offline once the two files are in place. The geometry is procedurally generated in-browser, Three.js is bundled locally, and there are no runtime network calls required for the 3D model to function.

---

## Controls Reference

| Input | Action |
|---|---|
| Left-drag | Rotate the model |
| Scroll wheel | Zoom in / out |
| Right-drag | Pan the view |
| Touch | Rotate / pinch-zoom / pan |
| Front / Side / Aerial / Downstream / Closeup / Top Down | Snap to preset camera angle |
| Auto-Rotate | Toggle continuous rotation |
| X-Ray | Boost transparency to see internal structure |
| Labels | Toggle the projected 3D labels and leader lines |
| Grid | Toggle the ground reference grid |

---

## Technology Stack

| Layer | Technology |
|---|---|
| 3D Engine | Three.js r128 (self-hosted), WebGL |
| Geometry | Procedurally generated in-browser |
| Orbit Controls | Hand-implemented (no external addon) |
| Labels | 3D-anchored, projected to 2D screen space each frame |
| Typography | Orbitron, Chakra Petch, Share Tech Mono, Courier Prime (with system fallbacks) |
| External Dependencies | **None at runtime** (Three.js bundled locally) |

---

## Notes

- The model is a **stylized engineering schematic**, not a survey-accurate CAD model — dimensions in the HUD reflect published figures for Hoover Dam, while the geometry is a faithful but simplified procedural representation.
- This is a **visualization / demonstration** asset. It contains no vulnerable code and is safe to host publicly, unlike the intentionally-vulnerable lab server it was originally paired with.

---

## License

MIT License — See [LICENSE](LICENSE) for details.

Built for authorized cybersecurity training at [Higher Echelon, Inc.](https://higherechelon.com)
