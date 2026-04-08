---
tags: [vault-health, action-item, reference]
created: 2026-04-03
type: project
status: active
---

# Vault Health Remediation Plan — 2026-04-03

> Source: [[20260403_VaultHealthReport]]
> All issues resolved → update `status: complete` and file to `04-Projects/0401-VaultSetUp/`

---

## Overview

18 issues split into two tracks:

| Track | Description | Files Affected | Decision Required |
|---|---|---|---|
| **A — Quick Fixes** | Claude can execute immediately, no judgment calls | 12 files | No |
| **B — Stacey Decides** | Need your input before acting | 6 items | Yes |

---

## Track A — Quick Fixes (No Decisions Needed)

Claude can execute all of these. Say **"run Track A"** and I'll work through them in order.

---

### A1 · Fix Backslash Wikilinks in Active Work Ledger
*1 file · 7 links*

`Active Work Ledger.md` uses `[[Note\|Alias]]` (backslash before pipe) on 7 links. Standard syntax is `[[Note|Alias]]`. Will fix all 7 in one pass.

- [ ] `[[Brown_Phyllis\|...]]` → `[[Brown_Phyllis|Phyllis Brown]]`
- [ ] `[[Heinzelmann_Karl\|...]]` → `[[Heinzelmann_Karl|Karl Heinzelmann]]`
- [ ] `[[Watson_Kelley\|...]]` → `[[Watson_Kelley|Kelley Watson]]`
- [ ] `[[Coleman_Scott\|...]]` → `[[Coleman_Scott|Scott Coleman]]`
- [ ] `[[20260403_VaultBuildCompletionPlan\|...]]` → standard syntax
- [ ] `[[20260323_BoldTrailEnrichment_ProjectSummary\|...]]` → standard syntax
- [ ] `[[20260323_VaultSyncSkill_DesignBrief\|...]]` → standard syntax

---

### A2 · Fix Broken Folder-Path Links in Old Health Report
*1 file · 9 links*

`04-Projects/0401-VaultSetUp/20260323_VaultHealthReport.md` has links pointing to folder paths that don't match actual note names, plus two backslash links.

- [ ] `[[02-Real-Estate/Listings/Active]]` → `[[Active Listings]]`
- [ ] `[[02-Real-Estate/Transactions/Active]]` → `[[Active Transactions]]`
- [ ] `[[02-Real-Estate/Rentals/Properties]]` → `[[Rental Properties]]`
- [ ] `[[02-Real-Estate/Vendors-and-Contacts]]` → `[[Vendors and Contacts]]`
- [ ] `[[03-Business/Goals-and-KPIs]]` → `[[Goals and KPIs]]`
- [ ] `[[05-Resources/Scripts-and-Templates]]` → `[[Scripts and Templates]]`
- [ ] `[[05-Resources/Legal-Forms]]` → `[[Legal Forms]]`
- [ ] `[[20260322_VaultSetup\]]` (×2) → `[[20260322_VaultSetup]]`

---

### A3 · Add Frontmatter to Missing-FM Files
*5 files*

Add minimal compliant frontmatter to the 5 files with none:

- [ ] `90-Archive/Welcome.md` → type: `reference`, status: `archived`
- [ ] `04-Projects/0402-BoldTrailClientStatus/reports/impact-report-2026-03-27.md` → type: `research`, status: `complete`
- [ ] `04-Projects/0402-BoldTrailClientStatus/reports/impact-report-2026-03-27-backup.md` → type: `research`, status: `archived`
- [ ] `04-Projects/0402-BoldTrailClientStatus/boldtrail-client-status-manager/references/status_definitions.md` → type: `reference`, status: `active`
- [ ] `04-Projects/0402-BoldTrailClientStatus/boldtrail-client-status-manager/references/campaign_registry.md` → type: `reference`, status: `active`

> Note: The impact-report backup is identical to the main file. Tagging it `archived` in frontmatter flags it visually. See Track B4 to decide whether to archive the file itself.

---

### A4 · Fix Incomplete Frontmatter on SKILL.md
*1 file*

`04-Projects/0402-BoldTrailClientStatus/boldtrail-client-status-manager/SKILL.md` is missing all 4 required fields. Will add: `tags: [reference]`, `created: 2026-03-24`, `type: reference`, `status: active`.

- [ ] Add frontmatter to SKILL.md

---

### A5 · Link Client Briefs from Buyer Cards
*5 files*

The 5 client briefs in `05-Resources/Client-Briefs/` are orphaned because the buyer cards don't link to them. Will add a `Related` or `Resources` section to each buyer card with a wikilink:

