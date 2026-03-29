# DECISIONS_LOG.md — Pillar 4: Reasoning

> Every major decision is logged here with the reasoning and alternatives considered. This prevents relitigating past decisions and helps any AI session (or human) understand why things are the way they are.

---

## D-001 | CSV as primary inventory format
**Date**: 2026-03-29
**Decision**: Store the inventory as a CSV file (`inventory.csv`).
**Why**: CSV is universally readable, importable into Google Sheets/Docs, works in VS Code, and is plain text (version-controlled well in git). The user wants a Google Doc for final presentation.
**Alternatives considered**:
- JSON: More structured but harder to read/edit manually.
- Google Sheets as primary: No offline access, not git-friendly.
- SQLite: Overkill for this use case, harder to edit without tooling.

---

## D-002 | GitHub as source of truth
**Date**: 2026-03-29
**Decision**: The GitHub repo `khudsonjd/home-inventory` is the authoritative version of all inventory data. All changes from any device must eventually be pushed here.
**Why**: The user works from both a Windows PC (VS Code) and an Android phone (Claude Projects). A single remote source prevents conflicting versions. GitHub is already familiar to the user.
**Alternatives considered**:
- Google Drive: No version history, no branching.
- Dropbox/OneDrive: No meaningful diff/merge support.
- Local-only: Loses the phone workflow entirely.

---

## D-003 | Three-stage inventory process (A/B/C)
**Date**: 2026-03-29
**Decision**: Each room progresses through three stages: Stage_A (memory/verbal), Stage_B (photos), Stage_C (video).
**Why**: No single method captures everything. Memory is fast but incomplete. Photos catch missed items. Video provides proof of existence for insurance purposes. Stages allow partial progress and clear "done" criteria.
**Alternatives considered**:
- Single-pass inventory: Too much pressure per session; misses items.
- Photo-first: Requires being stationary; can't do on a walk.
- Video-only: Hard to process systematically; no structured data output.

---

## D-004 | Option C sync workflow (paste at desk)
**Date**: 2026-03-29
**Decision**: For now, syncing from phone sessions to GitHub is done manually: copy session output from Claude Projects → paste into files in VS Code → commit and push.
**Why**: Lowest friction to get started today. No additional app setup required. User is heading out on a walk in ~20 minutes.
**Alternatives considered**:
- Option B (GitHub mobile app): Better long-term — allows in-walk commits. Deferred because it requires setup time. See D-005.
- Option A (paste into GitHub.com browser): Works but slower than VS Code.

---

## D-005 | Option B deferred — GitHub mobile app
**Date**: 2026-03-29
**Decision**: Set up GitHub mobile app on Android in a future session to enable committing directly from the phone during or after a walk.
**Why**: Would eliminate the desk step entirely. The user expressed clear interest ("each session results in an update to the repo").
**Status**: TODO — schedule a setup session in Claude Code.

---

## D-006 | Video storage approach — undecided
**Date**: 2026-03-29
**Decision**: Deferred. Two viable options:
- **GitHub LFS**: Keeps everything in one repo. Free tier = 1GB storage. Room videos can be large (hundreds of MB each). Could hit limits.
- **Google Drive / iCloud**: Unlimited storage. Store a shareable link in the `Video_Reference` CSV column. Slightly more manual.
**Status**: Open — decide before first Stage_C session.

---

## D-007 | Kerry's AI Method applied to project structure
**Date**: 2026-03-29
**Decision**: Adopted Kerry's AI Method (6 phases, 4 Pillars) as the structural framework for this project.
**Why**: The method solves the exact problem this project has — a long-running multi-session project where the AI needs to resume context without re-explaining. The four Pillar documents (PROJECT_STATUS.md, ARCHITECTURE.md, DECISIONS_LOG.md, SYSTEM_PROMPT.md) map cleanly onto the project's needs.
**What changed**: Added PROJECT_STATUS.md, ARCHITECTURE.md, DECISIONS_LOG.md. Updated SYSTEM_PROMPT.md to require reading PROJECT_STATUS.md at session start. Added "Last Session Summary" and "Known Patterns" to PROJECT_STATUS.md.

---

## D-008 | PROJECT_STATUS.md as the primary upload for each session
**Date**: 2026-03-29
**Decision**: The user uploads only `PROJECT_STATUS.md` to Claude Projects at the start of each session (not all files). PROJECT_STATUS.md contains everything the AI needs: current state, room stages, schema, known patterns, and next action.
**Why**: Claude Projects has a file size/count limit. One focused file is faster to upload and easier to maintain. ARCHITECTURE.md and DECISIONS_LOG.md are reference documents the AI reads when needed, not every session.
**Alternatives considered**:
- Upload all 4 Pillar docs every session: More complete but slower and noisier.
- Paste content into chat: Works but loses the file attachment benefits.
