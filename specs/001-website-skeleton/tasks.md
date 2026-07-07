# Tasks: Website Skeleton

**Input**: Design documents from `specs/001-website-skeleton/`

**Prerequisites**: plan.md ✅ | spec.md ✅ | research.md ✅ | data-model.md ✅ | contracts/ ✅ | quickstart.md ✅

**Tests**: Not requested — no test tasks generated.

**Organization**: Tasks are grouped by user story. US1 and US2 both target Home/About and are sequenced accordingly; US3 and US4 are independent of each other and of US1/US2.

---

## Phase 1: Setup

**Purpose**: Verify and configure the Hugo project foundation — site title, navigation menu entries, and static asset directory scaffolding.

- [ ] T001 Update hugo.toml: set `title`, confirm `theme = "xmin"`, and add `[menu]` entries for Home/About (weight 1), Research (weight 2), CV (weight 3) in hugo.toml
- [ ] T002 [P] Create static asset directories: `static/images/` and `static/cv/` (referenced in plan.md project structure)
- [ ] T003 [P] Verify XMin theme loads cleanly with `hugo server -D` and no template errors before any overrides

**Checkpoint**: Hugo builds successfully; navigation shows Home/About, Research, CV; no extra items.

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Establish the shared layout override and baseline static asset so all user story pages can render consistently.

**⚠️ CRITICAL**: US1–US4 homepage and page templates depend on the header partial override established here.

- [ ] T004 Copy `themes/xmin/layouts/_partials/header.html` → `layouts/_partials/header.html` and restrict menu rendering to the three declared menu items only (per Global Navigation Contract in `contracts/site-skeleton-contract.md`)
- [ ] T005 [P] Add placeholder profile image `static/images/profile-placeholder.jpg` (any JPEG) — referenced by ResearcherProfile entity in `data-model.md`

**Checkpoint**: Navigation is limited to Home/About, Research, CV; News does NOT appear as a top-level link; profile image asset resolves without 404.

---

## Phase 3: User Story 1 — Visitor discovers researcher's academic profile (Priority: P1) 🎯 MVP

**Goal**: Homepage renders researcher bio, profile image with alt text, and research summary — the core academic identity block.

**Independent Test**: Open `http://localhost:1313/`; confirm bio text, profile image, and research direction summary all render; confirm navigation shows only Research and CV links.

- [ ] T006 [US1] Create `content/_index.md` with Hugo front matter: `title`, `bio` (placeholder text), `research_summary` (placeholder text), `profile_image` path pointing to `static/images/profile-placeholder.jpg`
- [ ] T007 [US1] Create `layouts/index.html` custom homepage template that renders: researcher name/title heading, profile image (`<img>` with descriptive `alt` attribute and CSS `background-color` or `min-height` block-level fallback), bio paragraph, and research summary paragraph — satisfying FR-001, FR-010, FR-011, SC-009 (image fallback), and Accessibility Contract
- [ ] T008 [P] [US1] Verify semantic heading order in `layouts/index.html`: page heading uses `<h1>`, section headings use `<h2>` per Accessibility Contract in `contracts/site-skeleton-contract.md`

**Checkpoint**: Homepage at `/` renders all four elements; profile image alt text is present; navigation links to Research and CV are keyboard-focusable.

---

## Phase 4: User Story 2 — Researcher announces career milestones (Priority: P1)

**Goal**: News subsection appears on the Home/About page below the profile block, showing dated entries in reverse chronological order with an empty-state fallback.

**Independent Test**: Open homepage; confirm a "News" heading renders below the research summary; confirm at least one placeholder news item displays with a date; remove all entries and confirm empty-state placeholder text appears.

- [ ] T009 [US2] Extend `layouts/index.html` with a News subsection block below the profile content: render `<h2>News</h2>` heading, iterate news entries from front matter in reverse date order, and display empty-state placeholder text when list is empty — satisfying FR-003 and News subsection contract in `contracts/site-skeleton-contract.md`
- [ ] T010 [US2] Add placeholder news entries to `content/_index.md` front matter (at least two items with `title`, `date`, `summary` fields) — satisfying NewsItem entity requirements in `data-model.md`

**Checkpoint**: News section is visible on Homepage only (not in nav); entries display in reverse chronological order; empty state renders correct placeholder text.

---

## Phase 5: User Story 3 — Visitor reviews researcher's publications (Priority: P1)

**Goal**: Research page renders a publication list with all required fields per the Research Contract, in reverse chronological order, with an empty-state fallback.

**Independent Test**: Open `/research/`; confirm publication list renders with title, authors, venue, date, and DOI/link fields; publications appear newest-first; remove entries and confirm empty-state placeholder text.

