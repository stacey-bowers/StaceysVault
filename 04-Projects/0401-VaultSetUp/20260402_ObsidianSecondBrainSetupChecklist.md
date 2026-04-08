---
tags: [obsidian, knowledge-management, setup, reference, cowork]
created: 2026-04-02
type: reference
status: active
---

# Obsidian Second Brain — Setup Checklist for Claude Cowork

*Created: 2026-04-02 | Author: Jimmy Bowers | Purpose: Reproducible setup guide for new Obsidian vaults built on the JBVaultWorkspace architecture*

This document is intended to be handed directly to a Claude Cowork instance at the start of a new Obsidian vault build. It covers every component of the Second Brain setup, with enough context for Claude to understand the purpose behind each item and verify or complete it independently. Steps are ordered by dependency — earlier phases must be complete before later ones will work correctly.

Use the checkboxes to track progress. If Claude is verifying an existing partial install, it should read each item, check the vault, and report status before taking any action.

---

## How to Use This Document

Hand this file to Claude Cowork and say: *"Read this checklist and verify where we are with the vault setup. For anything that is not yet done, tell me what is missing and confirm before taking action."*

Claude should:
1. Read every item in each phase
2. Check the vault for the presence and correctness of each component
3. Report a status for each item: ✅ Complete | ⚠️ Partial | ❌ Missing
4. Propose a plan to close any gaps before acting

---

## Phase 1 — Foundation Files and Contracts

These are the two instruction files that tell Claude how to behave in this vault. They must exist and be accurate before any other work begins.

- [ ] **Global CLAUDE.md** exists at `~/.claude/CLAUDE.md`
  - *Why:* This file governs Claude's behavior across all Cowork sessions — tone, output standards, file naming, safety rules, and communication style. Without it, Claude operates on defaults.
  - *Verify:* File exists and contains sections for: WHO I AM, DEFAULT BEHAVIOR, OUTPUT STANDARDS, FILE NAMING, MARKDOWN & OBSIDIAN CONVENTIONS, SAFETY.

- [ ] **Workspace CLAUDE.md** exists at the vault root (e.g., `JBVaultWorkspace/CLAUDE.md`)
  - *Why:* This file contains vault-specific rules that override or extend the global file — folder structure, frontmatter schema, link conventions, permissions, and the Active Work Ledger location. It is the contract Claude references every session.
  - *Verify:* File exists and contains sections for: VAULT PURPOSE, FOLDER STRUCTURE, FILE NAMING CONVENTIONS, FRONTMATTER SCHEMA, LINK CONVENTIONS, TAG TAXONOMY, CLAUDE'S PERMISSIONS, OBSIDIAN CLI, ACTIVE WORK LEDGER, SKILLS IN USE.
  - *Note:* This file should be versioned (e.g., `v1.0`) and updated whenever vault conventions change.

---

## Phase 2 — Folder Structure

The vault uses a numbered folder system. Every folder must exist with the correct name and casing.

- [ ] `00-Inbox/` — Unprocessed captures; everything new lands here first
- [ ] `00-Templates/` — Note templates (daily notes, project hubs, meetings, reviews)
- [ ] `01-Daily Notes/` — One daily note per day, date-prefixed (`YYYYMMDD.md`)
- [ ] `02-Projects/` — Active projects; one subfolder per project
- [ ] `03-Research/` — Aggregated research, summaries, reference material
- [ ] `04-Indexes/` — Navigation indexes (ChatIndex, ProjectIndex, TopicIndex, SkillIndex)
- [ ] `05-Skills/` — Skill packages, agent definitions, and reference docs
  - [ ] `05-Skills/Packages/` — Installable `.skill` files (current versions only)
- [ ] `10-PersonalDevelopment/` — Learning notes, books, growth content
- [ ] `20-Reflection/` — Weekly reviews, retrospectives
- [ ] `90-Archive/` — Completed or inactive material (never delete — archive here)
  - [ ] `90-Archive/Skills/` — Prior versions of skill packages
