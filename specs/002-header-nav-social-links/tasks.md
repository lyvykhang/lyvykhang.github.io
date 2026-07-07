# Tasks: Header Navigation & Social Links Redesign

**Input**: Design documents from `specs/002-header-nav-social-links/`

**Prerequisites**: [plan.md](plan.md) ✅, [spec.md](spec.md) ✅, [research.md](research.md) ✅, [data-model.md](data-model.md) ✅, [contracts/header-contract.md](contracts/header-contract.md) ✅

**Tests**: Manual visual verification via `hugo server -D` per [quickstart.md](quickstart.md); no automated tests requested in feature specification.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

---

## Phase 1: Setup (Project-Level Files)

**Purpose**: Prepare project-level CSS and partial structure for header overrides

- [X] T001 Create project-level `layouts/_partials/head_custom.html` with link to `css/header.css`
- [X] T002 Create project-level `static/css/header.css` with initial structure (empty rule sets for header components)

---

## Phase 2: Foundational (Header Partial Restructuring)

**Purpose**: Update the header partial to support flexbox layout and social links — shared infrastructure for all user stories

**⚠️ CRITICAL**: This phase must complete before any user story work can begin. The restructured header template is the baseline all stories depend on.

- [X] T003 Update `layouts/_partials/header.html` to wrap nav content in `<div class="header-nav">` flexbox container
- [X] T004 Add social links markup (`<div class="header-social">` with Email, LinkedIn, Google Scholar `<a>` tags) to `layouts/_partials/header.html`
- [X] T005 Add active navigation link detection logic (Hugo `IsMenuCurrent` / `HasMenuCurrent`) to `layouts/_partials/header.html` template loop
- [X] T006 Verify header partial renders without errors via `hugo server -D` (no CSS styling applied yet)

**Checkpoint**: Foundation ready — header partial is restructured with all required markup. CSS styling now ready to be applied per user story.

---

## Phase 3: User Story 1 - Clean, standalone navigation links (Priority: P1) 🎯 MVP

**Goal**: Remove gray button styling from navigation links and display them as plain text

**Independent Test**: Load any page via `hugo server -D` and confirm navigation items (About, Research, CV) appear as plain text links with no gray background, rounded corners, or button padding.

### Implementation for User Story 1

- [X] T007 [P] [US1] Add CSS rule to remove button styling: `.menu a { background: none; padding: 0; border-radius: 0; text-decoration: none; }` in `static/css/header.css`
- [X] T008 [US1] Add CSS rule for active navigation link distinction: `.menu a.active { font-weight: bold; text-decoration: underline; }` in `static/css/header.css`
- [X] T009 [US1] Verify via `hugo server -D`: All nav links appear as plain text, active link is bold/underlined, inactive links have no styling

**Checkpoint**: User Story 1 complete and independently testable. Navigation links now display as plain text with active-state distinction.

---

## Phase 4: User Story 2 - Right-aligned navigation (Priority: P2)

**Goal**: Position primary navigation links on the right side of the header

**Independent Test**: Load any page and confirm About, Research, and CV links are positioned toward the right edge of the header.

### Implementation for User Story 2

- [X] T010 [P] [US2] Add CSS flexbox rules to `static/css/header.css`: `.header-nav { display: flex; justify-content: space-between; align-items: center; }` (separates left and right groups)
- [X] T011 [US2] Verify via `hugo server -D`: Social links appear on the left, nav links appear on the right, both on same row
- [X] T012 [P] [US2] Add mobile breakpoint rule to `static/css/header.css`: `@media (max-width: 480px) { .header-nav { flex-direction: column; align-items: flex-start; gap: 1em; } }` (prevents overlap on narrow viewports)
- [X] T013 [US2] Test on narrow viewport (320px width via DevTools): Links stack vertically without overlap, remain readable

**Checkpoint**: User Story 2 complete. Navigation links are right-aligned, social links are positioned for left-alignment in the next story, and layout is responsive on narrow viewports.

---

## Phase 5: User Story 3 - Left-aligned social & contact links (Priority: P3)

**Goal**: Add Email, LinkedIn, and Google Scholar links to the header, positioned on the left

**Independent Test**: Load any page and confirm Email, LinkedIn, and Google Scholar links appear left-aligned and each link opens the correct destination (email client, LinkedIn profile, Google Scholar profile).

### Implementation for User Story 3

