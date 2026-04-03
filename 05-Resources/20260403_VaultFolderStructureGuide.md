---
tags: [reference, vault-setup, obsidian, knowledge-management]
created: 2026-04-03
type: reference
status: active
---

# StaceysVault — Obsidian Folder Structure Guide

*A real estate agent's second brain, built on Obsidian + Claude Cowork. Share this with anyone who wants to set up a similar vault.*

---

## Philosophy

This vault uses a **numbered folder system** (00–90) so folders always sort in the intended order in Obsidian's sidebar, regardless of alphabetical sorting. Everything new lands in `00-Inbox/` first — never directly into a destination folder. That single rule keeps the vault clean without slowing down capture.

The vault is split into three zones:
- **Operations** (02, 03) — live real estate work and business management
- **Knowledge** (04, 05, 06) — projects, resources, and templates
- **Life** (10, 20, 90) — personal, reflection, and archive

---

## Root-Level Files

These four files live at the vault root and serve as the navigation and governance layer. Claude reads them at the start of every session.

| File | Purpose |
|---|---|
| `Home.md` | Main dashboard — quick links to everything |
| `Active Work Ledger.md` | What's live right now — deals, listings, rentals, projects |
| `Decision Log.md` | All documented decisions with date, rationale, and source |
| `CLAUDE.md` | Instruction contract for Claude Cowork — vault rules, permissions, schema |

---

## Full Folder Tree

```
StaceysVault/
│
├── 00-Inbox/                        # Everything lands here first — unprocessed captures
│
├── 01-Daily-Notes/                  # One note per day — YYYYMMDD.md format
│
├── 02-Real-Estate/                  # All active real estate operations
│   ├── Clients/
│   │   ├── Buyers/                  # One note per buyer client — LastName_FirstName.md
│   │   ├── Sellers/                 # One note per seller client
│   │   ├── Tenants/                 # One note per tenant
│   │   └── Landlords/               # One note per landlord
│   ├── Listings/
│   │   ├── Active/                  # Current active listings
│   │   ├── Pending/                 # Under contract, not yet closed
│   │   ├── Sold/                    # Closed listing-side deals
│   │   └── Expired/                 # Expired or withdrawn listings
│   ├── Transactions/
│   │   ├── Active/                  # Deals currently in contract
│   │   └── Closed/                  # Completed transactions
│   ├── Rentals/
│   │   ├── Properties/              # Rental property notes
│   │   ├── Leases/                  # Lease documents and terms
│   │   └── Maintenance/             # Maintenance requests and vendor work
│   ├── Comps/                       # CMA data and comparable sales notes
│   ├── Showings/                    # Showing notes and buyer feedback
│   ├── Open-Houses/                 # Open house plans and sign-in sheets
│   ├── Vendors-and-Contacts/        # Inspectors, lenders, title, contractors
│   ├── Market-Research/
│   │   └── Communities/             # Neighborhood and community research
│   └── Marketing/
│       ├── Branding/
│       ├── Email-Campaigns/
│       ├── Farming-and-Mailers/
│       ├── Print-Materials/
│       ├── Social-Media/
│       └── Video-Content/
│
├── 03-Business/                     # Business management — behind the scenes
│   ├── Lead-Pipeline/
│   │   └── Sources/                 # Notes by lead source (Zillow, referral, etc.)
│   ├── CRM/
│   │   ├── Past-Clients/            # Former clients — keep for referrals
│   │   ├── Referral-Partners/       # Lenders, attorneys, CPAs, contractors
│   │   ├── Sphere-of-Influence/     # SOI contacts
│   │   └── Drip-Campaigns/          # Campaign notes and sequences
│   ├── Goals-and-KPIs/              # Annual/quarterly goals and production tracking
│   ├── Financials/
│   │   ├── Commissions/             # Deal-by-deal commission tracking
│   │   ├── Expenses/                # Business expenses
│   │   ├── Monthly-Reports/         # Month-end summaries
│   │   └── Tax-Docs/                # Tax preparation materials
│   ├── SOPs/                        # Standard operating procedures
│   │   ├── Buyer-Process/
│   │   ├── Listing-Process/
│   │   ├── Rental-Process/
│   │   └── Admin-and-Compliance/
│   └── Continuing-Education/
│       ├── Courses/
│       ├── Certifications/
│       └── Notes/
│
├── 04-Projects/                     # Active projects with defined scope
│   ├── Projects Dashboard.md        # Navigation hub — links to all project hubs
│   └── XXXX-ProjectName/            # One folder per project (4-digit ID, CamelCase)
│       ├── ProjectHub_Name.md       # Project overview note (lives at folder root)
│       ├── Chats/                   # Raw conversation exports
│       ├── Summaries/               # Session notes — YYYYMMDD_NoteTitle.md
│       ├── Assets/                  # Reference files (PDFs, PPTXs, etc.)
│       └── Outputs/                 # Final deliverables (docx, xlsx, reports)
│
├── 05-Resources/                    # The toolbox — reference material
│   ├── Checklists/
│   │   ├── Buyer/
│   │   ├── Seller/
│   │   ├── Rental/
│   │   └── General/
│   ├── Scripts-and-Templates/
│   │   ├── Cold-Call-Scripts/
│   │   ├── Email-Templates/
│   │   ├── Follow-Up-Templates/
│   │   ├── Listing-Presentation/
│   │   └── Objection-Handlers/
│   ├── Legal-Forms/
│   │   ├── Purchase-Agreements/
│   │   ├── Listing-Agreements/
│   │   ├── Lease-Agreements/
│   │   ├── Addenda/
│   │   └── Disclosures/
│   └── Client-Briefs/               # Quick-reference briefs, phone-readable
│
├── 06-Templates/                    # Obsidian note templates (do not edit without care)
│   ├── Daily Note.md
│   ├── Buyer Client.md
│   ├── Seller Client.md
│   ├── Tenant.md
│   ├── Landlord Client.md
│   ├── Listing.md
│   ├── Transaction.md
│   ├── Showing.md
│   ├── Open House.md
│   ├── Rental Property.md
│   ├── Vendor Contact.md
│   ├── Meeting Note.md
│   ├── CMA Report.md
│   ├── Client Brief.md
│   ├── Project.md
│   └── Weekly Review.md
│
├── 10-Personal/                     # Life outside real estate
│   ├── Family-and-Home/
│   │   ├── Kids/
│   │   ├── Events/
│   │   └── Home-Maintenance/
│   ├── Health-and-Wellness/
│   │   ├── Appointments/
│   │   ├── Fitness/
│   │   └── Medical-Records/
│   └── Recipes/
│       ├── Favorites/
│       ├── Meal-Prep/
│       └── Quick-Meals/
│
├── 20-Reflection/                   # Weekly reviews and retrospectives
│
└── 90-Archive/                      # Nothing is ever deleted — archive here
    ├── Closed-Deals/                # Completed transaction files
    ├── Completed-Projects/          # Finished project folders
    ├── Past-Clients/                # Inactive clients (keep for referrals)
    └── SkillArchive/                # Prior versions of Claude skill packages
```

