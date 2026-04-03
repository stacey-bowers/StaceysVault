---
type: project
status: active
tags:
  - project
  - real-estate
  - CRM
  - pipeline
  - decision
created: 2026-03-24
---

# Session Notes — Vault-Sync Build & Testing (2026-03-24)

## Session Summary

Built the `boldtrail-vault-sync` skill from the [[20260323_VaultSyncSkill_DesignBrief|design brief]], upgraded all client templates with critical missing fields, tested on 3 contacts, and created a Client Brief system for on-the-go phone lookups.

## What Was Built

### boldtrail-vault-sync Skill (v2)
- Standalone skill — separate from lead-enrichment per architecture decision
- One-directional flow: BoldTrail → vault (manual vault edits are sacred)
- Merge strategy: BoldTrail supplements, never overwrites manual edits
- Packaged as `boldtrail-vault-sync.skill` in vault root
- Built at `/tmp/boldtrail-vault-sync/` (sandbox filesystem is read-only for skills directory)

### Template Upgrades (All 4 Client Templates)
All client templates now include standardized sections:

| Section | Why |
| ------- | --- |
| **Compliance** | TCPA 2025 requires documented consent for marketing texts/calls — legal liability |
| **Spouse/Partner** | Co-decision-makers in RE, especially SW FL couples and snowbirds |
| **Social Profiles** | Marketing strategy, referral identification, personal connection |
| **Last Activity** | BoldTrail timestamps drive follow-up timing and lead scoring |

Buyer-specific additions:
- **BoldTrail Search Behavior** — avg_price, avg_beds, avg_baths from website activity (reveals actual vs. stated preferences)
- **Financing Details** — type, down payment, source (critical for offer competitiveness)
- **Expanded housing context** — current housing, reason for buying

New template created:
- **Landlord Client** — was missing entirely; includes property portfolio, financials, cap rate, maintenance tracking

### Client Brief System
- **Template:** `06-Templates/Client Brief.md`
- **Output folder:** `05-Resources/Client-Briefs/`
- **Purpose:** Phone-friendly quick-reference when a client texts/calls unexpectedly
- **Format:** One-screen brief with compliance check, what they want, last conversation, 3 talking points, draft reply
- **Access:** iCloud sync means Stacey can pull up briefs on her phone via Obsidian mobile

## Testing Results

### Test 1: Karl Heinzelmann (BoldTrail #213119)
- **Type:** Buyer/Renter (dual interest)
- **Data richness:** Rich — 5-star, 4 phones (skip trace), TCPA consent dated, 10 BoldTrail notes, call history
- **Result:** Full card generated with all v2 sections populated. Communication log auto-populated from BoldTrail notes (website registration + phone call). Search criteria pulled from Stacey's call notes (Highland Woods, golf/pickleball, March 2027, 1-month only).
- **Filed to:** `02-Real-Estate/Clients/Buyers/Heinzelmann_Karl.md`

### Test 2: Scott Coleman (BoldTrail #165231)
- **Type:** Buyer
- **Data richness:** Thin — 2-star FB lead, one phone, one email, no notes, no address, no occupation
- **Result:** Card generated with BoldTrail Search Behavior as primary intel ($349K / 2bd / 1ba). TCPA gap flagged (consent flags set but date zeroed out). 7 actionable next steps including re-engagement (dormant 1+ year).
- **Filed to:** `02-Real-Estate/Clients/Buyers/Coleman_Scott.md`

### Test 3: Client Brief — Karl Heinzelmann (Estero scenario)
- **Scenario:** "I just got a text from (917) 293-5737 asking about Estero"
- **Result:** Phone lookup found Karl instantly. Brief generated in <30 seconds with compliance clearance, context from last call, 3 talking points specific to Estero inquiry, and draft reply ready to copy-paste.
- **Filed to:** `05-Resources/Client-Briefs/20260324_Brief_Heinzelmann_Karl.md`

## Technical Notes

### API Access Pattern
All BoldTrail API calls go through Chrome JavaScript execution (`mcp__Claude_in_Chrome__javascript_tool`). Direct HTTP from the sandbox is blocked. Bearer token must be inline in every call — `window` variables don't persist across navigations.

### Key API Endpoints Used
- `GET /contacts/search?q=` — find contact by name
- `GET /contact/{id}` — full contact data pull
- `GET /contact/{id}/tags` — contact tags
- `GET /contact/{id}/action/note` — contact notes/activity

### Known Issues
- Combined `Promise.all` calls for tags + notes sometimes get blocked — splitting into sequential calls works
- BoldTrail returns `"0000-00-00 00:00:00"` for empty date fields — must be interpreted as "not documented"
- Unix timestamps in BoldTrail (`last_call`, `last_visit`) need conversion to YYYY-MM-DD
- Contact search returns truncated results — full `/contact/{id}` pull needed for complete data

### Vault-Sync Skill File Locations
- Skill source: `/tmp/boldtrail-vault-sync/`
- Main instructions: `/tmp/boldtrail-vault-sync/SKILL.md`
- Field mapping: `/tmp/boldtrail-vault-sync/config/vault_field_mapping.json`
- Merge strategy: `/tmp/boldtrail-vault-sync/references/merge_strategy.md`
- Credentials: `/tmp/boldtrail-vault-sync/config/boldtrail_credentials.json`
- Packaged skill: `/sessions/compassionate-confident-gates/mnt/StaceysVault/boldtrail-vault-sync.skill`

## Decisions Made This Session

| Decision | Rationale |
| -------- | --------- |
| Add TCPA/Compliance to all client templates | 2025 TCPA changes — legal liability without documented consent |
| Add Spouse/Partner to all client templates | Co-decision-makers, especially SW FL couples/snowbirds |
| Add Social Profiles to all client templates | Marketing, referral ID, personal connection |
| Add BoldTrail Search Behavior to Buyer template | Website activity reveals actual preferences vs. stated |
| Add Last Activity to all client templates | Timestamps drive follow-up timing and lead scoring |
| Create Landlord Client template | Vault had the folder but no template |
| Add Financing Details to Buyer template | Down payment type/source critical for offer competitiveness |
| Client Briefs to `05-Resources/Client-Briefs/` | Permanent, phone-accessible via iCloud, builds interaction history |

All decisions logged in [[Decision Log]].

## Vault Updates Made
- [[Decision Log]] — 10 new entries (7 Real Estate, 2 Business, 1 Client Brief)
- [[Active Work Ledger]] — vault-sync status updated to BUILT v2
- [[CLAUDE.md]] — updated to v2.1 (tag taxonomy, templates table, skills table, frontmatter docs)
- Daily note [[20260324]] — checked off vault-sync build, added 7 wins entries

## Open / Carry Forward
- [ ] Install `boldtrail-vault-sync.skill` formally to skills directory
- [ ] Update [[Watson_Kelley]] with new v2 fields (compliance, spouse, social, activity)
- [ ] Manual Collier County property appraiser lookup for Kelley Watson
- [ ] Test vault-sync on seller and tenant contacts (only tested buyers so far)
- [ ] Document SOP for on-demand vault-sync workflow
- [ ] Consider building Client Brief generation into a skill for faster triggering

## Links
- [[20260323_VaultSyncSkill_DesignBrief]] — Design brief
- [[20260323_BoldTrailEnrichment_ProjectSummary]] — Parent project summary
- [[Watson_Kelley]] | [[Heinzelmann_Karl]] | [[Coleman_Scott]] — Test contact cards
- [[Decision Log]] | [[Active Work Ledger]]
