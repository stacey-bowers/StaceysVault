# CLAUDE.md — StaceysVault
*Instruction contract for Claude Cowork. Update this file whenever vault conventions change.*
*Version 2.0 — 2026-03-23*

---

## NOTES FOR CLAUDE

- Reference this file at the start of every vault session
- This is Stacey Bowers' vault. She is a licensed real estate agent at Domain Realty Group. Everything in this vault is oriented around her real estate business, clients, deals, and personal life.
- **Documented vault decisions are explicit instructions.** If a proposed change conflicts with a documented decision in the [[Decision Log]], ask before acting.

---

## VAULT PURPOSE

This is a mixed-use personal knowledge vault for a working real estate agent. It covers:
- **Real Estate Operations:** Listings, clients (buyers/sellers/tenants/landlords), transactions, showings, open houses, rentals, comps, market research, and marketing
- **Business Management:** Lead pipeline, CRM/sphere, goals & KPIs, financials, SOPs, and continuing education
- **Projects:** Side projects, vault maintenance, and anything with a defined start/end
- **Resources:** Checklists, scripts & templates, legal forms — the toolbox
- **Daily Notes:** Day planning, task capture, showing schedules, follow-ups
- **Reflection:** Weekly reviews, retrospectives, personal insights
- **Personal:** Family, health & wellness, recipes, life outside real estate

---

## FOLDER STRUCTURE

| Folder | Purpose |
|---|---|
| `00-Inbox/` | Unprocessed captures — everything lands here first |
| `01-Daily-Notes/` | Daily notes (one per day, date-prefixed) |
| `02-Real-Estate/` | All active real estate operations (see breakdown below) |
| `03-Business/` | Business management — pipeline, financials, SOPs, CE, CRM |
| `04-Projects/` | Active projects with defined scope (vault setup, marketing campaigns, etc.) |
| `05-Resources/` | Checklists, scripts & templates, legal forms — reference material |
| `06-Templates/` | Obsidian note templates (do not edit without confirmation) |
| `10-Personal/` | Personal life — family, health, recipes |
| `20-Reflection/` | Weekly reviews, retrospectives, journaling |
| `90-Archive/` | Completed or inactive material — no deletions, archive here |

**When in doubt about where something goes, put it in `00-Inbox/` and flag it.**

### 02-Real-Estate Subfolders

| Subfolder | What goes here |
|---|---|
| `Clients/Buyers/` | One note per buyer client |
| `Clients/Sellers/` | One note per seller client |
| `Clients/Tenants/` | One note per tenant |
| `Clients/Landlords/` | One note per landlord |
| `Listings/Active/` | Active listings (move to `Sold/`, `Expired/`, or `Pending/` as status changes) |
| `Listings/Pending/` | Under contract, not yet closed |
| `Listings/Sold/` | Closed listing-side deals |
| `Listings/Expired/` | Expired or withdrawn listings |
| `Comps/` | CMA data, comparable sales notes |
| `Transactions/Active/` | Active transactions (move to `Closed/` at settlement) |
| `Transactions/Closed/` | Completed transactions |
| `Showings/` | Showing notes and feedback |
| `Open-Houses/` | Open house plans and sign-in sheets |
| `Rentals/Properties/` | Rental property notes |
| `Rentals/Leases/` | Lease documents and terms |
| `Rentals/Maintenance/` | Maintenance requests and vendor work |
| `Vendors-and-Contacts/` | Inspectors, lenders, title companies, contractors, etc. |
| `Market-Research/` | Market stats, neighborhood data, trend notes |
| `Marketing/` | Branding, social media, email campaigns, mailers, print, video |

### 03-Business Subfolders

| Subfolder | What goes here |
|---|---|
| `Lead-Pipeline/` | Lead tracker dashboard + `Sources/` subfolder |
| `CRM/` | Past clients, referral partners, sphere of influence, drip campaigns |
| `Goals-and-KPIs/` | Annual/quarterly goals, production tracking |
| `Financials/` | Commissions, expenses, monthly reports, tax docs |
| `SOPs/` | Standard operating procedures by process type (buyer, listing, rental, admin) |
| `Continuing-Education/` | Courses, certifications, study notes |

### 04-Projects Subfolder Standard

Each project gets its own folder under `04-Projects/`:

```
ProjectName/
├── YYYYMMDD_NoteTitle.md   ← Session notes, progress updates
└── (any supporting files)
```

The `Projects Dashboard.md` at `04-Projects/Projects Dashboard.md` is the navigation hub for all projects.

### 90-Archive Subfolders

| Subfolder | What gets archived here |
|---|---|
| `Closed-Deals/` | Completed transaction files |
| `Completed-Projects/` | Finished project folders |
| `Past-Clients/` | Clients no longer active (but keep for reference/referrals) |

