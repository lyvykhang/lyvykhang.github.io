# Research: Website Skeleton

## Decision 1: Keep Hugo + XMin default templating as baseline
- Decision: Use Hugo with the existing XMin theme and minimal template overrides only where required for Home/About + News subsection, Research page, and CV page.
- Rationale: Aligns with constitution principles (content-first, static-first, simplicity) and minimizes maintenance risk.
- Alternatives considered:
  - Full custom theme rebuild: rejected due to unnecessary complexity for a skeleton phase.
  - Theme switch: rejected because XMin already meets minimal/accessibility goals.

## Decision 2: Represent content with Hugo content files and front matter
- Decision: Store homepage/about content, News entries, Research publications, and CV metadata in markdown content files with front matter.
- Rationale: Non-technical editing workflow, versioned content, and straightforward static generation.
- Alternatives considered:
  - Data files only (`data/*.yaml`): rejected because markdown content is easier for narrative sections.
  - External CMS: rejected; violates static-first and introduces operational overhead.

## Decision 3: News remains a Home/About subsection, not navigation header
- Decision: Implement News as an on-page subsection under Home/About.
- Rationale: Matches user requirement and keeps primary navigation focused on Home/About, Research, CV.
- Alternatives considered:
  - Separate News top-level section: rejected per updated requirement.

## Decision 4: CV delivery mode for skeleton
- Decision: Support both a placeholder static PDF path and a placeholder markdown CV page, with one active route in nav.
- Rationale: Requirement allows either format; skeleton should keep both options open until final CV source is chosen.
- Alternatives considered:
  - Force PDF-only: rejected because user indicated format is undecided.
  - Force page-only: rejected for same reason.

## Decision 5: Validation approach for this feature
- Decision: Validate by local Hugo build/run and manual acceptance checks; no deployment validation included.
- Rationale: User explicitly excluded GitHub Pages deployment planning.
- Alternatives considered:
  - End-to-end deployment checks: rejected as out of scope.

## Decision 6: Accessibility baseline
- Decision: Require semantic headings, alt text for profile image, keyboard-reachable links, and readable contrast in existing theme styles.
- Rationale: Satisfies constitution accessibility principle with low implementation overhead.
- Alternatives considered:
  - Defer accessibility to later phase: rejected because accessibility is a core principle.