---

## File Naming Conventions

| Note Type | Convention | Example |
|---|---|---|
| Daily notes | `YYYYMMDD.md` | `20260403.md` |
| Session / project notes | `YYYYMMDD_NoteTitle.md` | `20260403_VaultSetup.md` |
| Client notes | `LastName_FirstName.md` | `Smith_John.md` |
| Listing notes | `Address_or_MLS.md` | `123_Oak_Street.md` |
| Transaction notes | `Address_Transaction.md` | `123_Oak_Street_Transaction.md` |
| Weekly reviews | `YYYY-WW_WeeklyReview.md` | `2026-14_WeeklyReview.md` |
| Dashboard / hub notes | Readable names with spaces | `Active Work Ledger.md` |

**Rules:** No spaces in filenames except dashboard/hub notes. Use underscores or CamelCase. All dates are date-first so everything sorts chronologically.

---

## YAML Frontmatter — Every Note Requires This

```yaml
---
tags: []
created: YYYY-MM-DD
type: <see valid types below>
status: <see valid statuses below>
---
```

### Valid `type` values
`daily` · `listing` · `transaction` · `client` · `showing` · `open-house` · `rental` · `vendor` · `lead` · `dashboard` · `ledger` · `checklist` · `sop` · `goals` · `project` · `research` · `reference` · `reflection` · `personal` · `home` · `inbox`

### Valid `status` values
`draft` · `active` · `pending` · `complete` · `closed` · `expired` · `archived`

### Extra fields for client notes
```yaml
boldtrail_id: 123456        # CRM contact ID (links vault card to BoldTrail)
last_synced: YYYY-MM-DD     # Date of last CRM sync
```

---

## Key Design Decisions

**Why numbered folders?** Obsidian sorts folders alphabetically. Numbers force the order you actually want — Inbox first, Archive last, no fighting the sidebar.

**Why `00-Inbox/` for everything new?** Capture speed matters more than perfect organization in the moment. Drop it in Inbox, process it later. The Inbox Processor skill handles the filing.

**Why archive instead of delete?** You never know when an old client re-engages or a closed deal comes back as a reference. Archive to `90-Archive/` — storage is cheap, lost context is expensive.

**Why templates in `06-Templates/` vs `00-Templates/`?** Templates are reference material, not captures — they shouldn't sort near Inbox. The 06 placement keeps them accessible but out of the operational flow.

**Why separate `05-Resources/` and `06-Templates/`?** Resources are things you reference and use (checklists, scripts, legal forms). Templates are blank note structures that Obsidian's Templates plugin fills in. Different purpose, different folder.

---

## Claude Cowork Skills In Use

These skills automate the repetitive workflows in this vault:

| Skill | What It Does |
|---|---|
| `obsidian-inbox-processor` | Classifies and files notes from `00-Inbox/` |
| `obsidian-vault-health-checker` | Finds orphan notes, broken links, missing frontmatter |
| `obsidian-session-initializer` | Loads active context at the start of every session |
| `obsidian-daily-note-manager` | Creates today's note with carry-over tasks |
| `obsidian-weekly-review-generator` | Builds weekly review from daily notes |
| `obsidian-meeting-note-processor` | Turns meeting transcripts into structured notes |
| `obsidian-note-formatter` | Converts rough text/voice-to-text into vault notes |
| `obsidian-backlink-builder` | Inserts `[[wikilinks]]` to connect related notes |
| `obsidian-deep-research-aggregator` | Synthesizes multi-note research into a summary |
| `obsidian-decision-log-updater` | Centralizes decisions from tagged notes |
| `lead-enrichment` | Enriches contacts in BoldTrail CRM from public sources |
| `boldtrail-vault-sync` | Syncs BoldTrail CRM contacts into vault cards |

---

## Obsidian Settings That Matter

- **Core plugins enabled:** File explorer, Global search, Graph, Backlinks, Outgoing links, Tag pane, Properties, Page preview, Daily notes, Templates, Command palette, Bookmarks, File recovery
- **Templates plugin configured to:** `06-Templates/`
- **Daily notes configured to:** `01-Daily-Notes/`, format `YYYYMMDD`
- **Community plugins:** Obsidian Git (auto-commit every 120 min + after stopping edits, push to private GitHub repo)

---

*Vault design: Stacey Bowers — Domain Realty Group | Built with Claude Cowork | v1.0 — 2026-04-03*
