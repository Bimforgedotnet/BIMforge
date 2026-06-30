# BIMforge Curriculum

All coordinates are in millimetres as displayed in the UI (internally stored in metres).

---

## Chapter 1 — First Room

**Goal:** Build a complete 3000 × 3000 mm room from scratch.  
**Lessons:** 5 (lessons 1–4 are guided; lesson 5 is an unguided final challenge)

---

### Lesson 1 — Place First Wall

**Objective:** Place a wall along the X-axis from (0, 0) to (3000, 0).  
**Interaction:** Two clicks — start point, then end point.  
**View:** Auto-switches to Top view.  
**Scoring:**
- Endpoint accuracy: 50%
- Length accuracy: 30%
- Axis alignment (X-axis): 20%

**Pass threshold:** 80%

---

### Lesson 2 — Place Second Wall

**Objective:** Place a wall along the Z-axis from (0, 0) to (0, 3000).  
**Interaction:** Same two-click wall placement.  
**View:** Top view.  
**Scoring:** Same formula as Lesson 1, checking Z-axis alignment.

---

### Lesson 3 — Complete the Room

**Objective:** Place 2 closing walls to enclose the room.
- Wall A: (3000, 0) → (3000, 3000)
- Wall B: (0, 3000) → (3000, 3000)

**Order:** Either wall can be placed first.  
**Scoring:**
- Each wall scored independently (best-match assignment)
- Room closure score (25% weight): checks all 4 corners are met

**Colour feedback during placement:**
- Grey = accurate (< 200 mm error)
- Yellow = close (200–400 mm)
- Red = far off (> 400 mm)

---

### Lesson 4 — Door & Roof

**Two-phase lesson.**

**Phase 1 — Door:**
- Hover over any wall to highlight it; click to place a door.
- Door: 900 mm wide × 2100 mm tall, auto-aligned perpendicular to wall face.
- Scoring: distance from wall centreline (< 150 mm = 100%)

**Phase 2 — Roof:**
- Click the 4 top corners of the walls (green guide markers shown).
- Cursor snaps to wall top corners at height 2700 mm.
- Roof: flat extruded slab (150 mm thick) spanning the 4 clicked points.
- Scoring: corner accuracy (45%) + area match (30%) + right angles (25%)

**Overall lesson score:** door (30%) + roof (70%)

---

### Lesson 5 — Final Challenge ⭐

**Objective:** Build the complete room from scratch with no guides.  
**Sequence:** 4 walls → door → roof  
**View:** Auto-switches to Top view.

**Scoring breakdown:**
- Walls: 40% (average of 4 walls, optimal assignment)
- Door: 15% (must be on the bottom wall, centred near (1500, 0))
- Roof: 25%
- Room closure: 20%

**Reward:** Score × 10 XP awarded on pass.  
**Fail:** Retry button shown; no chapter unlock until 80%+ achieved.

---

## Chapter 2 — Windows & Openings

**Goal:** Place windows on existing walls using wall-hosted placement.  
**Setup:** The Chapter 1 room (4 walls + door + roof) is pre-built when Chapter 2 starts. User does not need to redraw it.  
**Lessons:** 2

---

### Lesson 1 — Place First Window

**Objective:** Hover over a wall to highlight it, then click to place a window.  
**Target wall:** Bottom wall — (0, 0) → (3000, 0)  
**Target position:** Centred at (1500, 0)

**Window specs:**
- Width: 1200 mm
- Height: 1200 mm
- Sill height: 900 mm

**Ghost preview:** Orange outline box shown on the wall face as cursor moves.  
**Scoring:**
- Correct wall: binary (wrong wall = 0%)
- Position accuracy: scored against (1500, 0) target

---

### Lesson 2 — Place Window at Offset

**Objective:** Place a window on a different wall, near the corner.  
**Target wall:** Right wall — (3000, 0) → (3000, 3000)  
**Target position:** 600 mm from the corner

**Scoring:** Same formula as Lesson 1.  
**Tip on score:** Tells the user exactly how many mm they were from the 600 mm offset target.

---

## Scoring reference

| Score | Colour | Label |
|-------|--------|-------|
| 95–100% | Green | Outstanding precision |
| 80–94% | Green | Good work — passed |
| 60–79% | Orange | Close, below 80% threshold |
| 0–59% | Red | Needs improvement |

Pass threshold for all lessons: **80%**