- [ ] `99-System/` — System artifacts: logs, scripts, eval outputs, health reports
  - [ ] `99-System/VaultHealthReports/` — Output folder for vault health check runs
  - [ ] `99-System/Scripts/` — Python or shell scripts used in vault workflows

*Why this structure:* The numbered folders create a predictable knowledge graph. Claude uses folder paths to route new notes correctly, and every skill in the library assumes this structure. Deviating from it breaks wikilinks and skill outputs.

---

## Phase 3 — Project Subfolder Standard

Every project under `02-Projects/` must follow this exact structure.

- [ ] Each project folder is named `XXXX-ProjectName` (4-digit ID, CamelCase, no spaces)
- [ ] Each project folder contains:
  - [ ] `ProjectHub_ProjectName.md` — at the root of the project folder (never inside a subfolder)
  - [ ] `Chats/` — Raw conversation exports from Claude or ChatGPT
  - [ ] `Summaries/` — All markdown session notes and analysis (named `YYYYMMDD_NoteTitle.md`)
  - [ ] `Assets/` — Non-markdown reference files only (PDFs, PPTXs, external docs)
  - [ ] `Outputs/` — Final deliverables (docx, xlsx, pptx, HTML briefs, etc.)

*Why:* Claude navigates by this structure when writing session notes, filing outputs, and updating project hubs. A consistent layout means zero ambiguity about where things go.

---

## Phase 4 — YAML Frontmatter Schema

Every note in the vault must have a YAML frontmatter block at the top. Claude uses this metadata for search, routing, health checks, and index maintenance.

- [ ] Frontmatter schema is documented in workspace CLAUDE.md
- [ ] Required fields are present in all notes:
  ```yaml
  ---
  tags: []
  created: YYYY-MM-DD
  type: daily | project | research | reflection | reference | personal-development | inbox
  status: draft | active | complete | archived
  ---
  ```
- [ ] Tags use lowercase hyphenated format (e.g., `lean-six-sigma`, `project-boomerang`)

*Why:* Without frontmatter, the Vault Health Checker cannot identify problem notes, the Inbox Processor cannot classify captures, and Claude cannot reliably filter or route content by type.

---

## Phase 5 — Navigation Index Files

These four files live in `04-Indexes/` and serve as the vault's navigation layer. Claude references them when orienting in a new session.

- [ ] **`04-Indexes/ChatIndex.md`** — Maps every conversation import to its project and summary note
- [ ] **`04-Indexes/ProjectIndex.md`** — One-line entry per project with ID, name, status, and link to ProjectHub
- [ ] **`04-Indexes/TopicIndex.md`** — Tag-based topic navigation across vault content
- [ ] **`04-Indexes/SkillIndex.md`** — Registry of all installed skills with version, description, package location, and version history

*Why:* These indexes let Claude navigate efficiently without scanning every folder. The SkillIndex is especially important — it is the authoritative record of what skills are installed, at what version, and when they were last updated.

---

## Phase 6 — Active Work Ledger and Decision Log

These two files are the operational core of the vault. Claude reads them at the start of every session.

- [ ] **`02-Projects/ActiveWorkLedger.md`** exists and contains:
  - [ ] 🟢 In Progress section
  - [ ] 🟡 Parked section
  - [ ] 🔴 Urgent section
  - [ ] ⏭️ Up Next section
  - [ ] 📁 Active Projects table (ID, name, context, status, link to ProjectHub)
  - [ ] ✅ Completed This Session section

- [ ] **`02-Projects/DecisionLog.md`** exists and contains:
  - [ ] Numbered decision entries (DEC-001, DEC-002, etc.)
  - [ ] Each entry includes: date, decision made, rationale, and status (active/superseded/archived)

