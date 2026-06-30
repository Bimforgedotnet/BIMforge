# BIMforge Roadmap

Features listed here are not yet built. Nothing on this list exists in the current codebase.

---

## Near-term

### Chapter 3 — Stairs & Levels
- Multi-storey model with level switching
- Stair placement between levels
- Introduce the concept of building phases

### Chapter 4 — Structural Grid
- Column and beam placement
- Structural grid overlay
- Grid naming (A/B/C, 1/2/3)

### Persistent progress
- Save `chapterState` to `localStorage` so progress survives page refresh
- Resume from where the user left off on next visit

### Retry & replay
- Allow re-attempting any completed lesson to improve score
- Show best score vs current attempt

---

## Medium-term

### Score leaderboard
- Optional username entry
- Submit scores to a lightweight backend
- Public board per chapter

### User accounts
- Email + password registration
- Score history across sessions and devices

### More element types
- Columns (structural)
- Floors / slabs
- Annotations and dimensions

### Assessment mode
- Timed lessons
- No ghost preview or snap guides
- Harder scoring thresholds

---

## Long-term / SaaS

### Company accounts
- Invite team members
- Track cohort progress as a manager

### Custom lesson builder
- Admin UI to define target geometry, scoring weights, and objectives
- Export/import lesson packs as JSON

### Revit export
- Generate a real `.rvt` or IFC file from what the user placed
- Download and open in desktop Revit

### Mobile support
- Touch-based orbit and placement
- Responsive layout for tablets
