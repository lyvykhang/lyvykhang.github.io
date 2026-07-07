# Quickstart: Validating the Header Navigation & Social Links Redesign

**Date**: 2026-07-07
**Branch**: `002-header-nav-social-links`

This guide describes how to run the site locally and verify that each acceptance scenario from the spec is satisfied. Implementation details (exact CSS values, Hugo template syntax) are in [contracts/header-contract.md](contracts/header-contract.md) and [data-model.md](data-model.md).

---

## Prerequisites

- Hugo installed and available on `PATH` (any recent version; the project uses the XMin theme bundled under `themes/`)
- Working directory: repository root (`c:\Repos\lyvykhang.github.io`)
- Branch checked out: `002-header-nav-social-links`

---

## Start the Development Server

```powershell
hugo server -D
```

Hugo will print the local URL (default: `http://localhost:1313/`). Open it in a browser.

---

## Validation Scenarios

### SC-001 / FR-001 — No gray button boxes on nav links

1. Open `http://localhost:1313/` (or any page).
2. Look at the top navigation area.
3. **Pass**: The labels "About", "Research", and "CV" appear as plain text links — no gray background, no rounded box, no visible button padding.
4. **Fail**: Any nav label has a visible gray/colored background or raised button appearance.

---

### SC-001 / FR-011 — Active nav link is visually distinguished

1. Open `http://localhost:1313/` (About page).
2. Check: the "About" link appears bold and/or underlined; "Research" and "CV" do not.
3. Navigate to `http://localhost:1313/research/`.
4. Check: "Research" is now distinguished; "About" and "CV" are not.
5. Navigate to `http://localhost:1313/cv/cv-placeholder.pdf` (or the CV URL).
6. Check: "CV" is distinguished.
7. **Pass**: Exactly one nav link is visually distinguished per page, matching the current section.

---

### SC-002 / FR-002 — Navigation links are right-aligned

1. Open any page.
2. **Pass**: "About", "Research", "CV" are positioned toward the right edge of the content area.
3. **Fail**: Nav links are centered or left-aligned.

---

### SC-002 / FR-004 — Social links are left-aligned

1. Open any page.
2. **Pass**: "Email", "LinkedIn", "Google Scholar" are positioned toward the left edge of the content area, on the same row as the nav links (or above them on narrow viewports).
3. **Fail**: Social links are centered or to the right of the nav links.

---

### SC-003 / FR-005 — Email link opens email client

1. Click "Email" in the header.
2. **Pass**: The default email client opens a new compose window addressed to `ly.vy.khang@gmail.com`.
3. **Fail**: Link is broken, opens a new browser tab with an error, or addresses a different email.

---

### SC-003 / FR-006 — LinkedIn link opens in new tab

1. Click "LinkedIn" in the header.
2. **Pass**: `https://www.linkedin.com/in/khang-l-39b9b5188/` opens in a **new browser tab**; the original site tab remains open.
3. **Fail**: LinkedIn opens in the same tab, or the URL is incorrect.

---

### SC-003 / FR-007 — Google Scholar link opens in new tab

1. Click "Google Scholar" in the header.
2. **Pass**: `https://scholar.google.com/citations?hl=en&user=XtAbZ3YAAAAJ` opens in a **new browser tab**; the original site tab remains open.
3. **Fail**: Google Scholar opens in the same tab, or the URL is incorrect.

---

### SC-004 / FR-009 — Mobile viewport (narrow)

1. In browser DevTools, set viewport width to **320px**.
2. Reload the page.
3. **Pass**: Social links and nav links are readable; no text is clipped or overlapping; links may wrap to a second line.
4. **Fail**: Links overflow the viewport, overlap each other, or become unreadable.

---

### SC-005 / FR-008 — Keyboard accessibility

1. With keyboard only (no mouse), press `Tab` from the top of any page.
2. **Pass**: Focus moves through "Email" → "LinkedIn" → "Google Scholar" → "About" → "Research" → "CV" in that order (document order). Each focused link is visibly highlighted by the browser's default focus ring.
3. **Fail**: Any link is skipped, focus order is unexpected, or no focus indicator is visible.

---

### Constitution Gate — No theme files modified

```powershell
git diff --name-only HEAD
```

**Pass**: Output does not include any path under `themes/`.
**Fail**: Any file under `themes/` appears in the diff.
