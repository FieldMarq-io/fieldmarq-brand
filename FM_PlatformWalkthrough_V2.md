# FIELDMARQ — Platform Customer Journey

**Complete Step-by-Step Walkthrough: Every Screen, Every Click, Every Feature**

Version 2.1 | March 25, 2026

*Living Document: Updated as features ship*

**CONFIDENTIAL**

*Serves as: Engineering Walkthrough | Training Manual Foundation | PRD/MRD Source | Marketing Content Source*

---

## Table of Contents

1. How to Read This Document
2. The 30-Second FieldMarq Story
3. Build Timeline (Batch 1 + Batch 2)
4. Phase 1: Sign Up and Onboarding
   - 4.1 Landing Page and Sign Up
   - 4.2 Company Profile Setup (AI-Powered)
   - 4.3 CRM Connection
   - 4.4 First Event Import
5. Phase 2: The Dashboard (Command Center)
   - 5.1 KPI Cards
   - 5.2 Operating Widgets
   - 5.3 Action Queue (AI-Powered)
   - 5.4 What Changed Feed
   - 5.5 Drag-and-Drop Customization
6. Phase 3: Events (The Core Workspace)
   - 6.1 Events List Page
   - 6.2 Creating an Event
   - 6.3 Checklist Wizard and Template System
   - 6.4 Checklist Reconciliation (Event Type Change)
   - 6.5 Bulk Event Import
   - 6.6 Event Detail: Overview Tab
   - 6.7 Event Detail: Tasks Tab (with Dependencies)
   - 6.8 Event Detail: People/Guests Tab (with RSVP Workflow)
   - 6.9 Event Detail: Outreach/Campaigns Tab
   - 6.10 Event Detail: Budget Tab
   - 6.11 Event Detail: Documents Tab
   - 6.12 Event Detail: Content Tab
   - 6.13 Event Detail: Results/ROI Tab (Report Engine)
7. Phase 4: Global Tasks Page
8. Phase 5: Calendar
9. Phase 6: Contacts and Lead Processing
   - 9.1 Contacts List Page
   - 9.2 CSV Upload Pipeline
   - 9.3 Lead Scoring Engine (V2)
   - 9.4 Lead Detail Drawer
   - 9.5 Deduplication and Merge
10. Phase 7: Campaigns and Email
    - 10.1 Campaigns List Page
    - 10.2 Create Campaign Modal
    - 10.3 AI Email Generation
    - 10.4 Dynamic Segment Builder
    - 10.5 Email Review Panel
    - 10.6 Email Review Queue (3-Panel Layout)
    - 10.7 Email Scheduling and Sending
    - 10.8 Campaign Clone
    - 10.9 Campaign Pause/Resume
    - 10.10 Send Confirmation Modal
    - 10.11 CAN-SPAM Unsubscribe Compliance
    - 10.12 Email Sequences (Multi-Step Campaigns)
    - 10.13 Re-engagement Worker (Automated)
11. Phase 8: Reports and Intelligence
    - 11.1 Reports Hub
    - 11.2 Report View (Individual Reports)
    - 11.3 Executive Reports Dashboard
    - 11.4 Event-Level Report Types (11 Types)
    - 11.5 Cross-Event Report Types (7 Types)
    - 11.6 Legacy CMO Narrative Report
12. Phase 9: Content Library (Intelligence Layer)
13. Phase 10: Analytics and Attribution
    - 13.1 Attribution Engine (3-Phase Matching)
    - 13.2 ROI Calculations
    - 13.3 Excel Exports
    - 13.4 Scoring Page (Placeholder)
    - 13.5 Pipeline Page (Placeholder)
    - 13.6 Attribution Page (Placeholder)
14. Phase 11: Settings and Integrations
    - 14.1 CRM Connections
    - 14.2 Slack Notifications
    - 14.3 Admin Tools
    - 14.4 Team Management (Not Built)
    - 14.5 Billing / Stripe (Not Built)
    - 14.6 Data Export and Account Management (Not Built)
15. Notification System (with Notification Banner)
16. Platform Architecture (Why We Built It This Way)
17. Copilot Roadmap (V2 Vision)

Appendix A: Build Status Summary
Appendix B: Backend API Endpoint Reference
Appendix C: Database Migration Index (001-026)
Appendix D: Jack's Main Branch Features (Post-Divergence)

---

## 1. How to Read This Document

This document walks through every area of the FieldMarq platform from the perspective of a new customer. It covers every screen, tab, button, dropdown, filter, widget, and report in the order a user encounters them. It serves four purposes simultaneously:

- **Engineering walkthrough** so Jack understands the build and the reasoning behind every design decision
- **Training manual foundation** for user onboarding documentation
- **PRD/MRD source** — the "why we built it this way" sections feed product requirements
- **Marketing content source** — user experience descriptions are raw content for one-pagers and ad copy

Every feature section includes three elements: what the user sees and does (the experience), why it exists and why we built it this way (the reasoning), and the current build status (shipped, partial, or not built).

> **Status Key**
> - **SHIPPED** = Live on Aubs-updates branch, fully wired to backend APIs, real data
> - **PARTIAL** = Component exists with some functionality, needs completion
> - **SHELL** = Page/component exists as placeholder, no backend wiring
> - **NOT BUILT** = Specified but no implementation exists yet

---

## 2. The 30-Second FieldMarq Story

FieldMarq replaces the spreadsheet chaos that field marketers deal with across the entire event lifecycle. A field marketer today manages 40 to 60 events per year using a patchwork of spreadsheets, email threads, CRM systems, and manual processes. After every event, they spend 3 to 5 business days cleaning lead data in Excel, manually cross-referencing CRM records, guessing at lead quality, and building slide decks to justify their budget to leadership.

FieldMarq condenses that into minutes. The platform covers the complete journey: company onboarding with AI website analysis, event creation with auto-generated checklists, pre-event campaigns with AI-generated personalized emails, post-event CSV upload with automated lead scoring and deduplication, CRM sync, an attribution engine that connects event attendance to pipeline, and an AI report engine that generates 18 report types a CMO can show a CFO without touching a spreadsheet.

The core insight: a field marketer's intelligence, built up over years of running events, can be captured in structured data during onboarding and then applied automatically to every downstream feature. Your company profile, ICP, messaging, competitive landscape, and content library are not just a setup step — they are the engine that powers AI email generation, lead scoring, content recommendations, and eventually a full copilot that acts on behalf of the FM by default.

---

## 3. Build Timeline (Batch 1 + Batch 2)

Work is split across two branches that need to converge.

### Jack's Main Branch (Ongoing)

While Aubs-updates was in progress, Jack continued building on `main`. 13 commits added after the branch divergence point, including: email sequences (multi-step campaigns), email review queue (3-panel layout), CAN-SPAM unsubscribe compliance, AI document generators (exec briefing, sales brief), notification banner, 19 new event operational fields, task dependencies, RSVP workflow, re-engagement worker, campaign pause/resume, onboarding route guard, and send confirmation modal. These features are **live on main** and need to be reconciled when Aubs-updates merges.

### Aubs Batch 1 — Committed March 14-22, 2026 (8 PR groups, 63 files)

On `Aubs-updates` branch, awaiting merge to `main` via Jack. Core platform infrastructure: prospectus upload + document handler, checklist system with milestone tasks, bug fixes + checklist reconciliation, dashboard endpoints (action queue, leads-by-status, campaign counts), campaigns (clone, content library, dynamic segments, email review), AI-generated CMO report, scheduler improvements (auto-resolve, phase grouping), and frontend hook/routing fixes.

### Aubs Batch 2 — Committed March 22-25, 2026 (~94 files across 7 groups)

On `Aubs-updates` branch. Design system brand refresh (37 files), events and import components (12 files), all 8 event detail tabs refreshed, campaigns design refresh (7 files), dashboard overhaul with drag-and-drop (1 file, ~980 lines), new page shells for scoring/pipeline/attribution, and the full report engine (25 files — backend handler, 5 migrations, 23 frontend widgets).

### Merge Order

Batch 1 merges first (8 groups in dependency order). Batch 2 merges after all of Batch 1 is on main (7 groups, design system first, report engine last). Full merge instructions in `docs/MERGE_ORDER.md`. Jack's main branch features will need conflict resolution during merge — particularly in campaigns.go, tasks.go, events.go, scheduler.go, DocumentsTab.tsx, TasksTab.tsx, and PeopleTab.tsx.

---

## 4. Phase 1: Sign Up and Onboarding

Onboarding is the most important 10 minutes a customer spends with FieldMarq. Everything downstream — email generation quality, lead scoring accuracy, content recommendations — depends on the intelligence layer built during this phase. We designed onboarding to be fast (under 10 minutes), AI-first (Claude does the extraction work), and progressive (you can always add more detail later).

### 4.1 Landing Page and Sign Up

The customer arrives at fieldmarq.io. The landing page shows the core value proposition with a Start Free Trial CTA. Clicking it opens the Clerk-powered sign-up flow: email, password, company name, and role selection (VP Marketing, Director of Marketing, Field Marketing Manager, Demand Gen Manager, Events Manager).

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Landing page at fieldmarq.io | SHIPPED | Hero section, feature highlights, CTA, auth links |
| Clerk sign-up flow | SHIPPED | Email/password + Google SSO. Company name collected |
| Role selection during signup | PARTIAL | Dropdown exists. Not yet used to personalize experience |

### 4.2 Company Profile Setup (AI-Powered)

This is a 4-step wizard at `/setup`: Company, Audience, Voice, and Done.

**Step 1: Company** — The user enters company name, website URL, industry (B2B SaaS, Cybersecurity, Data & Analytics, AI/ML, Fintech, Healthcare IT, Developer Tools, Enterprise Software, or Other), and core value proposition. The magic: entering a website URL and clicking **Analyze Website** triggers a Claude API call that scrapes the company's homepage, about page, and product pages. Claude extracts structured data — company description, differentiators, competitors, target personas, industry topics, and tone/voice signals. A loading state shows for 30–60 seconds while the async job runs (202 Accepted pattern with job polling every 1.5 seconds).

**Step 2: Audience (ICP Definition)** — The user defines their Ideal Customer Profile: who they sell to (target titles), company sizes, and problems they solve. AI analysis results pre-fill suggestions where available.

**Step 3: Voice** — The user selects communication tone: Executive (formal, data-driven), Conversational (warm, approachable), Direct (no fluff), or Consultative (advisory, strategic). This is stored in `company_profiles.messaging.tone` and applied to every AI-generated email and document.

**Step 4: Done** — Summary card + two CTAs: Go to Dashboard (primary) and Edit Profile (secondary).

> **Why This Matters**
>
> The website analysis is not a gimmick. It builds the `company_profiles` JSONB record that powers every AI feature downstream. When the platform generates an email campaign, it reads your `messaging.value_props` and `messaging.tone` to match your voice. When it scores a lead, it checks the contact's title against `icp_data.titles`. The quality of onboarding directly determines the quality of everything else.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| 4-step onboarding wizard UI | SHIPPED | All 4 steps render with validation, required fields enforced |
| Website URL analysis (Claude API) | SHIPPED | Async job polling, shows extracted results (description, differentiators, competitors, personas, topics) |
| company_profiles JSONB storage | SHIPPED | Schema exists with icp_data, competitors, products, messaging, personas columns |
| Onboarding backend persistence | SHIPPED | POST/GET/PUT /api/v1/onboarding/profile endpoints wired |
| Onboarding route guard | SHIPPED (main) | AppShell checks onboarding_completed flag, redirects to /setup if incomplete |
| Confidence-scored field review | NOT BUILT | No green/amber/red indicators on AI-extracted fields yet |
| Content library auto-seeding | NOT BUILT | No auto-generation of initial email templates from scraped data |
| Completeness score / progress bar | NOT BUILT | No visual indicator of profile completeness |

### 4.3 CRM Connection

After onboarding, the user can connect their CRM from the Settings page. Two options: Salesforce and HubSpot, each with a Connect button via OAuth (Merge.dev). On success, contacts and opportunities sync into the platform.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| CRM OAuth flow (Merge.dev) | SHIPPED | Salesforce and HubSpot connections work via Settings page |
| CRM sync (contacts + opportunities) | SHIPPED | Contacts and opportunities pull into the platform |
| Opportunity sync with job polling | SHIPPED | "Sync Now" button with async job status updates |
| CRM connection during onboarding | NOT BUILT | Connection only available from Settings, not in onboarding wizard |

