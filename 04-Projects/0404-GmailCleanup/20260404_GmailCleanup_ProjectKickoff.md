---
type: project
status: active
tags:
  - project
  - in-progress
start_date: "2026-04-04"
due_date: "2026-05-04"
priority: medium
created: 2026-04-04
---

# Gmail Cleanup

## Overview
- **Goal:** Achieve inbox zero on a ~50,000-email Gmail account through a structured, phased cleanup — unsubscribe, delete, archive, organize with labels, then reach zero and maintain it.
- **Why it matters:** Important emails (leads, client replies, critical info) are getting buried. The inbox is a source of mental clutter and a gap in business operations. A clean, organized Gmail is a core part of building tighter systems at Domain Realty Group.
- **Due:** ~May 4, 2026 (medium priority — within one month)
- **Execution model:** Claude does the heavy lifting (surfaces senders, drafts actions, identifies bulk targets). Stacey reviews and approves before anything is touched.

---

## Approach

Local-first, safety-first pipeline based on [[Gmail_Cleanup_Cowork_Prompt_Sequence]]. Phases 1–3 work entirely on a local copy of Gmail (no live inbox risk). Phases 4–5 execute browser-based actions in live Gmail only after classification is reviewed and approved.

| Phase | What happens | Mode | Reversible? |
|---|---|---|---|
| 1 — Parse | Google Takeout .mbox → SQLite database | Local file | Yes |
| 2 — Classify | Tag every email: Archive / Delete / Review (4-tier logic) | Local file | Yes |
| 3 — Export | Save .eml archive + attachments by category | Local file | Yes |
| 4 — Cleanup | Move DELETE emails to Gmail trash, empty trash | Browser (Chrome) | **NO** |
| 5 — Filters | Create auto-delete filters for top noise senders | Browser (Chrome) | Reversible |

---

## Phases

### Phase 1 — Parse
- [ ] Create `GmailCleanup/` working folder on local machine
- [ ] Request Google Takeout export of Gmail as .mbox (can take 30 min – several hours)
- [ ] Place .mbox file in `GmailCleanup/` folder when ready
- [ ] Run Python script to parse .mbox → `gmail_index.db` (SQLite)
- [ ] Verify: total email count, date range, top 20 senders look correct

### Phase 2 — Classify
- [ ] Define Tier 1 auto-archive rules (trusted senders/domains)
- [ ] Run classification engine — tags every email Archive / Delete / Review
- [ ] Export REVIEW list to CSV, Stacey reviews and adds manual decisions
- [ ] Apply manual decisions back to database
- [ ] Verify: no NULLs, REVIEW count manageable, spot-check classifications

### Phase 3 — Export Archive
- [ ] Export all ARCHIVE emails as .eml files organized by category into `GmailCleanup/Archive/`
- [ ] Extract attachments into `GmailCleanup/Attachments/`
- [ ] Back up Archive + Attachments to external location
- [ ] ⚠ Do not proceed to Phase 4 until backup is confirmed

### Phase 4 — Gmail Cleanup (Browser)
- [ ] Generate `gmail_delete_queries.txt` from DELETE classifications (senders with 10+ emails)
- [ ] Execute batch deletions via Claude in Chrome — one sender group at a time, Stacey confirms each
- [ ] Review trash before emptying — spot-check 10–15 emails
- [ ] Empty trash (irreversible — confirm explicitly)

### Phase 5 — Filters & Ongoing Prevention
- [ ] Create Gmail filters for top 30 DELETE senders (auto-delete on arrival)
- [ ] Mark all remaining emails as read
- [ ] Verify filters in Gmail Settings
- [ ] Document maintenance workflow in vault (SOP)
- [ ] Set up recurring weekly triage and monthly filter audit prompts

---

## Progress Log
| Date | Update |
| ---- | ------ |
| 2026-04-04 | Project initiated — kickoff note created, phases defined |
| 2026-04-07 | Plan revised — adopted local-first pipeline from Jimmy's Cowork prompt sequence doc; phases 1–3 local, 4–5 browser. Google Takeout export initiated. |

## Resources & Links
- [[Active Work Ledger]]
- [[20260404_GmailCleanup_ProjectKickoff]] (this note)
- [[Gmail_Cleanup_Cowork_Prompt_Sequence]] — full prompt sequence and phase reference (Jimmy, March 2026)

## Notes
- ~50,000 emails in inbox at project start
- Existing label system: ~5 labels, not well utilized — will redesign from scratch
- Keep label structure simple and broadly organized (not granular)
- Working folder: `GmailCleanup/` on local machine (create before Phase 1)
- Google Takeout export must complete before Phase 1 can begin
- Phases 4–5 are browser-based via Claude in Chrome — Stacey approves every batch before execution
- Phase 4 trash empty is irreversible — requires explicit confirmation
