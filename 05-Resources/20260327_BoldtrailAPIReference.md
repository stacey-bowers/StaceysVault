---
tags: [boldtrail, research, reference, api, kvcore, technical-reference, crm, platform-documentation]
created: 2026-03-27
type: research
status: active
project: "0402-BoldTrailClientStatus"
---

# BoldTrail Platform Learnings & Technical Reference

## Source
Session: 2026-03-27 — New Lead → Prospect batch migration (149 contacts)
Project: 0402-BoldTrailClientStatus

---

## kvCORE API (BoldTrail's Backend)

### Authentication
- Base URL: `https://api.kvcore.com/v2/public/`
- Auth: Bearer token in header — `Authorization: Bearer <token>`
- Token stored at: `.claude/skills/lead-enrichment/config/boldtrail_credentials.json`
- Current token expires: 2027-03-21
- Permissions on our token: GET/PUT contacts, tags, notes, calls. No campaign endpoints exist in the public API.

### Status Codes (Verified 2026-03-27)
The API uses integer codes, not text labels. There is no public documentation for this mapping — we had to reverse-engineer it by cross-referencing UI filter counts with API data.

| API Code | UI Label | Meaning |
|----------|----------|---------|
| 0 | New Lead | Just registered or imported |
| 1 | Client | Actively working with agent |
| 2 | Closed | Deal completed |
| 3 | Sphere | Personal contacts, SOI |
| 4 | Active Lead | Actively engaging with website |
| 5 | Contract | Under contract |
| 6 | Archived | Removed from active pipeline |
| 7 | Prospect | Initial contact made, qualifying |

Note: The UI button label says "ACTIVE" but the status badge reads "ACTIVE LEAD" and the API filter URL uses `status[]=Active Lead` for code 4.

### Contact Endpoints