### 4.4 First Event Import

The platform guides first-time users with empty states showing two options: Upload Your Event Calendar (CSV) or Create Your First Event (manual). The dashboard never shows a blank screen without guidance.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Manual event creation form | SHIPPED | Full create event form with all fields |
| Bulk event import from CSV/Excel | SHIPPED | BulkEventImportModal with upload, preview, execute (see Section 6.5) |
| Empty state with guidance | SHIPPED | Dashboard empty state shows Import and Create options |

---

## 5. Phase 2: The Dashboard (Command Center)

URL: `/dashboard`. This is what the FM opens every morning at 8:47 AM with their coffee. It answers three questions in 10 seconds: What happened since yesterday? What is at risk? What should I do right now?

The dashboard is fully customizable with drag-and-drop widget reordering, resizable widgets, and configurable KPI cards. Layout persists to localStorage.

### 5.1 KPI Cards

Four customizable metric cards across the top. The user can choose which 4 metrics to display from a registry of 10 available: Active Events, Open Tasks, Total Budget, Pipeline Generated, Upcoming Count, Overdue Tasks, Budget Utilization, Total Events, Total Leads, Tasks Completed. A gear icon opens the selector. Selection persists to localStorage.

All KPI data is computed from real API responses (events, tasks, leads-by-status).

> **Why This Matters**
>
> A VP of Marketing and a Field Marketing Manager care about different numbers. The VP wants pipeline and budget utilization. The FM wants overdue tasks and upcoming events. Customizable KPIs mean the same dashboard serves both without a separate "executive view."

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| 4 configurable KPI cards | SHIPPED | Choose from 10 metrics, gear icon to customize, persists to localStorage |
| Real-time metric calculation | SHIPPED | All values computed from live API data (events, tasks, leads) |

### 5.2 Operating Widgets

Seven draggable widgets in a 2-column grid:

**Upcoming Events** — Next 6 upcoming events with date badges, location, campaign count warning (amber badge if <14 days with 0 campaigns), and status pills. Links to /events and /calendar. Data: `useEvents()`.

**Top Tasks** — Up to 5 tasks assigned to current user, overdue in red, due dates shown. Data: `useMyTasks()` from `/tasks/my`.

**Pipeline by Event** — Horizontal bar chart of top 5 events by pipeline (sourced + influenced). Currency values displayed. Data: aggregated from event pipeline fields.

**Budget by Event** — Stacked progress bars for top 6 events showing spent/allocated. Red if >90% utilization. Data: from event budget fields.

**Leads by Status** — Horizontal stacked bars showing lead distribution by tag (hot/warm/cold/other). Color-coded. Data: `/dashboard/leads-by-status`.

> **Why This Matters**
>
> This is not a reporting dashboard — it's an operating system. Every widget is designed to trigger an action, not just display a number. An event with 0 campaigns and <14 days out gets an amber warning because that's a missed outreach opportunity. A budget bar turning red means the FM needs to reallocate before it becomes a conversation with their VP.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Upcoming Events widget | SHIPPED | Real events data, campaign count warnings, status pills |
| Top Tasks widget | SHIPPED | Real tasks from /tasks/my, overdue highlighting |
| Pipeline by Event widget | SHIPPED | Real pipeline data, horizontal bar chart |
| Budget by Event widget | SHIPPED | Real budget data, color-coded utilization bars |
| Leads by Status widget | SHIPPED | Real lead tag distribution from API |

### 5.3 Action Queue (AI-Powered)

**"What Should I Do Next"** — The standout widget. AI-powered priority list showing up to 5 recommended actions with urgency badges (critical/high/medium/low). Each action has a type (revenue_risk, time_sensitive, optimization, hygiene), title, description, and a direct link to the entity that needs attention.

Data: `useActionQueue()` calling `/dashboard/actions` — the backend uses Claude to analyze the FM's current state across events, tasks, leads, and campaigns, then generates prioritized recommendations. Auto-refetches every 5 minutes.

> **Why This Matters**
>
> This is the first visible piece of the Marq copilot. Instead of the FM scanning 40 events to figure out what needs attention, the platform tells them. "Revenue risk: Dreamforce has 12 hot leads with no follow-up campaign" is worth more than any chart. In V2, each action becomes a one-click execution ("Generate follow-up campaign" button right in the widget).

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| AI action queue widget | SHIPPED | Real AI-generated actions from /dashboard/actions, urgency badges, entity links |
| Auto-refetch (5 min) | SHIPPED | Stays current without manual refresh |

### 5.4 What Changed Feed

Activity feed showing last 8 entries from the past 48 hours — who did what, on which event, when. Data: `/dashboard/activity`.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Activity feed (48-hour window) | SHIPPED | Real activity_log entries with actor, event, timestamp |

### 5.5 Drag-and-Drop Customization

The entire dashboard layout is customizable:

- **Lock/Unlock toggle** — controls edit mode
- **Drag reordering** — widgets become draggable when unlocked with visual feedback (opacity on drag, ring border on drop target)
- **Resize handles** — bottom-right corner handle appears when unlocked; drag past 60% width to auto-expand a widget to full-width (col-span-2)
- **Layout persistence** — saved to localStorage, survives page reload
- **Reset button** — restores default layout

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Drag-and-drop widget reordering | SHIPPED | Full implementation with visual feedback |
| Widget resize (1-col / 2-col) | SHIPPED | Drag handle + threshold-based expansion |
| Layout persistence (localStorage) | SHIPPED | Survives reload and sessions |
| Lock/unlock edit mode | SHIPPED | Clean toggle, only shows handles when unlocked |

---

## 6. Phase 3: Events (The Core Workspace)

Events are the center of gravity in FieldMarq. Everything connects to an event: guests, campaigns, budget, tasks, documents, and attribution. The Event Detail page is where a field marketer lives every day — the equivalent of a deal record in Salesforce, except purpose-built for field marketing operations.

### 6.1 Events List Page

URL: `/events`. Shows all events as cards in a grid layout. Each card displays: event name, dates, location, event type badge, budget bar (allocated vs. spent), guest count, status badge (Active, Planned, Complete, Setup Needed), and **task badges** showing overdue count (red), due-this-week count (teal), and completion ratio.

Top of page: search bar (300ms debounce), filter dropdowns (by status, event type, region), 5 sort options (date asc/desc, name asc/desc, budget desc), and a green + New Event button.

> **Why Task Badges on Event Cards Matter**
>
> An FM scanning 40 events needs to know which ones need attention without clicking into each one. A red "3 overdue" badge on the Dreamforce card means that event needs immediate attention. This is faster than any filtered task view.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Events list with cards | SHIPPED | Cards with name, dates, budget bar, status, type badges |
| Search by name | SHIPPED | 300ms debounced text search |
| Filter by status | SHIPPED | planning, pre_event_active, day_of, post_event, completed |
| Filter by event type | SHIPPED | Dynamic from useEventTypes hook |
| Filter by region | SHIPPED | Regional filter dropdown |
| Sort (5 options) | SHIPPED | Date asc/desc, name asc/desc, budget desc |
| Task badges per event card | SHIPPED | Overdue (red), due this week (teal), completion ratio |
| Pagination | PARTIAL | Hardcoded limit=100, no UI pagination controls |

### 6.2 Creating an Event

Click + New Event to open the creation form. Fields: Event Name, Event Type (dynamic dropdown from event_types table — 15+ types including Conference/Trade Show, Executive Dinner, Happy Hour, Workshop, Webinar, Roadshow, Partner Event, Customer Advisory Board, Field Event + custom text input), Start Date, End Date (auto-syncs to start date), Location/Venue, City/State, Capacity, Budget Allocated, Sponsorship Level, Goals (multi-select), and Notes.

On save, the platform offers the **Checklist Wizard** (see 6.3).

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Event creation form | SHIPPED | All fields, dynamic event type dropdown + custom input |
| End date auto-sync | SHIPPED | Selecting start date auto-sets end date |
| Multi-select goals | SHIPPED | Pick multiple event goals from predefined list |
| Sponsorship as free text | SHIPPED | Not locked to dropdown — flexible input |

### 6.3 Checklist Wizard and Template System

After creating an event, a modal offers to generate a checklist from the matching event type template. The system includes 14 event type templates with 350+ tasks across 85+ milestones, each with backward-from-date offsets (tasks auto-calculate due dates from the event date, skipping weekends).

The wizard shows the generated checklist grouped by milestone phase (Planning, Pre-Event, Day-Of, Post-Event). The FM can customize tasks, then optionally "Save as Template" for future events. Custom templates appear in a dropdown alongside built-in templates.

> **Why Backward-From-Date Offsets**
>
> FMs think in "X weeks before the event." A venue needs booking 12 weeks out, shipping 3 weeks out, name badges 1 week out. The system calculates from the event date backward so every due date is automatically correct. Change the event date? All task dates recalculate.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Checklist wizard modal | SHIPPED | Post-creation modal with template generation |
| 14 event type templates | SHIPPED | 350+ tasks, 85+ milestones, backward offsets |
| Due date auto-calculation | SHIPPED | Backward from event date, skips weekends |
| Save as Template | SHIPPED | Custom templates saved for future events |
| Custom event type input | SHIPPED | Text input when no built-in type matches |

### 6.4 Checklist Reconciliation (Event Type Change)

When an FM changes an event's type (e.g., Conference to Executive Dinner), the platform shows a reconciliation modal previewing three task buckets:

- **Keep** — Tasks that exist in both templates (locked, cannot modify)
- **Remove** — Tasks only in the old template (toggleable, but completed tasks are always preserved)
- **Add** — Tasks from the new template (toggleable)

Completed and in-progress tasks are locked with visual indicators (lock icons). The FM reviews and confirms before the system soft-deletes removed tasks and inserts new ones. Activity log records the reconciliation.

> **Why This Matters**
>
> An FM realizes two weeks before the event that their "Conference" is actually more of a "Workshop." Without reconciliation, they'd lose all their completed tasks or start over. This preserves work done while adapting the remaining checklist to the new event type.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Reconcile preview (keep/remove/add) | SHIPPED | Full preview with three buckets, lock icons on completed tasks |
| Reconcile execute | SHIPPED | Soft-deletes removed, inserts new, preserves completed |
| Activity log entry | SHIPPED | Reconciliation logged for audit trail |

### 6.5 Bulk Event Import

For FMs who manage events in spreadsheets. The BulkEventImportModal accepts CSV/Excel files (.xlsx, .xls, .csv) via drag-and-drop or file picker. Three-step flow:

1. **Upload** — File parsed, columns mapped to FieldMarq fields
2. **Preview** — Table showing parsed events (name, type, status, date, location, region, budget) with expandable rows showing budget line items. Warnings displayed with yellow highlights. Select/deselect checkboxes per event.
3. **Execute** — Confirmation modal with summary (event count, total budget). Events created in batch. Result screen shows import count + total budget. Auto-redirects to /events after 3 seconds.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| CSV/Excel upload | SHIPPED | Drag-drop or file picker, accepts .xlsx/.xls/.csv |
| Column mapping + preview table | SHIPPED | Parsed events with expandable budget rows, warnings |
| Batch execute with confirmation | SHIPPED | Summary modal, batch creation, result screen |
| Import audit trail | SHIPPED | Tracked via event_import_batches table (migration 018) |

### 6.6 Event Detail: Overview Tab

URL: `/events/:id`. Page header shows event name, date range, days-until countdown, budget, and status. Below: 8 tabs (Overview, Tasks, People, Outreach, Budget, Documents, Content, Results).

Overview shows: RSVP/guest count with breakdown (confirmed/registered/declined/waitlisted), Budget Overview bar (allocated vs. spent with percentage), Task Progress bar (complete vs. total), Quick Actions row (lifecycle-aware — different buttons for planning/pre-event/day-of/post-event phases), Event Details card with 19 operational fields (date, time, venue, address, capacity, event type, tier, business objective, booth size — each editable), and an Event Health Indicator.

**Event Health Indicator** — Color-coded status (green/amber/red/grey) with a smart summary line that changes based on lifecycle phase. Pre-event: "X tasks overdue." Day-of: "Y guests not yet confirmed." Post-event: "Z follow-ups pending." This gives the FM instant situational awareness without scanning every tab.

