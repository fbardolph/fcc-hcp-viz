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
- **JS module**: Three.js scenes with atom spheres, layer generation, unit cell wireframes, clipping planes, atom size scaling, and button/slider logic

## Key Concepts Visualized
- **Stacking sequences**: FCC = ABCABC, HCP = ABABAB
- **Unit cells**: Cubic (FCC) vs hexagonal prism (HCP) wireframe overlays
- **Layer coloring**: A = blue (#60a5fa), B = green (#34d399), C = purple (#c084fc)

## User Controls
Each panel has three buttons:
- **Show Layers** — toggle full stacked-layer atom view
- **Unit Cell** — toggle wireframe unit cell overlay
- **Reset View** — reset camera to default position and all sliders

Each panel has sliders:
- **X / Y / Z Clip** — clipping planes that slice the structure along each axis, revealing interior atom arrangements. Slider at max = "Off" (no clipping). Uses `THREE.Plane` on materials with `side: DoubleSide` so cross-sections show solid interiors.
- **Atom Size (Radius)** — scales all atom spheres from 0.10 to 1.00 (default 0.35). Respects per-atom `userData.baseScale` so unit-cell atoms (0.8x) stay proportionally smaller.

## Conventions
- Atom base radius: 0.35 (Three.js units), unit-cell atoms have baseScale 0.8
- Vertical layer spacing: 0.816 (approx sqrt(2/3))
- Hex grid: rows/cols = 2 in each direction from origin

## How to Run
Open `index.html` in any modern browser. No server required (uses ES module import maps).
