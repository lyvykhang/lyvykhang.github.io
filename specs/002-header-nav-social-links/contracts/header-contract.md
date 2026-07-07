# Header Partial Contract

**Date**: 2026-07-07
**Branch**: `002-header-nav-social-links`
**File**: `layouts/_partials/header.html`

---

## Purpose

This contract defines the rendered HTML structure that `header.html` must produce and the CSS classes it exposes. Any implementation of the header partial must conform to this contract to satisfy FR-001 through FR-011 and the data model in [data-model.md](../data-model.md).

---

## Rendered HTML Structure

```html
<!DOCTYPE html>
<html lang="{locale}">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>{page title} | {site title}</title>
    <link rel="stylesheet" href="{base}/css/style.css" />
    <link rel="stylesheet" href="{base}/css/fonts.css" />
    <!-- head_custom.html injects: -->
    <link rel="stylesheet" href="{base}/css/header.css" />
  </head>
  <body>
    <nav aria-label="Main navigation">
      <div class="header-nav">

        <!-- LEFT: social/contact links -->
        <div class="header-social">
          <a href="mailto:ly.vy.khang@gmail.com">Email</a>
          <a href="https://www.linkedin.com/in/khang-l-39b9b5188/"
             target="_blank"
             rel="noopener noreferrer">LinkedIn</a>
          <a href="https://scholar.google.com/citations?hl=en&amp;user=XtAbZ3YAAAAJ"
             target="_blank"
             rel="noopener noreferrer">Google Scholar</a>
        </div>

        <!-- RIGHT: primary navigation links -->
        <ul class="menu">
          <!-- For each [[menu.main]] entry, ordered by weight: -->
          <li><a href="{url}"{' class="active"' if active}>About</a></li>
          <li><a href="{url}"{' class="active"' if active}>Research</a></li>
          <li><a href="{url}"{' class="active"' if active}>CV</a></li>
        </ul>

      </div>
      <hr/>
    </nav>
```

---

## Contracts / Rules

### Header layout (`<div class="header-nav">`)
- MUST be a flex container with social links on the left and navigation on the right.
- MUST NOT use JavaScript for layout.

### Social links (`<div class="header-social">`)
- MUST contain exactly three `<a>` elements with labels "Email", "LinkedIn", "Google Scholar" in that order.
- Email link MUST use `href="mailto:ly.vy.khang@gmail.com"`. MUST NOT carry `target` or `rel`.
- LinkedIn link MUST use `href="https://www.linkedin.com/in/khang-l-39b9b5188/"`, `target="_blank"`, `rel="noopener noreferrer"`.
- Google Scholar link MUST use `href="https://scholar.google.com/citations?hl=en&user=XtAbZ3YAAAAJ"`, `target="_blank"`, `rel="noopener noreferrer"`.
- All social `<a>` tags MUST have non-empty, human-readable text content (label).

### Navigation links (`<ul class="menu">`)
- MUST render one `<li>` per `[[menu.main]]` entry in `hugo.toml`, in weight order.
- Each `<a>` MUST carry `class="active"` when `IsMenuCurrent "main"` or `HasMenuCurrent "main"` is true for that entry.
- MUST NOT carry `target="_blank"` (internal links stay in same tab).

### CSS override file (`static/css/header.css`)
- MUST set `.menu a`: `background: none`, `padding: 0`, `border-radius: 0`.
- MUST set `.menu a.active`: visually distinguished (bold and/or underline).
- MUST set `.header-nav`: `display: flex`, `justify-content: space-between`, `align-items: center`.
- MUST provide a `@media (max-width: 480px)` rule that stacks groups vertically without overlap.
- MUST NOT modify any rule in `themes/xmin/static/css/style.css`.

### Accessibility
- `<nav>` element MUST carry `aria-label="Main navigation"`.
- All `<a>` elements MUST have visible, non-empty text content.
- Tab order MUST follow document order: social links first (left), then navigation links (right).

---

## What This Contract Does NOT Define

- Exact pixel measurements for gaps or font sizes (implementation detail).
- Whether `.menu a.active` uses bold, underline, or both (implementation may choose either; bold + underline is the recommended default per spec).
- Color values for link text (inherits from theme).