> **Why 19 Operational Fields**
>
> An FM needs to know parking details, WiFi password, venue contact phone, catering style, dress code, and lead retrieval method. These aren't "nice to have" — they're what gets asked at 7am on event day. Having them in the platform means the KBYG generator and Operations Guide report can pull them automatically instead of the FM writing them from memory.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Event header with countdown | SHIPPED | Name, dates, days-until, budget, status |
| Budget Overview bar | SHIPPED | Allocated vs. spent with percentage |
| Task Progress bar | SHIPPED | Complete/total with percentage |
| Event Details card (editable) | SHIPPED | Core fields + 19 operational fields (tier, objective, venue details, catering, dress code, booth size, etc.) |
| 19 operational fields (migration 011) | SHIPPED (main) | Event tier, business objective, target ICP, internal code, venue address/contact/room/capacity/setup/parking/wifi, catering style, dress code, booth size, organizer contact, lead retrieval method |
| Quick Actions row (lifecycle-aware) | SHIPPED (main) | Different action buttons based on event phase (planning/pre-event/day-of/post-event) |
| Event Health Indicator | SHIPPED (main) | Green/amber/red/grey status with smart summary line |
| RSVP KPI breakdown | SHIPPED (main) | Confirmed/registered/declined/waitlisted counts on Overview |
| Event Timeline with milestones | SHIPPED | Milestone markers render |

### 6.7 Event Detail: Tasks Tab (with Dependencies)

The Tasks tab is where operational rigor lives. Tasks are grouped by **milestone phase** (Planning, Pre-Event, Day-Of, Post-Event) with progress bars per phase. Each task shows: name, due date, milestone badge, completion status, and dependency indicators. Overdue tasks appear in red with a days-overdue counter.

The FM can: mark tasks done with a single click, add custom tasks, edit task details in a side panel (status, notes with auto-timestamp, Ctrl+S to save), navigate tasks with keyboard shortcuts (arrow keys, Esc to close panel), and **set task dependencies** (blocking relationships between tasks).

**Task Dependencies** (migration 012 on main): Tasks can depend on other tasks within the same event. The task edit modal shows a "Dependencies" section — current dependencies as removable amber pills, and a dropdown to add new dependencies. Blocked tasks show a visual indicator (disabled checkbox, grayed text). When a dependency is marked complete, unblock notifications fire. The system prevents self-dependencies and cycles via recursive CTE validation.

**Auto-resolution:** Pre-event and day-of tasks auto-mark complete when the event date passes. Post-event tasks auto-resolve 14 days after the event ends. Resolved tasks show `resolved_reason='assumed_complete'`.

> **Design Decision: Task Title Customization**
>
> The FM renames the display title freely (e.g., "Book venue" becomes "Reserve private dining room at The Guild"). The `platform_task_id` foreign key preserves the link to the canonical template task for analytics. In V2, Claude silently re-classifies renamed tasks and only interrupts when confidence is low.

> **Why Task Dependencies Matter**
>
> "Ship swag" can't happen until "Finalize swag design" is done. Without dependencies, an FM has to mentally track these chains across 50+ tasks. With dependencies, the platform grays out blocked tasks and auto-notifies when a blocker clears. This is the foundation for critical path analysis in V2.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Task list grouped by milestone/phase | SHIPPED | Phase grouping with progress bars, milestone badges |
| Overdue task highlighting | SHIPPED | Red background, overdue badge, separate filter tab |
| Single-click completion | SHIPPED | Toggle checkbox to complete/uncomplete |
| Task detail side panel | SHIPPED | Status, notes (auto-timestamp), keyboard shortcuts |
| Auto-resolution (pre-event/day-of) | SHIPPED | Scheduler auto-resolves when event date passes |
| Auto-resolution (post-event, 14d) | SHIPPED | Post-event tasks resolve 14 days after event |
| Custom task addition | SHIPPED | Add task button with milestone assignment |
| Task dependencies (blocking) | SHIPPED (main) | Add/remove dependencies in task modal, cycle prevention, blocked visual indicator, unblock notifications |
| Per-task owner assignment | NOT BUILT | All tasks owned by event creator |

### 6.8 Event Detail: People/Guests Tab (with RSVP Workflow)

Manages everyone associated with an event. Top actions: Add Guests, Upload CSV. The guest table shows: Name, Email, Organization, Title, engagement signals (booth visit, demo requested, session attended, badge scanned), Score with color-coded indicator, Lead Tag badge (hot/warm/cold/priority/dne), and **RSVP status**.

**RSVP Workflow** (on main): 7 statuses — invited, registered, confirmed, declined, waitlisted, cancelled, no_show. Per-guest dropdown in the table to change status. Status filter to view guests by RSVP state. Overview tab KPI breakdown shows confirmed/registered/declined/waitlisted counts.

Clicking a guest row opens the **Lead Detail Drawer** (see Section 9.4) — a full side panel with score breakdown, notes, AE notes, engagement signals, disposition controls, and Save & Next navigation.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Guest list table with scores | SHIPPED | Names, titles, scores, engagement signals, lead tags |
| CSV upload for guests | SHIPPED | Drag-and-drop CSV upload on the tab |
| Lead Detail Drawer on row click | SHIPPED | Full side panel (see Section 9.4) |
| Guest search and filters | PARTIAL | Basic search. Filter by lead tag works. RSVP status filter on main |
| RSVP lifecycle (7 statuses) | SHIPPED (main) | invited, registered, confirmed, declined, waitlisted, cancelled, no_show — per-guest dropdown |
| RSVP status filter | SHIPPED (main) | Filter guest list by RSVP status |
| AI talking points per guest | NOT BUILT | No AI conversation starters from CRM + event context |
| Import from CRM | NOT BUILT | No CRM contact import with search/filter |

### 6.9 Event Detail: Outreach/Campaigns Tab

Shows all campaigns associated with this event. Campaign table: name, type, status, recipients, open/click rates, scheduled date. Create Campaign button opens the campaign creation modal.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Campaign list with metrics | SHIPPED | Real campaign data with open/click rates |
| Create Campaign from event | SHIPPED | Opens CreateCampaignModal scoped to this event |

### 6.10 Event Detail: Budget Tab

Tracks every dollar. Budget bar (allocated vs. spent with percentage) and a table of expense line items. Each expense: vendor name, category (Venue, Catering, AV, Swag, Shipping, Travel, Sponsorship, Miscellaneous), amount, date, and notes. Adding an expense opens a modal.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Budget overview bar | SHIPPED | Allocated vs. spent with percentage |
| Expense line items (CRUD) | SHIPPED | Add, edit, delete expenses with categories |
| Vendor management | NOT BUILT | Vendors page is a shell. No vendor records or contract tracking |
| Invoice upload + AI extraction | NOT BUILT | No receipt upload. No Claude Vision extraction |
| Budget variance alerts | NOT BUILT | No amber/red alerts when approaching budget limits |

### 6.11 Event Detail: Documents Tab

Upload and manage event documents. Supports prospectus upload with AI extraction, and **three AI-generated document types** that pull from event data, guest intelligence, CRM context, and company profile.

**AI Document Generators** (on main):

1. **Know Before You Go (KBYG)** — Generates a guide for staff attending the event. Pulls event details, venue info, guest list, and operational fields to create a minute-by-minute timeline with vendor contacts, dietary notes, and logistics.

2. **Executive Briefing** — AI-generated intelligence document for attending execs. Sections: Executive Summary, Key Attendees to Meet (grouped by org), Account Intelligence (matching attendees to pipeline opportunities), Talking Points, Meeting Priorities (top 5 suggested 1:1s with reasoning), and Logistics Quick Reference. Pulls from confirmed/registered guests + top 20 CRM opportunities.

3. **Sales Team Brief** — Per-AE briefing with color-coded lead cards. Hot leads (score ≥70) get individual cards with name, title, company, engagement signal, and suggested follow-up. Warm leads (40-69) get grouped summary. Cold leads (<40) get count with nurture recommendation. Includes "Suggested Next Steps" section with specific 48-hour action items.

All three use the 202 Accepted async pattern (job polling) and are accessible via "Generate" buttons on the Documents tab.

> **Why Auto-Generated Event Documents**
>
> An FM spends 2-4 hours before every event writing a KBYG guide and briefing deck. With 40+ events per year, that's 80-160 hours of document creation. The AI generators produce these in seconds from data that already exists in the platform. The executive briefing is particularly valuable — it cross-references attendees against CRM pipeline to surface which conversations matter most.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Document upload/list/delete | SHIPPED | Full CRUD for event documents |
| Prospectus upload (ProspectusUploadV2) | SHIPPED | Dedicated prospectus upload component |
| AI prospectus extraction | PARTIAL | Schema exists (event_prospectus_extractions). Claude extraction endpoint exists. Not fully wired to frontend display |
| KBYG auto-generation | SHIPPED (main) | Generate button on Documents tab, AI-generated guide with job polling |
| Executive Briefing auto-generation | SHIPPED (main) | AI-generated attendee intelligence + account analysis + meeting priorities |
| Sales Team Brief auto-generation | SHIPPED (main) | Color-coded lead cards (hot/warm/cold) with follow-up suggestions |

### 6.12 Event Detail: Content Tab

Content items associated with this event. Read-only view linking to the Content Library.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Content tab display | SHIPPED | Shows content items linked to event |

### 6.13 Event Detail: Results/ROI Tab (Report Engine)

The Results tab is powered by the **Report Engine** — FieldMarq's AI-powered reporting system. It shows 11 event-level report types, each generated on demand by Claude. Every report has a "Generate" button that triggers an AI call, and results are cached in the `report_snapshots` table for instant retrieval on subsequent visits.

Each report renders with: KPI grid (currency, percentages, counts), visual charts (bar charts, donut charts, progress bars), data tables, and an AI-generated narrative that reads like a human analyst wrote it. Dual-view mode: "Visual" (charts) and "Narrative" (prose).

The 11 event-level report types are covered in detail in Section 11.4.

> **Why We Built a Full Report Engine**
>
> FMs spend days building post-event slide decks manually. The report engine generates a CMO-ready summary in seconds. More importantly, the reports are consistent — every event gets the same analytical rigor, so portfolio-level comparisons are meaningful. The narrative mode means an exec can read the report without interpreting charts.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Results tab with 11 report types | SHIPPED | All 11 event-level reports with generate + view |
| AI report generation (Claude) | SHIPPED | Each report generated by claude-sonnet-4 with custom prompts |
| Report snapshot caching | SHIPPED | Results stored in report_snapshots, instant on revisit |
| KPI grids + charts | SHIPPED | Dynamic rendering from structured API response |
| Narrative mode | SHIPPED | AI-generated prose with formatting (bold, currency) |
| Regenerate button | SHIPPED | Refresh any report with latest data |

---

## 7. Phase 4: Global Tasks Page

URL: `/tasks`. A cross-event view of every task the FM is responsible for. Tasks are organized in two major sections:

- **Post-Event** — Tasks for events that have already occurred (auto-resolved or pending post-event follow-up)
- **Active & Upcoming** — Tasks grouped by event, then by category/milestone

Each event group shows as a card with: event name, date, task count, overdue count, and expandable task list. Tasks show milestone badges, due dates, and status. Clicking a task opens a detail panel with full editing (status dropdown, notes with auto-timestamp, keyboard shortcuts).

Filter tabs: All, Overdue, Due Today, Due This Week. Overdue tasks get red badges and highlighting.

> **Why a Global Tasks Page**
>
> An FM running 40 events can't click into each one to check tasks. The global view answers "what do I need to do today across everything?" It's also the data source for the Dashboard's "Top Tasks" widget and the Action Queue's task-related recommendations.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Cross-event task view | SHIPPED | All tasks across all events in one page |
| Group by event with cards | SHIPPED | Event cards with task counts, overdue counts |
| Phase/milestone grouping | SHIPPED | Tasks grouped by category within events |
| Overdue highlighting | SHIPPED | Red badges, red backgrounds, filter tab |
| Task detail panel | SHIPPED | Status, notes, keyboard nav (arrows, Esc, Ctrl+S) |
| Filter tabs (All/Overdue/Today/Week) | SHIPPED | Real-time filtering |
| Bulk multi-select | NOT BUILT | One task at a time via detail panel |

---

## 8. Phase 5: Calendar

URL: `/calendar`. A visual time-based view of everything happening across the FM's portfolio. Two view modes:

- **4-Week Grid** (default) — Monthly overview showing all items per day
- **1-Week Detail** — Zoomed-in weekly view

Shows 5 item types with distinct visual treatment: Events (with days-until, lead count, budget), Tasks (with phase badge), Milestones (with task progress bar and overdue indicator), Campaigns (with type and recipient count), and Vendor Payments (with amount due).