---

## ROOT-LEVEL NOTES

These notes live at the vault root and serve as navigation hubs:

| File | Purpose |
|---|---|
| `Home.md` | Main dashboard — links to everything |
| `Active Work Ledger.md` | What's live right now — deals, listings, rentals, projects |
| `Decision Log.md` | All documented decisions with rationale |
| `CLAUDE.md` | This file — vault rules for Claude |

---

## FILE NAMING CONVENTIONS

- Daily notes: `YYYYMMDD.md` (e.g., `20260322.md`)
- Session / project notes: `YYYYMMDD_NoteTitle.md` (e.g., `20260322_VaultSetup.md`)
- Client notes: `LastName_FirstName.md` (e.g., `Smith_John.md`)
- Listing notes: `Address_or_MLS.md` (e.g., `123_Oak_Street.md` or `MLS_12345.md`)
- Transaction notes: `Address_Transaction.md` (e.g., `123_Oak_Street_Transaction.md`)
- Reflection: `YYYY-WW_WeeklyReview.md` (e.g., `2026-13_WeeklyReview.md`)
- No spaces in filenames — use underscores or CamelCase
- Dashboard / hub notes may use readable names with spaces (e.g., `Lead Pipeline.md`, `Active Work Ledger.md`)

---

## FRONTMATTER — REQUIRED SCHEMA

Every note must include a YAML frontmatter block. The **minimum required fields** are:

```yaml
---
tags: []
created: YYYY-MM-DD
type: <see valid types below>
status: <see valid statuses below>
---
```

### Valid `type` values

| Type | Use for |
|---|---|
| `daily` | Daily notes |
| `listing` | Property listings |
| `transaction` | Active/closed transactions |
| `client` | Buyer, seller, tenant, landlord notes |
| `showing` | Showing notes |
| `open-house` | Open house notes |
| `rental` | Rental property notes |
| `vendor` | Vendor/contact notes |
| `lead` | Lead notes |
| `dashboard` | Hub/dashboard/MOC notes |
| `ledger` | Active Work Ledger |
| `checklist` | Checklists |
| `sop` | Standard operating procedures |
| `goals` | Goals and KPI tracking |
| `project` | Project notes |
| `research` | Market research, comps, reference material |
| `reference` | General reference material |
| `reflection` | Weekly reviews, retrospectives |
| `personal` | Personal life notes |
| `home` | Home.md only |
| `inbox` | Unprocessed captures |

### Valid `status` values

| Status | Meaning |
|---|---|
| `draft` | Rough capture, not yet organized |
| `active` | Currently in use / in progress |
| `pending` | Under contract or waiting on something |
| `complete` | Done — ready to archive when no longer referenced |
| `closed` | Deal closed (transactions) |
| `expired` | Listing expired or withdrawn |
| `archived` | Moved to `90-Archive/` |

### Extended frontmatter for real estate notes

Templates in `06-Templates/` define additional frontmatter fields for specific note types (e.g., `address`, `mls_number`, `list_price`, `contract_date`, `buyer`, `seller`, etc.). When creating notes from templates, preserve all template fields.

All client contact cards (Buyer, Seller, Tenant, Landlord) include these additional frontmatter fields:
- `boldtrail_id` — BoldTrail CRM contact ID (integer, links vault card to CRM record)
- `last_synced` — Date of last BoldTrail vault sync (YYYY-MM-DD format)

---

## LINK CONVENTIONS

- Use `[[wikilink]]` syntax for all internal references — never standard markdown links for internal notes
- Link to clients, properties, transactions, decisions, and contacts inline when mentioned
- Do not create links to notes that don't exist yet unless explicitly asked to
- Folder-path links like `[[02-Real-Estate/Listings/Active]]` should point to index notes inside those folders, not to the folder itself. If no index note exists, create one or link to the relevant dashboard instead.

---

## TAG TAXONOMY

Extend as needed — do not delete tags already in use.

**Context**
`real-estate` · `personal` · `work` · `domain-realty`

**Note type**
`listing` · `transaction` · `client` · `showing` · `open-house` · `rental` · `lead` · `meeting` · `decision` · `action-item` · `research` · `reflection` · `reference` · `daily` · `dashboard` · `MOC`

**Status**
`active` · `pending` · `closed` · `expired` · `in-progress` · `parked` · `needs-review` · `archived`

**Deal side**
`buyer-side` · `listing-side` · `dual-agency` · `rental`

**Client type**
`buyer` · `seller` · `tenant` · `landlord`

**Lead source**
`referral` · `zillow` · `open-house` · `sign-call` · `website` · `sphere` · `social-media` · `cold-call`

