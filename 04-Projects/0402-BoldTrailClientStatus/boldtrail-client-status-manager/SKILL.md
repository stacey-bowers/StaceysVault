---
tags: [reference, real-estate, pipeline]
created: 2026-03-24
type: reference
status: active
name: boldtrail-client-status-manager
description: >
  Proactively manages and updates contact statuses in BoldTrail CRM (kvCORE).
  Handles bulk status transitions (e.g., New Lead to Prospect), audits
  campaign/drip impact before making changes, and generates action plans for
  re-enrollment. Uses the kvCORE API for contact reads/writes and Chrome UI
  for campaign/drip data that the API doesn't expose.

  ALWAYS use when Stacey says: "update status", "change status",
  "move leads to [status]", "fix client statuses", "status cleanup",
  "relabel contacts", "bulk status change", "new leads to prospects",
  "audit campaigns before status change", "what campaigns will break",
  "campaign impact", "drip impact", "status migration", "client status
  report", or any variation of wanting to change contact statuses in
  BoldTrail. Also use when Stacey asks about which contacts are in a
  given status, what smart campaigns are active, or wants a pre-change
  impact assessment. Also trigger when discussing BoldTrail campaign
  management, drip enrollment, or smart campaign rules, even if the
  user doesn't explicitly mention "status".
---

# BoldTrail Client Status Manager

## What This Skill Does

Manages contact status transitions in BoldTrail with full campaign impact
awareness. Every status change in BoldTrail can trigger or cancel smart
campaigns, drip sequences, and automated workflows. This skill ensures
Stacey never makes a bulk status change blind — it always shows what will
break and what needs to be rebuilt.

Three modes of operation:

1. **Recon Mode** — Audit only. Pull contacts in a given status, check
   what campaigns/drips they're on, and report back without changing
   anything. Use this to understand the landscape before acting.

2. **Migration Mode** — Full status transition. Runs recon first, presents
   an impact report for Stacey's approval, then executes the status change
   and generates an action plan for campaign re-enrollment.

3. **Monitor Mode** — Ongoing status hygiene. Check for contacts whose
   status doesn't match their actual activity level (e.g., "New Lead"
   who has been in the system for 90+ days with activity).

---

## Before You Start

Read these files:

- `{skills-dir}/lead-enrichment/config/boldtrail_credentials.json` —
  API token (shared with lead-enrichment and vault-sync skills)
- `references/status_definitions.md` — defines what each BoldTrail
  status means in Stacey's workflow and which campaigns are expected
  for each status
- `references/campaign_registry.md` — known campaigns, their triggers,
  and enrollment rules (updated as we learn more from Chrome audits)

---

## Critical Infrastructure — API Calls via Chrome

The Cowork sandbox blocks all direct HTTP. Every BoldTrail API call must
go through Chrome JavaScript:

- Use `mcp__Claude_in_Chrome__javascript_tool` for all API calls
- `curl`, `wget`, Python `requests`, `WebFetch` are ALL BLOCKED
- Embed the full Bearer token as a string literal in every JS call
- Never store tokens in `window` variables (cleared on navigation)

```javascript
// Standard API call pattern
(async () => {
  const token = '<FULL_TOKEN_HERE>';
  const res = await fetch('https://api.kvcore.com/v2/public/<endpoint>', {
    method: 'GET', // or PUT
    headers: {
      'Authorization': 'Bearer ' + token,
      'Content-Type': 'application/json'
    }
  });
  return JSON.stringify(await res.json());
})()
```