Right panel shows **Day Detail** — click any date to see all items for that day in a detailed list. Overdue count per day shown as badges.

**Calendar Copilot** (CalendarCopilot component) — The first Marq copilot frontend component. Available on the calendar page for AI-powered scheduling assistance.

> **Why Calendar is a Separate Page (Not Just a Widget)**
>
> FMs coordinate across events. "Can I run the exec dinner the same week as Dreamforce prep?" requires seeing everything in time context. The calendar is the spatial view that complements the list view (Events page) and the priority view (Dashboard). It's also the primary surface for Marq copilot in V2 — scheduling conflicts, optimal timing suggestions, and resource balancing all live here.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| 4-week grid view | SHIPPED | Monthly overview, all 5 item types |
| 1-week detail view | SHIPPED | Zoomed weekly view |
| Day detail panel | SHIPPED | Click date to see all items |
| Events with lead count + budget | SHIPPED | Real event data on calendar |
| Tasks with phase badges | SHIPPED | Real tasks on calendar |
| Milestones with progress | SHIPPED | Progress bar, overdue indicator |
| Campaigns with recipient count | SHIPPED | Real campaign data |
| Vendor payments with amounts | SHIPPED | Payment items on calendar |
| CalendarCopilot component | SHIPPED | AI copilot component renders (first Marq handler) |
| Calendar copilot backend | SHIPPED | POST /api/v1/calendar/copilot — multi-turn AI chat with calendar context |

---

## 9. Phase 6: Contacts and Lead Processing

The Contacts section is FieldMarq's core "aha moment." Upload a messy CSV from any event platform, and within minutes see scored, tagged, deduplicated leads ready for follow-up campaigns and CRM push. This replaces 3–5 days of manual spreadsheet work with a single drag-and-drop.

### 9.1 Contacts List Page

URL: `/contacts`. Table showing all contacts across all events: Name, Email, Organization, Title, Events attended count, Engagement Score (color-coded), and Lead Tag badge (hot/warm/cold/priority/dne/unscored).

Top of page: search bar (300ms debounce by name/email/org), Lead Tag filter dropdown, and a **Find Duplicates** button that opens a dedup modal.

Clicking any row opens the **Contact Detail Modal** showing: contact info, lead intelligence, score breakdown, event history, edit form, and delete (with confirmation).

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Contact list table | SHIPPED | Name, Email, Org, Title, Events, Score, Lead Tag columns |
| Search by name/email/org | SHIPPED | 300ms debounced text search |
| Lead Tag filter | SHIPPED | Filter by hot/warm/cold/priority/dne/unscored |
| Contact detail modal | SHIPPED | Full info, score breakdown, event history |
| Edit contact (inline) | SHIPPED | Edit name, title, org, phone, industry in modal |
| Delete contact | SHIPPED | Confirmation dialog, soft delete |
| Find Duplicates button | SHIPPED | Opens duplicate detection modal |

### 9.2 CSV Upload Pipeline

The technical heart of the Contacts section. Flow: FM drags a CSV onto the upload zone (or clicks to browse). The file is validated, columns are mapped (synonym dictionary handles headers from Cvent, Splash, Bizzabo, HubSpot, badge scanners), and the pipeline processes each row: validates emails, normalizes data, creates contact_profiles records, links to the global attendees identity table, parses AE notes for keywords (hot lead, demo requested, DNE, competitor mentions), runs the scoring engine, auto-tags by score threshold, and writes activity touchpoints.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| CSV upload handler + API | SHIPPED | POST /api/v1/events/:id/csv/upload — file parsing, profile creation, scoring, tagging |
| Column mapping engine | PARTIAL | Basic header matching works. No confidence scoring, no Claude fallback for unknown formats |
| Profile creation + attendee linking | SHIPPED | contact_profiles and attendees records created on upload |
| AE notes keyword parsing | SHIPPED | ae_notes_parsed JSONB populated |
| Scoring on upload | SHIPPED | V2 scoring engine runs on every upload |
| Data validation/normalization | PARTIAL | Basic email check. No E.164 phone normalization, no advanced name splitting |
| Post-upload summary cards | NOT BUILT | No visual summary after upload showing hot/warm/cold breakdown |

### 9.3 Lead Scoring Engine (V2)

The scoring engine transforms raw CSV rows into prioritized, actionable leads. V2 is a standalone engine (`scoring/engine_v2.go`) replacing the inline function that was in csv_upload.go.

Scoring uses configurable weights stored in `scoring_config` (not hardcoded). Signal types include: contact info quality, title/seniority matching, behavioral signals (booth visit, demo, session, badge scan), ICP matching (title, company, industry, persona), AE note keywords, engagement tier, and manual overrides. The ICP handler allows per-event ICP configuration and company-wide ICP templates.

Score thresholds auto-tag leads: Hot (70-100), Warm (40-69), Cold (10-39), DNE (AE-flagged, excluded from all campaigns).

The FM can configure scoring weights via **ScoringConfigSliders** — 6 weight groups with 15+ sliders (contact, title, behavioral, ICP, engagement, thresholds) with save/reset to API.

> **Why V2 Scoring is a Standalone Engine**
>
> V1 had scoring inline in csv_upload.go — the only path. That meant rescoring required re-uploading. V2 is a standalone package that any handler can call: CSV upload, manual rescore, bulk rescore, and eventually the copilot's auto-tune. Same engine, many entry points. The configurable weights table means AI can tune scoring in V2 without code changes.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| V2 scoring engine (standalone) | SHIPPED | scoring/engine_v2.go — single source of truth |
| Scoring config weights (tunable) | SHIPPED | scoring_config table, seeded with initial weights |
| ScoringConfigSliders UI | SHIPPED | 6 groups, 15+ sliders, save/reset to API |
| ICP templates (company-wide) | SHIPPED | CRUD for ICP templates via icp_handler.go |
| Per-event ICP configuration | SHIPPED | EventICPEditor component + apply-template |
| Score breakdown panel | SHIPPED | Signal-by-signal breakdown in 6 categories (contact, behavioral, ICP, title, AE notes, other) |
| Rescore routes (single/event/company) | SHIPPED | V1 + V2 rescore endpoints all wired |
| ICPTemplateSelector UI | SHIPPED | Template picker component |

### 9.4 Lead Detail Drawer

The LeadDetailDrawer is a full side panel that opens when clicking any lead/guest row. It shows:

- **Contact info** — email, organization, title, phone, LinkedIn (clickable)
- **Engagement signals** — booth visit, demo requested, session attended, badge scanned (visual indicators)
- **Score breakdown** — collapsible panel showing every signal and its point contribution, categorized into 6 groups
- **Lead tag** — hot/warm/cold/priority/dne as pill buttons
- **Had conversation toggle** — boolean flag for follow-up tracking
- **Notes** — editable textarea for FM notes
- **AE Notes** — read-only from CSV (sacred — never overwritten)
- **Engagement tier + title tier** — from scoring engine
- **Disposition** — dropdown with 8 options + custom input, manual_notes field

Keyboard shortcuts: arrow keys to navigate between leads, Escape to close, Ctrl+S to save, "Save & Next" button for rapid review.

> **Why "Save & Next" Matters**
>
> An FM reviewing 300 leads after an event needs to move fast. Tag, note, next. Tag, note, next. The drawer with keyboard shortcuts and Save & Next means reviewing 300 leads takes 30 minutes instead of 3 hours of clicking in and out of modals.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Lead detail side panel | SHIPPED | Full panel with all fields |
| Score breakdown (signal-by-signal) | SHIPPED | 6 categories, expandable, point values shown |
| Lead tag pill buttons | SHIPPED | hot/warm/cold/priority/dne selection |
| Disposition dropdown | SHIPPED | 8 options + custom input |
| Keyboard shortcuts (arrows, Esc, Ctrl+S) | SHIPPED | Rapid navigation and save |
| Save & Next button | SHIPPED | Save current lead, auto-advance to next |
| AE Notes (read-only) | SHIPPED | Sacred — never overwritten |
| CRM status badge + link | NOT BUILT | No sync status badge. No link to Salesforce/HubSpot record |
| Campaign history per contact | NOT BUILT | No record of campaigns sent to this contact |

### 9.5 Deduplication and Merge

The Find Duplicates button on the Contacts page opens a dedup modal. The system searches for contacts with matching names + organizations but different emails — potential duplicates.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Find Duplicates button | SHIPPED | Button triggers duplicate search |
| Duplicate detection algorithm | PARTIAL | Name + org matching. No fuzzy matching, no email domain matching |
| Merge UI | PARTIAL | Basic merge available. No side-by-side field-by-field selection |
| Merge with 30-day undo | NOT BUILT | merge_audit table exists. No undo handler |
| CRM dedup (cross-reference) | NOT BUILT | No dedup against CRM contacts |

---

## 10. Phase 7: Campaigns and Email

Campaigns are the outreach engine. Every campaign is tied to an event and a segment of contacts. The platform supports pre-event invitations, post-event follow-ups, reminders, KBYG distribution, and thank-you sends.

### 10.1 Campaigns List Page

URL: `/campaigns`. Table showing all campaigns across all events: Event, Campaign Name, Type, Status (Draft/Scheduled/Sent/Cancelled), Recipients, Open Rate, Click Rate, Scheduled date. Filters by event, status, and campaign type. Pagination (25 per page). + Create Campaign button.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Campaign list with metrics | SHIPPED | Real data, pagination, filters by event/status/type |
| Clone campaign | SHIPPED | Available in campaign detail modal |

### 10.2 Create Campaign Modal

Single-step form: select Event, Campaign Name, Type (Pre-Event, Post-Event, Reminder, Follow-Up, KBYG, Thank You), Target Segment, optional schedule date/time with timezone, and a collapsible **AI Brief** section (purpose, key message, CTA, tone override). Content Library picker lets the FM select content items that Claude will reference in generated emails.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Create Campaign modal | SHIPPED | Full form with AI brief, content library picker |
| Content Library integration | SHIPPED | Select content items for Claude to reference in emails |

### 10.3 AI Email Generation

The feature that makes people say "wait, really?" Claude generates personalized emails for every recipient using four layers of context:

1. **Company profile** — messaging, tone, value props from onboarding
2. **Content library** — matching content to each contact's persona and funnel stage
3. **Event details** — name, date, location, theme
4. **Per-contact context** — title, company, engagement signals, AE notes

The result: each email sounds like the FM personally wrote it, referencing relevant content with a personalized CTA. The FM previews each email in rendered HTML and can edit before sending.

Generation uses the 202 Accepted async pattern — the backend returns a job ID, and the frontend polls for completion.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| AI email generation (Claude) | SHIPPED | Personalized HTML emails from 4 context layers |
| Email preview (rendered HTML) | SHIPPED | Preview modal renders generated HTML |
| Async generation with job polling | SHIPPED | 202 Accepted pattern, progress indication |
| Mobile preview toggle | NOT BUILT | No responsive preview mode |
| Multi-step sequences | NOT BUILT | Single sends only. No invite > reminder > KBYG > thank you drip |

### 10.4 Dynamic Segment Builder

Build audience segments with configurable rules. Available filters: Lead Score (numeric operators), Lead Tag (hot/warm/cold), Title/Organization (text contains/equals), behavioral signals (booth visit, demo, session, badge — boolean), Engagement Tier (high/medium/low), Title Tier (C-suite/VP/Director/Manager/Individual), CSV Lead Status.

Preview button calls the API and shows match count + sample contacts. Segments can be saved and reused.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Rule-based segment builder | SHIPPED | Multiple filter types with appropriate operators |
| Segment preview (match count) | SHIPPED | Real API call showing matched contacts |
| Save custom segments | SHIPPED | Persist and reuse segments across campaigns |

### 10.5 Email Review Panel

Before sending, the FM reviews each email individually. The panel shows: contact info, engagement signals, email subject + body in rendered HTML (iframe), and review status (pending/approved/edited/skipped). Progress bar shows approved vs. pending.

The FM can: edit subject and body HTML (contenteditable), approve, skip, or send a test email to themselves. Keyboard shortcuts for rapid review.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Email review panel | SHIPPED | Per-email review with rendered HTML preview |
| Edit subject + body | SHIPPED | Inline editing of generated content |
| Approve/Skip/Test Send | SHIPPED | Full review workflow |
| Progress bar (approved vs pending) | SHIPPED | Visual progress through email list |
| Keyboard shortcuts | SHIPPED | Rapid navigation |