- [X] T014 [P] [US3] Add CSS rule for social link text: `.header-social a { color: inherit; text-decoration: none; }` in `static/css/header.css`
- [X] T015 [P] [US3] Add CSS rule for social link spacing: `.header-social { display: flex; gap: 1em; }` in `static/css/header.css` (horizontal layout with gaps)
- [X] T016 [US3] Manually test Email link via `hugo server -D`: Click Email, confirm default email client opens with `ly.vy.khang@gmail.com` in the `To:` field
- [X] T017 [US3] Manually test LinkedIn link: Click LinkedIn, confirm browser opens `https://www.linkedin.com/in/khang-l-39b9b5188/` in a **new tab**
- [X] T018 [US3] Manually test Google Scholar link: Click Google Scholar, confirm browser opens `https://scholar.google.com/citations?hl=en&user=XtAbZ3YAAAAJ` in a **new tab**
- [X] T019 [US3] Verify `rel="noopener noreferrer"` attributes are present on LinkedIn and Google Scholar `<a>` tags in header markup (security best practice for new-tab links)

**Checkpoint**: All user stories now complete and independently functional. Email, LinkedIn, and Google Scholar links are present and working correctly.

---

## Phase N: Polish & Cross-Cutting Concerns

**Purpose**: Final validation and documentation

- [X] T020 [P] Run quickstart.md validation checklist: Verify SC-001 through SC-005 all pass
- [X] T021 [P] Run keyboard accessibility test: Tab through header links and verify focus order is Email → LinkedIn → Scholar → About → Research → CV
- [X] T022 Verify `git diff` shows NO modifications under `themes/` directory (constitution requirement: no theme files touched)
- [X] T023 [P] Test on desktop (1920px), tablet (768px), and mobile (320px) viewports; confirm layout adapts correctly without overlap or clipping
- [ ] T024 Commit implementation with clear message referencing feature and user stories

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS all user stories
- **User Stories (Phase 3+)**: All depend on Foundational phase completion
  - User stories can then proceed in parallel (if staffed)
  - Or sequentially in priority order (P1 → P2 → P3)
- **Polish (Phase N)**: Depends on all desired user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Can start after Foundational (Phase 2) — No dependencies on other stories. MVP: Can deploy after this story alone.
- **User Story 2 (P2)**: Can start after Foundational (Phase 2) — Builds on US1 but independently testable. Can deploy US1 + US2 together.
- **User Story 3 (P3)**: Can start after Foundational (Phase 2) — Complements US1 + US2 but independently testable. Full feature ready after all three.

### Within Each User Story

- CSS rules before verification/testing
- All parts of a story must be testable before moving to next priority
- Story complete before moving to next

### Parallel Opportunities

- **Phase 1**: Both setup files (T001, T002) can be created in parallel → no dependency
- **Phase 2**: All template updates (T003–006) are sequential changes to the same file → must be done in order
- **Phase 3 (US1)**: T007 and T008 are CSS rules (different rules); T009 is verification
  - T007 + T008 can be written in parallel, but T009 depends on both
- **Phase 4 (US2)**: T010, T012 can be written in parallel (different CSS rules); T011, T013 are verification tests
- **Phase 5 (US3)**: T014, T015 are CSS rules (can be parallel); T016–019 are manual tests; T020 onwards are final validation

**Practical parallel example (single developer)**:
1. Complete Phase 1 (Setup) → 5 minutes
2. Complete Phase 2 (Foundational) → 15 minutes (template updates)
3. Do Phase 3, 4, 5 sequentially (CSS + tests for each story) → ~20 minutes total

**Parallel example (multiple developers)**:
1. Developer writes Phase 1 + 2 (shared setup) → 20 minutes
2. Once Phase 2 done:
   - Developer A: Phase 3 (US1)
   - Developer B: Phase 4 (US2) — can write CSS rules while A tests
   - Developer C: Phase 5 (US3) — can write CSS rules while A + B test
3. All meet for Phase N (cross-story validation)

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup → `.layouts/_partials/head_custom.html` and `static/css/header.css` ready
2. Complete Phase 2: Foundational → Header partial restructured with flexbox + social markup
3. Complete Phase 3: User Story 1 → Navigation links display as plain text with active state
4. **STOP and VALIDATE** via quickstart.md: Can you see plain text nav links? Does active state work?
5. **DEPLOY**: Commit and push to `main` — MVP ships

### Incremental Delivery

1. Deploy User Story 1 (plain text nav, active state) → MVP working
2. Add User Story 2 (right-align nav + responsive layout) → Enhanced layout
3. Add User Story 3 (social links) → Full feature complete

### Quick Full Implementation

1. Complete Setup + Foundational → infrastructure ready
2. Parallel: Write all CSS rules for US1 + US2 + US3 simultaneously (they don't conflict)
3. Sequential: Test and verify each story in priority order
4. Polish & commit
