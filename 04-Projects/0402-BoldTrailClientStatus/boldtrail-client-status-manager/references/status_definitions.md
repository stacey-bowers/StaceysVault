# BoldTrail Status Definitions — Domain Realty Group

## API Status Code Mapping (Verified 2026-03-27)

| API Code | BoldTrail UI Label | Current Count |
|----------|-------------------|---------------|
| 0 | New Lead | 149 |
| 1 | Client | 2 |
| 2 | Closed | 3 |
| 3 | Sphere | 8 |
| 4 | Active Lead | 108 |
| 5 | Contract | 0 (not seen in data) |
| 6 | Archived | 0 (not seen in data) |
| 7 | Prospect | 85 |

> **Note:** The UI button says "ACTIVE" but the status badge reads "ACTIVE LEAD".
> The API filter URL uses `status[]=Active Lead` for code 4.
> Total contacts: 355 (as of 2026-03-27).

---

## Stacey's Status Workflow

These definitions reflect how Stacey uses statuses at Domain Realty Group,
which may differ from BoldTrail's defaults.

### New Lead
- **Meaning:** Contact just entered the system (web registration, import,
  referral, manual add). No human contact has been made.
- **Expected campaigns:** Default new-lead drip (welcome sequence, property
  alerts setup). These are typically BoldTrail's out-of-the-box smart campaigns.
- **Transition trigger:** First meaningful contact (call, email reply, text
  exchange) → move to Prospect.
- **Red flag if:** Contact has been "New Lead" for 30+ days — likely
  mislabeled or fell through the cracks.

### Prospect
- **Meaning:** Initial contact made. Stacey is qualifying — learning needs,
  timeline, budget, motivation.
- **Expected campaigns:** Prospect nurture drip (market updates, neighborhood
  guides, buyer/seller tips). More personalized than new-lead sequence.
- **Transition trigger:** Active engagement begins (showing scheduled,
  listing appointment set) → move to Active.
- **Red flag if:** No activity in 60+ days — may need to go back to
  nurture or mark inactive.

### Active
- **Meaning:** Actively working together. Showings happening, offers being
  made, listing is live.
- **Expected campaigns:** Minimal automated campaigns — Stacey is doing
  direct, high-touch communication. Maybe transactional updates only.
- **Transition trigger:** Offer accepted → Under Contract. Goes cold →
  back to Prospect or Inactive.

### Under Contract
- **Meaning:** Deal in progress. Inspection, appraisal, financing,
  closing timeline.
- **Expected campaigns:** Transaction management drip (milestone reminders,
  document checklists, closing countdown). Highly automated.
- **Transition trigger:** Closing → Closed. Falls through → back to Active.

### Closed
- **Meaning:** Deal completed. Client is now in the post-close/sphere
  of influence category.
- **Expected campaigns:** Post-close nurture (anniversary reminders,
  home maintenance tips, referral requests, market updates). Long-term
  relationship maintenance.
- **Transition trigger:** Rarely changes. May reactivate if client wants
  to buy/sell again.

### Inactive
- **Meaning:** Gone cold. No response to outreach, not engaging with
  content, timeline pushed out indefinitely.
- **Expected campaigns:** Low-frequency re-engagement drip (quarterly
  check-in, market snapshot). Not aggressive.
- **Transition trigger:** Re-engagement (responds to email, visits
  website, calls back) → Prospect or Active.

### Trash
- **Meaning:** Junk lead, spam, wrong number, not a real person.
- **Expected campaigns:** None. Remove from all campaigns.
- **Transition trigger:** Should not transition. If mistakenly trashed,
  restore to appropriate status.

---

## Status Change Impact Matrix

This matrix shows what typically happens to campaigns when moving between
statuses. "Auto" means BoldTrail's smart campaigns handle it. "Manual"
means Stacey needs to take action.

| From → To | Campaign Impact | Action Required |
|-----------|----------------|-----------------|
| New Lead → Prospect | New-lead drip stops (auto). Prospect nurture should start. | Check if prospect drip auto-enrolls. If not, manually enroll. |
| New Lead → Active | New-lead drip stops. No auto prospect drip. | Manually set up active client communications. |
| Prospect → Active | Prospect nurture stops (auto). | Switch to direct communication. Pause automations if needed. |
| Active → Under Contract | | Enroll in transaction management drip. |
| Under Contract → Closed | Transaction drip stops. | Enroll in post-close nurture. |
| Any → Inactive | Current campaigns should stop. | Enroll in re-engagement drip. |
| Inactive → Prospect | Re-engagement drip stops. | Enroll in prospect nurture. |

> **These are Stacey's intended workflows.** Actual BoldTrail behavior
> may differ depending on how smart campaigns are configured. Always
> verify via Chrome UI audit before bulk changes.
