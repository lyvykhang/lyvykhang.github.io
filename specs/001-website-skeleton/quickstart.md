# Quickstart: Website Skeleton Validation

## Purpose
Validate the website templating skeleton for Home/About (+ News subsection), Research, and CV.

## Prerequisites
- Hugo installed and available in PATH.
- Repository cloned locally.
- Feature branch: `001-website-skeleton`.

## Setup
1. From repository root, ensure content and layout placeholder files are present for:
   - Home/About page with News subsection
   - Research page
   - CV destination (PDF or page)
2. Start local server:

```powershell
hugo server -D
```

## Validation Scenarios

### Scenario 1: Navigation skeleton
1. Open the local site.
2. Confirm top navigation has exactly:
   - Home/About
   - Research
   - CV
3. Confirm News is not a top-level header.

Expected outcome:
- Navigation is limited to Home/About, Research, CV.
- News appears only within Home/About content.

### Scenario 2: Home/About content block
1. Open Home/About page.
2. Verify presence of:
   - Bio placeholder
   - Profile image placeholder with alt text
   - Research summary placeholder
   - News subsection heading and placeholder entries

Expected outcome:
- All required sections render with semantic heading order.

### Scenario 3: Research page structure
1. Open Research page.
2. Verify publication list placeholders include fields:
   - Title
   - Authors
   - Venue
   - Date
   - DOI/URL placeholder

Expected outcome:
- Entries are displayed in reverse chronological order.

### Scenario 4: CV route behavior
1. Open CV from top navigation.
2. Confirm destination resolves to configured placeholder:
   - PDF asset OR markdown page.

Expected outcome:
- CV destination loads without broken links.

## Contract References
- Navigation/content contract: `contracts/site-skeleton-contract.md`
- Data entities and validation: `data-model.md`

## Out of Scope
- GitHub Pages deployment tasks and deployment validation.
- Analytics, comments, search, or dynamic backend features.
