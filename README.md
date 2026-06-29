# BIMforge

Interactive Revit/BIM training platform — Duolingo-style lessons for construction professionals.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![Three.js](https://img.shields.io/badge/Three.js-000000?style=flat&logo=threedotjs&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat&logo=tailwindcss&logoColor=white)

## What is this?

A single-file HTML prototype that teaches BIM fundamentals through hands-on 3D exercises. Users build a room step-by-step — placing walls, doors, and a roof — with real-time feedback and geometry-based scoring.

Built to demonstrate interactive BIM training to construction companies.

## Chapter 1 — First Room

| Lesson | Task | Interaction |
|--------|------|-------------|
| 1 | Place first wall | Two-click placement along X-axis |
| 2 | Place second wall | Two-click placement along Z-axis |
| 3 | Complete the room | Place 2 closing walls (any order) |
| 4 | Add door & roof | Wall-hosted door + 4-click roof sketch |

## Features

- **3D viewport** with orbit, pan, and zoom controls
- **300mm grid snapping** with endpoint snap assist
- **Wall corner joining** — perpendicular walls connect cleanly
- **Wall-hosted doors** — snap perpendicular to nearest wall face
- **Roof sketching** — 4-click boundary with corner guides
- **Geometry-based scoring** — length accuracy, endpoint position, axis alignment
- **Educational feedback** — tips explain what went wrong and how to fix it
- **Live measurements** — length, angle, and coordinates shown during placement
- **Chapter complete screen** — rotating 3D preview of the finished room
- **Dark professional UI** with orange (#F5620F) accent

## Quick Start

Open `index.html` in any modern browser. No build step, no dependencies to install.

## Tech Stack

- **Three.js r128** — 3D rendering, raycasting, shadow mapping
- **Tailwind CSS** (CDN) — utility-first styling
- **Font Awesome 6.5** — icons
- **Space Grotesk + Inter** — typography

## License

MIT