### Key API Endpoints

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/contacts?per_page=500&page=N` | GET | Page through all contacts |
| `/contacts/search?q=keyword` | GET | Search by email, name, phone |
| `/contact/{id}` | GET | Full contact detail |
| `/contact/{id}` | PUT | Update contact fields (including status) |
| `/contact/{id}/tags` | GET | Read contact tags |
| `/contact/{id}/tags` | PUT | Add tags (must be `{ tags: [{ name: "tag" }] }`) |
| `/contact/{id}/action/note` | GET | Read existing notes |
| `/contact/{id}/action/note` | PUT | Add note (field is `details`, not `note`) |

### What the API CAN'T Do

The kvCORE public API does NOT expose:
- Campaign/drip enrollment data
- Smart campaign definitions or triggers
- Campaign enrollment/unenrollment actions
- Automated workflow rules

For campaign data, we use Chrome to navigate the BoldTrail UI directly.

---

## Phase 1 — Recon (Always Runs First)

### Step 1: Pull Contacts by Status

Pull all contacts from BoldTrail and filter by the source status. The API
doesn't support status filtering directly, so page through all contacts
and filter client-side.

```javascript
// Pull contacts page by page — repeat incrementing page until data is empty
(async () => {
  const token = '<TOKEN>';
  const res = await fetch('https://api.kvcore.com/v2/public/contacts?per_page=500&page=1', {
    headers: { 'Authorization': 'Bearer ' + token, 'Content-Type': 'application/json' }
  });
  const data = await res.json();
  // Filter for target status
  const matches = data.data.filter(c =>
    (c.status || '').toLowerCase() === '<target_status>'.toLowerCase()
  );
  JSON.stringify({
    total_contacts: data.total,
    page: data.page,
    matches_this_page: matches.length,
    contacts: matches.map(c => ({
      id: c.id,
      name: (c.first_name || '') + ' ' + (c.last_name || ''),
      email: c.email,
      status: c.status,
      created_at: c.created_at,
      updated_at: c.updated_at,
      source: c.source,
      assign_type: c.assign_type
    }))
  });
})()
```

Continue paging until you've retrieved all contacts. Keep a running list
of matches.

**Important:** The API returns contacts sorted by ID ascending — sort
params are ignored. New leads will have the highest IDs.

### Step 2: Build the Contact Inventory

For each matched contact, compile:
- Contact ID, name, email, phone
- Current status
- Created date (how long they've been in this status)
- Source (where the lead came from)
- Tags (via GET `/contact/{id}/tags`)
- Assign type (buyer/seller/tenant/landlord)
- Last activity date

Save this as a structured inventory — it becomes the foundation for the
impact report.

### Step 3: Audit Campaign Impact via Chrome UI

This is the critical step the API can't handle. Navigate to BoldTrail's
Smart Campaigns section to understand what campaigns are tied to the
source and destination statuses.

**Strategy for 75+ contacts — work top-down, not contact-by-contact:**

1. **System-level audit first:** Navigate to BoldTrail's Smart Campaigns
   management page. Identify:
   - Which campaigns trigger on the SOURCE status (these will be disrupted)
   - Which campaigns trigger on the DESTINATION status (these will auto-enroll)
   - Any campaigns that trigger on status *change* events

2. **Spot-check sample contacts:** Pick 5-10 contacts from the inventory
   and navigate to their individual profile pages in BoldTrail. Look at:
   - Current campaign/drip enrollments
   - Activity history (emails sent, opened, clicked)
   - Any manual campaign assignments that wouldn't show in system rules

3. **Cross-reference:** Compare what the system rules say should happen
   with what you actually see on individual contacts. Document any
   discrepancies.

#### Chrome Navigation for Campaign Audit

Navigate to the Smart Campaigns page:
```
https://platform.boldtrail.com/smart-campaigns
```
or from the dashboard:
Dashboard → Marketing → Smart Campaigns

For individual contact campaign history:
```
https://platform.boldtrail.com/contact/{id}
```
Look for the "Campaigns" or "Drips" tab/section on the contact detail page.

**Reading campaign data from the UI:** Use `read_page` or `get_page_text`
to extract campaign names, statuses (active/paused/completed), enrollment
dates, and trigger conditions.

### Step 4: Generate the Impact Report

Compile everything into a structured report. Save to the project folder:
`0402-BoldTrailClientStatus/reports/`

The impact report must include:

**Section 1 — Summary**
- Total contacts affected
- Source status → Destination status
- Date of assessment

**Section 2 — Campaign Impact**
- Campaigns that will AUTO-STOP when status changes
  - Campaign name, type (smart/drip/manual), contacts enrolled
- Campaigns that will AUTO-START at new status
  - Campaign name, type, what it does
- Manual campaigns that need human action
  - Campaign name, what needs to happen

**Section 3 — Contact Roster**
- Full list of contacts being moved
- Per-contact: name, email, current campaigns, flags/concerns

**Section 4 — Action Plan**
- Ordered list of things Stacey needs to do after the status change
- Which contacts need manual campaign re-enrollment
- Which campaigns to pause/start/modify
- Suggested timeline

**Present this to Stacey and WAIT for approval before proceeding.**

---

## Phase 2 — Execution (Only After Stacey Approves)

### Step 5: Execute the Status Change

Update each contact's status via the API:

```javascript
(async () => {
  const token = '<TOKEN>';
  const res = await fetch('https://api.kvcore.com/v2/public/contact/<ID>', {
    method: 'PUT',
    headers: {
      'Authorization': 'Bearer ' + token,
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ status: '<NEW_STATUS>' })
  });
  return JSON.stringify(await res.json());
})()
```

**Processing order:**
- Work in batches of 10-20 contacts
- Log each update result (success/fail)
- If any fail, stop and report before continuing
- Tag each changed contact: `status-migrated-YYYY-MM-DD`
- Add a note to each contact documenting the change:
  `"Status changed from [old] to [new] on YYYY-MM-DD via bulk migration.
  Previous campaigns: [list]. See impact report for action items."`