- [ ] `Brown_Phyllis.md` → link to `[[20260324_Brief_Brown_Phyllis]]`
- [ ] `Heinzelmann_Karl.md` → link to `[[20260324_Brief_Heinzelmann_Karl]]`
- [ ] `Boland_Mark.md` → link to `[[20260326_Brief_Boland_Mark]]`
- [ ] `StLouis_Sacha.md` → link to `[[20260326_Brief_StLouis_Sacha]]`
- [ ] `Tapanainen_Jorma.md` → link to `[[20260326_Brief_Tapanainen_Jorma]]`

---

### A6 · Link BoldTrail Project Artifacts from Project Note
*1 file*

`04-Projects/0402-BoldTrailClientStatus/20260327_StatusMigrationImpactReport.md` is orphaned. Will add a link to it from `20260323_BoldTrailEnrichment_ProjectSummary.md` or the project's main note.

- [ ] Add `[[20260327_StatusMigrationImpactReport]]` to BoldTrail project note

---

## Track B — Stacey Decides

These require a judgment call before Claude acts. Review and reply with your decision for each.

---

### B1 · DeNapoli_Patricia and Villazan_Faust — What's their status?

Both buyer cards are unlinked from anything. Neither appears in the Active Work Ledger.

**Patricia DeNapoli** — enriched, `status: lead`, source: privatehomesearch.com, has phone/email. Looks like a real but cold lead.

**Faust Villazan** — minimal data, no phone/email, no BoldTrail ID, `status: active`. May be a placeholder or incomplete import.

**Options:**
- [ ] Add both to Active Work Ledger under a "Parked / Monitor" section
- [ ] Change Villazan to `status: draft` or `status: archived` pending more info
- [ ] Leave as-is (they'll remain orphaned)

---

### B2 · `03-Business/Lead-Pipeline.md` — Archive or keep?

This is a stub redirect note that says *"see [[Lead Pipeline]] in `03-Business/Lead-Pipeline/`"*. The real dashboard is `03-Business/Lead-Pipeline/Lead Pipeline.md`. The stub is not linked from anywhere.

**Options:**
- [ ] Archive it (move to `90-Archive/`) — it adds no value if nothing links to it
- [ ] Link it from `Home.md` or `Active Work Ledger.md` as a shortcut
- [ ] Leave as-is

---

### B3 · `20260403_IonashoresCommunityOverview.md` — Link or leave?

Market research note sitting unlinked. Is it tied to an active buyer or listing?

**Options:**
- [ ] Link it from the relevant buyer card(s) (e.g., Heinzelmann if he's looking in that area)
- [ ] Leave it — reference material doesn't always need incoming links
- [ ] Archive it if research is no longer relevant

---

### B4 · Impact Report Backup — Archive or delete?

`04-Projects/0402-BoldTrailClientStatus/reports/impact-report-2026-03-27-backup.md` is byte-for-byte identical to the main report. It's a redundant file.

**Options:**
- [ ] Archive it (move to `90-Archive/Completed-Projects/`)
- [ ] Leave it in place (Track A3 will tag it `archived` in frontmatter to flag it visually)

---

### B5 · Skill/Tool Reference Files — Exempt from frontmatter schema?

Three files deep in the BoldTrail status manager are skill assets, not vault knowledge notes:
- `boldtrail-client-status-manager/SKILL.md`
- `boldtrail-client-status-manager/references/status_definitions.md`
- `boldtrail-client-status-manager/references/campaign_registry.md`

**Options:**
- [ ] Apply vault-standard frontmatter (Track A3 and A4 handle this)
- [ ] Formally exempt skill/tool asset files from frontmatter requirements — document in [[Decision Log]]

---

### B6 · Placeholder Bracket Text — Remove brackets or leave?

Six notes contain `[[wikilinks]]`, `[[wikilink]]`, or `[[create a link]]` as concept references (not actual links). These show up as broken links in any graph view.

Affected files: both resource guide notes, `20260323_VaultHealthReport.md`, and `90-Archive/Welcome.md`.

**Options:**
- [ ] Remove brackets (turn into plain text or backtick code)
- [ ] Leave as-is (cosmetic issue only)

---

## Execution Order (if running Track A in full)

1. A1 — Active Work Ledger backslash fixes (quick, high visibility)
2. A2 — Old health report link fixes (quick, 1 file)
3. A3 + A4 — Frontmatter additions (5 files + 1 file)
4. A5 — Brief links in buyer cards (5 files)
5. A6 — BoldTrail project artifact link (1 file)

**Total files touched: 14 · Estimated time: ~10 minutes**