- [ ] T011 [US3] Create `content/research/_index.md` as the Research section landing page with `title: "Research"` front matter
- [ ] T012 [P] [US3] Create placeholder publication entry `content/research/placeholder-paper.md` with front matter: `title`, `authors` (list), `venue`, `date`, `doi_or_url` — satisfying Publication entity in `data-model.md`
- [ ] T013 [US3] Create `layouts/research/list.html` to render the publication list: each entry shows title (linked to doi_or_url if present), authors, venue, and date in reverse chronological order; render explicit empty-state placeholder when no entries exist — satisfying FR-006, FR-007 and Research Contract in `contracts/site-skeleton-contract.md`

**Checkpoint**: `/research/` renders placeholder publication with all five required fields; list is sorted newest-first; empty state renders when no content files are present.

---

## Phase 6: User Story 4 — Visitor accesses researcher's full CV (Priority: P1)

**Goal**: CV nav link resolves without error to a placeholder CV page with standard section headings, satisfying the CV Contract.

**Independent Test**: Click CV in navigation; confirm destination loads (no 404); confirm page or PDF is reachable; confirm standard CV section headings (Education, Experience, Skills, Publications, Awards) are present.

- [ ] T014 [US4] Create `content/cv/_index.md` with `title: "CV"` front matter and placeholder section headings: Education, Work Experience, Skills, Publications, Awards/Honors — satisfying FR-008, FR-009 and CV Contract in `contracts/site-skeleton-contract.md`
  - **NOTE**: This page is an optional fallback. T015 (PDF) is the primary CV delivery mode for the skeleton.
- [ ] T015 [P] [US4] Add `static/cv/cv-placeholder.pdf` as the primary placeholder PDF asset for CV delivery (PNG or image placeholder is acceptable; recommend 1-page PDF stub). Update `hugo.toml` menu weight or `content/cv/_index.md` front matter to point CV nav link to `/static/cv/cv-placeholder.pdf` — this is the default mode for the skeleton per Accessibility and Simplicity Principles

**Checkpoint**: CV link in navigation resolves to `/cv/` without error; placeholder section headings are visible; no broken link contract violations.

---

## Phase 7: Polish & Cross-Cutting Concerns

**Purpose**: Accessibility pass across all pages and final quickstart validation.

- [ ] T016 [P] Verify all `<img>` elements across `layouts/index.html` and any other templates have non-empty, descriptive `alt` attributes per Accessibility Contract in `contracts/site-skeleton-contract.md`
- [ ] T017 [P] Verify all interactive nav links (Research, CV, any DOI/URL links) are reachable via keyboard Tab navigation — no mouse-only interactions per FR-011
- [ ] T018 Run `hugo server -D` and manually complete all four validation scenarios in `specs/001-website-skeleton/quickstart.md` to confirm skeleton meets all acceptance criteria

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies — start immediately
- **Foundational (Phase 2)**: Depends on Phase 1 — blocks all page template work
- **US1 (Phase 3)**: Depends on Phase 2 — establishes homepage template
- **US2 (Phase 4)**: Depends on Phase 3 — extends homepage template with News block
- **US3 (Phase 5)**: Depends on Phase 2 — independent of US1/US2
- **US4 (Phase 6)**: Depends on Phase 2 — independent of US1/US2/US3
- **Polish (Phase 7)**: Depends on all story phases complete

### User Story Dependencies

- **US1 (P1)**: Can start after Foundational. Blocks US2 (both edit `layouts/index.html`).
- **US2 (P1)**: Depends on US1 completion (extends the same template).
- **US3 (P1)**: Can start after Foundational, in parallel with US1/US2.
- **US4 (P1)**: Can start after Foundational, in parallel with US1/US2/US3.

### Parallel Opportunities

- T002, T003 can run in parallel within Phase 1
- T005 can start alongside T004 in Phase 2
- T008 can run in parallel with T006/T007 within Phase 3
- T012 can run in parallel with T011/T013 within Phase 5
- T015 can run in parallel with T014 within Phase 6
- T016, T017 can run in parallel within Phase 7
- US3 (Phase 5) and US4 (Phase 6) can be worked fully in parallel with each other

---

## Parallel Example: US3 and US4 (can run simultaneously after Phase 2)

**Developer A — US3 (Research)**:
1. T011 — create `content/research/_index.md`
2. T012 — create `content/research/placeholder-paper.md`
3. T013 — create `layouts/research/list.html`

**Developer B — US4 (CV)**:
1. T014 — create `content/cv/_index.md`
2. T015 — add `static/cv/cv-placeholder.pdf`

Both complete independently; neither blocks the other.
