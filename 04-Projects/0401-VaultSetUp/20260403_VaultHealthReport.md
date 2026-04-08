---
tags: [vault-health, reference]
created: 2026-04-03
type: research
status: active
---

# Vault Health Report — 2026-04-03

## Summary

| Check | Scope | Issues Found | Health |
|---|---|---|---|
| Frontmatter completeness | 63 files | 6 issues | 🟡 |
| Broken wikilinks | 63 files scanned | 26 flagged (14 true breaks) | 🔴 |
| Orphan notes | 63 files (inboxes/daily notes excluded) | 18 orphans | 🔴 |
| Stale drafts | All draft-status notes | 0 | 🟢 |

Health key: 🟢 0 issues · 🟡 1–5 issues · 🔴 6+ issues

---

## Frontmatter Issues

### ❌ Missing Frontmatter (5 files)

These files have no YAML frontmatter block at all:

- `90-Archive/Welcome.md`
- `04-Projects/0402-BoldTrailClientStatus/boldtrail-client-status-manager/references/status_definitions.md`
- `04-Projects/0402-BoldTrailClientStatus/boldtrail-client-status-manager/references/campaign_registry.md`
- `04-Projects/0402-BoldTrailClientStatus/reports/impact-report-2026-03-27.md`
- `04-Projects/0402-BoldTrailClientStatus/reports/impact-report-2026-03-27-backup.md`

### ⚠️ Incomplete Frontmatter (1 file)

- `04-Projects/0402-BoldTrailClientStatus/boldtrail-client-status-manager/SKILL.md` — missing: `tags`, `created`, `type`, `status`

> **Note:** The boldtrail-client-status-manager files are skill/tool assets, not vault knowledge notes. These may not need standard vault frontmatter — worth deciding explicitly and documenting in [[Decision Log]].

---

## Broken Wikilinks (26 flagged, 14 true breaks)

### ⚠️ Formatting Issue — Non-Standard Backslash Syntax (7 links)

These links in `Active Work Ledger.md` use `[[Note\|Alias]]` (backslash before pipe) instead of the standard `[[Note|Alias]]` syntax. They resolve to the correct notes in Obsidian on most platforms, but the backslash is non-standard and may cause issues on some systems. Low priority to fix.

- `Active Work Ledger.md` → `[[Brown_Phyllis\|Phyllis Brown]]`
- `Active Work Ledger.md` → `[[Heinzelmann_Karl\|Karl Heinzelmann]]`
- `Active Work Ledger.md` → `[[Watson_Kelley\|Kelley Watson]]`
- `Active Work Ledger.md` → `[[Coleman_Scott\|Scott Coleman]]`
- `Active Work Ledger.md` → `[[20260403_VaultBuildCompletionPlan\|Vault Build — Completion Plan]]`
- `Active Work Ledger.md` → `[[20260323_BoldTrailEnrichment_ProjectSummary\|BoldTrail Enrichment]]`
- `Active Work Ledger.md` → `[[20260323_VaultSyncSkill_DesignBrief\|boldtrail-vault-sync Skill]]`

### ❌ True Broken Links (14 links)

**Placeholder / concept references** — these appear in guide/reference notes and reference words like "wikilinks" as Obsidian concepts, not as actual note names. Safe to remove the brackets or leave as-is:

- `05-Resources/20260403_VaultFolderStructureGuide.md` → `[[wikilinks]]`
- `05-Resources/20260402_ObsidianSecondBrainSetupChecklist.md` → `[[wikilinks]]`
- `04-Projects/0401-VaultSetUp/20260323_VaultHealthReport.md` → `[[wikilink]]`
- `04-Projects/0401-VaultSetUp/20260323_VaultHealthReport.md` → `[[wikilinks]]`
- `90-Archive/Welcome.md` → `[[create a link]]`
- `04-Projects/0401-VaultSetUp/20260323_VaultHealthReport.md` → `[[create a link]]`

**Template references** — these point to templates in `06-Templates/` (excluded from scan). The templates exist; these links are valid but flagged due to scan exclusion:

- `04-Projects/0402-BoldTrailClientStatus/20260323_VaultSyncSkill_DesignBrief.md` → `[[Buyer Client]]`
- `04-Projects/0402-BoldTrailClientStatus/20260323_VaultSyncSkill_DesignBrief.md` → `[[Seller Client]]`
- `04-Projects/0402-BoldTrailClientStatus/20260323_VaultSyncSkill_DesignBrief.md` → `[[Tenant]]`

**Folder-path links with no index note** — these use `[[folder/path]]` syntax expecting an index note that doesn't exist by that name:

- `04-Projects/0401-VaultSetUp/20260323_VaultHealthReport.md` → `[[02-Real-Estate/Listings/Active]]` *(file is `Active Listings.md`)*
- `04-Projects/0401-VaultSetUp/20260323_VaultHealthReport.md` → `[[02-Real-Estate/Transactions/Active]]` *(file is `Active Transactions.md`)*
- `04-Projects/0401-VaultSetUp/20260323_VaultHealthReport.md` → `[[02-Real-Estate/Rentals/Properties]]` *(file is `Rental Properties.md`)*
- `04-Projects/0401-VaultSetUp/20260323_VaultHealthReport.md` → `[[02-Real-Estate/Vendors-and-Contacts]]` *(file is `Vendors and Contacts.md`)*
- `04-Projects/0401-VaultSetUp/20260323_VaultHealthReport.md` → `[[03-Business/Goals-and-KPIs]]` *(file is `Goals and KPIs.md`)*
- `04-Projects/0401-VaultSetUp/20260323_VaultHealthReport.md` → `[[05-Resources/Scripts-and-Templates]]` *(file is `Scripts and Templates.md`)*
- `04-Projects/0401-VaultSetUp/20260323_VaultHealthReport.md` → `[[05-Resources/Legal-Forms]]` *(file is `Legal Forms.md`)*

