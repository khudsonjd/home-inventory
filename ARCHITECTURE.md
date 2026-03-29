# ARCHITECTURE.md — Pillar 2: Structure

> A new person (or AI session) should be able to understand the full system within 5 minutes of reading this file.

---

## System Map

```
┌─────────────────────────────────────────────────────────────┐
│                    SOURCE OF TRUTH                          │
│           GitHub: khudsonjd/home-inventory                  │
│                                                             │
│  inventory.csv         — all items, all rooms               │
│  PROJECT_STATUS.md     — current state + next action        │
│  ARCHITECTURE.md       — this file                          │
│  DECISIONS_LOG.md      — why things are the way they are    │
│  SYSTEM_PROMPT.md      — Claude Projects persona            │
│  README.md             — quick-start for humans             │
└──────────────────┬──────────────────┬───────────────────────┘
                   │                  │
        ┌──────────▼──────┐  ┌────────▼──────────┐
        │  VS Code / PC   │  │  Claude Projects  │
        │  (Claude Code)  │  │  (Android phone)  │
        │                 │  │                   │
        │ - Edit CSV      │  │ - Walk sessions   │
        │ - Git commit    │  │ - Voice input     │
        │ - Git push      │  │ - Photo upload    │
        │ - Review/fix    │  │ - Video guidance  │
        └──────────┬──────┘  └────────┬──────────┘
                   │                  │
                   │         Manual transfer (Option C):
                   │         Copy session output from phone
                   │         → Paste into files in VS Code
                   │         → Commit and push
                   └──────────────────┘
                          (both paths lead back to GitHub)
```

---

## File Registry

| File | Role | Updated By | When |
|------|------|------------|------|
| `inventory.csv` | Master item list | Human (paste from session) | After each walk session |
| `PROJECT_STATUS.md` | Session state + progress | Human (paste from session) | After each walk session |
| `ARCHITECTURE.md` | System map | Human (with AI help) | When system design changes |
| `DECISIONS_LOG.md` | Decision history | Human (with AI help) | When a key decision is made |
| `SYSTEM_PROMPT.md` | Claude Projects instructions | Human | When persona needs updating |
| `README.md` | Human quick-start | Human | When workflow changes |
| `videos/` *(future)* | Room walkthrough videos | Human | After each video session |

---

## Data Flow: A Single Walk Session

```
1. START SESSION
   User uploads PROJECT_STATUS.md to Claude Projects
   AI reads file → knows current state, resumes where left off

2. INVENTORY CONVERSATION
   User speaks → voice-to-text → Claude Projects
   AI confirms what it heard
   AI asks follow-up questions (value, quantity, description)
   AI holds items in context during session

3. END OF SESSION OUTPUT (AI produces 3 blocks)
   Block A: Updated PROJECT_STATUS.md sections (metrics + progress table)
   Block B: New CSV rows ready to paste into inventory.csv
   Block C: Next session suggestion

4. SYNC TO GITHUB (back at desk)
   User pastes Block A into PROJECT_STATUS.md
   User pastes Block B into inventory.csv
   git add -A
   git commit -m "Stage A: [Room name]"
   git push

5. PREPARE FOR NEXT SESSION
   Upload updated PROJECT_STATUS.md to Claude Projects
```

---

## Inventory Stages

| Stage | Description | Input Method | AI Role |
|-------|-------------|--------------|---------|
| Pending | Not started | — | — |
| Stage_A | From memory | Voice conversation | Guide, confirm, format as CSV |
| Stage_B | Photo review | Image upload | Identify items, fill gaps, estimate values |
| Stage_C | Video walkthrough | Video + narration | Parse speech, cross-reference video as proof |
| Complete | All stages done | — | — |

---

## CSV Schema (v1.0)

```
Room,Section,Item_Name,Description,Quantity,Estimated_Value,Video_Reference,Notes
```

| Column | Type | Example | Notes |
|--------|------|---------|-------|
| Room | String | `Kitchen` | Matches room name in progress table |
| Section | String | `Pantry` | Sub-area within the room |
| Item_Name | String | `Stand mixer` | Short label |
| Description | String | `KitchenAid, red, 5qt` | Brand, model, color, serial if known |
| Quantity | Integer | `1` | Count of identical items |
| Estimated_Value | Number | `350` | USD replacement cost, no $ sign |
| Video_Reference | String | `kitchen_2026-03-29.mp4` | Filename or timestamp |
| Notes | String | `Receipt in filing cabinet` | Anything else |

**To add a column**: Log the decision in DECISIONS_LOG.md, increment schema version here, update SYSTEM_PROMPT.md.

---

## Naming Conventions

| Thing | Convention | Example |
|-------|-----------|---------|
| Video files | `[room]_[YYYY-MM-DD].mp4` | `garage_2026-04-05.mp4` |
| Git commit messages | `Stage [A/B/C]: [Room name]` | `Stage A: Kitchen` |
| Git branches (future) | `session/[YYYY-MM-DD]-[room]` | `session/2026-04-05-garage` |
| Room names in CSV | Title case, match progress table | `Master Bedroom` |

---

## Glossary

| Term | Definition |
|------|-----------|
| Stage_A | First-pass inventory from memory, conducted verbally during a walk |
| Stage_B | Photo-assisted review to fill gaps and verify Stage_A entries |
| Stage_C | Video walkthrough that serves as visual proof of item existence |
| Complete | A room that has passed all three stages |
| Session | One Claude Projects conversation covering one or more rooms |
| Sync | The act of copying session output into files and committing to GitHub |
| Source of Truth | The GitHub repo — always the authoritative version of the inventory |
| Option B | Future workflow: commit directly from Android using GitHub mobile app |

---

## Future: Option B Workflow (GitHub Mobile)
When set up, the sync step will happen during the walk:
1. AI outputs CSV rows mid-session
2. User commits directly from GitHub mobile app
3. No desk step required
See DECISIONS_LOG.md entry D-005.
