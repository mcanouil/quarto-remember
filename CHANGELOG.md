# Changelog

## Unreleased

### New Features

- feat: Read the Quarto project type from `QUARTO_EXECUTE_INFO` in the Lua filter and inject it into the page as a JSON `<script id="quarto-remember-config">` block, so `remember.js` distinguishes book, website, and single-document projects deterministically instead of guessing from theme-specific DOM selectors.
- feat: Add `extensions.remember.page-exclude` to opt out of navigation persistence for specific pathnames (literal substrings or `*` globs).
- feat: Add `extensions.remember.separate-chapter-state` to track the current chapter independently from the scroll position inside that chapter for Quarto books.

### Bug Fixes

- fix: Invalidate the cached page identifier on `popstate`, `hashchange`, `pushState`, and `replaceState` so SPA-style navigation no longer reads or writes the previous page's state.
- fix: Feature-detect `localStorage` and `sessionStorage` with a probe write so private browsing modes that throw on write disable persistence cleanly instead of erroring per operation.
- fix: Drop the redundant `aria-live="assertive"` on the modal `alertdialog` (the role already implies live behaviour for assistive technologies).

### Documentation

- docs: Document the new deterministic project-type mechanism, the `page-exclude` option, and the `separate-chapter-state` option in the README and `_schema.yml`.

## 1.2.0 (2026-03-23)

### Refactoring

- refactor: Replace monolithic `utils.lua` with focused modules (`string.lua`, `logging.lua`, `metadata.lua`, `pandoc-helpers.lua`, `html.lua`, `paths.lua`, `colour.lua`).

## 1.1.0 (2026-02-21)

### New Features

- feat: Add _schema.yml for configuration validation and IDE support (#4).

## 1.0.1 (2026-02-11)

### Bug Fixes

- fix: Update copyright year.
- fix: Use british english spelling.

## 1.0.0 (2025-10-30)

### New Features

- feat: Remember extension - initial commit.
