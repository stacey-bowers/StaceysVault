---
type: project
status: "active"
tags:
  - project
  - real-estate
  - CRM
  - lead
  - pipeline
start_date: "2026-03-23"
due_date: ""
priority: "high"
created: 2026-03-23
---

# BoldTrail Enrichment

## Overview
- **Goal:** Build and maintain an on-demand lead enrichment pipeline that pulls data from public records, people-search engines, Apollo, and county property appraisers — then writes it back to BoldTrail CRM and syncs enriched contact cards into the Obsidian vault.
- **Why it matters:** Richer contact data means better follow-up, snowbird detection, and property-owner intelligence for every lead in the pipeline — without paying for expensive skip-tracing on every contact.
- **Due:** Ongoing (on-demand workflow, no scheduled runs)

## Scope
- **CRM:** BoldTrail (kvCORE API v2)
- **Geography:** SW Florida — Lee, Collier, Charlotte counties
- **Contact volume:** ~500 contacts
- **Enrichment modes:**
  - **Free pipeline:** Voter records, people-search sites (TruePeopleSearch, FastPeopleSearch, ThatsThem, PeekYou), Apollo (basic match)
  - **Advanced pipeline:** All free sources + Apollo credit-based enrichment + skip tracing (future)

## Completed Work

### Phase 1 — Skill Customization (2026-03-23)
- [x] Reviewed Jesse's lead-enrichment skill and mapped all required changes
- [x] Copied skill to editable workspace, updated all references from Jesse → Stacey
- [x] Removed scheduled/automated pipeline section (on-demand only)
- [x] Swapped BoldTrail API token to Stacey's credentials (token expires 2027-03-21)
- [x] Updated workspace path references to StaceysVault
- [x] Verified BoldTrail API connectivity via Chrome JS execution
- [x] Packaged updated skill as `lead-enrichment.skill`

### Phase 2 — Live Enrichment Test (2026-03-23)
- [x] Ran full free-pipeline enrichment on Kelley Watson (pilatesbykelley@gmail.com, contact ID 116)
- [x] Sources queried: voter records (match), TruePeopleSearch (partial — captcha on detail page), FastPeopleSearch (match — 7 phones, 6 past addresses, 14 relatives), ThatsThem (blocked — captcha), PeekYou (blocked — redirect), Apollo (match — title, company, employment history), Collier County appraiser (blocked — frames)
- [x] Data written to BoldTrail: primary address (2401 Poinciana Dr, Naples FL 34105), cell_phone_2, home_phone, work_phone, job title (Certified Pilates Instructor), company (Pilates of Cashiers)
- [x] Tags applied: enriched-free, enriched-2026-03-23, voter-record-match, snowbird-potential, needs-property-review
- [x] Enrichment log entry written with full rollback data
- [x] Snowbird flag detected (Clearwater voter record + Naples current address + Illinois history)

### Phase 3 — Vault Integration (2026-03-23)
- [x] Created buyer client contact card [[Watson_Kelley]] from enrichment data using Buyer Client template
- [x] Filed to `02-Real-Estate/Clients/Buyers/Watson_Kelley.md`
- [x] Card includes all enrichment data: 4 phone numbers + 3 overflow, Apollo employment history, addresses, voter record data, relatives, and next steps

## Open Tasks
- [x] Decide architecture: extend enrichment skill with vault-sync step vs. create separate BoldTrail-to-vault skill → **DECIDED: separate skill** — see [[20260323_VaultSyncSkill_DesignBrief]]
- [x] **HIGH PRIORITY:** Build `boldtrail-vault-sync` skill — design brief complete at [[20260323_VaultSyncSkill_DesignBrief]] ✅ BUILT v2, packaged as `.skill`
- [ ] Manual Collier County property appraiser lookup for Kelley Watson
- [ ] Test enrichment on 2-3 more contacts to validate reliability
- [ ] Document SOP for on-demand enrichment workflow
- [ ] Evaluate advanced pipeline (skip tracing) when volume justifies cost

## Technical Notes

### API Access Pattern
All BoldTrail API calls must go through Chrome JavaScript execution (`mcp__Claude_in_Chrome__javascript_tool`) — direct HTTP from the sandbox is blocked by the network proxy. The Bearer token must be embedded as a string literal in every call since `window` variables clear on navigation.

### Key Endpoints
- `GET /v2/public/contacts?email=` — contact lookup
- `PUT /v2/public/contacts/{id}` — update contact fields
- `PUT /v2/public/contacts/{id}/tags` — add tags (must use `{name: "tag"}` object format)
- `PUT /v2/public/contacts/{id}/action/note` — add note (field is `details`, not `note`)

### Known Limitations
- People-search sites frequently trigger captcha/bot-blocking (ThatsThem, FastPeopleSearch Cloudflare, TruePeopleSearch detail pages)
- Collier County Property Appraiser uses HTML framesets that block automated scraping
- Apollo works best with business emails; personal Gmail/Yahoo often miss

### File Locations
- Skill config: `/tmp/lead-enrichment/config/`
- Enrichment logs: `/tmp/lead-enrichment/logs/enrichment_log.json`
- Enrichment state: `/tmp/lead-enrichment/state/enrichment_state.json`
- Field mapping reference: skill's `config/field_mapping.json`
- Troubleshooting guide: skill's `references/troubleshooting.md`

## Progress Log
| Date | Update |
| ---- | ------ |
| 2026-03-23 | Project initiated — customized skill from Jesse's template, swapped API credentials, ran first live enrichment on Kelley Watson, created vault contact card, created project folder |
| 2026-03-23 | Architecture decision: build separate `boldtrail-vault-sync` skill. Design brief written at [[20260323_VaultSyncSkill_DesignBrief]] with full scope, data mapping, merge strategy, and open questions |
| 2026-03-24 | Built vault-sync skill v2 — added Compliance, Spouse, Social Profiles, Last Activity, BoldTrail Search Behavior sections. Upgraded all 4 client templates. Packaged as `boldtrail-vault-sync.skill` |
| 2026-03-24 | Tested vault-sync on 3 contacts: Kelley Watson (existing card comparison), Karl Heinzelmann (rich data — 5-star, TCPA, 4 phones, call notes), Scott Coleman (thin FB lead — search behavior only). All cards filed to `02-Real-Estate/Clients/Buyers/` |
| 2026-03-24 | Created Client Brief system — quick-reference phone-friendly briefs with compliance check, talking points, and draft reply. Template in `06-Templates/`, briefs save to `05-Resources/Client-Briefs/` |

## Resources & Links
- [[Watson_Kelley]] — First enriched contact card
- [[Heinzelmann_Karl]] — Vault-sync test #2 (rich data, dual buyer/renter)
- [[Coleman_Scott]] — Vault-sync test #3 (thin FB lead)
- [[20260323_VaultSyncSkill_DesignBrief]] — Vault-sync skill design brief
- [[20260324_Session_VaultSync_Build]] — Session notes for vault-sync build and testing
- [[20260327_StatusMigrationImpactReport]] — Status migration impact report (New Lead → Prospect, 149 contacts)
- [[Active Work Ledger]] — Vault work tracker
- [[Decision Log]] — Architecture and template decisions
- BoldTrail API Docs: https://apidocs.kvcore.com/

## Notes
- The packaged `.skill` file was saved to the vault root as `lead-enrichment.skill` for installation
- Enrichment runs take ~3 minutes per contact due to waterfall source checking and bot-blocking delays
- Snowbird detection is a high-value signal for SW Florida real estate — Kelley Watson's first enrichment immediately flagged this pattern (IL history + Clearwater voter registration + Naples current address)
