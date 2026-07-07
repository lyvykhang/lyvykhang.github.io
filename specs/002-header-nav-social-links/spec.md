# Feature Specification: Header Navigation & Social Links Redesign

**Feature Branch**: `002-header-nav-social-links`

**Created**: 2026-07-07

**Status**: Draft

**Input**: User description: "Open a new branch for changes to the website header. Overview of the planned changes: According to the theme, the header buttons are currently enclosed in gray buttons. They should just be standalone text. Header buttons should be right-aligned. Add some new buttons for email, LinkedIn, Google Scholar, which should be left-aligned."

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Clean, standalone navigation links (Priority: P1)

A visitor arrives at the site and looks at the top navigation. Instead of the current gray, rounded button boxes around each navigation label, they see clean standalone text links (About, Research, CV). The visual presentation is minimal and reads as text, consistent with an academic site's aesthetic.

**Why this priority**: This is the core visual correction requested and applies to every page of the site. It directly serves the content-first, minimalist design principle and is the most immediately visible change.

**Independent Test**: Load any page and confirm the navigation labels appear as plain text links with no gray background box, no rounded corners, and no button padding, while still being clickable and navigating to the correct destinations.

**Acceptance Scenarios**:

1. **Given** a visitor is on any page of the site, **When** the header renders, **Then** each navigation item (About, Research, CV) appears as standalone text without a gray background, rounded box, or button-like padding.
2. **Given** a visitor clicks a navigation text link, **When** the link is activated, **Then** they are taken to the correct destination (same behavior as before the styling change).
3. **Given** a visitor is on a specific page (e.g. Research), **When** the header renders, **Then** the corresponding navigation link (e.g. "Research") is visually distinguished from the inactive links (e.g. by bold weight or underline).

---

### User Story 2 - Right-aligned navigation (Priority: P2)

A visitor sees the primary navigation links (About, Research, CV) positioned to the right side of the header, distinguishing them from other header elements.

**Why this priority**: Alignment establishes the layout structure that separates primary navigation from the new social/contact links. It depends on the navigation links existing (P1) but is a distinct, independently verifiable change.

**Independent Test**: Load any page and confirm the primary navigation links are aligned to the right edge of the header content area.

**Acceptance Scenarios**:

1. **Given** a visitor is on any page, **When** the header renders, **Then** the primary navigation links (About, Research, CV) are right-aligned within the header.

---

### User Story 3 - Left-aligned social & contact links (Priority: P3)

A visitor sees a set of links for Email, LinkedIn, and Google Scholar on the left side of the header, allowing them to quickly reach the site owner's contact and professional profiles.

**Why this priority**: This adds new functionality (contact/social reach) rather than correcting existing presentation. It builds on the layout established by the previous stories and complements the academic profile.

**Independent Test**: Load any page and confirm Email, LinkedIn, and Google Scholar links appear left-aligned in the header and each opens the correct target (email client, LinkedIn profile, Google Scholar profile).

**Acceptance Scenarios**:

1. **Given** a visitor is on any page, **When** the header renders, **Then** links for Email, LinkedIn, and Google Scholar appear left-aligned within the header.
2. **Given** a visitor activates the Email link, **When** the link is clicked, **Then** their email client opens a new message addressed to the site owner.
3. **Given** a visitor activates the LinkedIn link, **When** the link is clicked, **Then** the site owner's LinkedIn profile opens.
4. **Given** a visitor activates the Google Scholar link, **When** the link is clicked, **Then** the site owner's Google Scholar profile opens.

---

### Edge Cases