### 10.6 Email Review Queue — 3-Panel Layout

A more advanced review interface built on main. Full-screen overlay with three panels:

- **Left panel** — Contact navigator with search + filter buttons (All, Pending, Approved, Rejected, Skipped)
- **Center panel** — Email preview with desktop/mobile toggle, subject + recipient info
- **Right panel** — Contact context showing title, company, lead_score, event_history, AE_notes

Per-email actions: Approve (green checkmark), Reject (red X with reason input), Skip, and Regenerate (opens RegenerateModal). **"Approve All"** bulk action when pending count > 0. Completion state shows green "Review Complete" with "Ready to Send" button. Auto-navigates to next pending email after each action. Previously-reviewed emails can have their decisions changed.

Review statuses tracked in DB (migration 010): pending_review, approved, rejected, skipped. SendCampaign now automatically excludes rejected/skipped emails.

> **Why Two Review Interfaces**
>
> The Email Review Panel (10.5, Aubs-updates) is a lightweight inline review. The Review Queue (10.6, main) is a full-screen dedicated workflow with contact context. They serve different use cases: quick review of 10 emails vs. thorough review of 300 emails with AE context for each. Both will coexist after merge.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| 3-panel review queue | SHIPPED (main) | Full-screen overlay with contact navigator, email preview, contact context |
| Desktop/mobile preview toggle | SHIPPED (main) | Switch between desktop and mobile email rendering |
| Approve/Reject/Skip per email | SHIPPED (main) | Individual review with reject reason input |
| Approve All bulk action | SHIPPED (main) | One-click approve all pending emails |
| Review completion state | SHIPPED (main) | Green "Review Complete" + "Ready to Send" button |
| Change previous decisions | SHIPPED (main) | Re-review already-decided emails |
| Review status in DB (migration 010) | SHIPPED (main) | pending_review, approved, rejected, skipped with reject_reason |

### 10.7 Email Scheduling and Sending

Emails sent through SendGrid. Timezone-aware scheduler (schedule_handler.go) handles scheduling with ParseAndValidate, Upsert, Cancel, and GetSchedule operations. The CampaignDetailModal shows schedule status bar when a send is pending.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| SendGrid send | SHIPPED | Email delivery via SendGrid |
| Timezone-aware scheduling | SHIPPED | Schedule with timezone, cancel, reschedule |
| Webhook tracking (delivery/open/click) | PARTIAL | SendGrid webhook endpoint exists. Tracking back to campaign_emails partially wired |

### 10.8 Campaign Clone

Clone any existing campaign to create a new one with the same settings, segment, and AI brief. Available from the campaign detail modal.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Campaign clone | SHIPPED | One-click clone from detail modal |

### 10.9 Campaign Pause/Resume

Scheduled campaigns can be paused and resumed. Pause button appears on scheduled campaigns (not drafts). Resume returns the campaign to its previous state. If the campaign is part of a sequence, pausing cascades to the parent sequence.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Pause campaign | SHIPPED (main) | Pause button on scheduled campaigns |
| Resume campaign | SHIPPED (main) | Resume returns to previous state |
| Sequence cascade | SHIPPED (main) | Pausing a sequence step pauses the parent sequence |

### 10.10 Send Confirmation Modal

Before sending, a confirmation modal replaces the browser's window.confirm with a proper UI. Shows: send summary (approved/rejected/skipped counts), "Send Now" vs "Schedule" toggle, timezone picker for scheduled sends, tracking checkboxes (track opens/clicks), and an optimal send time tip.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Send confirmation modal | SHIPPED (main) | Rich confirmation UI with summary counts, schedule toggle, timezone picker |

### 10.11 CAN-SPAM Unsubscribe Compliance

Every outgoing email now includes an unsubscribe footer injected automatically before send. The `injectUnsubscribeFooter()` function adds an unsubscribe link and company mailing address to both SendCampaign and SendSingleEmail paths. Contacts with `email_consent = false` are automatically excluded from all sends.

> **Why This Was a Legal Blocker**
>
> Without CAN-SPAM compliance, FieldMarq could not legally send marketing emails. This was flagged as a compliance risk in V1 and is now resolved. Every email includes an unsubscribe mechanism and physical mailing address as required by federal law.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Unsubscribe footer injection | SHIPPED (main) | Automatic on all campaign emails |
| Email consent check | SHIPPED (main) | Contacts with consent=false excluded from sends |
| Company mailing address in footer | SHIPPED (main) | Configurable per company |

### 10.12 Email Sequences (Multi-Step Campaigns)

Sequences are multi-step email campaigns — invite → reminder → KBYG → thank you — where each step triggers automatically based on configurable delays. This was the most requested feature from the "NOT BUILT" list.

**How it works:** The FM creates a sequence, adds steps (each step is a campaign with a delay in days and content focus), and enrolls contacts. The **Sequence Worker** (background job running every 5 minutes) checks for due enrollments and advances them to `pending_review` status — the FM must approve each batch before emails generate. This preserves the human-in-the-loop principle while automating the timing.

**Database:** Migration 009 adds `sequences`, `sequence_enrollments`, and `sequence_events` tables. The `campaigns` table is extended with `sequence_id`, `step_order`, `delay_days`, `step_status`, `content_focus`, and `content_item_ids`.

**Frontend:** Sequences page with CreateSequenceModal, SequenceDetail (shows steps with status pills, enrollments table, audit trail), and AddStepModal.

> **Why Sequences Are "Pending Review" Not "Auto-Send"**
>
> An FM needs to see what's going out before it goes out. Auto-sending 300 emails without review is a career risk. The sequence worker advances steps to "pending review" and notifies the FM — they approve, review emails, then send. This matches the copilot-first design: the system does the work, the human confirms.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Sequence CRUD | SHIPPED (main) | Create, view, edit, delete multi-step sequences |
| Add/update/remove steps | SHIPPED (main) | Each step has delay_days, content_focus, campaign_type |
| Enroll contacts | SHIPPED (main) | Idempotent enrollment with status tracking |
| Sequence worker (5-min ticker) | SHIPPED (main) | Auto-advances due steps to pending_review |
| Pause/resume individual enrollments | SHIPPED (main) | Per-contact enrollment control |
| Sequence audit trail | SHIPPED (main) | Immutable event log (sequence_events table) |
| "sequence_step_ready" notification | SHIPPED (main) | FM notified when a step is due for review |

### 10.13 Re-engagement Worker (Automated)

A background worker (runs daily) that automatically creates draft re-engagement campaigns for stale post-event contacts. Fires when: an event ended 30+ days ago, had at least one sent campaign, has 3+ disengaged contacts (zero opens on any email), and doesn't already have a re-engagement campaign.

The worker auto-creates a draft campaign with a pre-filled AI prompt: low-pressure, acknowledge the time gap, provide new value, soft CTA. The FM reviews and sends (or deletes) — the worker never sends automatically.

Broadcasts a "reengagement_created" notification so the FM knows a draft is waiting.

> **Why Auto-Create Drafts, Not Auto-Send**
>
> Re-engagement is a judgment call. Some events don't warrant follow-up (one-off happy hours). The worker surfaces the opportunity and writes the brief — the FM decides whether to act. This is the copilot pattern: platform proposes, human disposes.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Re-engagement worker (daily) | SHIPPED (main) | Auto-creates draft campaigns for stale post-event contacts |
| Pre-filled AI prompt | SHIPPED (main) | Low-pressure re-engagement brief ready for review |
| "reengagement_created" notification | SHIPPED (main) | FM notified when draft is available |

---

## 11. Phase 8: Reports and Intelligence

The Report Engine is FieldMarq's AI-powered reporting system — 18 report types generated on demand by Claude. This is a major feature area, not a subsection.

### 11.1 Reports Hub

URL: `/reports`. Four tabs organizing all available reports:

- **Overview** — Cross-event company-level reports (CMO Narrative, QBR, Event Comparison, ABM Heatmap, etc.)
- **Pre-Event** — Reports for event preparation (Executive Briefing, Operations Guide, Sales Briefing, KBYG, ROI Forecast)
- **Post-Event** — Reports for event analysis (Executive Summary, Sales Handoff, Pipeline Attribution, Budget Reconciliation, etc.)
- **Intelligence** — Cross-event analytical reports

Each report card shows: name, description, status badge (generated/pending based on existing snapshot), and preview text from the last generation. Clicking a report navigates to the Report View.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Reports hub with 4 tabs | SHIPPED | All 21 report types listed with status badges |
| Snapshot status detection | SHIPPED | Shows "generated" vs "pending" from real DB snapshots |
| Preview text from last generation | SHIPPED | Excerpt from narrative on card |

### 11.2 Report View (Individual Reports)

URL: `/reports/:reportType` or `/events/:eventId/reports/:reportType`. Full report display with:

- **KPI grid** — Dynamic metrics extracted from report data (currency, percentages, counts)
- **Visual mode** — Bar charts, donut charts, data tables rendered from structured API response
- **Narrative mode** — AI-generated prose formatted with bold text and currency amounts
- **Dual-view toggle** — Switch between Visual and Narrative
- **Refresh button** — Regenerate with latest data

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Report view with KPIs + charts | SHIPPED | Dynamic rendering from structured API data |
| Narrative mode (AI prose) | SHIPPED | Formatted text that reads like a human analyst |
| Dual-view toggle | SHIPPED | Switch between Visual and Narrative |
| Refresh/regenerate | SHIPPED | One-click regeneration with latest data |

### 11.3 Executive Reports Dashboard

URL: `/reports/executive`. A dedicated view for leadership showing:

- **Post-event reports** — Inline expandable reports per event
- **Cross-event reports** — Company-level analytics
- **Pre-event reports** — Upcoming event preparation
- **AI recommendations** — Auto-generated next steps

Event filtering dropdown to scope reports to specific events. KPIs and narratives fetched from real API. "Generated X minutes ago" timestamps show freshness.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Executive reports dashboard | SHIPPED | Multi-report inline expansion, per-event filtering |
| AI recommendations | SHIPPED | Generated next steps based on data |

### 11.4 Event-Level Report Types (11 Types)

All event-level reports follow the same pattern: extract event data + leads + pipeline from PostgreSQL, aggregate and compute metrics, call Claude with a custom system prompt, persist narrative + structured data to `report_snapshots`, return to frontend.

1. **Post-Event Executive Summary** — Attendance, pipeline impact, key wins, recommendations. The "send to your CMO" report.
2. **Operations Guide** — Day-of operations checklist, vendor contacts, timeline, contingency plans.
3. **Budget Reconciliation** — Actual vs. budgeted spend by category with variance analysis. Red/green styling for over/under.
4. **ROI Forecast** — Predicted ROI based on current pipeline, historical conversion rates, spend.
5. **Sponsorship Tracker** — Sponsorship ROI tracking, deliverable status, value assessment.
6. **No-Show Analysis** — RSVP vs. attendance gaps, no-show patterns, follow-up recommendations.
7. **Survey Analysis** — Event survey results aggregation and insights.
8. **Executive Briefing** — Pre-event intelligence: attendee analysis, key accounts, talking points.
9. **Sales Team Briefing** — Per-AE briefing with their attendees, deal context, conversation starters.
10. **Sales Handoff** — Hot/warm lead action cards with recommended next steps per lead.
11. **Pipeline Tracking** — 30/60/90 day pipeline progression with opportunity-level detail.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| All 11 event-level report types | SHIPPED | Full backend generation + frontend rendering for all 11 |
| AI narrative generation | SHIPPED | Claude-sonnet-4 with custom prompts per report type |
| Report snapshot caching | SHIPPED | Stored in report_snapshots table, instant on revisit |
| Activity log on generation | SHIPPED | Every report generation logged for audit |

### 11.5 Cross-Event Report Types (7 Types)

Company-level reports that analyze patterns across all events:

1. **CMO Narrative (Enhanced)** — AI-generated executive summary for board meetings. Portfolio performance, top events, budget utilization, pipeline trends.
2. **Quarterly Business Review (QBR)** — Quarter-over-quarter event performance, budget efficiency, pipeline contribution.
3. **Cross-Event Leads** — Repeat attendee patterns, multi-event engagement trends, loyalty indicators.
4. **Event Comparison** — Benchmarking events against each other (ROI, attendance, pipeline-to-spend ratio).
5. **ABM Heatmap** — Account coverage visualization showing which target accounts have been touched across events.
6. **Scheduling Conflicts** — Conflict detection across upcoming events (date overlaps, resource conflicts).
7. **Content Performance** — Which content items drive the most engagement across campaigns and events.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| All 7 cross-event report types | SHIPPED | Full backend generation + frontend rendering for all 7 |
| Company-level snapshot caching | SHIPPED | Same report_snapshots table, event_id nullable for cross-event |

