# Implementation Plan: Website Skeleton

**Branch**: `001-website-skeleton` | **Date**: 2026-06-24 | **Spec**: `specs/001-website-skeleton/spec.md`

**Input**: Feature specification from `/specs/001-website-skeleton/spec.md`

## Summary

Build a static website skeleton for an academic profile using Hugo + XMin with three top-level headers (Home/About, Research, CV). Home/About includes bio, profile image, research summary, and a News subsection. Research provides publication placeholders with required metadata. CV resolves to either a placeholder page or placeholder PDF path. This plan explicitly excludes GitHub Pages deployment work and focuses only on website templating/content structure.

## Technical Context

**Language/Version**: Markdown content + Hugo templates (Go template syntax), Hugo project configuration

**Primary Dependencies**: Hugo static site generator, XMin theme

**Storage**: File-based content and static assets in repository (`content/`, `static/`, `layouts/`)

**Testing**: Local static validation via `hugo server -D` and manual acceptance checks from `quickstart.md`

**Target Platform**: Static website served in modern desktop/mobile browsers

**Project Type**: Static website templating project

**Performance Goals**: Main pages (Home/About, Research, CV) load within 2 seconds on standard broadband (from spec SC-006)

**Constraints**:
- Static-first: no backend, no database, no required JavaScript behavior
- Accessibility baseline: semantic HTML, alt text, keyboard reachable navigation
- News must be a Home/About subsection, not a top-level header
- Exclude deployment planning/tasks (GitHub Pages already configured)

**Scale/Scope**:
- 3 top-level navigation destinations
- Placeholder content/assets for initial skeleton
- No analytics, comments, search, or dynamic features

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

### Pre-Phase 0 Gate Review
- Principle I (Content-First Design): PASS
  - Plan centers on required academic content blocks and navigation clarity.
- Principle II (Accuracy & Attribution): PASS
  - Publication and news structures include dated/source fields for future accurate content.
- Principle III (Static-First Implementation): PASS
  - File-based content/templates only; no runtime backend.
- Principle IV (Simplicity & Accessibility): PASS
  - Minimal XMin-aligned structure with accessibility checks defined.

Gate status: PASS. Proceed to Phase 0.

### Post-Phase 1 Re-Check
- `research.md` resolves technical choices without adding complexity.
- `data-model.md` keeps entities minimal and content-focused.
- `contracts/site-skeleton-contract.md` enforces nav and accessibility contracts, including News as Home/About subsection.
- `quickstart.md` validates templating behavior only; deployment excluded.

Gate status: PASS after design.

## Project Structure

### Documentation (this feature)

```text
specs/001-website-skeleton/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── site-skeleton-contract.md
└── tasks.md
```

### Source Code (repository root)

```text
content/
├── _index.md                  # Home/About content with News subsection
├── research/
│   └── _index.md              # Research landing page and publication placeholders
└── cv/
    └── _index.md              # CV page placeholder (if page mode)

layouts/
├── _default/
│   ├── list.html              # Section/list rendering (if overridden)
│   └── single.html            # Single page rendering (if overridden)
└── _partials/
    └── header.html            # Navigation labels/ordering if customization needed

static/
├── images/
│   └── profile-placeholder.jpg
└── cv/
    └── cv-placeholder.pdf     # Optional if CV uses PDF mode

themes/xmin/
└── ...                        # Existing theme implementation retained
```

**Structure Decision**: Use Hugo's existing content/layout/static directories with minimal overrides. No new application layers are introduced.

## Complexity Tracking

No constitution violations or complexity exceptions identified.
