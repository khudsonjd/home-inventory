# Home Inventory — Insurance Documentation

A complete room-by-room inventory of the home and yard for insurance claim purposes.

## Files
| File | Purpose |
|------|---------|
| `inventory.csv` | Master inventory — all items, all rooms |
| `room_progress.md` | Stage tracker — upload to Claude Project each session |
| `SYSTEM_PROMPT.md` | Instructions to paste into the Claude Project |

## Workflow

### On a morning walk (phone)
1. Open Claude Projects on your phone
2. Upload the current `room_progress.md` to the conversation
3. Walk and talk — the assistant guides you room by room
4. At end of session, copy the assistant's CSV output and updated progress table

### Back at your desk (VS Code)
1. Paste new CSV rows into `inventory.csv`
2. Paste updated progress table into `room_progress.md`
3. Commit and push to this repo
4. Upload updated `room_progress.md` to the Claude Project for next session

## Inventory Stages Per Room
| Stage | Meaning |
|-------|---------|
| Pending | Not started |
| Stage_A | Inventoried from memory (verbal walk) |
| Stage_B | Photos uploaded and AI-analyzed |
| Stage_C | Video recorded and cross-referenced |
| Complete | All stages done |

## Schema
```
Room,Section,Item_Name,Description,Quantity,Estimated_Value,Video_Reference,Notes
```

## TODO
- [ ] Set up GitHub mobile app on Android for in-walk commits (Option B workflow)
- [ ] Research Git LFS for storing room walkthrough videos in this repo
- [ ] Consider Google Drive/iCloud as video storage with links in Video_Reference column