### 11.6 Legacy CMO Narrative Report

The original CMO report generation from Batch 1 (`report_generation_handler.go`). Generates a narrative report with copy-to-clipboard. Superseded by the Enhanced CMO report in the Report Engine but still functional.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Legacy CMO report generation | SHIPPED | POST /api/v1/reports/generate with copy-to-clipboard |

---

## 12. Phase 9: Content Library (Intelligence Layer)

URL: `/content`. The Content Library is not a file cabinet — it is the intelligence layer that powers every AI feature. Each content item is tagged with metadata: content type, status, content stage (top/mid/bottom funnel), CTA type, key themes (the critical field Claude reads for email generation), and performance notes.

When Claude generates an email, it cross-references the recipient's title, company, and engagement level against the content library to select relevant content. A case study about financial services gets matched to a financial services lead. A technical whitepaper gets matched to an IT buyer.

Full CRUD: create, read, update, delete with table view showing name, type, stage, status, last updated, and key themes preview. Search by name, filter by type and status.

> **Why Content Quality Determines Email Quality**
>
> The AI email generator is only as good as the content it can reference. An empty content library means generic emails. A rich library with persona-tagged, stage-aligned content means hyper-personalized emails that reference exactly the right asset for each recipient. This is why we push content setup during onboarding.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Content CRUD (create/read/update/delete) | SHIPPED | Full API endpoints + frontend forms |
| Content metadata tagging | SHIPPED | Type, stage, CTA, key themes, performance notes |
| Search and filter | SHIPPED | By name, type, status |
| AI email gen using content library | SHIPPED | Content items selectable in CreateCampaignModal, passed to Claude |
| Content health widgets (usage heatmap) | NOT BUILT | No usage tracking, persona coverage, or staleness alerts |

---

## 13. Phase 10: Analytics and Attribution

Analytics is the "Prove" section. It answers the only question that matters to leadership: are events generating pipeline?

### 13.1 Attribution Engine (3-Phase Matching)

The attribution engine matches event attendees to CRM opportunities:

- **Phase 1: Email match** — attendee email matches CRM contact email
- **Phase 2: Domain match** — attendee email domain matches CRM opportunity account domain
- **Phase 3: Fuzzy company name match** — company name similarity matching

Each match is classified as **sourced** (event was the first touchpoint before opportunity creation) or **influenced** (contact attended during opportunity lifecycle). Results stored in `event_attributions` table.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| 3-phase attribution engine | SHIPPED | Email + domain + fuzzy matching |
| Sourced/influenced classification | SHIPPED | Correct classification based on opportunity timeline |
| Run Attribution button | SHIPPED | POST /api/v1/events/:id/attribution/run |
| Attribution data in Results tab | SHIPPED | Pipeline tracking report shows attributed opportunities |

### 13.2 ROI Calculations

ROI calculated at two levels: per-event (pipeline influenced, cost per pipeline dollar, pipeline-to-spend ratio) and portfolio (aggregate across all events in a date range).

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Per-event ROI calculations | SHIPPED | Pipeline influenced, cost ratios, spend efficiency |
| Portfolio ROI aggregation | SHIPPED | Cross-event totals and averages |

### 13.3 Excel Exports

Three streaming .xlsx exports: leads (all contacts with scores, tags, event associations), attribution (per-event with sourced/influenced, pipeline, spend, ratio), and campaigns (metadata + performance metrics).

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Excel export (3 types) | SHIPPED | Leads, attribution, campaigns as streaming .xlsx |

### 13.4–13.6 Scoring, Pipeline, Attribution Pages

These three pages (`/scoring`, `/pipeline`, `/attribution`) are intentional **shells** — "Coming Soon" placeholders with description of future capabilities.

> **Why Ship Shells**
>
> These pages exist in the sidebar navigation so the FM can see where the platform is headed. The underlying engines exist (scoring engine is fully built, attribution engine is fully built) — these pages will eventually surface configurable UIs for those engines. The shells leave the door open without shipping half-baked interfaces.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Scoring page | SHELL | "Coming Soon" with future capability description |
| Pipeline page | SHELL | "Coming Soon" with future capability description |
| Attribution page | SHELL | "Coming Soon" with future capability description |

---

## 14. Phase 11: Settings and Integrations

URL: `/settings`.

### 14.1 CRM Connections

Salesforce and HubSpot cards, each with connect/disconnect button and status indicator. OAuth flow via Merge.dev. Opportunity Sync section shows last sync time + count with "Sync Now" button (async job polling).

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| CRM OAuth (Salesforce + HubSpot) | SHIPPED | Connect, disconnect, status indicator |
| Opportunity sync with polling | SHIPPED | Sync Now button, job status updates |
| CRM push (write-back to SF/HS) | NOT BUILT | Must ship for beta. Merge.dev write-back needed |

### 14.2 Slack Notifications

"Add to Slack" button, connected webhook list with delete option. Five typed triggers: lead_upload, campaign_sent, attribution_hit, contract_missing, generic. Rate-limited to prevent spam.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Slack OAuth + webhook config | SHIPPED | Connect, select channel, configure triggers, manage webhooks |
| 5 notification triggers | SHIPPED | lead_upload, campaign_sent, attribution_hit, contract_missing, generic |

### 14.3 Admin Tools

"Clear Mock Data" button (admin-only) for development/demo cleanup.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Clear Mock Data (admin) | SHIPPED | One-click demo data cleanup |

### 14.4–14.6 Not Built Features

| Feature | Status | Notes |
|---------|--------|-------|
| Team management (invite, roles) | NOT BUILT | No invite flow, role assignment, or team activity view |
| Stripe billing | NOT BUILT | Blocked on stripe-go dependency approval from Jack |
| Full data export (ZIP) | NOT BUILT | Specified: admin exports all data as CSVs in ZIP |
| Account deletion flow | NOT BUILT | Specified: confirm by typing company name, 30-day retention, then hard delete |

---

## 15. Notification System (with Notification Banner)

FieldMarq communicates through three channels: Slack (fully shipped), in-app notification banner (shipped on main), and email digest (not started).

**Scheduler** (runs every 6 hours):
1. Task deadline notifications — tasks due within 3 days
2. Event stagnation alerts — events inactive 7+ days
3. Auto-resolve past-event tasks — pre-event/day-of when event passes, post-event 14 days after
4. Hot lead follow-up alerts — leads not contacted in 72+ hours
5. Lead score decay alert — hot/warm leads untouched 30+ days (fires if 5+ affected)
6. Review deadline checker — campaigns scheduled within 24 hours with unreviewed emails (on main)

**Notification Banner** (on main): A persistent banner at the top of the app (between Header and main content) that shows the most urgent unread notification. Five notification types with color-coded backgrounds:
- `review_deadline` (amber) — emails need review before scheduled send
- `send_failure` (red) — campaign send failed
- `sequence_step_ready` (blue) — sequence step due for review
- `reengagement_created` (teal) — auto-generated draft ready
- `engagement_anomaly` (amber) — unusual engagement pattern

Each banner is clickable (navigates to the relevant entity) and dismissible (marks as read). Only one banner shows at a time — the most urgent.

| Feature | Status | What the FM Experiences |
|---------|--------|------------------------|
| Slack notifications (5 triggers) | SHIPPED | Fire-and-forget with rate limiting |
| Scheduler (6-hour cycle, 5 jobs) | SHIPPED | Task deadlines, stagnation, auto-resolve, hot lead decay, score decay |
| Notification banner (5 types) | SHIPPED (main) | Persistent top-of-app banner, color-coded, clickable, dismissible |
| Review deadline checker | SHIPPED (main) | Scheduler alerts when emails unreviewed <24h before scheduled send |
| In-app notification bell/dropdown | NOT BUILT | Bell icon in nav. No dropdown panel for browsing all notifications |
| Email digest (weekly summary) | NOT BUILT | No cron job, template, or opt-in flow |

---

## 16. Platform Architecture (Why We Built It This Way)

### Multi-Tenant Isolation

Every database query filters by `company_id`. Zero possibility of cross-tenant data leakage. Enforced at middleware level (`middleware.GetCompanyID` extracts from Clerk JWT). Non-negotiable for every feature.

### Non-Destructive CRM Philosophy

FieldMarq never overwrites CRM records. When we push to Salesforce/HubSpot, we create Tasks (not Leads or Contacts) — "guest in their house" philosophy. AE notes are sacred and never discarded in any merge or processing. DNE leads are never included in campaigns or CRM pushes.

### Async Processing Pattern (202 Accepted)

Any operation over ~200ms returns `202 Accepted` with a `job_id`. Frontend polls for completion. This applies to: CSV uploads, attribution runs, AI report generation, website analysis, email generation, and data exports. Pattern: `jobs.Create` → goroutine with `context.WithoutCancel` and `recover` → `jobs.Update` on completion/failure. Exceptions: `tracker.Track` and `notify.Send` are always fire-and-forget.

### Additive-Only Development

New files always. Never modify existing handler files without explicit instruction. V2 suffix for files that would overwrite Jack's work. `_patch` suffix for instruction-only files. Every PR is safe to review: new files can be accepted or rejected without risk to existing functionality.

### Copilot-Ready Architecture

Every V1 feature is designed so the copilot layer snaps on top without schema changes:

- Scoring engine uses configurable `scoring_config` table so AI can tune weights
- Task names have `platform_task_id` FK so Claude can silently reclassify renamed tasks
- Notification triggers are separated from outputs so the copilot can transform alerts into proposed actions
- Calendar copilot handler (`calendar_copilot_handler.go`) is the first shipped Marq backend — multi-turn AI chat with calendar context, max 300 words, concise and actionable
- Action queue handler is the second copilot surface — AI analyzes FM state and generates prioritized recommendations

> **The Copilot Rule**
>
> Design for the copilot end-state (schema and API must support future AI action without rework). Build for V1 analog reality (ship clean manual interactions if the AI layer is not ready). Never build copilot on top of incomplete plumbing (get the data flowing correctly first).

### Rate Limiting

- Default: 10 requests / 30 seconds (global)
- Demo requests: 2 requests / 5 seconds (stricter)
- Webhooks: exempt (SendGrid high-frequency batches)
- Public routes (unsubscribe, health): rate-limited separately

---

## 17. Copilot Roadmap (V2 Vision)

FieldMarq's destination is a full copilot platform. The system acts on behalf of the FM by default and only surfaces for confirmation when it cannot proceed alone.

V2 features the V1 architecture supports without rework:

- **Silent task reclassification** — Claude re-slots renamed tasks to canonical templates. Only interrupts on low confidence.
- **Proactive notification actions** — "CSV upload complete. 45 hot leads. Generate follow-up campaign?" with a one-click action button.
- **Auto-tuned scoring weights** — AI adjusts scoring_config based on which leads convert to opportunities across all tenants.
- **Send-time optimization** — Correlate open rates against send_time + timezone to recommend optimal send windows.
- **Auto-generated event documents** — KBYG, executive briefings, and post-event summaries generated without FM triggering.
- **Cross-tenant intelligence** — Benchmark event ROI against anonymized portfolio averages.

Every V1 design decision in this document was evaluated against this V2 vision. If a V1 implementation would require rework to add the copilot layer, it was redesigned before build.

---

## Appendix A: Build Status Summary

High-level status across all major platform areas as of March 25, 2026. Features marked **(main)** are on Jack's main branch. Features without a branch note are on Aubs-updates. Both must merge for the complete platform.

