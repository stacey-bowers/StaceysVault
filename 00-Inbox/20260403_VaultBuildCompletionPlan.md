---
tags: [reference, vault-setup, project, active]
created: 2026-04-03
type: project
status: active
---

# Vault Build — Completion Plan

*Generated: 2026-04-03 | Source: Second Brain Setup Checklist (Jimmy Bowers, v1.0)*
*Tracks remaining work to bring StaceysVault to a fully operational, backed-up, production state.*

---

## Status Legend
✅ Complete | ⚠️ Partial | ❌ Not Started | 🔄 In Progress

---

## Step 1 — Global CLAUDE.md ❌ → 🔄
**What:** Create `~/.claude/CLAUDE.md` — the global instruction file that governs Claude's behavior across ALL Cowork sessions on this Mac, not just this vault.
**Why:** Without it, Claude operates on defaults every session. This file sets tone, output standards, safety rules, and Obsidian conventions that apply everywhere.
**How:** File has been drafted and saved to `00-Inbox/` as `global_CLAUDE.md`. One Terminal command copies it into place.
**Terminal command:**
```bash
mkdir -p ~/.claude && cp ~/Library/Mobile\ Documents/com~apple~CloudDocs/StaceysVault/00-Inbox/global_CLAUDE.md ~/.claude/CLAUDE.md
```
**Verify:** `cat ~/.claude/CLAUDE.md` — should print the file contents.

---

## Step 2 — GitHub + Obsidian Git Setup ❌
**What:** Initialize the vault as a Git repository, connect it to a private GitHub repo, and install the Obsidian Git plugin for auto-backup.
**Why:** iCloud syncs files but gives you zero version history. GitHub gives you a full undo button — every note change is recoverable. If a skill goes haywire or you accidentally delete something, you can roll back.
**Steps (you do these — Claude will guide):**
- [ ] Create GitHub account at github.com (if you don't have one)
- [ ] Install GitHub Desktop from desktop.github.com (Apple Silicon version)
- [ ] Create new **private** repo named `StaceysVault` — do NOT initialize with README
- [ ] Copy the HTTPS URL (e.g. `https://github.com/yourusername/StaceysVault.git`)
- [ ] Run in Terminal: `git -C ~/Library/Mobile\ Documents/com~apple~CloudDocs/StaceysVault init`
- [ ] Run: `git -C ~/Library/Mobile\ Documents/com~apple~CloudDocs/StaceysVault remote add origin <your repo URL>`
- [ ] Claude will handle initial commit + push
- [ ] In Obsidian: Settings → Community plugins → enable community plugins → Browse → search "Git" → install **Vinzent** plugin
- [ ] Claude will configure plugin settings

**Obsidian Git settings (Claude configures):**
- Auto commit-and-sync interval: `120` minutes
- Auto commit after stopping edits: ON
- Push on sync: ON
- Pull on sync: ON
- Merge strategy: Merge

---

## Step 3 — Fix Project Folder Standards ⚠️
**What:** Bring `04-Projects/` subfolders into alignment with the vault standard — each project needs a `ProjectHub` note and standard subfolders (`Chats/`, `Summaries/`, `Assets/`, `Outputs/`).
**Why:** Skills navigate projects by expected structure. Without standard subfolders, the Session Initializer and Research Aggregator can't reliably find project context.
**Affects:**
- `0401-VaultSetUp/` — needs ProjectHub note; has stray `.obsidian/` folder to archive
- `0402-BoldTrailClientStatus/` — needs ProjectHub note and standard subfolders
**Claude does this** after confirmation.

---

## Step 4 — Restructure Active Work Ledger ⚠️
**What:** Upgrade the AWL from simple tables to the full structured format with priority sections.
**Why:** The current AWL works but lacks the urgency-flagging sections that make it a true session-start brief.
**New structure:**
- 🔴 Urgent — needs attention today
- 🟢 In Progress — actively working
- 🟡 Parked — waiting on something external
- ⏭️ Up Next — queued, not started
- 📁 Active Projects table
- ✅ Completed This Session

**Claude does this** after confirmation.

---

## Step 5 — Create Skill Index ❌
**What:** Build a `SkillIndex.md` cataloging every installed skill — name, version, purpose, install date.
**Why:** As the skill library grows, there's no central record of what's installed, what version it's at, or when it was last updated. This becomes the maintenance log.
**Claude creates this** and drops it in `00-Inbox/`.

---

## Step 6 — Fix Home.md Broken Wikilinks ⚠️
**What:** Several links in `Home.md` point to notes that don't exist (`Active Listings`, `Clients`, `Active Transactions`, `Health Dashboard`, `Family Dashboard`, etc.).
**Why:** Obsidian marks these as unresolved — they clutter the graph and break navigation.
**Options:** Create stub index notes for each, or update links to point to existing folders/dashboards.
**Claude does this** after confirming preferred approach.

---

## Step 7 — Create Today's Daily Note 🔄
**What:** Run the Daily Note Manager skill to create today's note (`20260403.md`) and catch up the ledger.
**Why:** Last daily note was March 27 — a week gap. The note manager can carry forward open tasks.
**Claude does this** on request.

---

## Step 8 — Install evaluator-skill ❌
**What:** Install the skill evaluation and benchmarking tool.
**Why:** Used to test and measure skill performance. Not urgent until active skill development resumes.
**Defer until:** Next skill-building session.

---

## Step 9 — Phase 11 Formal Verification ❌
**What:** Run end-to-end verification checklist after all other steps complete.
**Checklist:**
- [ ] Run Vault Health Checker — 0 broken links, 0 orphans, 0 missing frontmatter
- [ ] Run Session Initializer — produces clean session brief
- [ ] Confirm Obsidian Git auto-sync — edit a note, wait, check GitHub for commit
- [ ] Run manual backup — `Cmd+P` → "Obsidian Git: Create backup"

---

## Priority Order

| Step | What | Who | Urgency |
|---|---|---|---|
| 1 | Global CLAUDE.md | You + Claude | 🔴 Do now |
| 2 | GitHub + Git plugin | You + Claude | 🔴 Do now |
| 7 | Today's daily note | Claude | 🟢 Ongoing |
| 3 | Fix project folder structure | Claude | 🟡 This week |
| 4 | Restructure AWL | Claude | 🟡 This week |
| 5 | Skill Index | Claude | 🟡 This week |
| 6 | Fix Home.md links | Claude | 🟡 This week |
| 9 | Phase 11 verification | Claude | 🟡 After Step 2 |
| 8 | evaluator-skill | Claude | ⬜ Defer |

---

*Related: [[Active Work Ledger]] | [[Decision Log]] | [[Projects Dashboard]]*
*Source checklist: [[20260402_ObsidianSecondBrainSetupChecklist]]*
