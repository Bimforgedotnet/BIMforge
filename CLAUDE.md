# CLAUDE.md — BIMforge Project Context

## Project overview

BIMforge is a single-file HTML application that teaches BIM/Revit fundamentals through interactive 3D exercises, structured as Duolingo-style lessons. Target audience: construction professionals learning Revit.

## Architecture

Everything lives in `index.html`. There is no build step, no bundler, no framework.

**External CDN dependencies (all loaded at runtime):**
- Three.js r128 — 3D rendering, raycasting, shadows
- Tailwind CSS (CDN) — utility-first styling
- Font Awesome 6.5 — icons
- Google Fonts — Space Grotesk (display) + Inter (body)

## Key constants

```js
GRID_SNAP = 0.3         // 300 mm snap grid
WALL_HEIGHT = 2.7       // 2700 mm
WALL_THICKNESS = 0.2    // 200 mm
PASS_THRESHOLD = 80     // % needed to pass a lesson
WINDOW_WIDTH/HEIGHT = 1.2 / 1.2
SILL_HEIGHT = 0.9
```

All coordinates are in **metres** internally; displayed as **millimetres** in the UI.

## State model

```js
currentChapter          // 1 or 2
currentLesson           // 1–N within chapter
chapterState[ch]        // { completed: bool[], scores: number[] }
placedElements[]        // Three.js meshes with userData.type
```

Lesson phases (L4 + L5): `'door'` → `'roof'` → `'done'`
Lesson 5 phase: `'walls'` → `'door'` → `'roof'` → `'done'`

## Content structure

### Chapter 1 — First Room (5 lessons)
1. Place first wall — X-axis, (0,0)→(3000,0)
2. Place second wall — Z-axis, (0,0)→(0,3000)
3. Complete room — 2 closing walls
4. Door & Roof — wall-hosted door + 4-click roof sketch
5. Final Challenge — full room from scratch, no guides, 80% to pass

### Chapter 2 — Windows & Openings (2 lessons)
- Pre-builds the Ch1 room on start (4 walls + door + roof)
1. Place first window — on bottom wall
2. Place window at offset — on right wall, near corner

## Scoring system

Each lesson scores 0–100%. Weights vary by lesson:
- **Walls**: endpoint accuracy (50%) + length (30%) + axis alignment (20%)
- **Roof**: corner accuracy (45%) + area (30%) + right angles (25%)
- **Door**: distance from wall centreline
- **Window**: correct wall (binary) + position accuracy
- **L5 overall**: walls (40%) + door (15%) + roof (25%) + room closure (20%)

`optimalWallMatch()` uses permutation search across all wall-to-target assignments so order of placement doesn't penalise the user.

## Raycasting modes

- **Wall drawing** (Ch1 L1–L3, L5 walls phase): raycast against ground plane → snap to grid → snap to existing endpoints
- **Wall-hosted placement** (door + Ch2 windows): raycast against wall meshes → project hit point along wall → show ghost outline preview
- **Roof** (L4 + L5 roof phase): raycast walls first, fall back to ground; snaps to wall top corners at `WALL_HEIGHT`

## Camera controls

| Action | Control |
|--------|---------|
| Orbit | Right-click drag / Alt + left drag |
| Pan | Shift + left drag |
| Zoom | Scroll wheel |

Views: 3D (default), Top (auto-switches for wall drawing), Front.

## UI panels

- **Landing page** — chapter cards; Ch2 locked until Ch1 complete
- **App shell** — header / tab bar / 3D viewport / right sidebar
- **Sidebar** — lesson objective, reference SVG (L5 only), properties, placed elements list
- **Results panel** — slides up from bottom right after each lesson
- **Chapter complete overlay** — animated rotating 3D preview of built room

## Adding a new chapter

1. Add entry to `CHAPTERS` object with `title`, `totalLessons`, `tabs[]`, `objectives{}`, `instructions{}`
2. Add entry to `chapterState`
3. Add scoring branch in `scoreAndComplete()`
4. Add chapter card to the landing page HTML
5. Wire up `startChapter(N)` for the new chapter

## Adding a new lesson to an existing chapter

1. Add tab label to `CHAPTERS[ch].tabs`
2. Add objective and instruction strings
3. Add scoring target to `LESSON_TARGETS` (Ch1) or `CH2_TARGETS` (Ch2)
4. Add scoring branch in `scoreAndComplete()`
5. Update `totalLessons` count in `CHAPTERS[ch]`

## File structure

```
/
├── index.html          # Entire application
├── CLAUDE.md           # This file
├── README.md           # Public-facing overview
├── ROADMAP.md          # Planned features
├── CURRICULUM.md       # Full lesson curriculum
├── assets/
│   ├── logos/          # Brand logos (place BIMforge PNGs here)
│   ├── icons/
│   └── images/
└── docs/
    ├── screenshots/
    └── notes/
```

## Constraints

- No build tools, no frameworks, no npm
- Do not split into multiple JS/CSS files unless the user explicitly requests it
- Do not introduce TypeScript, React, Vue, or any module system
- All external libraries must remain on CDN
