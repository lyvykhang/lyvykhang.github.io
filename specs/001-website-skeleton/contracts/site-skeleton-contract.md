# Contract: Site Skeleton Interface

## Scope
Defines user-visible interface expectations for the static website skeleton.

## Global Navigation Contract
- Top-level headers MUST be:
  - `Home/About`
  - `Research`
  - `CV`
- `News` MUST NOT appear as a top-level navigation item.
- Navigation links MUST be keyboard focusable and screen-reader readable.

## Home/About Contract
- MUST render the following sections in order:
  1. About (bio)
  2. Profile image
  3. Research summary
  4. News subsection
- News subsection:
  - Shows list of dated items in reverse chronological order.
  - Supports empty state placeholder text.

## Research Contract
- MUST render a publication list where each item supports:
  - Title
  - Authors
  - Venue
  - Date
  - DOI/URL (if available)
- List order MUST be reverse chronological by publication date.
- Empty state placeholder MUST be displayed when no publications exist.

## CV Contract
- `CV` nav link MUST resolve to one of:
  - Static PDF asset path, or
  - Dedicated CV content page path
- Broken destination links are considered contract violations.

## Accessibility Contract
- Semantic headings and landmarks must be present.
- Profile image must include alt text.
- All interactive links and controls must be keyboard reachable.

## Error/Edge Behavior Contract
- Missing profile image: render alt text/fallback and preserve layout flow.
- Empty News/Research: render explicit placeholder state.
- Broken publication links: mark for correction in content review workflow.
