---
tags: [vault-health, reference]
created: 2026-04-03
type: research
status: active
---

# Vault Health Report — 2026-04-03 (Post-Remediation)

> Second run — follows [[20260403_VaultHealthReport]] and [[20260403_VaultHealthRemediation_Plan]].
> All Track A and Track B items complete as of today's session.

---

## Summary — Before vs. After

| Check | Before | After | Change |
|---|---|---|---|
| Total files | 63 | 65 | +2 (new project note + archive backup) |
| Missing frontmatter | 5 | **0** | ✅ Resolved |
| Incomplete frontmatter | 1 | **0** | ✅ Resolved |
| Broken wikilinks (real) | 14 | **5** | ✅ 9 resolved |
| Orphan notes | 18 | **10** | ✅ 8 resolved |
| Stale drafts | 0 | 0 | 🟢 Clean |

---

## Overall Health

| Check | Issues | Health |
|---|---|---|
| Frontmatter completeness | 0 of 65 | 🟢 |
| Broken wikilinks (real) | 5 | 🟡 |
| Orphan notes | 10 (4 accepted, 6 residual) | 🟡 |
| Stale drafts | 0 | 🟢 |

---

## Frontmatter — 🟢 Perfect

All 65 notes have complete, valid frontmatter. Nothing to do here.

---

## Broken Wikilinks — 🟡 5 Real Issues

> **Note on this run's count:** The scanner flagged 56 links total, but 51 of those are false positives — they appear inside backtick code spans in the health report, remediation plan, and old vault setup notes (e.g., `` `[[02-Real-Estate/Listings/Active]]` ``). Obsidian does not parse those as links. The 5 real broken links below are all in live, active notes.

### Template references (3) — Low priority, effectively false positives

These links exist in a design brief note and point to templates in `06-Templates/` which is excluded from the link scanner. The templates exist on disk.

- `04-Projects/0402-BoldTrailClientStatus/20260323_VaultSyncSkill_DesignBrief.md` → `[[Buyer Client]]`
- `04-Projects/0402-BoldTrailClientStatus/20260323_VaultSyncSkill_DesignBrief.md` → `[[Seller Client]]`
- `04-Projects/0402-BoldTrailClientStatus/20260323_VaultSyncSkill_DesignBrief.md` → `[[Tenant]]`

### CLAUDE.md reference (1) — False positive

- `04-Projects/0402-BoldTrailClientStatus/20260324_Session_VaultSync_Build.md` → `[[CLAUDE.md]]`

CLAUDE.md exists but is intentionally excluded from the link graph (it's a system file). This link works in Obsidian.

### Concept text (1) — Cosmetic only

- `90-Archive/Welcome.md` → `[[create a link]]` — Obsidian default welcome note tutorial text. Archived. No action needed.

**Effective broken link count: 0 actionable items.**

---

## Orphan Notes — 🟡 10 Total (4 accepted, 6 residual)

### ✅ Accepted orphans — no action needed (4)

These were reviewed and intentionally left without incoming links:

- `02-Real-Estate/Clients/Buyers/DeNapoli_Patricia.md` — B1 decision: keep, still in development
- `02-Real-Estate/Clients/Buyers/Villazan_Faust.md` — B1 decision: keep, still in development
- `90-Archive/Welcome.md` — archived file, expected orphan
- `90-Archive/Completed-Projects/impact-report-2026-03-27-backup.md` — just archived, expected orphan

### 🟡 Residual orphans — worth linking when convenient (6)

These aren't urgent but would strengthen the knowledge graph:

**Resource guides (2)** — useful reference docs with no incoming links:
- `05-Resources/20260327_BoldtrailAPIReference.md` — could be linked from the BoldTrail Enrichment project note
- `05-Resources/20260403_VaultFolderStructureGuide.md` — could be linked from Home.md or the Vault Setup project

**BoldTrail status manager skill assets (3)** — deep project files:
- `04-Projects/0402-BoldTrailClientStatus/boldtrail-client-status-manager/SKILL.md`
- `04-Projects/0402-BoldTrailClientStatus/boldtrail-client-status-manager/references/status_definitions.md`
- `04-Projects/0402-BoldTrailClientStatus/boldtrail-client-status-manager/references/campaign_registry.md`

These could be linked from `20260323_BoldTrailEnrichment_ProjectSummary.md` or the status manager project notes. Low priority — they're operational tools, not knowledge notes.

**Impact report (1)**:
- `04-Projects/0402-BoldTrailClientStatus/reports/impact-report-2026-03-27.md` — Note: this is a *different file* from `[[20260327_StatusMigrationImpactReport]]` (which was linked in A6). This one lives in the `reports/` subfolder and has a different filename. Should be linked from the project note or cross-referenced with the other impact report.

---

## Stale Drafts — 🟢 Clean

No stale drafts. Nothing to do.

---

## What Was Fixed This Session

| Item | Action |
|---|---|
| 7 backslash wikilinks in Active Work Ledger | Fixed — `[[Note\|Alias]]` → `[[Note|Alias]]` |
| 5 files with missing frontmatter | Added compliant YAML frontmatter |
| 1 file with incomplete frontmatter (SKILL.md) | Added 4 required fields |
| 5 client briefs orphaned from buyer cards | Added `## Related Documents` section + wikilink to each buyer card |
| BoldTrail impact report orphaned | Linked from `20260323_BoldTrailEnrichment_ProjectSummary` |
| `03-Business/Lead-Pipeline.md` stub | Transformed into proper project kickoff, moved to `04-Projects/0403-LeadPipeline/` |
| `20260403_IonashoresCommunityOverview.md` orphan | Linked from Home.md under new Market Research section |
| Impact report backup | Archived to `90-Archive/Completed-Projects/` |
| Skill asset frontmatter convention | Documented in [[Decision Log]] |
| Lead Pipeline as formal project | Documented in [[Decision Log]] |
| Market Research community overview structure | Documented in [[Decision Log]] |

---

## Recommended Next Actions (Low Priority)

1. Link `reports/impact-report-2026-03-27.md` from the BoldTrail project note — it's a different file from the status migration report and still unlinked.
2. Link the two resource guides (`BoldtrailAPIReference`, `VaultFolderStructureGuide`) from their natural homes when it comes up naturally.
3. The 3 skill asset files in `boldtrail-client-status-manager/` can be linked from the project note if desired — not urgent.

**The vault is in strong shape. All critical issues resolved.**
