---
tags: [vault-health, reference]
created: 2026-03-23
type: research
status: active
---

# Vault Health Report — 2026-03-23

## Summary

| Check | Total Files | Issues Found | Health |
|---|---|---|---|
| Frontmatter completeness | 15 | 12 | 🔴 |
| Broken wikilinks | 19 raw / 16 real | 16 | 🔴 |
| Orphan notes | 15 files checked | 4 | 🟡 |
| Stale drafts | 0 drafts | 0 | 🟢 |

Health key: 🟢 0 issues · 🟡 1–5 issues · 🔴 6+ issues

> **Note:** This vault is in early setup. Many issues below reflect scaffolding that hasn't been filled in yet — not decay. The main priority is getting frontmatter and folder structure aligned with CLAUDE.md conventions.

---

## Frontmatter Issues

### ❌ Missing Frontmatter (3 files)

- `Welcome.md` — Obsidian default welcome note, no frontmatter at all
- `CLAUDE.md` — vault instruction file (frontmatter optional here, but flagged for completeness)
- `05-Resources/Checklists.md` — resource note with no YAML block

### ⚠️ Incomplete Frontmatter (9 files)

These files have frontmatter but are missing required fields or use `type` values not in the CLAUDE.md schema (`daily | project | research | reflection | reference | personal-development | inbox`).

- `Active Work Ledger.md` — missing: `created`, `status`; invalid type `ledger`
- `Home.md` — missing: `created`, `status`; invalid type `home`
- `10-Personal/Family-and-Home/Family Dashboard.md` — missing: `created`, `status`; invalid type `dashboard`
- `10-Personal/Health-and-Wellness/Health Dashboard.md` — missing: `created`, `status`; invalid type `dashboard`
- `03-Business/Goals-and-KPIs/2026 Goals.md` — missing: `created`, `status`; invalid type `goals`
- `03-Business/Lead-Pipeline/Lead Pipeline.md` — missing: `created`, `status`; invalid type `dashboard`
- `05-Resources/Checklists/Buyer Transaction Checklist.md` — missing: `created`, `status`; invalid type `checklist`
- `05-Resources/Checklists/Listing Checklist.md` — missing: `created`, `status`; invalid type `checklist`
- `04-Projects/Projects Dashboard.md` — missing: `created`, `status`; invalid type `dashboard`

**Pattern:** Almost every file is missing `created` and `status`, and many use `type` values (`dashboard`, `ledger`, `checklist`, `goals`, `home`) that aren't in the CLAUDE.md schema. Consider expanding the valid `type` list or remapping these.

---

## Broken Wikilinks (16)

*Excluded 3 false positives from CLAUDE.md (documentation examples: `[[wikilink]]`, `[[wikilinks]]`).*

Most of these are from `Home.md` — it's a hub page linking to folders and sections that don't have matching notes yet.

**From `Home.md` (14 broken links):**

- `[[02-Real-Estate/Listings/Active]]`
- `[[02-Real-Estate/Clients]]`
- `[[02-Real-Estate/Transactions/Active]]`
- `[[02-Real-Estate/Rentals/Properties]]`
- `[[02-Real-Estate/Showings]]`
- `[[02-Real-Estate/Vendors-and-Contacts]]`
- `[[03-Business/Lead-Pipeline]]`
- `[[03-Business/Goals-and-KPIs]]`
- `[[03-Business/SOPs]]`
- `[[03-Business/Financials]]`
- `[[10-Personal/Recipes]]`
- `[[05-Resources/Checklists]]`
- `[[05-Resources/Scripts-and-Templates]]`
- `[[05-Resources/Legal-Forms]]`

**From `Welcome.md` (1):**

- `[[create a link]]` — Obsidian tutorial placeholder

**From `04-Projects/Projects Dashboard.md` (1):**

- `[[20260322_VaultSetup\]]` — malformed link (trailing backslash)

---

## Orphan Notes (4)

These notes have no incoming wikilinks from any other note in the vault:

- `Welcome.md` — Obsidian default file, safe to archive
- `03-Business/Goals-and-KPIs/2026 Goals.md` — should be linked from a hub page
- `05-Resources/Checklists.md` — duplicate? There's also a `Checklists/` folder
- `05-Resources/Checklists/Listing Checklist.md` — should be linked from a checklist index or hub

---

## Stale Drafts (0)

No stale drafts found. 🟢

---

## Folder Structure vs. CLAUDE.md

The CLAUDE.md spec defines a folder structure that doesn't fully match what's on disk. Notable differences:

| CLAUDE.md Expected | Actual on Disk | Status |
|---|---|---|
| `00-Templates/` | `06-Templates/` | Different numbering |
| `02-Projects/` | `04-Projects/` + `Projects/` | Split across two folders |
| `03-Research/` | `03-Business/` | Different purpose |
| `04-Indexes/` | Not present | Missing |
| `05-Reflection/` | `20-Reflection/` | Different numbering |
| `10-PersonalDevelopment/` | `10-Personal/` | Different name |
| `99-System/` | Not present | Missing |
| N/A | `02-Real-Estate/` | Not in spec |

**Recommendation:** Either update CLAUDE.md to match the actual vault layout, or restructure the vault to match the spec. The current mismatch means skills and automations may file notes to the wrong locations.

---

## Recommended Actions

1. **🔴 Sync CLAUDE.md with actual folder structure** — This is the highest-impact fix. Every skill reads CLAUDE.md for routing, so the mismatch will cause misfiled notes. Either update the spec or restructure folders.
2. **🔴 Fix `Home.md` broken links** — Home is the vault's main navigation hub. Create stub notes for each broken link target, or update the links to match existing paths.
3. **🔴 Expand the `type` taxonomy** — Add `dashboard`, `ledger`, `checklist`, `goals`, and `home` as valid frontmatter types in CLAUDE.md, since the vault actively uses them.
4. **🟡 Add `created` and `status` to all notes** — Every incomplete note is missing these two fields. A batch frontmatter fix would clean this up fast.
5. **🟡 Fix the malformed wikilink** in `Projects Dashboard.md` — `[[20260322_VaultSetup\]]` has a trailing backslash.
6. **🟡 Link orphan notes** — Wire `2026 Goals.md` and the checklist files into their respective hub pages.
7. **🟢 Archive `Welcome.md`** — Default Obsidian file, not part of your vault structure.
