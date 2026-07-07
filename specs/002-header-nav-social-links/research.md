# Research: Header Navigation & Social Links Redesign

**Date**: 2026-07-07
**Branch**: `002-header-nav-social-links`
**Status**: Complete — no NEEDS CLARIFICATION items remain

---

## 1. Hugo Project-Level CSS Override Pattern

**Decision**: Create `static/css/header.css` in the project root and reference it from a project-level `layouts/_partials/head_custom.html`.

**Rationale**: Hugo merges the project's `static/` directory with the theme's `static/` directory at build time. Files with the same relative path in the project take precedence over theme files. By adding a *new* file `static/css/header.css` (a path that does not exist in the theme), we append an additional stylesheet without touching any theme file. The existing `header.html` already calls `{{ partial "head_custom.html" . }}`; creating a project-level `layouts/_partials/head_custom.html` with a `<link>` tag to `css/header.css` is the idiomatic Hugo extension point.

**Alternatives considered**:
- Copy-and-modify `themes/xmin/static/css/style.css` into `static/css/style.css`: Rejected — replaces the entire theme stylesheet, making theme upgrades difficult and requiring full re-synchronisation on each theme update.
- Inline `<style>` block in `head_custom.html`: Rejected — acceptable but a separate file is easier to maintain, diff, and test.
- Modify `themes/xmin/static/css/style.css` directly: Rejected per spec constraint (FR constraint: no theme file modifications).

---

## 2. Hugo Active Menu Item Detection

**Decision**: Use Hugo's built-in `IsMenuCurrent` and `HasMenuCurrent` methods inside the `range .Site.Menus.main` loop to conditionally apply a CSS `class="active"` attribute.

**Rationale**: These are the idiomatic Hugo methods for active menu detection. `IsMenuCurrent "main" .` returns true when the menu entry is the exact current page. `HasMenuCurrent "main" .` returns true when the current page is a descendant of the menu entry's section — useful for section landing pages (e.g. marking "Research" active when viewing a paper detail page). Using both handles both flat pages and section hierarchies.

**Template pattern**:
```html
{{ $currentPage := . }}
{{ range .Site.Menus.main }}
<li><a href="{{ .URL | relURL }}"
  {{- if or ($currentPage.IsMenuCurrent "main" .) ($currentPage.HasMenuCurrent "main" .) }} class="active"{{ end }}>{{ .Name }}</a></li>
{{ end }}
```

**Alternatives considered**:
- Comparing `.Permalink` to `.Site.BaseURL`: Rejected — fragile, breaks with trailing slashes and subtree pages.
- JavaScript-based active detection: Rejected per constitution Principle III (no JavaScript) and spec constraint.

---

## 3. Flexbox Split-Header Layout

**Decision**: Wrap the header contents in a `<div class="header-nav">` using `display: flex; justify-content: space-between`. Place social links in a `<div class="header-social">` on the left and the existing `<ul class="menu">` on the right.

**Rationale**: CSS Flexbox with `justify-content: space-between` is the simplest, well-supported approach to place two groups at opposite ends of a row. No grid, table, or float hacks are needed. The existing `<ul class="menu">` element is preserved — the theme's `.menu li` inline-block rule still applies within the right group. At narrow viewports, `flex-direction: column` in a `@media` query stacks the groups vertically without overlap.

**Alternatives considered**:
- CSS Grid: Rejected — more verbose for a simple two-column header; flexbox is sufficient.
- Absolute positioning: Rejected — breaks document flow and conflicts with the site's `max-width: 800px` body constraint.
- `float: right` on the menu: Rejected — clearfix issues and poorer alignment control.

---

## 4. External Link Security Attributes

**Decision**: LinkedIn and Google Scholar links use `target="_blank" rel="noopener noreferrer"`.

**Rationale**: `target="_blank"` without `rel="noopener"` allows the opened page to access the opener's `window` object via `window.opener`, a known security risk (reverse tabnapping). `noopener` prevents this. `noreferrer` additionally suppresses the `Referer` header, which is appropriate for external links from a personal academic site. Modern browsers implement `noopener` by default for `target="_blank"` links but explicitly including both attributes ensures compatibility and communicates intent.

**Alternatives considered**:
- `rel="noopener"` only: Acceptable but `noreferrer` adds privacy protection for no cost.
- No `rel` attribute: Rejected for security reasons noted above.

---

## 5. Theme CSS Override Specificity

**Decision**: The project-level `header.css` overrides `.menu a` (and adds `.header-nav`, `.header-social`, `.menu a.active`) with the same or lower specificity selectors, relying on CSS cascade order (later stylesheet wins at equal specificity).

**Rationale**: The theme sets `.article-meta, .menu a { background: #eee; padding: 5px; border-radius: 5px; }` at specificity 0,1,1 (one class + one element). Our override `.menu a { background: none; padding: 0; border-radius: 0; }` has the same specificity 0,1,1. Since `header.css` is loaded after `style.css` (via `head_custom.html`, which appears after the theme CSS `<link>` tags in `header.html`), our rules win. No `!important` is needed.

**Alternatives considered**:
- Using `!important`: Rejected — creates maintenance burden and violates CSS best practices.
- Higher-specificity selectors (e.g. `nav .menu a`): Unnecessary given load-order precedence.
