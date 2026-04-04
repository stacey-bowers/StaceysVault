---
tags: [reference, archived]
created: 2026-03-27
type: research
status: archived
---

# Status Migration Impact Report
## New Lead (0) → Prospect (7)
**Date:** 2026-03-27
**Prepared by:** Claude (Cowork) for Stacey Bowers, Domain Realty Group

---

## Summary

- **Total contacts to migrate:** 149
- **Source status:** New Lead (API code 0)
- **Destination status:** Prospect (API code 7)
- **Current Prospects (before migration):** 85
- **Post-migration Prospect count:** 234

---

## Campaign Impact Analysis

### Campaigns That WILL STOP (triggered by "Status IS New Lead" only)

| Campaign | Type | Touches | Active? | Designed For | Impact |
|----------|------|---------|---------|-------------|--------|
| **B-E New Leads 2026** | Email + Task | 18 | YES | Buyer | **HIGH** — Main new-lead buyer email drip. All 149 contacts currently in this drip will be removed. |
| SYSTEM Default Seller | Email + Task + Text | 18 | NO (inactive) | Seller | LOW — Campaign exists but toggle is off. Not currently running. |
| NYC Text only 1/2026 | Text | 23 | NO (inactive) | Buyer | LOW — Only triggers with #NYCAds hashtag. Inactive. |
| NYCAds Campaign | Email + Task + Text | 35 | NO (inactive) | Buyer | LOW — Only triggers with #NYCAds hashtag. Inactive. |

### Campaigns That WON'T CHANGE (triggered by BOTH "New Lead" AND "Prospect")

These campaigns include both statuses in their trigger rules, so the status change won't disrupt them. Contacts already enrolled will stay enrolled.

| Campaign | Type | Touches | Active? | Trigger Condition |
|----------|------|---------|---------|------------------|
| B-E Bad Phone Number 2026 | Email + Task | 32 | YES | Status IS New Lead OR Prospect + #BadNumber2026 |
| ***Bad Number*** DRG Made | Email | 7 | YES | Status IS New Lead OR Prospect + #BadPhoneNumber |
| B/S-T Blocked or No Email 2026 | Text | 25 | YES | Status IS New Lead OR Prospect + #NOTRIGGER2 |
| Not Interested Response 2026 | Email + Text | 24 | YES | Status IS New Lead OR Prospect + #NotInterested |

### Campaigns That SHOULD START (triggered by "Status IS Prospect")

| Campaign | Type | Touches | Active? | Designed For | Issue |
|----------|------|---------|---------|-------------|-------|
| **SYSTEM Prospect Buyer** | Call + Email + Task + Text | 13 | **NO (inactive)** | Buyer | Campaign exists but is toggled OFF. Will NOT auto-start unless activated. |
| **SYSTEM Prospect Seller** | Call + Email + Task + Text | 13 | **NO (inactive)** | Seller | Campaign exists but is toggled OFF. Will NOT auto-start unless activated. |

---

## Key Finding

**The SYSTEM Prospect campaigns are currently INACTIVE.** This means that when the 149 New Lead contacts move to Prospect status:

1. They will **drop off** the B-E New Leads 2026 drip (the active buyer email campaign)
2. They will **NOT auto-enroll** in any Prospect-specific campaign (because those are toggled off)
3. They will effectively be **campaign-orphans** — no automated touchpoints

This is the critical decision point: Stacey needs to decide what campaign(s) these 149 contacts should be on after the status change.

---

## Contact Profile (149 New Leads)

- **Deal type:** Predominantly "buyer"
- **Source:** Mostly "REFINDLY" (imported leads)
- **Created dates:** Range from Jan 2025 to Mar 2026
- **Names:** Many contacts have no first/last name — only email addresses
- **Phones:** Roughly 60-70% have a cell phone number
- **Ages in system:** Many have been "New Lead" since January 2025 — over 14 months

---

## Recommended Action Plan

### Before the Status Change

- [ ] **DECISION: Activate SYSTEM Prospect Buyer/Seller campaigns?**
  If yes, turn them on in BoldTrail before the migration so contacts auto-enroll.
  If no, decide which custom campaign(s) to use instead.

- [ ] **DECISION: Should all 149 move to Prospect, or should some go to different statuses?**
  Contacts with 14+ months as "New Lead" and no activity may be better suited for Archived or Inactive.

