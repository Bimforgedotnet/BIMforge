# Changelog

All notable bug fixes and behavioural changes to `index.html` are logged here, newest first.
Use this to trace "did fix X cause regression Y" — each entry names the affected functions/state
so you can grep `index.html` for them.

Format loosely follows [Keep a Changelog](https://keepachangelog.com/).

## Unreleased

### Fixed — 2026-06-30

- **`loadProgress()` no longer trusts mismatched localStorage saves.** Chapter 2 grew from
  2 lessons to 5; old saves had `chapterState[2].completed`/`scores` arrays of length 2.
  `loadProgress()` now checks each chapter's saved array length against
  `CHAPTERS[n].totalLessons` and discards (and clears) the save if it doesn't match, instead
  of silently desyncing `renderTabs()`'s `every(Boolean)` completion check, lesson locking,
  and the progress bar.
  _If chapter-complete state or lesson unlocking ever looks wrong again, check whether a
  `CHAPTERS[n].totalLessons` change shipped without a matching save-shape bump here._

- **Added `lessonLocked` state to stop single-shot lessons from accumulating extra elements.**
  Previously, clicking past a completed Ch1 L1/L2 wall, a completed Ch1 L3 pair of walls, or
  a completed Ch2 L1–4 window kept adding more meshes to `placedElements` with no way to
  remove them — clutter in the viewport and inflated counts in the "Placed Elements" panel
  and Chapter Complete summary. `lessonLocked` is now set in `handleWallPlacement()` /
  `handleWindowPlacement()` once a lesson's goal is met, checked at the top of both
  functions, and reset to `false` in `switchLesson()` and `clearCurrentPlacement()`.
  _If a lesson seems "stuck" and won't accept new placements, check `lessonLocked` is being
  reset wherever that lesson's state is cleared._

- **`clearCurrentPlacement()` did nothing for Chapter 1 Lessons 1 & 2.** It had cleanup
  branches for L3/L4/L5 (Ch1) and Ch2's lessons but no branch for L1/L2 — clicking "Clear
  Current Placement" after placing the first wall was a silent no-op. Added an `l1l2Walls`
  tracking array and a matching cleanup branch.
  _If Clear stops working for a specific lesson again, check `clearCurrentPlacement()` has a
  branch for that `currentChapter`/`currentLesson` combination — it's an explicit if-list, not
  a generic handler._

- **`nearEndpoint()` snap-indicator threshold (0.4) didn't match `snapToEndpoint()`'s actual
  snap radius (`SNAP_THRESHOLD` = 0.25).** The cursor showed a "will snap" indicator out to
  400mm from an endpoint, but clicks only actually snapped within 250mm — misleading visual
  feedback. `nearEndpoint()` now uses `SNAP_THRESHOLD` directly.

- **Removed dead code:** unused `findNearestWall()` (superseded by wall-face raycasting,
  never called) and a `document.getElementById('btn-start')?.remove()` referencing an
  element that doesn't exist in the DOM.

- **Docs:** `CLAUDE.md` and `README.md` updated — Chapter 2 was still documented as 2
  lessons; it's 5. Added `ch2L5Phase` and `lessonLocked` to the state-model docs.

## Earlier history

Pre-dates this changelog — see `git log` for the full commit history. Notable milestones:

- Chapter 2 (Windows & Openings) expanded from 2 lessons to a full 5-lesson arc with an
  from-scratch assessment lesson.
- Wall-face raycasting replaced ground-plane raycasting for door/window placement (Revit-style
  wall-hosted families).
- Roof sketch clicks raycast against wall surfaces first, falling back to ground, and snap to
  wall-top corners.
- Ghost preview for doors/windows changed from a filled plane to an outline-only preview.