**List contacts:**
`GET /contacts?per_page=500&page=1`
- Returns ALL contacts for the account — query params like `status=0` and `agent_id=` are silently ignored (they don't filter server-side)
- Must filter client-side by checking `c.status` and `c.assigned_agent_id`
- The `total` field in the response reflects total contacts, not filtered count
- List response includes: `id`, `status`, `assigned_agent_id`, `firstname`, `lastname`, `email`, `phone`, `leadtype`, `hashtags`, `allPhones`, `created`, `lastVisit`, `source`, `system_source`
- List response does NOT include: `owner` object (use `assigned_agent_id` instead), full address details, qualifications
- Many contacts return empty `firstname`/`lastname` in the list endpoint — the detail endpoint (`GET /contact/{id}`) returns the actual names

**Search contacts:**
`GET /contacts/search?q=Name`
- Returns richer data per contact than the list endpoint
- Includes `owner.user_id`, `contactOwner`, full `extra` fields (address, birthday), `tasks`, `permissions`

**Update contact:**
`PUT /contact/{id}` (singular — no 's')
- Body: `{ status: 7 }` — just the fields to change
- Returns the full updated contact object
- Status change is immediate in the UI
- No timeline event is created — the change is "silent" in BoldTrail's activity log
- No automatic campaign enrollment/unenrollment is triggered

**Add note:**
`PUT /contact/{id}/action/note`
- Body: `{ details: "note text" }` — field name is `details`, NOT `note`
- Returns `{ action_id, date, action_owner_user_id, title, details }`

**Add tags:**
`PUT /contact/{id}/tags`
- Body: `{ tags: [{ name: "tag-name" }] }` — must be array of objects with `name` key
- NOT `{ tags: ["tag-name"] }` — that format fails with validation error
- Returns the full tag list for the contact (existing + new)
- Tags are additive — existing tags are preserved

### API Gotchas
- No campaign/drip endpoints exist in the public API at all
- No way to read or manage Smart Campaign enrollment via API
- No BoldTrail/kvCORE MCP exists on the Claude MCP registry (confirmed 2026-03-27)
- Rate limiting: We successfully ran 5 concurrent PUT requests with 500ms delay between batches without hitting rate limits. 148 contacts processed in ~30 seconds.

---

## BoldTrail UI (Chrome Navigation)

### URLs
- Platform: `https://app.boldtrail.com/` (NOT platform.boldtrail.com, NOT app.kvcore.com)
- Contact card: `https://app.boldtrail.com/contacts/{id}` (with 's' — `/contact/{id}` returns 404)
- Contact list filtered: `https://app.boldtrail.com/contacts?status%5B%5D=New%20Lead&agents%5B%5D=1912313`
- Smart Campaigns: `https://app.boldtrail.com/marketing-autopilot/campaigns`

### Contact Card Layout
Three tabs: **Contact Info**, **Timeline**, **Actions**

**Contact Info tab:**
- Name, status badge, phone, email, address
- Qualifications (Timeline, Pre-Approved, Has a home to sell, Has an Agent)
- Hashtags
- Web Activity (Search Criteria, Average Price, Last Visit, Registered, Source, System Source)
- Ownership (Assigned To, Assigned Lender, Shared With)

**Timeline tab:**
- Activity feed with date stamps
- Filter dropdown: All Activity, All Inbound, All Outbound, Appointments, Calls, Notes, Properties - All/Favorited/Viewed, Questions, Showing Requests
- No "Campaigns" filter option
- API status changes do NOT appear in the timeline

**Actions tab (top to bottom):**
- Quick actions: Calls, Texts, Emails count, Notes, Add Task, More
- Tasks
- Appointments
- Search Alerts (with frequency and last-sent date)
- **Active Campaigns** (this is the per-contact campaign enrollment section)
- Market Reports
- Present
- Listing Valuation
- Seller Report
- CoreHome
- Files
- Transactions

### Dashboard Metrics (contact list header)
- Agent Total Score (percentage)
- Awaiting Response (count)
- New & Needs Contact (count)
- Have Past Due Tasks (count)
- Not on Campaign (count)

---

## Smart Campaigns — Critical Architecture Discovery

This was the most important finding of the session.

### How Smart Campaigns Actually Work
BoldTrail's Smart Campaigns operate at the **system level** — they fire based on status-matching triggers, NOT per-contact enrollment. When a campaign has a trigger like "Status IS New Lead," it doesn't individually enroll each New Lead contact. Instead, at its scheduled send time, it queries for all contacts matching the trigger criteria and sends to them.

### Evidence
- Three separate contacts (Garry Moore, Michael Michael, David Straub) all had **empty** "Active Campaigns" sections on their contact cards despite being New Leads and the B-E New Leads 2026 campaign being active with a "Status IS New Lead" trigger
- Changing David Straub's status from New Lead to Prospect did NOT trigger any campaign enrollment/unenrollment events in his timeline
- The "Active Campaigns" section on a contact card shows only **manually-enrolled** drip campaigns, not system-level Smart Campaign matches

### Implications
- Changing a contact's status doesn't "remove" them from a Smart Campaign — it just means they stop matching the trigger criteria at the next scheduled send
- There's no API or UI action needed to "unenroll" contacts from Smart Campaigns during status migrations
- The "Not on Campaign" dashboard metric likely counts contacts not matching ANY Smart Campaign trigger AND not manually enrolled in any campaign
- Smart Campaign impact assessment should focus on trigger criteria matching, not per-contact enrollment records

### Campaign Registry (68 total as of 2026-03-27)
- Most SYSTEM campaigns are toggled OFF
- Active campaigns are mostly manual-trigger or hashtag-triggered
- Only one active status-triggered campaign for New Leads: **B-E New Leads 2026**
- No active Prospect-triggered campaigns exist (SYSTEM Prospect Buyer/Seller are OFF)
- Full registry documented in: `0402-BoldTrailClientStatus/reports/impact-report-2026-03-27.md`
- Full registry also in: `0402-BoldTrailClientStatus/boldtrail-client-status-manager/references/campaign_registry.md`

---

## Chrome MCP Patterns for BoldTrail

### Working with the kvCORE API via Chrome
Since the Cowork sandbox blocks all direct HTTP, every API call must go through `mcp__Claude_in_Chrome__javascript_tool`.

**Critical pattern — use document.title for return values:**
```javascript
fetch('https://api.kvcore.com/v2/public/contacts?per_page=500&page=1', {
  headers: {
    'Authorization': 'Bearer <TOKEN>',
    'Content-Type': 'application/json'
  }
}).then(r => r.json()).then(data => {
  document.title = JSON.stringify(result);
})
```

The async IIFE pattern `(async () => { ... })()` returns `undefined` from the Chrome JS tool. Writing to `document.title` is the reliable workaround.

**Token must be inline:** Window variables clear on navigation, so the full token must be embedded as a string literal in every fetch call. If you store it in a window variable, it only survives until the next page navigation.

**chrome://newtab blocks JS execution:** Even `1+1` times out on newtab. Always navigate to a real page (e.g., `https://example.com`) before running any JS.

### Batch Processing Pattern
For bulk operations, use a self-contained function that:
1. Stores IDs in a window variable
2. Processes in batches of 5 with 500ms delay
3. Writes progress to `document.title` (e.g., "MIGRATING: 50/148")
4. Writes final results to `document.title` as JSON

This pattern successfully processed 148 status changes, 148 tag additions, and 148 note additions without failures or rate limiting.

### Chrome Extension Disconnects
The Chrome extension's background service worker gets suspended by Chrome after ~30 seconds of inactivity. Keep browser interactions continuous to prevent disconnects. If disconnected, user needs to click "Connect" in the extension dialog.

---

## Stacey's Contact Data Profile

### Stacey's Agent ID: 1912313
### Account ID: 13071

### Contact Volume (as of 2026-03-27, post-migration)
| Status | Count |
|--------|-------|
| New Lead | 0 (was 149) |
| Client | 2 |
| Closed | 3 |
| Sphere | 8 |
| Active Lead | 108 |
| Prospect | 234 (was 85) |
| **Total** | **355** |

### Contact Characteristics
- Predominantly "buyer" type
- Sources: REFINDLY (imported), BT_MRKTCENTRAL_VISITORS, DIRECT
- Many contacts have no first/last name — only email addresses
- Phone coverage: ~60-70% have a cell phone
- Geographic focus: Southwest Florida (Naples, Fort Myers, Cape Coral area)
- Many contacts had been "New Lead" since January 2025 (14+ months stale)

---

## Blocked Resources / Egress Issues
The Cowork sandbox egress proxy blocks many domains. These all failed during this session:
- studylib.net
- help.insiderealestate.com
- github.com
- apidocs.kvcore.com
- Various real estate documentation sites

Workaround: Use Chrome MCP to navigate to pages and extract information via `get_page_text` or `javascript_tool` instead of trying to fetch from the sandbox.

---

## File Locations

| What | Where |
|------|-------|
| Skill (in progress) | `0402-BoldTrailClientStatus/boldtrail-client-status-manager/SKILL.md` |
| Status definitions | `0402-BoldTrailClientStatus/boldtrail-client-status-manager/references/status_definitions.md` |
| Campaign registry | `0402-BoldTrailClientStatus/boldtrail-client-status-manager/references/campaign_registry.md` |
| Migration impact report | `0402-BoldTrailClientStatus/reports/impact-report-2026-03-27.md` |
| Status change audit log | `0402-BoldTrailClientStatus/boldtrail-client-status-manager/logs/status_change_log.json` |
| API credentials | `.claude/skills/lead-enrichment/config/boldtrail_credentials.json` |
