# Data Model: Website Skeleton

## Entity: ResearcherProfile
- Purpose: Represents homepage/about identity content.
- Fields:
  - `name` (string, required)
  - `bio` (markdown text, required)
  - `research_summary` (markdown text, required)
  - `profile_image_path` (string path, required)
  - `contact_links` (list of `{label, url}`, optional)
- Validation rules:
  - `profile_image_path` must reference an existing static asset.
  - `bio` and `research_summary` must not be empty.
- Relationships:
  - One-to-many with `NewsItem` (displayed as subsection on Home/About).

## Entity: NewsItem
- Purpose: Represents dated announcements shown under Home/About.
- Fields:
  - `title` (string, required)
  - `date` (date, required)
  - `summary` (markdown text, required)
  - `link` (URL, optional)
- Validation rules:
  - `date` must be valid ISO date.
  - Items must render in reverse chronological order.
- State transitions:
  - Draft -> Published (via content file presence/status convention).

## Entity: Publication
- Purpose: Represents entries on the Research page.
- Fields:
  - `title` (string, required)
  - `authors` (list of strings, required)
  - `venue` (string, required)
  - `publication_date` (date, required)
  - `doi_or_url` (string URL, optional but recommended)
  - `abstract_or_note` (markdown text, optional)
- Validation rules:
  - `title`, `authors`, `venue`, `publication_date` required.
  - Sort by `publication_date` descending.

## Entity: CVResource
- Purpose: Represents CV destination from nav.
- Fields:
  - `mode` (enum: `pdf` | `page`, required)
  - `path` (string path, required)
  - `last_updated` (date, optional)
- Validation rules:
  - If `mode=pdf`, `path` must exist in static assets.
  - If `mode=page`, `path` must resolve to a Hugo content page.

## Relationship Summary
- `ResearcherProfile` 1..1 owns Home/About section content.
- `ResearcherProfile` 1..N includes `NewsItem` subsection items.
- Research page aggregates `Publication` entries.
- Header CV link resolves through `CVResource`.
