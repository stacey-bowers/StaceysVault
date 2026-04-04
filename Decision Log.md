---
tags:
  - decision
  - dashboard
  - MOC
created: 2026-03-22
type: reference
status: active
---

# Decision Log

> Every decision worth remembering goes here — what was decided, why, and when. No more "wait, why did we do it that way?"

## How to Use This Log
- Tag any note containing a decision with `decision` in its frontmatter tags
- Log the decision here with date, context, and rationale
- Link back to the source note where the decision was made
- Revisit quarterly to confirm decisions still hold

---

## Vault & System Decisions

| Date | Decision | Rationale | Source |
| ---- | -------- | --------- | ------ |
| 2026-04-03 | Skill asset files in project folders (SKILL.md, campaign_registry.md, status_definitions.md, etc.) use vault-standard frontmatter (`tags`, `created`, `type: reference`, `status`) | Keeps them visible in Obsidian queries and the health checker; minimal overhead; doesn't interfere with their skill-specific fields | [[20260403_VaultHealthReport]] |
| 2026-04-03 | Lead Pipeline is a formal project in `04-Projects/0403-LeadPipeline/` | Elevates pipeline work from a loose business folder stub to a tracked project with scope, progress log, and links — consistent with how enrichment and vault setup are managed | [[20260403_LeadPipeline_ProjectKickoff]] |
| 2026-04-03 | Market Research community overviews live in `02-Real-Estate/Market-Research/Communities/` with links from Home.md | First of a series of community knowledge articles; Home.md Market Research section will grow as more communities are documented | [[20260403_IonashoresCommunityOverview]] |
| 2026-03-22 | Use numbered folder prefixes (00–90) for vault structure | Keeps sidebar sorted logically regardless of Obsidian sort settings — no fighting alphabetical order | [[20260322_VaultSetup]] |
| 2026-03-22 | Vault lives on iCloud (`~/Library/Mobile Documents/`) | Automatic sync across all Apple devices without a third-party sync service | [[20260322_VaultSetup]] |
| 2026-03-22 | All new captures go to `00-Inbox/` first, then get processed and filed | Separates capture from organization — never lose a thought, never clutter a folder | [[20260322_VaultSetup]] |
| 2026-03-22 | Templates use Obsidian core Templates plugin (not Templater) | Simpler setup, no community plugin dependency — can upgrade later if needed | [[20260322_VaultSetup]] |
| 2026-03-22 | No spaces in filenames — underscores or CamelCase only | Prevents linking issues and keeps CLI/scripting friendly | [[20260322_VaultSetup]] |
| 2026-03-22 | Archive to `90-Archive/` instead of deleting notes | Nothing is ever truly gone — protects against accidental loss and preserves history | [[20260322_VaultSetup]] |
| 2026-03-22 | Daily notes use `YYYYMMDD.md` format, project notes use `YYYYMMDD_NoteTitle.md` | Consistent date-first naming makes everything sortable by time | [[20260322_VaultSetup]] |
| 2026-03-22 | Decision Log lives at vault root (same level as Active Work Ledger) | It's a vault-wide reference doc, not tied to any single project | — |
| 2026-04-03 | Use GitHub for vault version history (private repo: `stacey-bowers/StaceysVault`) | iCloud protects against device loss but has no rollback; GitHub gives complete undo history if a skill goes haywire or notes get overwritten | [[20260322_VaultSetup]] |
| 2026-04-03 | Use Obsidian Git plugin (v2.38.0) for auto-commits — not manual git | Plugin integrates directly into Obsidian; auto commit-and-sync every 120 min + on file edit stop; no Terminal required after initial setup | [[20260322_VaultSetup]] |
| 2026-04-03 | PAT (Personal Access Token) stored in macOS Keychain, not SSH | HTTPS + PAT is simpler to configure for a solo user on one Mac; Keychain stores it so future commits are fully silent | [[20260322_VaultSetup]] |
| 2026-04-03 | GitHub account uses Domain Realty email (`stacey@domainrealtygroup.com`), username `stacey-bowers` | Account already existed under that email; using domain email keeps business tools centralized | [[20260322_VaultSetup]] |

## Real Estate Decisions

| Date | Decision | Rationale | Source |
| ---- | -------- | --------- | ------ |
| 2026-03-24 | Add TCPA/compliance section to all client templates | 2025 TCPA changes require documented consent for marketing texts/calls — legal liability without tracking | [[20260323_VaultSyncSkill_DesignBrief]] |
| 2026-03-24 | Add Spouse/Partner section to all client templates | Co-decision-makers in real estate (co-borrowers, joint deed holders); critical for SW FL couple/snowbird clientele | [[20260323_VaultSyncSkill_DesignBrief]] |
| 2026-03-24 | Add Social Profiles section to all client templates | Agents need client social presence for marketing strategy, referral identification, and personal connection | [[20260323_VaultSyncSkill_DesignBrief]] |
| 2026-03-24 | Add BoldTrail Search Behavior subsection to Buyer template | BoldTrail tracks what leads search on the website (avg price/beds/baths) — reveals actual preferences vs stated | [[20260323_VaultSyncSkill_DesignBrief]] |
| 2026-03-24 | Add Last Activity section to all client templates | Activity timestamps from BoldTrail drive follow-up timing and lead scoring | [[20260323_VaultSyncSkill_DesignBrief]] |
| 2026-03-24 | Create Landlord Client template | Vault had the folder but no template — rental operations need proper landlord tracking with property portfolio and financials | [[20260323_VaultSyncSkill_DesignBrief]] |
| 2026-03-24 | Add Financing Details to Buyer template (type, down payment, source) | Industry research shows financing type and down payment are critical for offer competitiveness | [[20260323_VaultSyncSkill_DesignBrief]] |

## Business Decisions

| Date | Decision | Rationale | Source |
| ---- | -------- | --------- | ------ |
| 2026-03-23 | Build separate boldtrail-vault-sync skill (not embedded in lead-enrichment) | Composability — vault-sync runs independently of enrichment; reliability — enrichment failures don't block vault writes; clean boundaries — each skill has one job | [[20260323_VaultSyncSkill_DesignBrief]] |
| 2026-03-24 | Vault-sync uses one-directional flow (BoldTrail → vault only) for v1 | Keep scope manageable; vault edits are manual and sacred; two-way sync adds complexity with conflict resolution | [[20260323_VaultSyncSkill_DesignBrief]] |
| 2026-03-24 | Client Briefs saved to `05-Resources/Client-Briefs/` as permanent quick-reference files | Stacey accesses vault via iCloud on her phone — briefs need to be findable, phone-readable, and include a draft reply; permanent folder builds a history of client interactions | — |

## Personal Decisions

| Date | Decision | Rationale | Source |
| ---- | -------- | --------- | ------ |
|      |          |           |        |

---
*Links:* [[Active Work Ledger]] | [[Projects Dashboard]] | [[Home]]
