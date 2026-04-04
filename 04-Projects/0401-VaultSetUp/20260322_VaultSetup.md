---
tags:
  - project
  - vault-setup
created: 2026-03-22
type: project
status: active
start_date: "2026-03-22"
due_date: ""
priority: "high"
---

# Vault Setup

## Overview
- **Goal:** Build out a fully functional Obsidian vault tailored to Stacey's real estate business at Domain Realty Group — covering deals, clients, listings, rentals, lead tracking, and personal life.
- **Why it matters:** A well-organized vault is the command center. No more scattered notes, lost follow-ups, or forgotten tasks. Everything lives in one place, linked and searchable.
- **Due:** Ongoing — core structure complete, now in populate-and-refine phase.

## What's Been Done
- [x] Created full vault folder structure (00-Inbox through 90-Archive)
- [x] Built 02-Real-Estate subfolders: Clients, Listings, Transactions, Showings, Comps, Rentals, Marketing, Open-Houses, Vendors-and-Contacts, Market-Research
- [x] Built 03-Business subfolders: Lead-Pipeline, Goals-and-KPIs, Financials, SOPs, CRM, Continuing-Education
- [x] Built 10-Personal subfolders: Family-and-Home, Health-and-Wellness, Recipes
- [x] Created 14 templates in 06-Templates (Daily Note, Project, Meeting Note, Listing, Buyer Client, Seller Client, Transaction, CMA Report, Showing, Open House, Rental Property, Tenant, Vendor Contact, Weekly Review)
- [x] Created hub/dashboard notes: Home.md, Active Work Ledger.md, Projects Dashboard.md, Lead Pipeline.md, 2026 Goals.md, Health Dashboard.md, Family Dashboard.md
- [x] Created resource checklists: Buyer Transaction Checklist, Listing Checklist
- [x] Configured .obsidian settings
- [x] Set up CLAUDE.md for AI context
- [x] **GitHub + Git version control (Phase 10)** — Initialized git repo in vault, created private GitHub repo (`stacey-bowers/StaceysVault`), pushed full vault (144 files), stored PAT in macOS Keychain
- [x] **Obsidian Git plugin (Phase 8/10)** — Installed and enabled community plugin v2.38.0; configured auto commit-and-sync every 120 minutes + after stopping file edits; push on every commit; verified end-to-end pipeline working

## What's Next
- [ ] Populate Active Work Ledger with current deals, listings, and clients
- [ ] Fill in 2026 Goals with actual targets (volume, transactions, GCI)
- [ ] Create first client and listing notes using templates
- [ ] Add vendor/contact notes for key relationships (lender, title company, inspector, etc.)
- [ ] Set up SOPs for repeatable workflows (listing launch, buyer onboarding, closing process)
- [ ] Build out Lead Pipeline with current prospects
- [ ] Test inbox processing workflow (drop notes in 00-Inbox → process → file)
- [ ] Configure Obsidian Git to remember origin/main automatically (runs silently after first auto-commit)

## Progress Log
| Date | Update |
| ---- | ------ |
| 2026-03-22 | Vault structure fully built — all folders, templates, dashboards, and checklists created. Migrated from VaultSetUp subfolder to StaceysVault root. |
| 2026-04-03 | **GitHub + Obsidian Git fully operational.** Git repo initialized, .gitignore created, 144 files pushed to private GitHub repo (`stacey-bowers/StaceysVault`). PAT stored in macOS Keychain. Obsidian Git v2.38.0 installed and configured — auto commit-and-sync every 120 min + on file edit stop. Verified end-to-end: 4 files committed and pushed from within Obsidian. Vault now has full version history and rollback capability. |

## Resources & Links
- [[Home]]
- [[Active Work Ledger]]
- [[Projects Dashboard]]

## Notes
- The vault uses a numbered folder system (00–90) for clean sorting in the sidebar.
- Templates live in 06-Templates and are designed for Obsidian's core Templates plugin.
- 00-Inbox is the drop zone — anything unprocessed goes here first, then gets filed.
