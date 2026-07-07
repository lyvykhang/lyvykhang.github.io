# Implementation Plan: Header Navigation & Social Links Redesign

**Branch**: `002-header-nav-social-links` | **Date**: 2026-07-07 | **Spec**: [spec.md](spec.md)

**Input**: Feature specification from `specs/002-header-nav-social-links/spec.md`

## Summary

Restructure the site header to replace the XMin theme's gray button-styled navigation links with clean standalone text, split the header into a flexbox row with social/contact links (Email, LinkedIn, Google Scholar) on the left and primary navigation (About, Research, CV) on the right, and add active-page highlighting to the nav links. All changes are applied at the project level via a new CSS override file and an updated header partial — no theme files are modified.

## Technical Context

**Language/Version**: Hugo static site generator (Go templates); HTML5 / CSS3

**Primary Dependencies**: XMin theme (baseline); no additional libraries or icon fonts required

**Storage**: N/A — static site, no database

**Testing**: Manual visual verification via `hugo server -D`; automated screenshot/viewport testing optional

**Target Platform**: Static HTML served via GitHub Pages

**Project Type**: Static website (Hugo)

**Performance Goals**: N/A — changes are pure HTML/CSS with no runtime overhead

**Constraints**: No JavaScript; no external CDN dependencies; theme files under `themes/` must not be modified; all changes must render correctly without JS

**Scale/Scope**: Single shared header partial — affects every rendered page of the site

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Principle | Pre-Design | Post-Design |
|-----------|-----------|-------------|
| **I. Content-First Design** | ✅ Header restructuring serves navigation clarity; no content is hidden or delayed | ✅ Flexbox layout keeps nav and social links minimal and non-intrusive |
| **II. Accuracy & Attribution** | ✅ Not applicable to header styling changes | ✅ Social link URLs are verified and accurate |
| **III. Static-First** | ✅ Pure HTML/CSS; no JavaScript added; no external CDN | ✅ CSS override file is self-hosted static asset; `target="_blank"` requires no JS |
| **IV. Simplicity & Accessibility** | ✅ Removing button boxes simplifies UI; text labels + active state improve orientation | ✅ `rel="noopener noreferrer"` on external links; accessible nav landmark preserved; keyboard order maintained |

**Verdict**: All gates pass. No violations. Complexity Tracking table not required.

## Project Structure

### Documentation (this feature)

```text
specs/002-header-nav-social-links/
├── plan.md              # This file
├── research.md          # Phase 0 output
├── data-model.md        # Phase 1 output
├── quickstart.md        # Phase 1 output
├── contracts/
│   └── header-contract.md  # Phase 1 output
└── tasks.md             # Phase 2 output (/speckit.tasks — NOT created here)
```

### Source Code (repository root)

```text
layouts/
└── _partials/
    ├── header.html          # MODIFY: restructure nav into flexbox with social + nav groups
    └── head_custom.html     # CREATE: link to project-level CSS override

static/
└── css/
    └── header.css           # CREATE: CSS overrides for button removal, flexbox layout,
                             #         active-link style, mobile responsive wrapping
```

**Structure Decision**: Hugo's file-merge means project-level files in `layouts/` and `static/` override or extend theme files of the same path. No theme files are touched. `head_custom.html` is already referenced in `header.html` via `{{ partial "head_custom.html" . }}`; creating a project-level version of this partial is the correct Hugo extension point for injecting additional CSS.
