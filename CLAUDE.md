# HCP - Crystal Structure Visualizer

## Project Overview
An interactive 3D web visualization comparing FCC (Face-Centered Cubic) and HCP (Hexagonal Close-Packed) crystal structures. Built as an educational tool for beginners learning crystallography.

## Tech Stack
- Single-file HTML application (`index.html`)
- **Three.js v0.162.0** (loaded via CDN import map)
- **OrbitControls** for 3D camera interaction
- No build tools, no dependencies to install — just open in a browser

## Architecture
Everything lives in `index.html`:
- **CSS**: Dark theme, responsive two-panel layout, info cards below
- **HTML**: Two 3D canvas panels (FCC left, HCP right), control buttons, info section with stacking diagrams and comparison table
- **JS module**: Three.js scenes with atom spheres, layer generation, unit cell wireframes, clipping planes, atom size scaling, click-to-hide with undo/redo stacks, clip-aware raycasting, and button/slider/keyboard logic

## Key Concepts Visualized
- **Stacking sequences**: FCC = ABCABC, HCP = ABABAB
- **Unit cells**: Cubic (FCC) vs hexagonal prism (HCP) wireframe overlays
- **Layer coloring**: A = blue (#60a5fa), B = green (#34d399), C = purple (#c084fc)

## User Controls

### Buttons (each panel)
- **Unit Cell** — toggle wireframe unit cell overlay
- **Unhide Last** — restore the last hidden atom (same as `Ctrl+Z`)
- **Unhide All** — restore all hidden atoms
- **Reset View** — reset camera, sliders, and all hidden atoms

### Click-to-hide
- **Click** an atom to hide it — useful for carving into the structure to see interiors
- Raycasting is **clip-aware**: clicking only targets atoms visible after slicing (atoms behind active clipping planes are ignored via `isPointVisible()` which checks `plane.distanceToPoint()`)
- Hidden atoms are tracked in a stack per panel; a counter shows "N hidden"

### Keyboard shortcuts (hover over a panel first)
- **Ctrl+Z** — unhide last hidden atom (pushes to redo stack)
- **Ctrl+Y** — re-hide last unhidden atom (redo)
- Redo stack clears when a new atom is click-hidden (standard undo/redo behavior)

### Sliders (each panel)
- **X / Y / Z Clip** — clipping planes that slice the structure along each axis, revealing interior atom arrangements. Slider at max = "Off" (no clipping). Uses `THREE.Plane` on materials with `side: DoubleSide` so cross-sections show solid interiors.
- **Atom Size (Radius)** — scales all atom spheres from 0.10 to 1.00 (default 0.35). Respects per-atom `userData.baseScale` so unit-cell atoms (0.8x) stay proportionally smaller.

## Conventions
- Atom base radius: 0.35 (Three.js units), unit-cell atoms have baseScale 0.8
- Vertical layer spacing: 0.816 (approx sqrt(2/3))
- Hex grid: rows/cols = 2 in each direction from origin

## Hosting & Sharing
- **Live URL**: https://fbardolph.github.io/fcc-hcp-viz/
- Hosted via **GitHub Pages** (deploy from `main` branch, root folder)
- **Repository**: https://github.com/fbardolph/fcc-hcp-viz
- Open Graph meta tags included for link preview support (og:image points to `FCCImage.png`)

## How to Run Locally
Open `index.html` in any modern browser. No server required (uses ES module import maps).

## Files
- `index.html` — the entire application (HTML + CSS + JS in one file)
- `FCCImage.png` — preview image used for Open Graph link previews
- `CLAUDE.md` — this project reference file