*Why:* The ActiveWorkLedger is Jimmy's (or the owner's) external memory for what's in flight. The DecisionLog prevents the same decisions from being re-litigated across sessions — Claude checks it before making structural changes to the vault.

---

## Phase 7 — Templates Library

Templates live in `00-Templates/` and are used by skills to generate consistent note formats.

- [ ] Daily note template (`00-Templates/DailyNote_Template.md` or similar)
  - Should include: date heading, focus priorities, task list, carry-overs, end-of-day reflection
- [ ] Project hub template
  - Should include: frontmatter, What This Project Is, Key Outputs, Open Items, Claude Session Index
- [ ] Meeting note template
  - Should include: frontmatter, attendees, decisions, action items, parking lot
- [ ] Weekly review template
  - Should include: wins, challenges, open loops, patterns, next week priorities
- [ ] Research / reference note template

*Why:* Skills like the Daily Note Manager and Meeting Note Processor depend on templates being present. If a template is missing, the skill will either fail or generate an unstructured output.

---

## Phase 8 — Obsidian Application Settings

These are configuration items inside the Obsidian app itself.

- [ ] **Community plugins enabled** (Settings → Community plugins → Turn on community plugins)
  - *Why:* Obsidian ships with community plugins disabled by default. They must be enabled before any plugin can be installed.

- [ ] **Obsidian CLI installed and configured**
  - The CLI (`obsidian`) must be available at `/Applications/Obsidian.app/Contents/MacOS/obsidian`
  - Claude uses the CLI for vault relationship queries (orphan notes, backlinks, broken links, tag counts) — it is orders of magnitude faster than file scanning
  - *Verify:* Run `obsidian files` from terminal — if it returns a file list, the CLI is working
  - The Bash permission for `git -C "<vault path>" init` should exist in `.claude/settings.local.json`

---

## Phase 9 — Skills Installation

The vault uses a library of Claude Cowork skills for repeatable workflows. All skills must be installed to `~/.claude/skills/` on the Mac to be active.

Skills follow this versioning convention:
- Package filename: `skill-name-vN.skill`
- Description prefix: `[vN]`
- Current version packages live in `05-Skills/Packages/`; prior versions go to `90-Archive/Skills/`

**Core Vault Skills — verify all are installed:**

- [ ] **obsidian-inbox-processor** — Classifies and files notes from `00-Inbox/`
- [ ] **obsidian-vault-health-checker** — Finds orphan notes, broken links, missing frontmatter
- [ ] **obsidian-session-initializer** — Loads active context from ledger and recent notes at session start
- [ ] **obsidian-deep-research-aggregator** — Synthesizes multi-note research into summary notes
- [ ] **obsidian-backlink-builder** — Inserts `[[wikilinks]]` to related vault notes
- [ ] **obsidian-weekly-review-generator** — Builds structured weekly review from daily notes
- [ ] **obsidian-daily-note-manager** — Creates daily note with carry-over tasks from previous day
- [ ] **obsidian-decision-log-updater** — Extracts and centralizes decisions from tagged notes
- [ ] **obsidian-meeting-note-processor** — Processes meeting transcripts into structured notes
- [ ] **obsidian-note-formatter** — Converts rough text/transcripts into formatted vault notes
- [ ] **skill-creator-custom** — Creates new skills, modifies existing skills, runs performance evals
- [ ] **evaluator-skill** — Evaluates completed agent workflow runs against benchmark specs

*How to verify installation:* In Claude Cowork, skills appear in the skill picker. Alternatively, check `~/.claude/skills/` for the installed skill folders.

*Why skills matter:* Each skill encodes best practices and step-by-step workflows that would otherwise require manual prompting every session. They are the automation layer of the vault.

---

## Phase 10 — GitHub and Version Control

This phase sets up off-machine backup and full version history for the vault. Every note, skill file, and config change is tracked and recoverable.

