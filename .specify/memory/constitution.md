<!-- SYNC IMPACT REPORT (v1.0.0)
  Version Bump: INITIAL → 1.0.0 (New constitution)
  Added Principles: I. Content-First Design, II. Accuracy & Attribution, III. Static-First, IV. Simplicity & Accessibility
  Added Sections: Structure & Organization, Development Workflow, Governance
  No principles removed or renamed (initial constitution)
  Templates requiring updates: ✅ plan-template.md, ✅ spec-template.md, ✅ tasks-template.md
  No intentionally deferred placeholders
-->

# lyvykhang.github.io: Academic CV & Publications Constitution

## Core Principles

### I. Content-First Design
Every page prioritizes substantive academic and professional content; navigation and styling serve
content, not the reverse. Content structure drives layout decisions. The site exists to showcase
research, credentials, and professional milestones—UI must never obscure or delay access to this
information. All design choices must justify their value in surfacing or contextualizing content.

### II. Accuracy & Attribution
All publications, credentials, career information, and announcements must be verifiable and
accurately dated. Every research claim has source attribution (DOI, link, or permanent archive).
News and career updates reflect actual changes (new publications, position changes, etc.).
Corrections and updates take absolute priority over new content—misinformation or outdated
claims MUST be addressed immediately upon discovery.

### III. Static-First Implementation
The site is generated as static HTML, CSS, and assets via Hugo; external dependencies are
minimized. All pages render correctly without JavaScript. PDFs, images, and other academic
assets are self-hosted as static files. Dynamic content (e.g., external widget feeds) is
avoided unless it has clear academic value and graceful fallback behavior.

### IV. Simplicity & Accessibility
The XMin theme enforces minimalism; unnecessary UI elements are removed. Semantic HTML ensures
proper document structure. The site is readable and navigable via keyboard and screen readers.
Readability is prioritized: sufficient contrast, legible fonts, clear hierarchy. Mobile rendering
must be functional (not necessarily beautiful) but never sacrifices content accessibility.

## Structure & Organization

**Mandatory Pages:**
- **Homepage (About Me)**: Bio paragraph(s), profile picture, brief research direction summary, subsection for news & announcements (career milestones, new publications, etc.)
- **Research**: Listing of publications (sorted by date, with links/PDIs, co-authors)
- **CV**: Static PDF asset, LaTeX-generated page, or regular markdown page with full CV content

Content is organized by publication date and career timeline. Archives are maintained for historical
reference. Each publication entry includes: title, authors, venue, date, link/DOI, and short description
if needed for context.

## Development Workflow

Local testing is performed via `hugo server -D` before publishing to GitHub Pages. Content updates
are made via Markdown files in `content/posts/` or appropriate section directory. Commits use clear,
descriptive messages referencing the type of update (publication, bio update, news, etc.). GitHub
Pages auto-deploys on `main` branch push. All changes are tracked in Git history for audit and
recovery purposes.

## Governance

This constitution supersedes all other development practices for the site. All updates must preserve
content accuracy (Principle II takes precedence over speed of deployment). Theme customizations must
not violate Principles I or IV (content-first, simplicity, accessibility). A quarterly review of
publications and career milestones is performed to ensure currency and accuracy. Amendments to this
constitution require clear documentation of rationale and impact on existing content.

**Version**: 1.0.0 | **Ratified**: 2026-06-23 | **Last Amended**: 2026-06-23