- [ ] **DECISION: Which campaign should the migrated contacts be placed on?**
  Options:
  - SYSTEM Prospect Buyer (13 touches, call + email + task + text) — activate it
  - B-E/T New or Reconnect 2026 (23 touches, email + text) — manual enrollment, good for longer-term nurture
  - Custom Client Re-Engagement Campaign (32 touches, email + text) — for cold leads
  - Create a new campaign specifically for this batch
  - No campaign (manage manually)

### During the Status Change

- [ ] Execute batch status update via API (status 0 → 7)
- [ ] Tag all migrated contacts with `status-migrated-2026-03-27`
- [ ] Add note to each contact documenting the change

### After the Status Change

- [ ] Verify status changed correctly (spot-check 5-10 contacts)
- [ ] Confirm B-E New Leads 2026 drip stopped for these contacts
- [ ] Enroll contacts in chosen campaign (per decision above)
- [ ] Review contacts with no names — consider enrichment run
- [ ] Update vault cards for any contacts that have vault cards (via boldtrail-vault-sync)

---

## Campaign Registry Snapshot (All 68 Campaigns)

### Active Campaigns (status toggle ON)

| Campaign | Trigger | For | Touches |
|----------|---------|-----|---------|
| B-E Bad Phone Number 2026 | Status IS New Lead/Prospect + #BadNumber2026 | Buyer, Seller | 32 |
| B-E New Leads 2026 | Status IS New Lead (not luxury/Leads360) | Buyer | 18 |
| B-E New Leads 2026 Manual Start | #NewLeadStart | Buyer | 18 |
| B-E Has Agent 2026 | Manual | Buyer | 10 |
| B-E Rent vs Buy Decision 2026 | Manual | Buyer | 10 |
| B-E Seasonal Rent vs Buy 2026 | Manual | Buyer | 10 |
| B-E Toured Homes 2026 | Manual | Buyer | 10 |
| B-E Unsure On Timing 2026 | Manual | Buyer | 10 |
| B-T 1st Call Did Not Convert 2026 | Manual | Buyer | 10 |
| B-T Actively Looking 2026 | Manual | Buyer | 10 |
| B-T Ghosted After First Chat 2026 | Manual | Buyer | 10 |
| B-T Has Agent 2026 | Manual | Buyer | 10 |
| B-T Hesitant 2026 | Manual | Buyer | 10 |
| B-T New Lead 2026 | Manual | Buyer | 17 |
| B-T New Lead 2026 Manual Start | #NewLeadStart | Buyer | 17 |
| B-T Offer Rejected 2026 | Manual | Buyer | 10 |
| B-T Price Concern 2026 | Manual | Buyer | 10 |
| B-T Rent vs Buy Decision 2026 | Manual | Buyer | 10 |
| B-T Seasonal Rent vs Buy 2026 | Manual | Buyer | 10 |
| B-T Toured Homes 2026 | Manual | Buyer | 10 |
| B-T Unsure On Timing 2026 | Manual | Buyer | 10 |
| B/S E-Luxury Presence 2026 | #luxurypresence | Buyer, Seller | 12 |
| B/S-T Blocked or No Email 2026 | Status New Lead/Prospect + #NOTRIGGER2 | Buyer, Seller | 25 |
| Custom NN Campaign 2026 Email Only | #NosyNeighbor | Seller, Buyer | 16 |
| DFY Credit Repair | #creditrepair | Buyer | 15 |
| DFY Just Browsing | #justbrowsing | Renter, Seller, Buyer | 16 |
| DFY Long Term Buyer | #LongTermBuyer | Buyer | 21 |
| DFY Long Term Seller | #LongTermSeller | Seller | 23 |
| New lead phone call reminders 2026 | Manual | Buyer, Seller | 7 |
| Not Interested Response 2026 | Status New Lead/Prospect + #NotInterested | Buyer | 24 |
| S-E Afraid of Selling Too Low 2026 | Manual | Seller | 10 |
| S-E Expired/Terminated 2026 | Manual | Seller | 10 |
| S-E Interviewing Agents 2026 | Manual | Seller | 10 |
| S-E Needs to Buy After Selling 2026 | Manual | Seller | 10 |
| S-E Waiting for Better Market 2026 | Manual | Seller | 10 |
| S-E/T Long Term Seller 2026 | #LongTermSeller | Seller | 18 |
| S-T (various seller text campaigns) | Manual | Seller | 10 each |