- [ ] **GitHub account created** at github.com
- [ ] **GitHub Desktop installed** — download from desktop.github.com (use Apple Silicon version on M-series Macs)
  - Sign in with GitHub account during setup
  - *Why Desktop vs. command line:* GitHub Desktop handles authentication via macOS keychain, gives visual confirmation of staged files, and requires no command-line knowledge.

- [ ] **Private GitHub repository created**
  - Go to github.com → "+" → New repository
  - Name it to match the vault folder (e.g., `JBVaultWorkspace`)
  - Set to **Private**
  - Do NOT initialize with a README (repo must be empty)
  - Copy the HTTPS URL (e.g., `https://github.com/username/JBVaultWorkspace.git`)

- [ ] **Local vault initialized as a Git repository**
  - Run: `git -C "<vault path>" init`
  - Confirm: a `.git` folder exists inside the vault folder

- [ ] **Remote origin configured**
  - Run: `git -C "<vault path>" remote add origin <repo URL>`
  - Verify: `git -C "<vault path>" remote -v` returns the correct URL for both fetch and push

- [ ] **Initial commit created and pushed**
  - Stage all files, commit with a descriptive message, and push to `main`
  - Verify: navigate to the GitHub repo in a browser — all vault files should be visible

- [ ] **Obsidian Git plugin installed**
  - In Obsidian: Settings → Community plugins → Browse → search "Git" → install the plugin by **Vinzent (Denis Olehov)** (~2.3M downloads)
  - Enable the plugin after installing

- [ ] **Obsidian Git plugin configured**
  - Auto commit-and-sync interval: `120` minutes
  - Auto commit-and-sync after stopping file edits: **ON**
  - Push on commit-and-sync: **ON**
  - Pull on commit-and-sync: **ON**
  - Merge strategy: **Merge**
  - All other toggles: leave at default (off)
  - *Why 120 minutes + after stopping edits:* The interval is a safety net; the "after stopping file edits" toggle captures work at natural stopping points regardless of the timer. Together they ensure nothing is lost even if Obsidian closes unexpectedly.

- [ ] **`.gitignore` configured** to exclude large binary files from Assets folders (optional but recommended)
  - Add rule: `**/Assets/*.pptx`, `**/Assets/*.pdf` — or a general `**/Assets/` exclusion if Assets will only contain large reference files
  - *Why:* Git is optimized for text files. Large binaries (PPTXs, PDFs) inflate repo size and can hit GitHub's 100MB per-file limit.

---

## Phase 11 — First Run Verification

Once all phases are complete, run these verification steps to confirm the vault is functioning end-to-end.

- [ ] **Run Vault Health Checker** — should return 0 broken links, 0 orphan notes, and no notes with missing frontmatter (minor issues are acceptable on a fresh vault)
- [ ] **Run Session Initializer** — should produce a structured session brief pulling from ActiveWorkLedger and recent daily notes; time should reflect actual current time (not assumed)
- [ ] **Create first daily note** using the Daily Note Manager skill
- [ ] **Confirm Obsidian Git auto-sync** — make a small edit to any note, wait 2–3 minutes after stopping, then check GitHub to confirm the commit appeared
- [ ] **Run a manual backup** — in Obsidian, press `Cmd+P` → type "Obsidian Git: Create backup" → confirm it completes without error

---

## Notes for the Installing Claude Instance

- Always read both CLAUDE.md files at the start of every session before taking any action
- The DecisionLog is the authoritative record of structural choices — check it before proposing changes that touch naming conventions, folder structure, or skill architecture
- When a skill is updated, the old version must be archived to `90-Archive/Skills/` and the SkillIndex updated to reflect the new version
- Never delete files — archive to `90-Archive/` instead
- If something is missing from this checklist that you encounter in practice, flag it to the vault owner so it can be added

---

*Version 1.0 — Created 2026-04-02 | Jimmy Bowers | Filed: [[02-Projects/0201-ObsidianAsSecondBrain/Summaries/20260402_ObsidianSecondBrainSetupChecklist]]*
