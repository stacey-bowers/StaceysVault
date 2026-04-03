---
type: project
status: "active"
tags:
  - project
  - real-estate
  - CRM
  - decision
  - action-item
created: 2026-03-23
priority: "high"
---

# boldtrail-vault-sync — Skill Design Brief

> **Priority: HIGH** — This skill is the missing link between BoldTrail CRM and the Obsidian vault. Without it, every enriched contact requires manual vault card creation.

## Decision

**Build a separate skill** (`boldtrail-vault-sync`) rather than embedding vault-write logic into the existing `lead-enrichment` skill.

Documented in [[Decision Log]] — pending formal entry.

## Why Separate

1. **Composability.** Vault-sync can run independently of enrichment. Use cases where enrichment isn't needed but a vault card is:
   - Manually updated contacts in BoldTrail
   - Bulk imports from open house sign-in sheets
   - New leads from Zillow/website that already have decent data
   - Refreshing an existing vault card after a BoldTrail field change

2. **Reliability.** Enrichment is fragile — captchas, bot-blocking, API timeouts. If enrichment fails mid-waterfall, vault-sync can still run on whatever BoldTrail already has. Bundling them means one failure kills both.

3. **Clean skill boundaries.** Each skill has one job:
   - `lead-enrichment` → sources external data → writes to BoldTrail
   - `boldtrail-vault-sync` → reads from BoldTrail → writes/updates vault contact cards

## Intended Workflow

```
User: "enrich jane@email.com"
  → lead-enrichment skill runs waterfall, writes to BoldTrail
  → on success, prompts: "Enrichment complete. Sync to vault?"
  → User confirms → boldtrail-vault-sync creates/updates vault card

User: "sync contact jane@email.com to vault"
  → boldtrail-vault-sync runs standalone (no enrichment)
  → Pulls current BoldTrail data, creates/updates vault card
```

## Skill Scope — What It Needs To Do

### Core Functions
- **Create new contact cards** from BoldTrail contact data using the appropriate vault template (Buyer Client, Seller Client, Tenant, Landlord)
- **Update existing contact cards** when BoldTrail data has changed (never overwrite manual vault edits — merge strategy needed)
- **Route to correct folder** based on contact type:
  - Buyers → `02-Real-Estate/Clients/Buyers/`
  - Sellers → `02-Real-Estate/Clients/Sellers/`
  - Tenants → `02-Real-Estate/Clients/Tenants/`
  - Landlords → `02-Real-Estate/Clients/Landlords/`
- **Handle naming convention** → `LastName_FirstName.md`

### Data Mapping (BoldTrail → Vault Card)
| BoldTrail Field | Vault Card Section |
| --------------- | ------------------ |
| first_name, last_name | Filename + header |
| email, emails[] | Contact Info |
| cell_phone_1, cell_phone_2, home_phone, work_phone | Contact Info — phones |
| addresses[] | Address section |
| tags[] | Frontmatter tags + inline tags |
| notes/details | Notes section (append, don't overwrite) |
| source | Lead Source in frontmatter |
| birthday | Personal details |
| assign_type (buyer/seller/etc.) | Determines template + folder routing |
| custom fields (job_title, company) | Background section |

### Merge Strategy for Updates
- **Never overwrite** fields that have been manually edited in the vault (detect by comparing against last-synced BoldTrail snapshot)
- **Append** new notes, don't replace existing ones
- **Add** new phone numbers / emails to the card without removing manually-added ones
- **Flag conflicts** — if BoldTrail says one thing and vault says another, add a `needs-review` tag and note the conflict

### Trigger Phrases
- "sync contact [email/name] to vault"
- "create vault card for [email/name]"
- "update vault card from BoldTrail"
- "pull [name] from BoldTrail into vault"
- "vault sync"

### API Requirements
- Same Chrome JS execution pattern as lead-enrichment (BoldTrail API via `javascript_tool`)
- Read vault templates from `06-Templates/`
- Write to appropriate `02-Real-Estate/Clients/` subfolder
- Check for existing vault card before creating (prevent duplicates)

## Templates To Reference
- [[Buyer Client]] → `06-Templates/Buyer Client.md`
- [[Seller Client]] → `06-Templates/Seller Client.md`
- [[Tenant]] → `06-Templates/Tenant.md`
- (Landlord template may need to be created)

## Open Questions
- [ ] Should vault-sync auto-trigger after every enrichment, or always require user confirmation?
- [ ] How to handle contacts with no assign_type in BoldTrail — default to Buyer?
- [ ] Batch mode — "sync all enriched contacts to vault" vs. one-at-a-time?
- [ ] Should the skill also sync *from* vault *to* BoldTrail (two-way sync), or keep it one-directional for now?

## Next Steps
- [ ] Build the skill using skill-creator
- [ ] Read all four client templates to map exact field placement
- [ ] Implement BoldTrail→vault field mapping
- [ ] Test on [[Watson_Kelley]] (compare manual card vs. auto-generated)
- [ ] Test on 2-3 more contacts
- [ ] Add trigger to lead-enrichment skill to prompt vault-sync after enrichment completes

## Resources
- [[20260323_BoldTrailEnrichment_ProjectSummary]] — Parent project
- [[Watson_Kelley]] — First manually-created vault card (reference for what output should look like)
- BoldTrail API: https://apidocs.kvcore.com/
- Skill creator: use `skill-creator` skill to scaffold and package
