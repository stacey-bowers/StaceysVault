# BoldTrail Campaign Registry — Domain Realty Group

## Purpose

This file tracks all known campaigns, drips, and smart campaigns in
Stacey's BoldTrail instance. It is updated each time a Chrome UI audit
reveals campaign details. Think of it as the skill's "memory" of what
campaigns exist and how they work.

## How to Update This File

After any Chrome UI audit of BoldTrail's campaign pages, update the
relevant sections below. Include:
- Campaign name (exact as shown in BoldTrail)
- Type: smart campaign, drip, or manual
- Trigger: what causes enrollment (status change, tag, manual, etc.)
- Status: active, paused, or archived
- Description: what the campaign does
- Date last verified via Chrome

---

## Smart Campaigns

> Smart campaigns auto-enroll contacts based on rules (status, tags, etc.)

| Campaign Name | Trigger | Status | Description | Last Verified |
|--------------|---------|--------|-------------|---------------|
| *(to be populated via Chrome audit)* | | | | |

---

## Drip Campaigns

> Drip campaigns send a sequence of emails/texts on a schedule

| Campaign Name | Enrollment Method | Status | Description | Last Verified |
|--------------|-------------------|--------|-------------|---------------|
| *(to be populated via Chrome audit)* | | | | |

---

## Manual Campaigns / One-Off

> Campaigns where Stacey manually adds contacts

| Campaign Name | Purpose | Status | Last Verified |
|--------------|---------|--------|---------------|
| *(to be populated via Chrome audit)* | | | |

---

## Campaign-Status Mapping (Verified 2026-03-27)

| Status | Auto-Triggered Campaigns | Active? |
|--------|--------------------------|---------|
| New Lead (0) | B-E New Leads 2026 (buyer email, 18 touches) | YES |
| New Lead (0) | SYSTEM Default Seller (seller, 18 touches) | NO |
| New Lead (0) | NYC/NYCAds campaigns (require #NYCAds tag) | NO |
| Prospect (7) | SYSTEM Prospect Buyer (13 touches) | NO |
| Prospect (7) | SYSTEM Prospect Seller (13 touches) | NO |
| Active Lead (4) | SYSTEM Active Buyer (1 touch) | NO |
| Active Lead (4) | SYSTEM Active Seller (1 touch) | NO |
| Closed (2) | SYSTEM Closed (21 touches) x2 | NO |
| Sphere (3) | SYSTEM Sphere Homeowner (17 touches) x2 | NO |
| Both NL + Prospect | B-E Bad Phone Number 2026 (+ #BadNumber2026) | YES |
| Both NL + Prospect | Bad Number DRG Made (+ #BadPhoneNumber) | YES |
| Both NL + Prospect | B/S-T Blocked or No Email 2026 (+ #NOTRIGGER2) | YES |
| Both NL + Prospect | Not Interested Response 2026 (+ #NotInterested) | YES |

> **Key insight:** Most SYSTEM campaigns are toggled OFF. The only active
> status-triggered campaign for New Leads is B-E New Leads 2026 (buyer email).
> There are NO active Prospect-triggered campaigns. Most custom campaigns
> are manual-start only (triggered by hashtags or manual enrollment).

---

## Audit Log

| Date | Auditor | What Was Checked | Findings |
|------|---------|-----------------|----------|
| 2026-03-27 | Claude (Cowork) | All 68 campaigns via Marketing > Smart Campaigns | Full campaign inventory captured. Status codes mapped. See impact-report-2026-03-27.md |