| Area | Status | Branch | Summary |
|------|--------|--------|---------|
| Onboarding Wizard (4-step) | SHIPPED | Aubs | All steps, AI website analysis, backend persistence |
| Onboarding Route Guard | SHIPPED | main | Redirects to /setup if onboarding incomplete |
| Events CRUD | SHIPPED | both | Create, read, update, soft-delete with filters, search, sort |
| Event Detail (8 tabs) | SHIPPED | both | All 8 tabs built with real API data |
| Event Operational Fields (19 new) | SHIPPED | main | Tier, objective, venue details, parking, wifi, catering, dress code, booth size, etc. |
| Event Health Indicator | SHIPPED | main | Green/amber/red status with lifecycle-aware smart summary |
| Checklist Templates (14 types) | SHIPPED | Aubs | 350+ tasks, 85+ milestones, backward offsets, save as template |
| Checklist Reconciliation | SHIPPED | Aubs | Keep/remove/add preview on event type change |
| Task Dependencies | SHIPPED | main | Blocking relationships, cycle prevention, unblock notifications |
| RSVP Workflow (7 statuses) | SHIPPED | main | invited → registered → confirmed → attended (and declined/waitlisted/no-show) |
| Bulk Event Import | SHIPPED | both | CSV/Excel upload, preview, batch execute |
| Global Tasks Page | SHIPPED | Aubs | Cross-event view, phase grouping, overdue highlighting, detail panel |
| Calendar (week + month views) | SHIPPED | Aubs | 5 item types, day detail, calendar copilot |
| Dashboard (7 widgets + KPIs) | SHIPPED | Aubs | Drag-drop, resize, customizable KPIs, all real data |
| Action Queue (AI-powered) | SHIPPED | Aubs | Claude-generated priority recommendations |
| CSV Upload Pipeline | SHIPPED | both | Upload, parse, score, tag, link attendees |
| Lead Scoring Engine V2 | SHIPPED | Aubs | Standalone engine, configurable weights, ICP templates |
| Score Breakdown UI | SHIPPED | Aubs | Signal-by-signal panel with 6 categories |
| Lead Detail Drawer | SHIPPED | Aubs | Full panel with score, notes, disposition, keyboard nav |
| Attribution Engine (3-phase) | SHIPPED | both | Email + domain + fuzzy matching, sourced/influenced |
| Report Engine (18 types) | SHIPPED | Aubs | 11 event-level + 7 cross-event, Claude-generated, snapshot caching |
| Executive Reports Dashboard | SHIPPED | Aubs | Multi-report inline expansion, per-event filtering |
| Campaign Builder + AI Email Gen | SHIPPED | both | Personalized emails from 4 context layers |
| Dynamic Segment Builder | SHIPPED | Aubs | Rule-based segments with preview |
| Email Review Panel | SHIPPED | Aubs | Per-email review, edit, approve, test send |
| Email Review Queue (3-panel) | SHIPPED | main | Full-screen review with contact context, approve/reject/skip |
| Email Sequences (multi-step) | SHIPPED | main | Sequences with steps, delays, auto-advance, enrollment tracking |
| Sequence Worker (5-min ticker) | SHIPPED | main | Auto-advances due steps to pending_review |
| Campaign Clone | SHIPPED | Aubs | One-click clone from detail modal |
| Campaign Pause/Resume | SHIPPED | main | Pause scheduled campaigns, resume to previous state |
| Send Confirmation Modal | SHIPPED | main | Rich confirmation UI with summary, schedule toggle, timezone |
| CAN-SPAM Unsubscribe | SHIPPED | main | Automatic footer injection, email consent checks |
| Re-engagement Worker (daily) | SHIPPED | main | Auto-creates draft campaigns for stale post-event contacts |
| AI Document Generators (3 types) | SHIPPED | main | KBYG, Executive Briefing, Sales Team Brief |
| Timezone-Aware Scheduler | SHIPPED | both | Full schedule handler with email_schedule_queue |
| Content Library CRUD | SHIPPED | both | Full metadata tagging, AI integration |
| Excel Exports (3 types) | SHIPPED | both | Leads, attribution, campaigns as streaming .xlsx |
| CRM Connection (Merge.dev) | SHIPPED | both | Salesforce/HubSpot OAuth, sync, disconnect |
| Slack Notifications (5 triggers) | SHIPPED | both | Fire-and-forget with rate limiting |
| Notification Banner (5 types) | SHIPPED | main | Persistent top-of-app banner, color-coded, clickable |
| Scheduler (6+ automated jobs) | SHIPPED | both | Task deadlines, stagnation, auto-resolve, lead decay, review deadline checker |
| Contacts (CRUD + dedup) | SHIPPED | both | Full CRUD, search, filter, find duplicates |
| Settings (CRM + Slack) | SHIPPED | both | OAuth connections, webhook management |
| Design System / Brand Refresh | SHIPPED | Aubs | Teal ombre palette, Cabinet Grotesk, fm-* tokens (37 files) |
| Scoring/Pipeline/Attribution pages | SHELL | Aubs | Intentional placeholders for future UI |
| Budgets/Vendors pages | SHELL | Aubs | Intentional placeholders for future features |
| In-App Notification Bell/Dropdown | NOT BUILT | — | Bell icon present. No dropdown for browsing all notifications |
| CRM Push (write-back) | NOT BUILT | — | Must ship for beta. Merge.dev write-back needed |
| Team Management | NOT BUILT | — | No invite flow or role assignment |
| Stripe Billing | NOT BUILT | — | Blocked on dependency approval |
| Full Data Export | NOT BUILT | — | Specified but no implementation |
| Email Digest (weekly) | NOT BUILT | — | No cron job, template, or opt-in flow |

---

## Appendix B: Backend API Endpoint Reference

### Auth & Onboarding
- `POST /api/v1/auth/onboard` — Create company + user
- `GET /api/v1/auth/me` — Current user profile
- `POST /api/v1/onboarding/profile` — Save onboarding profile
- `GET /api/v1/onboarding/profile` — Get onboarding profile
- `PUT /api/v1/onboarding/profile` — Update onboarding profile

### Company
- `GET /api/v1/company` — Get company
- `PUT /api/v1/company` — Update company
- `POST /api/v1/company/onboarding` — Complete onboarding
- `GET /api/v1/company/profile` — Get profile
- `PUT /api/v1/company/profile` — Update profile
- `POST /api/v1/company/analyze-website` — AI website analysis (async)
- `GET /api/v1/jobs/{jobID}` — Poll job status

### Events
- `GET /api/v1/events` — List events
- `POST /api/v1/events` — Create event
- `GET /api/v1/events/{eventID}` — Get event
- `PUT /api/v1/events/{eventID}` — Update event
- `DELETE /api/v1/events/{eventID}` — Delete event
- `POST /api/v1/events/{eventID}/prospectus` — Upload prospectus
- `POST /api/v1/events/import/upload` — Bulk import upload
- `POST /api/v1/events/import/preview` — Bulk import preview
- `POST /api/v1/events/import/execute` — Bulk import execute

### Event Sub-Resources
- `GET /api/v1/events/{eventID}/tasks` — List tasks
- `GET /api/v1/events/{eventID}/campaigns` — List campaigns
- `GET /api/v1/events/{eventID}/guests` — List guests
- `POST /api/v1/events/{eventID}/guests/scan` — Scan guests
- `GET /api/v1/events/{eventID}/expenses` — List expenses
- `POST /api/v1/events/{eventID}/expenses` — Create expense
- `PUT /api/v1/events/{eventID}/expenses/{expenseID}` — Update expense
- `DELETE /api/v1/events/{eventID}/expenses/{expenseID}` — Delete expense
- `GET /api/v1/events/{eventID}/attributions` — List attributions

### Tasks
- `POST /api/v1/events/{eventID}/tasks` — Create task
- `PUT /api/v1/events/{eventID}/tasks/{taskID}` — Update task
- `DELETE /api/v1/events/{eventID}/tasks/{taskID}` — Delete task (soft)
- `POST /api/v1/events/{eventID}/activate` — Activate event
- `POST /api/v1/events/{eventID}/complete` — Complete event
- `GET /api/v1/tasks/my` — My tasks
- `GET /api/v1/tasks/all` — All tasks
- `GET /api/v1/tasks/summary` — Task summary
- `POST /api/v1/tasks/auto-resolve` — Auto-resolve past events

### Checklists
- `GET /api/v1/event-types` — List event types
- `POST /api/v1/events/{eventID}/checklist/generate` — Generate checklist
- `GET /api/v1/events/{eventID}/checklist` — Get checklist
- `POST /api/v1/events/{eventID}/checklist/save-template` — Save as template
- `POST /api/v1/events/{eventID}/checklist/import` — Import checklist (AI)
- `POST /api/v1/events/{eventID}/checklist/import/confirm` — Confirm import
- `POST /api/v1/events/{eventID}/checklist/gap-analysis` — Gap analysis (AI)
- `POST /api/v1/events/{eventID}/checklist/reconcile/preview` — Reconcile preview
- `POST /api/v1/events/{eventID}/checklist/reconcile/apply` — Reconcile apply

### Documents
- `POST /api/v1/events/{eventID}/documents` — Upload document
- `GET /api/v1/events/{eventID}/documents` — List documents
- `GET /api/v1/events/{eventID}/documents/{docId}` — Get document
- `DELETE /api/v1/events/{eventID}/documents/{docId}` — Delete document
- `GET /api/v1/events/{eventID}/prospectus/extraction` — Get extraction
- `POST /api/v1/events/{eventID}/prospectus/extract` — Trigger extraction (AI)
- `PUT /api/v1/events/{eventID}/prospectus/extraction/{id}/verify` — Verify extraction
- `POST /api/v1/events/{eventID}/documents/kbyg` — Generate KBYG (AI)
- `POST /api/v1/events/{eventID}/documents/exec-briefing` — Generate Executive Briefing (AI, main)
- `POST /api/v1/events/{eventID}/documents/sales-brief` — Generate Sales Team Brief (AI, main)

### CSV Upload & Leads
- `POST /api/v1/events/{eventID}/csv/upload` — Upload CSV
- `GET /api/v1/events/{eventID}/csv/status/{batchID}` — Upload status
- `GET /api/v1/events/{eventID}/leads` — List leads
- `GET /api/v1/events/{eventID}/leads/{profileID}` — Get lead detail
- `PATCH /api/v1/events/{eventID}/leads/{profileID}` — Patch lead
- `POST /api/v1/events/{eventID}/leads/{profileID}/tag` — Tag lead
- `POST /api/v1/events/{eventID}/leads/assign` — Assign leads

### Scoring
- `POST /api/v1/events/{eventID}/leads/{profileID}/rescore` — Rescore single (V1)
- `POST /api/v1/events/{eventID}/leads/rescore-all` — Rescore event (V1)
- `POST /api/v1/leads/rescore-company` — Rescore company (V1)
- `POST /api/v1/events/{eventID}/leads/{profileID}/rescore-v2` — Rescore single (V2)
- `POST /api/v1/events/{eventID}/leads/rescore-all-v2` — Rescore event (V2)
- `POST /api/v1/leads/rescore-company-v2` — Rescore company (V2)
- `GET /api/v1/scoring/weights` — Get scoring weights
- `PUT /api/v1/scoring/weights` — Update scoring weights
- `POST /api/v1/scoring/weights/reset` — Reset scoring weights
- `POST /api/v1/scoring/preview` — Preview score

### ICP
- `GET /api/v1/events/{eventID}/icp` — Get event ICP
- `PUT /api/v1/events/{eventID}/icp` — Update event ICP
- `POST /api/v1/events/{eventID}/icp/apply-template` — Apply ICP template
- `GET /api/v1/icp-templates` — List ICP templates
- `POST /api/v1/icp-templates` — Create ICP template
- `PUT /api/v1/icp-templates/{templateID}` — Update ICP template
- `DELETE /api/v1/icp-templates/{templateID}` — Delete ICP template

### Campaigns
- `POST /api/v1/events/{eventID}/campaigns` — Create campaign
- `GET /api/v1/campaigns` — List all campaigns
- `GET /api/v1/campaigns/{campaignID}` — Get campaign
- `PATCH /api/v1/campaigns/{campaignID}` — Update campaign
- `DELETE /api/v1/campaigns/{campaignID}` — Delete campaign
- `GET /api/v1/campaigns/{campaignID}/emails` — List emails
- `PATCH /api/v1/campaigns/{campaignID}/emails/{emailID}` — Update email
- `POST /api/v1/campaigns/{campaignID}/emails/{emailID}/regenerate` — Regenerate email (AI)
- `POST /api/v1/campaigns/{campaignID}/emails/{emailID}/send` — Send single email
- `POST /api/v1/campaigns/{campaignID}/generate` — Generate emails (AI)
- `POST /api/v1/campaigns/{campaignID}/send` — Send campaign
- `POST /api/v1/campaigns/{campaignID}/clone` — Clone campaign
- `POST /api/v1/campaigns/{campaignID}/schedule` — Set schedule
- `DELETE /api/v1/campaigns/{campaignID}/schedule` — Cancel schedule
- `GET /api/v1/campaigns/{campaignID}/schedule` — Get schedule