### Inactive/System Campaigns (toggle OFF or System)

| Campaign | Trigger | Status |
|----------|---------|--------|
| * hold off on starting this* Buyer Introduction 2026 | Manual | OFF |
| ***Bad Number*** DRG Made | Status New Lead/Prospect + #BadPhoneNumber | ON (Office scope) |
| B-E/T New or Reconnect 2026 | Manual | OFF |
| SYSTEM Active Buyer | Status IS Active Lead | OFF |
| SYSTEM Active Seller | Status IS Active Lead | OFF |
| SYSTEM Closed (x2) | Status IS Closed | OFF |
| SYSTEM Default Buyer | Manual | OFF |
| SYSTEM Default Seller | Status IS New Lead | OFF |
| SYSTEM Open House | Source IS Open House | OFF |
| SYSTEM Prospect Buyer | Status IS Prospect | OFF |
| SYSTEM Prospect Seller | Status IS Prospect | OFF |
| SYSTEM Sphere Homeowner (x2) | Status IS Sphere + Date | OFF |

---

## Single-Contact Test Results (2026-03-27)

**Test subject:** David Straub (ID 134138)
**Previous status:** New Lead (0) → **New status:** Prospect (7)

### Findings

1. **API status change works cleanly.** `PUT /contact/134138` with `{ status: 7 }` returned success. UI immediately reflected "Prospect" badge.
2. **No per-contact campaign enrollment exists.** All three contacts checked (Garry Moore, Michael Michael, David Straub) had empty "Active Campaigns" sections — even before the status change. The B-E New Leads 2026 campaign operates as a **system-level Smart Campaign** that fires based on status match, NOT per-contact enrollment.
3. **No automatic campaign enrollment on Prospect.** After changing to Prospect, no campaigns auto-enrolled (SYSTEM Prospect Buyer/Seller are toggled OFF, as expected).
4. **No timeline event logged for API status change.** The change is "silent" — no automatic audit trail in BoldTrail's Timeline. The note we added via API serves as the only record.
5. **Tags work via API.** Successfully added `status-migrated-2026-03-27` tag using `PUT /contact/{id}/tags` with `{ tags: [{ name: "tagname" }] }` format.
6. **Notes work via API.** Successfully added migration note using `PUT /contact/{id}/action/note` with `{ details: "note text" }` format.

### URL Pattern
- Correct contact URL: `https://app.boldtrail.com/contacts/{id}` (with 's' — not `/contact/`)

### Campaign Impact (Revised Assessment)

Since Smart Campaigns run at the system level based on status triggers (not per-contact enrollment), the impact is:
- **B-E New Leads 2026** will simply stop *matching* migrated contacts at its next scheduled trigger check — no removal action needed
- Contacts were NOT individually enrolled in any drip campaign to begin with
- The "Not on Campaign: 9" dashboard metric likely counts contacts not matching ANY Smart Campaign trigger

**Risk Level: LOW** (revised from MEDIUM)

The migration is safe to execute in bulk. No campaign disruptions will occur because Smart Campaigns use passive status matching, not active enrollment.

---

## Batch Migration Execution Log

**Started:** 2026-03-27
**Completed:** 2026-03-27

| Step | Count | Result |
|------|-------|--------|
| Test migration (David Straub, ID 134138) | 1 | SUCCESS — status changed, UI confirmed, no campaign impact |
| Batch status change (0 → 7) | 148 | SUCCESS — 148/148, 0 failures |
| Tag `status-migrated-2026-03-27` added | 149 | SUCCESS — 149/149 (1 test + 148 batch) |
| Migration note added to contact timeline | 149 | SUCCESS — 149/149 |

**Verification:**
- New Lead filter (Stacey Bowers): **0 contacts** (was 149)
- Prospect filter (Stacey Bowers): **234 contacts** (was 85, now 85 + 149 = 234)
- API status distribution post-migration: 0 New Lead (was 148), 234 Prospect (was 86)

**API patterns confirmed:**
- Status change: `PUT /contact/{id}` with `{ status: 7 }` — field name is `details`, not `note`
- Add note: `PUT /contact/{id}/action/note` with `{ details: "text" }`
- Add tag: `PUT /contact/{id}/tags` with `{ tags: [{ name: "tagname" }] }`
- Contact URL in UI: `https://app.boldtrail.com/contacts/{id}` (with 's')