**Business**
`pipeline` · `CRM` · `financials` · `goals` · `sop` · `continuing-education`

**Compliance**
`email-optin` · `phone-consent` · `text-consent` · `tcpa-documented` · `do-not-call` · `DNC`

**Enrichment**
`enriched-free` · `enriched-full` · `voter-record-match` · `snowbird-potential` · `needs-property-review` · `needs-manual-review` · `BTQualify`

**Topic**
`marketing` · `negotiation` · `contracts` · `pricing` · `staging` · `inspections` · `appraisals` · `title` · `lending`

---

## CLAUDE'S PERMISSIONS — WHAT YOU CAN AND CANNOT DO

### Always allowed (no confirmation needed)
- Read any file in the vault
- Fix frontmatter (add missing fields, correct formatting, add `created`/`status` where missing)
- Insert or correct `[[wikilinks]]` to existing notes
- Reorganize structure within a note (headers, formatting)
- Move files to `90-Archive/` when explicitly asked

### Requires staging to `00-Inbox/` first
- **All new notes — no exceptions.** Every new note Claude creates (contact cards, summaries, research notes, daily notes, weekly reviews, report outputs, etc.) must be written to `00-Inbox/`. Do not file directly to destination folders, and do not offer to move or file the note after creation. The note stays in `00-Inbox/` until Stacey processes it or explicitly asks for it to be moved.

### Requires explicit confirmation before acting
- Moving or renaming existing notes
- Any bulk operation affecting more than 3 files at once
- Deleting anything (prefer archiving to `90-Archive/`)
- Modifying templates in `06-Templates/`

### Never do
- Modify `.obsidian/` config files
- Delete files (archive instead)
- Write opinionated content into notes marked as personal reflection
- Overwrite notes with `status: complete` or `status: closed` without confirmation

---

## ACTIVE WORK LEDGER

The `Active Work Ledger.md` lives at the vault root. At the start of each session, read it first to understand what's live:
- Active listings
- Active buyer clients
- Active transactions
- Rental properties
- Active projects

Update it when deals move, close, or new ones come in.

---

## DECISION LOG

The `Decision Log.md` lives at the vault root. All significant decisions — vault structure, business process, deal strategy — get logged here with date, rationale, and a link back to the source note.

---

## TEMPLATES

Templates live in `06-Templates/` and use Obsidian's core Templates plugin. Available templates:

| Template | Creates |
|---|---|
| `Daily Note.md` | Daily planning note with priorities, showings, follow-ups |
| `Listing.md` | Full listing note with property details, marketing plan, showing feedback |
| `Transaction.md` | Transaction tracker with key dates, contingencies, commission breakdown |
| `Buyer Client.md` | Buyer client profile with compliance, spouse, financing, search behavior, social profiles |
| `Seller Client.md` | Seller client profile with compliance, spouse, property details, social profiles |
| `Tenant.md` | Tenant profile with compliance, screening, lease details, maintenance tracking |
| `Landlord Client.md` | Landlord profile with rental properties, financials, investment goals |
| `Showing.md` | Showing notes and feedback |
| `Open House.md` | Open house plan and results |
| `Rental Property.md` | Rental property details |
| `Vendor Contact.md` | Vendor/contact info |
| `Meeting Note.md` | Meeting notes with action items |
| `CMA Report.md` | Comparative market analysis |
| `Project.md` | Project tracking note |
| `Weekly Review.md` | End-of-week reflection and review |

**Do not modify templates without explicit confirmation.**

---

## SKILLS IN USE

| Skill | Purpose |
|---|---|
| Inbox Processor | Classify and file notes from `00-Inbox/` |
| Vault Health Checker | Find orphan notes, broken links, missing frontmatter |
| Session Initializer | Load active context from ledger and recent notes |
| Research Aggregator | Synthesize multi-note research into summary notes |
| Backlink Builder | Insert `[[wikilinks]]` to related vault notes |
| Weekly Review Generator | Build structured weekly review from daily notes |
| Daily Note Manager | Create daily note with carry-over tasks from previous day |
| Decision Log Updater | Extract and centralize decisions from tagged notes |
| Meeting Note Processor | Process meeting transcripts into structured notes |
| Note Formatter | Convert rough text/transcripts into formatted vault notes |
| Lead Enrichment | On-demand enrichment pipeline — pulls data from public sources into BoldTrail |
| BoldTrail Vault Sync | Syncs BoldTrail CRM contacts into vault contact cards (create + update) |

---

*Last updated: 2026-03-26 | Stacey Bowers | v2.2 — tightened 00-Inbox staging rule: all new notes stay in Inbox with no offer to bypass; clarified that Claude must not offer to file or move notes after creation*
