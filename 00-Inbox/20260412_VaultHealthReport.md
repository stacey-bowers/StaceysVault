---
tags:
  - vault-health
  - reference
created: 2026-04-12
type: research
status: active
---

# Vault Health Report — 2026-04-12

## Summary
| Check | Total Files | Issues Found | Health |
|---|---|---|---|
| Frontmatter completeness | 74 | 0 real issues | 🟢 |
| Broken wikilinks | 390 links checked | 3 real broken | 🟡 |
| Orphan notes | 74 files checked | 12 orphans | 🔴 |
| Stale drafts | 74 files | 0 stale | 🟢 |

Health key: 🟢 0 issues · 🟡 1–5 issues · 🔴 6+ issues

---

## Frontmatter Issues

### ✅ All Clear
72 of 74 files have complete, valid frontmatter. The 2 flagged files (`CLAUDE.md` and `90-Archive/global_CLAUDE.md`) are configuration/system files that don't require standard frontmatter — no action needed.

---

## Broken Wikilinks — Real Issues (3)

Most of the 86 raw hits are **false positives** — example syntax in CLAUDE.md and old health reports (`[[wikilink]]`, `[[create a link]]`, `[[Note|Alias]]`). The following are genuinely broken:

| Source | Broken Link | Fix |
|---|---|---|
| `04-Projects/0404-GmailCleanup/20260404_GmailCleanup_ProjectKickoff.md` | `[[Gmail_Cleanup_Cowork_Prompt_Sequence]]` (×2) | Create the note or remove the link |
| `CLAUDE.md` | `[[02-Real-Estate/Listings/Active]]` | Points to folder, not a note — link to `[[Active Listings]]` instead |

**Note:** Several old health reports and remediation plans in `04-Projects/0401-VaultSetUp/` contain escaped pipe characters in wikilinks (e.g., `[[Brown_Phyllis\|Phyllis Brown]]`). These render incorrectly in Obsidian. There are ~20 instances across 4 files. Low priority since they're project documentation, not active reference notes.

---

## Orphan Notes (12)

No other vault note links to these files.

### 🔴 High Priority — Client cards with no incoming links
| File | Suggested Fix |
|---|---|
| `02-Real-Estate/Clients/Buyers/DeNapoli_Patricia.md` | Add to [[Active Work Ledger]] or [[Lead Pipeline]] — she's a 5-star rated active lead |
| `02-Real-Estate/Clients/Buyers/Villazan_Faust.md` | Add to [[Active Work Ledger]] or [[Lead Pipeline]] — active site visitor |

### 🟡 Medium Priority — Useful reference notes not linked
| File | Suggested Fix |
|---|---|
| `05-Resources/20260327_BoldtrailAPIReference.md` | Link from [[20260323_BoldTrailEnrichment_ProjectSummary]] |
| `04-Projects/0401-VaultSetUp/20260403_VaultFolderStructureGuide.md` | Link from [[20260322_VaultSetup]] or [[Home]] |
| `04-Projects/0401-VaultSetUp/20260403_VaultHealthReport_v2.md` | Link from the vault setup project or archive |
| `04-Projects/0402-BoldTrailClientStatus/boldtrail-client-status-manager/SKILL.md` | Link from [[20260323_BoldTrailEnrichment_ProjectSummary]] |
| `04-Projects/0402-BoldTrailClientStatus/boldtrail-client-status-manager/references/status_definitions.md` | Link from SKILL.md or project summary |
| `04-Projects/0402-BoldTrailClientStatus/boldtrail-client-status-manager/references/campaign_registry.md` | Link from SKILL.md or project summary |
| `04-Projects/0402-BoldTrailClientStatus/reports/impact-report-2026-03-27.md` | Link from project summary |

### 🟢 Low Priority — Archive files (expected orphans)
| File | Notes |
|---|---|
| `90-Archive/Welcome.md` | Obsidian default welcome note — can stay orphaned |
| `90-Archive/global_CLAUDE.md` | Old CLAUDE.md version — archived, no action needed |
| `90-Archive/Completed-Projects/impact-report-2026-03-27-backup.md` | Backup copy — expected orphan |

---

## Stale Drafts

### ✅ None
No notes with `status: draft` older than 30 days.

---

## Recommended Actions (Prioritized)

1. **Link DeNapoli_Patricia and Villazan_Faust to the Lead Pipeline or Active Work Ledger** — these are active leads with no vault connectivity. DeNapoli is 5-star rated. High impact.
2. **Create or remove `[[Gmail_Cleanup_Cowork_Prompt_Sequence]]`** — broken link in the Gmail Cleanup project kickoff.
3. **Fix CLAUDE.md folder-path link** — `[[02-Real-Estate/Listings/Active]]` should point to `[[Active Listings]]`.
4. **Link BoldTrail reference notes** — connect API reference, status definitions, and campaign registry to the enrichment project summary.
5. **Fix escaped pipe characters in old health reports** — cosmetic, ~20 instances across 4 files in `04-Projects/0401-VaultSetUp/`. Low priority.

---
*Links:* [[Active Work Ledger]] | [[20260412]] | [[20260403_VaultHealthReport]]
