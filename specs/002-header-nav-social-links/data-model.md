# Data Model: Header Navigation & Social Links Redesign

**Date**: 2026-07-07
**Branch**: `002-header-nav-social-links`

---

## Overview

The header is composed of two ordered groups rendered in a single flexbox row. There is no database or dynamic data source — all values are either Hugo configuration (`hugo.toml`) or hardcoded in the header partial template.

---

## Entity: Navigation Link

Represents a primary site-section link rendered on the right side of the header.

| Attribute | Type | Source | Constraint |
|-----------|------|--------|------------|
| `Name` | string | `hugo.toml` `[[menu.main]]` | Non-empty; display label (e.g. "About", "Research", "CV") |
| `URL` | string | `hugo.toml` `[[menu.main]]` | Non-empty; relative or absolute URL |
| `Weight` | integer | `hugo.toml` `[[menu.main]]` | Controls display order; lower = first |
| `IsActive` | boolean (computed) | Hugo template (`IsMenuCurrent` / `HasMenuCurrent`) | True when the rendered page matches this entry or is a descendant section |

**Lifecycle**: Defined statically in `hugo.toml`. No create/update/delete at runtime.

**State transitions**: None — `IsActive` is computed per-render from the current request path.

**Validation rules**:
- There must be at least one navigation link for the right group to render.
- `URL` must resolve to a valid page or asset within the site.

**Current values** (from `hugo.toml`):

| Name | URL | Weight |
|------|-----|--------|
| About | `/` | 1 |
| Research | `/research/` | 2 |
| CV | `/cv/cv-placeholder.pdf` | 3 |

---

## Entity: Social Link

Represents a contact or external-profile link rendered on the left side of the header.

| Attribute | Type | Source | Constraint |
|-----------|------|--------|------------|
| `Label` | string | Hardcoded in `header.html` | Non-empty; plain text display label |
| `URL` | string | Hardcoded in `header.html` | Non-empty; `mailto:` or `https://` URL |
| `OpensNewTab` | boolean | Hardcoded in `header.html` | True for `https://` URLs; false (N/A) for `mailto:` |
| `RelAttribute` | string | Hardcoded in `header.html` | `"noopener noreferrer"` for new-tab links; absent for `mailto:` |

**Lifecycle**: Defined statically in `layouts/_partials/header.html`. No runtime data source.

**Validation rules**:
- `mailto:` links must carry a valid email address.
- `https://` links that use `target="_blank"` must carry `rel="noopener noreferrer"`.
- All links must have a non-empty, human-readable `Label`.

**Defined values**:

| Label | URL | OpensNewTab | RelAttribute |
|-------|-----|-------------|--------------|
| Email | `mailto:ly.vy.khang@gmail.com` | false | — |
| LinkedIn | `https://www.linkedin.com/in/khang-l-39b9b5188/` | true | `noopener noreferrer` |
| Google Scholar | `https://scholar.google.com/citations?hl=en&user=XtAbZ3YAAAAJ` | true | `noopener noreferrer` |

---

## Entity: Header Layout

The structural container that positions the two groups.

| Attribute | Type | Value |
|-----------|------|-------|
| `Layout` | CSS | Flexbox row, `justify-content: space-between` |
| `LeftGroup` | component | Social Links (ordered: Email, LinkedIn, Google Scholar) |
| `RightGroup` | component | Navigation Links (ordered by `Weight`) |
| `MobileBreakpoint` | CSS media query | `max-width: 480px` → stacks vertically, left-aligned |

---

## CSS Class Map

| Class | Applied To | Purpose |
|-------|-----------|---------|
| `.header-nav` | wrapper `<div>` | Flexbox row containing both groups |
| `.header-social` | left `<div>` | Social link group |
| `.menu` | right `<ul>` | Navigation link group (existing theme class, reused) |
| `.menu a` | nav `<a>` tags | Override: remove button styling (background, padding, border-radius) |
| `.menu a.active` | active nav `<a>` | Bold + underline to indicate current page |
| `.header-social a` | social `<a>` tags | Remove underline decoration |