**Other:**

- `04-Projects/0402-BoldTrailClientStatus/20260324_Session_VaultSync_Build.md` → `[[CLAUDE.md]]` *(CLAUDE.md exists but is excluded from the link graph by convention)*
- `04-Projects/0401-VaultSetUp/20260323_VaultHealthReport.md` → `[[20260322_VaultSetup\]]` *(note exists as `20260322_VaultSetup.md` — likely a backslash formatting issue)*

---

## Orphan Notes (18)

These notes have no incoming `[[wikilinks]]` from any other vault note. Daily notes and `00-Inbox/` files are excluded from this check.

### 🔴 Client cards with no incoming links (2)

These buyers exist in the vault but are not referenced from the Active Work Ledger or any other note:

- `02-Real-Estate/Clients/Buyers/DeNapoli_Patricia.md`
- `02-Real-Estate/Clients/Buyers/Villazan_Faust.md`

### 🟡 Client briefs with no incoming links (5)

These briefs in `05-Resources/Client-Briefs/` are not linked from the corresponding client cards:

- `05-Resources/Client-Briefs/20260324_Brief_Brown_Phyllis.md`
- `05-Resources/Client-Briefs/20260324_Brief_Heinzelmann_Karl.md`
- `05-Resources/Client-Briefs/20260326_Brief_Boland_Mark.md`
- `05-Resources/Client-Briefs/20260326_Brief_StLouis_Sacha.md`
- `05-Resources/Client-Briefs/20260326_Brief_Tapanainen_Jorma.md`

### 🟡 Market research with no incoming links (1)

- `02-Real-Estate/Market-Research/Communities/20260403_IonashoresCommunityOverview.md`

### 🟡 Resources with no incoming links (2)

- `05-Resources/20260327_BoldtrailAPIReference.md`
- `05-Resources/20260403_VaultFolderStructureGuide.md`

### 🟡 Project artifacts with no incoming links (6)

These are deep in the BoldTrail status manager project and not linked from the project's main note:

- `04-Projects/0402-BoldTrailClientStatus/20260327_StatusMigrationImpactReport.md`
- `04-Projects/0402-BoldTrailClientStatus/boldtrail-client-status-manager/SKILL.md`
- `04-Projects/0402-BoldTrailClientStatus/boldtrail-client-status-manager/references/status_definitions.md`
- `04-Projects/0402-BoldTrailClientStatus/boldtrail-client-status-manager/references/campaign_registry.md`
- `04-Projects/0402-BoldTrailClientStatus/reports/impact-report-2026-03-27.md`
- `04-Projects/0402-BoldTrailClientStatus/reports/impact-report-2026-03-27-backup.md`

### 🟡 Structural oddity (1)

A `Lead-Pipeline.md` file sits loose in `03-Business/` alongside the `Lead-Pipeline/` folder. The folder's `Lead Pipeline.md` is the actual dashboard. The loose file appears to be a duplicate or stale artifact:

- `03-Business/Lead-Pipeline.md`

### 🟡 Archive (1)

- `90-Archive/Welcome.md` — expected orphan (archive); low priority

---

## Stale Drafts

🟢 **None.** No notes with `status: draft` are older than 30 days.

---

## Recommended Actions

1. **Fix the 7 broken folder-path links in the March 23 health report** (`04-Projects/0401-VaultSetUp/20260323_VaultHealthReport.md`) — update to match actual note names (e.g., `[[Active Listings]]` instead of `[[02-Real-Estate/Listings/Active]]`). This is a one-time cleanup on an older report.

2. **Link client briefs into their client cards** — the 5 briefs in `05-Resources/Client-Briefs/` should have `[[wikilinks]]` from the corresponding buyer card (e.g., `Brown_Phyllis.md` should link to `[[20260324_Brief_Brown_Phyllis]]`). Run the Backlink Builder skill or do manually.

3. **Check `DeNapoli_Patricia` and `Villazan_Faust`** — two buyer cards with no links anywhere. Are they in the Active Work Ledger? Should they be? Add links or confirm they're parked.

4. **Add frontmatter to the 5 missing-FM files** — the 4 BoldTrail project reports and the `Welcome.md` in archive. Decide whether skill/tool reference files (SKILL.md, campaign_registry.md, status_definitions.md) need vault-standard frontmatter or a different convention.

5. **Fix the `[[20260322_VaultSetup\]]` backslash links** in the March 23 health report — remove the backslash.

6. **Investigate the loose `03-Business/Lead-Pipeline.md`** — if it's a duplicate of `03-Business/Lead-Pipeline/Lead Pipeline.md`, archive or delete it.

7. **Link `20260327_StatusMigrationImpactReport.md` and the impact report** from the BoldTrail project note — these are orphaned project deliverables.

8. **Low priority:** Remove brackets from `[[wikilinks]]` / `[[wikilink]]` / `[[create a link]]` placeholder text in guide notes and the archive Welcome note.