### Step 6: Post-Change Verification

After all updates complete:

1. Re-pull the updated contacts to confirm status changed
2. Spot-check 3-5 contacts in Chrome UI to verify campaign changes
   happened as expected
3. Document any surprises

### Step 7: Generate Final Action Plan

Write the definitive action plan to:
`0402-BoldTrailClientStatus/reports/action-plan-YYYY-MM-DD.md`

This is Stacey's checklist for campaign re-enrollment and follow-up.
Format as an actionable markdown document with checkboxes.

---

## Phase 3 — Monitor Mode (Optional / Ongoing)

### Status Hygiene Checks

When triggered for monitoring (not migration), look for:

- **Stale New Leads:** Contacts with "New Lead" status but
  `created_at` > 30 days ago — likely need reclassification
- **Ghost Prospects:** "Prospect" status but no activity in 60+ days
- **Mismatched Types:** Status doesn't match assign_type or tags
  (e.g., tagged "seller" but status is "buyer lead")

Report findings without making changes — Stacey decides what to act on.

---

## BoldTrail Status Values (Verified 2026-03-27)

The API uses numeric status codes. Here is the confirmed mapping:

| API Code | UI Label | Meaning |
|----------|----------|---------|
| 0 | New Lead | Just registered/imported, no contact made |
| 1 | Client | Actively working with agent on a deal |
| 2 | Closed | Deal completed |
| 3 | Sphere | Personal contacts, SOI, past relationships |
| 4 | Active Lead | Actively engaging with website/content |
| 5 | Contract | Under contract (not yet seen in data) |
| 6 | Archived | Removed from active pipeline |
| 7 | Prospect | Initial contact made, qualifying |

> **Important:** When reading contacts via GET, the `status` field returns
> an integer (0, 1, 2, etc.). When writing via PUT, use the integer value:
> `{ "status": 7 }` to set a contact to Prospect.
> Always verify the PUT format works by testing on a single contact first.

---

## Safety Rules

1. **Never change statuses without presenting the impact report first.**
   Stacey must approve before any writes happen.

2. **Always tag migrated contacts** with `status-migrated-YYYY-MM-DD`
   so changes can be traced and potentially reversed.

3. **Always add a note** to each contact documenting the status change,
   the reason, and any campaign impacts.

4. **Log every write** to `logs/status_change_log.json` for audit trail.

5. **If the API returns errors on more than 3 consecutive contacts,**
   stop and investigate. Don't keep hammering a broken endpoint.

6. **Campaign re-enrollment is MANUAL.** This skill documents what needs
   to happen but does not auto-enroll contacts in campaigns. Stacey or
   the BoldTrail UI handles actual campaign enrollment.

7. **Preserve the credential file.** Token lives in the lead-enrichment
   skill's config — read it, never modify it.

---

## API Gotchas (Same as Lead Enrichment)

| Issue | Wrong | Correct |
|-------|-------|---------|
| Tag format | `{ "tags": ["tag-name"] }` | `{ "tags": [{ "name": "tag-name" }] }` |
| Note field | `{ "note": "text" }` | `{ "details": "text" }` |
| Token storage | `window._token = '...'` | Inline string literal every call |
| Phone format | `2395550100` | `(239) 555-0100` |
| API sort | `sort=-created_at` | Ignored — sort by ID asc only |
| Status field write | `{ "lead_status": "..." }` | `{ "status": "..." }` (verify via GET first) |

---

## Output Files

All outputs go to the project folder: `0402-BoldTrailClientStatus/`

```
0402-BoldTrailClientStatus/
  reports/
    impact-report-YYYY-MM-DD.md      ← Pre-change impact assessment
    action-plan-YYYY-MM-DD.md         ← Post-change task list
    status-hygiene-YYYY-MM-DD.md      ← Monitor mode findings
  logs/
    status_change_log.json             ← Append-only audit trail
  data/
    contact-inventory-YYYY-MM-DD.json  ← Snapshot of contacts before change
```

---

## Interaction with Other Skills

- **lead-enrichment** — Shares the API token. If contacts being migrated
  haven't been enriched yet, suggest running enrichment first.
- **boldtrail-vault-sync** — After status changes, vault cards may need
  updating. Suggest running vault-sync for affected contacts.
- **obsidian-daily-note-manager** — Major status migrations should be
  noted in the daily note as a significant CRM activity.
