# PROJECT_STATUS.md — Pillar 1: Memory

> **AI INSTRUCTION**: Read this file first at the start of every session. Do not proceed until you have read and confirmed the current state below.

---

## NORTH STAR
**"Create a complete, stage-verified inventory of every item in the home and yard that enables accurate and substantiated insurance claims following any disaster."**

---

## Current State

| Metric | Value |
|--------|-------|
| Overall Completion | 0% |
| Rooms Pending | 15 |
| Rooms at Stage_A | 0 |
| Rooms at Stage_B | 0 |
| Rooms at Stage_C | 0 |
| Rooms Complete | 0 |
| Total Items Logged | 0 |
| Total Estimated Value | $0 |

---

## Last Session Summary
**Date**: 2026-03-29
**What happened**: Project initialized. GitHub repo created at github.com/khudsonjd/home-inventory. System prompt written. All 4 Pillar documents created. Kerry's AI Method applied to project structure.
**What was decided**: See DECISIONS_LOG.md entries D-001 through D-007.
**Next required action**: Conduct first Stage_A walk session. Start with Living Room.

---

## Room Progress

| Room/Area | Sections | Stage | Last Updated | Notes |
|-----------|----------|-------|--------------|-------|
| Living Room | Main area, Closet | Pending | — | Start here |
| Kitchen | Counters, Cabinets, Pantry | Pending | — | |
| Master Bedroom | Main area, Closet, En-suite Bath | Pending | — | |
| Bedroom 2 | Main area, Closet | Pending | — | |
| Bedroom 3 | Main area, Closet | Pending | — | |
| Master Bathroom | Main area, Cabinets | Pending | — | |
| Hall Bathroom | Main area, Cabinets | Pending | — | |
| Home Office | Desk area, Shelving, Closet | Pending | — | |
| Dining Room | Main area, Buffet/Storage | Pending | — | |
| Laundry Room | Main area, Cabinets | Pending | — | |
| Basement / Bonus Room | Main area, Storage | Pending | — | |
| Garage | Tools, Vehicles, Storage shelves | Pending | — | |
| Front Yard | Landscaping, Outdoor furniture | Pending | — | |
| Back Yard | Patio, Grill, Tools, Play/Storage | Pending | — | |
| Attic / Storage | Boxes, Seasonal items | Pending | — | |

---

## Current CSV Schema
```
Room,Section,Item_Name,Description,Quantity,Estimated_Value,Video_Reference,Notes
```
**Schema version**: 1.0 — If columns are added, increment version and log the decision in DECISIONS_LOG.md.

---

## Known Patterns
*(Add patterns that work well here so future sessions can reuse them.)*

- Asking "what would it cost to replace that today?" gets better value estimates than asking for purchase price.
- Working section-by-section within a room prevents items from being missed.
- Confirming back what you heard before writing inventory rows catches voice-to-text errors.

---

## Open Questions / Blockers
- [ ] Confirm actual room names and update the progress table above
- [ ] Decide video storage location: GitHub LFS vs. Google Drive link in Video_Reference column (see D-006)
- [ ] Set up GitHub mobile app on Android for in-walk commits (Option B workflow)

---

## How to Update This File
At the end of every Claude Projects session, the assistant will output an updated version of:
1. The "Current State" metrics table
2. The "Room Progress" table
3. The "Last Session Summary" block
4. Any new "Known Patterns"

Paste those outputs into this file, commit, and push to GitHub before your next session.