### Segments
- `GET /api/v1/campaigns/segments` — List segments
- `POST /api/v1/campaigns/segments` — Save segment
- `POST /api/v1/campaigns/segments/preview` — Preview segment
- `DELETE /api/v1/campaigns/segments/{segmentID}` — Delete segment

### Reports
- `POST /api/v1/reports/generate` — Generate CMO report (legacy)
- `POST /api/v1/reports/generate-enhanced` — Generate CMO enhanced
- `POST /api/v1/reports/qbr` — Generate QBR
- `POST /api/v1/reports/cross-event-leads` — Generate cross-event leads
- `POST /api/v1/reports/event-comparison` — Generate event comparison
- `POST /api/v1/reports/abm-heatmap` — Generate ABM heatmap
- `POST /api/v1/reports/scheduling-conflicts` — Generate scheduling conflicts
- `POST /api/v1/reports/content-performance` — Generate content performance
- `GET /api/v1/reports/{reportType}/snapshot` — Get company report snapshot
- `POST /api/v1/events/{eventID}/reports/post-event-summary` — Generate post-event summary
- `POST /api/v1/events/{eventID}/reports/operations-guide` — Generate operations guide
- `POST /api/v1/events/{eventID}/reports/budget-reconciliation` — Generate budget reconciliation
- `POST /api/v1/events/{eventID}/reports/roi-forecast` — Generate ROI forecast
- `POST /api/v1/events/{eventID}/reports/sponsorship-tracker` — Generate sponsorship tracker
- `POST /api/v1/events/{eventID}/reports/no-show-analysis` — Generate no-show analysis
- `POST /api/v1/events/{eventID}/reports/survey-analysis` — Generate survey analysis
- `POST /api/v1/events/{eventID}/reports/executive-briefing` — Generate executive briefing
- `POST /api/v1/events/{eventID}/reports/sales-briefing` — Generate sales briefing
- `POST /api/v1/events/{eventID}/reports/sales-handoff` — Generate sales handoff
- `POST /api/v1/events/{eventID}/reports/pipeline-tracking` — Generate pipeline tracking
- `GET /api/v1/events/{eventID}/reports/{reportType}/snapshot` — Get event report snapshot

### Dashboard
- `GET /api/v1/dashboard/activity` — Recent activity
- `GET /api/v1/dashboard/leads-by-status` — Leads by status
- `GET /api/v1/dashboard/event-campaign-counts` — Event campaign counts
- `GET /api/v1/dashboard/actions` — AI action queue

### Calendar
- `GET /api/v1/calendar` — Calendar feed
- `POST /api/v1/calendar/copilot` — Calendar copilot chat (AI)

### Attribution
- `POST /api/v1/events/{eventID}/attribution/run` — Run event attribution
- `GET /api/v1/events/{eventID}/attribution` — Get event attribution
- `GET /api/v1/attribution/summary` — Company attribution summary

### CRM
- `GET /api/v1/crm/connections` — Get connections
- `POST /api/v1/crm/authorize` — Authorize
- `GET /api/v1/crm/callback/{provider}` — OAuth callback
- `POST /api/v1/crm/disconnect` — Disconnect
- `POST /api/v1/crm/sync` — Sync
- `GET /api/v1/crm/sync-status` — Sync status
- `GET /api/v1/crm/opportunities` — List opportunities
- `GET /api/v1/crm/attribution-summary` — Attribution summary

### Contacts
- `GET /api/v1/contacts` — List contacts
- `GET /api/v1/contacts/duplicates` — Find duplicates
- `GET /api/v1/contacts/{contactID}` — Get contact
- `PUT /api/v1/contacts/{contactID}` — Update contact
- `DELETE /api/v1/contacts/{contactID}` — Delete contact
- `POST /api/v1/contacts/{contactID}/merge` — Merge contacts

### Content
- `GET /api/v1/content-items` — List content
- `POST /api/v1/content-items` — Create content
- `GET /api/v1/content-items/{contentID}` — Get content
- `PUT /api/v1/content-items/{contentID}` — Update content
- `DELETE /api/v1/content-items/{contentID}` — Delete content

### Notifications
- `GET /api/v1/notifications` — List
- `GET /api/v1/notifications/unread-count` — Unread count
- `POST /api/v1/notifications/read-all` — Mark all read
- `POST /api/v1/notifications/{notificationID}/read` — Mark read

### Exports
- `GET /api/v1/events/{eventID}/export/leads` — Export leads (.xlsx)
- `GET /api/v1/events/{eventID}/export/attribution` — Export attribution (.xlsx)
- `GET /api/v1/events/{eventID}/export/campaigns` — Export campaigns (.xlsx)

### Sequences (main)
- `POST /api/v1/sequences` — Create sequence
- `GET /api/v1/sequences` — List sequences
- `GET /api/v1/sequences/{sequenceID}` — Get sequence
- `PATCH /api/v1/sequences/{sequenceID}` — Update sequence
- `DELETE /api/v1/sequences/{sequenceID}` — Delete sequence
- `POST /api/v1/sequences/{sequenceID}/enrollments` — Enroll contacts
- `POST /api/v1/sequences/{sequenceID}/enrollments/{enrollmentID}/pause` — Pause enrollment
- `POST /api/v1/sequences/{sequenceID}/enrollments/{enrollmentID}/resume` — Resume enrollment

### Review Queue (main)
- `POST /api/v1/campaigns/{campaignID}/emails/{emailID}/approve` — Approve email
- `POST /api/v1/campaigns/{campaignID}/emails/{emailID}/reject` — Reject email
- `POST /api/v1/campaigns/{campaignID}/emails/{emailID}/skip` — Skip email
- `POST /api/v1/campaigns/{campaignID}/approve-all` — Approve all pending
- `GET /api/v1/campaigns/{campaignID}/review-summary` — Review status counts

### Admin (main)
- `POST /api/v1/admin/reset-seed-data` — Reset all company data (admin-only)

### Other
- `GET /health` — Health check
- `POST /api/v1/track` — Activity tracking
- `POST /api/v1/demo-requests` — Demo request (rate-limited)
- `GET /unsubscribe` — Unsubscribe (public, no auth)
- `POST /webhooks/sendgrid` — SendGrid webhook

---

## Appendix C: Database Migration Index (001–026 + main branch 009–012)

| # | File | What It Creates/Changes |
|---|------|------------------------|
| 001 | initial_schema.sql | companies, users, events, event_tasks, import_batches, checklist_templates, contacts, contact_profiles, campaigns, crm_* (5 tables), activity_log |
| 002 | demo_requests.sql | demo_requests table |
| 003 | import_raw_data.sql | ALTER import_batches: ADD raw_data JSONB |
| 004 | seed_checklist_templates.sql | Seed data: Conference Booth, Virtual Summit, etc. |
| 005 | crm_opp_created_date.sql | ALTER crm_opportunities: ADD opp_created_at |
| 006 | notifications_metadata.sql | ALTER notifications: ADD metadata JSONB, link VARCHAR |
| 007 | aubs_enhancements.sql | attendees, notes, contact_profiles extensions, merge_candidates, merge_decisions, upload_batches, import_jobs, vendor_contracts, crm_push_queue, activity_audit |
| 008 | contacts_lead_tag_index.sql | CREATE INDEX on contacts (company_id, lead_tag) |
| 009 | onboarding_columns.sql | ALTER companies: ADD onboarding_completed_at, industry |
| 010 | event_documents_prospectus.sql | event_documents, event_prospectus_extractions, event_catalog |
| 011 | checklist_milestones.sql | event_types, checklist_milestones, checklist_template_tasks, custom_checklist_templates |
| 012 | task_resolution_fields.sql | ALTER event_tasks: ADD resolved_reason, resolved_at |
| 013 | event_form_enhancements.sql | ALTER events: ADD promotional_activities, prospectus_file_*, expo_logistics |
| 014 | seed_checklist_templates.sql | Seed 14 event types + milestones + template tasks |
| 015 | checklist_tracking.sql | ALTER event_tasks: ADD source, external_id, external_*; CREATE platform_events |
| 016 | lead_scoring_v2.sql | ALTER contact_profiles: ADD csv_lead_status, had_conversation; ALTER events: ADD icp_profile; CREATE icp_templates |
| 017 | lead_manual_overrides.sql | ALTER contact_profiles: ADD manual_disposition, manual_notes, disposition_set_by/at |
| 018 | event_import_batch.sql | ALTER events: ADD raw_import_row; CREATE event_import_batches |
| 019 | nullable_event_date_start.sql | ALTER events: event_date_start DROP NOT NULL |
| 020 | date_precision.sql | ALTER events: ADD date_precision |
| 021 | custom_segments.sql | CREATE custom_segments; ALTER campaigns: ADD segment_rules |
| 022 | report_snapshots.sql | CREATE report_snapshots |
| 023 | scheduled_reports.sql | CREATE scheduled_reports |
| 024 | sponsorship_deliverables.sql | CREATE sponsorship_deliverables |
| 025 | event_content.sql | CREATE event_content |
| 026 | surveys.sql | CREATE surveys, survey_responses |

---

**Note on migration numbering:** Aubs-updates and main have divergent migration numbers. Main uses 009-012 for sequences, review queue, event fields, and task dependencies. Aubs-updates uses 009+ for onboarding, documents, checklists, scoring, etc. These will need renumbering during merge to avoid conflicts. Jack should renumber the Aubs migrations to start after main's highest migration number.

---

## Appendix D: Jack's Main Branch Features (Post-Divergence)

These 13 commits on main were built after Aubs-updates diverged (commit 88e9ec1). They are **live on main** but **not on Aubs-updates**. Merge will require conflict resolution in shared files.

### Features Added on Main

| Feature | Key Files | Migration |
|---------|-----------|-----------|
| Email Sequences (multi-step) | sequences.go (859L), sequence_worker.go (254L), Sequences.tsx | 009 |
| Email Review Queue (3-panel) | campaigns.go (updated), ReviewQueue.tsx (492L) | 010 |
| CAN-SPAM Unsubscribe | campaigns.go (injectUnsubscribeFooter) | — |
| AI Doc: Executive Briefing | documents.go (GenerateExecBriefing) | — |
| AI Doc: Sales Team Brief | documents.go (GenerateSalesBrief) | — |
| Notification Banner | NotificationBanner.tsx, AppShell.tsx | — |
| Review Deadline Checker | scheduler.go (checkReviewDeadlines) | — |
| Event Operational Fields (19) | events.go, EventEdit.tsx | 011 |
| Task Dependencies | tasks.go, TasksTab.tsx | 012 |
| RSVP Workflow (7 statuses) | event_sub.go, PeopleTab.tsx | — |
| Event Health Indicator | OverviewTab.tsx | — |
| Re-engagement Worker | reengagement.go (159L) | — |
| Campaign Pause/Resume | campaigns.go | — |
| Send Confirmation Modal | SendConfirmModal.tsx (173L) | — |
| Onboarding Route Guard | AppShell.tsx | — |
| Reset Seed Data (admin) | crm.go (ResetSeedData) | — |

### Likely Merge Conflicts

These files were modified on **both** branches and will need manual resolution:

| File | Main Changes | Aubs Changes |
|------|-------------|--------------|
| `campaigns.go` | Review queue, pause/resume, CAN-SPAM, send filters | Clone, schedule, content library |
| `tasks.go` | Dependencies, add/remove dependency endpoints | Extended task endpoints, soft delete |
| `events.go` | 19 operational fields, calendar queries | Calendar queries, filter support |
| `scheduler.go` | Review deadline checker, data race fix | Auto-resolve improvements, phase grouping |
| `router.go` | Sequence routes, review routes, admin routes | Calendar, copilot, import, report engine routes |
| `TasksTab.tsx` | Dependency UI, blocked indicators | Phase grouping, milestone badges, design refresh |
| `PeopleTab.tsx` | RSVP dropdown, status filter | Lead detail drawer, design refresh |
| `OverviewTab.tsx` | Health indicator, lifecycle actions, KPI breakdown | Design refresh |
| `DocumentsTab.tsx` | Exec briefing + sales brief generate buttons | Prospectus upload, design refresh |
| `AppShell.tsx` | Onboarding guard, notification banner | Layout updates |
| `EventEdit.tsx` | 19 operational field inputs | Custom event type, reconcile trigger |

---

*FM_PlatformWalkthrough_V2.md — Version 2.1 — Supersedes V1*

*This is a living document. Updated as features ship.*