- **Narrow / mobile viewport**: When the header width is constrained, the left-aligned social links and right-aligned navigation must remain readable and usable without overlapping or being cut off (they may wrap to multiple lines).
- **Missing profile URL**: If a social/contact destination is not yet configured, the corresponding link should not render as a broken or empty link.
- **Keyboard & screen reader access**: All links (navigation and social) must remain reachable and identifiable via keyboard navigation and assistive technologies, since they are now text/icon links rather than buttons.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The site MUST render the primary navigation items (About, Research, CV) as standalone text links without a gray background, rounded corners, or button-style padding.
- **FR-002**: The primary navigation links MUST be right-aligned within the header on every page.
- **FR-003**: The site MUST display Email, LinkedIn, and Google Scholar links in the header as text labels ("Email", "LinkedIn", "Google Scholar") with no icons.
- **FR-004**: The Email, LinkedIn, and Google Scholar links MUST be left-aligned within the header on every page.
- **FR-005**: The Email link MUST open a new message addressed to `ly.vy.khang@gmail.com`.
- **FR-006**: The LinkedIn link MUST navigate to `https://www.linkedin.com/in/khang-l-39b9b5188/` and MUST open in a new browser tab.
- **FR-007**: The Google Scholar link MUST navigate to `https://scholar.google.com/citations?hl=en&user=XtAbZ3YAAAAJ` and MUST open in a new browser tab.
- **FR-008**: All navigation and social/contact links MUST preserve keyboard accessibility and provide accessible labels for assistive technologies.
- **FR-009**: The header layout MUST remain functional and readable on narrow (mobile) viewports, with links wrapping rather than overlapping or being clipped.
- **FR-010**: The styling change MUST apply consistently across all pages that render the site header.
- **FR-011**: The navigation link corresponding to the current page MUST be visually distinguished from inactive navigation links (e.g. via bold weight or underline).

### Key Entities *(include if feature involves data)*

- **Navigation link**: A primary site-section link with a display label (About, Research, CV) and a destination URL.
- **Social/contact link**: An external or contact link with a display label and/or icon (Email, LinkedIn, Google Scholar), a destination (mailto address or profile URL), and an accessible label.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: 100% of site pages display the primary navigation as standalone text (no gray button box) after the change, with the active page link visually distinguished from inactive links.
- **SC-002**: On every page, the primary navigation links are positioned on the right and the social/contact links are positioned on the left of the header.
- **SC-003**: All three social/contact links (Email, LinkedIn, Google Scholar) are present and each successfully reaches its intended destination when activated.
- **SC-004**: The header remains usable on viewports as narrow as 320px wide, with no link text overlapping or clipped.
- **SC-005**: All header links are reachable via keyboard-only navigation and expose a meaningful accessible name.

## Clarifications

### Session 2026-07-07

- Q: What are the actual destination values for the three social/contact header links? → A: Email: `ly.vy.khang@gmail.com`; LinkedIn: `https://www.linkedin.com/in/khang-l-39b9b5188/`; Google Scholar: `https://scholar.google.com/citations?hl=en&user=XtAbZ3YAAAAJ`
- Q: Should LinkedIn and Google Scholar links open in a new browser tab or the same tab? → A: New tab for external links (LinkedIn, Google Scholar); Email (`mailto:`) opens in the default email client
- Q: How should social/contact links be presented — text labels, icons only, or text with icons? → A: Text labels only ("Email", "LinkedIn", "Google Scholar")
- Q: Should the currently active navigation link be visually distinguished from the others? → A: Yes, the active nav link should be visually distinguished (e.g. bold or underlined)
- Q: Should the header style override be applied in a project-level CSS file or by editing the theme directly? → A: Project-level CSS override only; theme files must not be modified

## Assumptions

- The contact email address is `ly.vy.khang@gmail.com`. The LinkedIn profile is `https://www.linkedin.com/in/khang-l-39b9b5188/`. The Google Scholar profile is `https://scholar.google.com/citations?hl=en&user=XtAbZ3YAAAAJ`. No placeholder values are needed.
- The existing XMin theme and its centered-menu styling are the baseline being modified; all overrides MUST be applied at the project level (e.g. a file in `static/css/` or via `layouts/_partials/head_custom.html`) without touching any file under `themes/`.
- LinkedIn and Google Scholar links open in a new browser tab (`target="_blank"` with appropriate security attributes). The Email `mailto:` link opens in the default email client (standard browser behavior).
- Social/contact links use plain text labels only ("Email", "LinkedIn", "Google Scholar"); no icon library or icon assets are needed.
- The change is styling and header-markup only and does not alter page content, routing, or the build/deploy process.
