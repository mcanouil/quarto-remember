# Remember Extension For Quarto

`remember` is an extension for Quarto to save and restore navigation position across page visits for HTML documents, Quarto books, and Reveal.js presentations.

## Installation

```bash
quarto add mcanouil/quarto-remember@1.2.0
```

This will install the extension under the `_extensions` subdirectory.

If you're using version control, you will want to check in this directory.

## Usage

To activate the filter, add the following to your YAML front matter:

```yaml
filters:
  - remember
```

## How It Works

### HTML Documents

The extension automatically tracks:

- **Scroll Position:** Saves your vertical scroll position as you navigate the page.
- **Hash Anchors:** Remembers which section you were viewing (e.g., `#section-name`).
- **Visit Timestamp:** Records when you last visited the page.

When you return to the page, you'll be prompted with a modal asking if you want to resume from where you left off.

### Quarto Books

For Quarto books, the extension provides cross-chapter navigation tracking:

- **Current Chapter:** Remembers which chapter you were reading.
- **Scroll Position:** Saves your position within that chapter.
- **Automatic Redirect:** When you return to any page in the book, you'll be automatically redirected to the chapter you were reading.
- **Visit Timestamp:** Records when you last visited the book.

The extension detects Quarto books deterministically.
The Lua filter reads the project type from `QUARTO_EXECUTE_INFO` at render time and injects a small JSON configuration block into the page head:

```html
<script id="quarto-remember-config" type="application/json">
  {"project-type":"book","page-exclude":[],"separate-chapter-state":false}
</script>
```

`remember.js` reads that block at startup, so detection no longer relies on theme-specific DOM selectors and survives theme changes, custom HTML layouts, and SPA-style navigation.

### Reveal.js Presentations

The extension automatically tracks:

- **Slide Indices:** Saves the current horizontal, vertical, and fragment indices.
- **Visit Timestamp:** Records when you last viewed the presentation.

When you return to the presentation, you'll be prompted to resume from your last viewed slide.

## Features

- **Non-Intrusive:** Only prompts when there's a meaningful position to restore (scroll > 100px or at a specific slide).
- **User Control:** Users can choose to resume or start fresh. Declining clears the stored position.
- **Page-Specific:** Each page/book tracked separately.
- **Cross-Chapter Navigation:** For books, automatically redirects to the correct chapter.
- **Prompt Debouncing:** Won't show the prompt more than once every 5 seconds to avoid annoyance.
- **Time-Aware:** Shows "X minutes/hours/days ago" to help users decide whether to resume.
- **Privacy-Focused:** All data stored locally in browser `localStorage`, nothing sent to external servers.
- **Accessible:** Keyboard navigation support (Escape to dismiss prompt), ARIA attributes for screen readers.
- **Responsive:** Mobile-friendly modal design.
- **Dark Mode:** Adapts to user's colour scheme preference (supports both system preference and Quarto's `.quarto-dark`/`.quarto-light` classes).

## Configuration

All options are optional and live under `extensions.remember` in either the document front matter or a project `_quarto.yml`.

```yaml
extensions:
  remember:
    page-exclude:
      - /drafts/*
      - /search.html
    separate-chapter-state: true
```

- `page-exclude` is a list of pathname patterns to opt out of persistence.
  Each entry is matched against `window.location.pathname` as a literal substring or as a glob where `*` stands for one path segment.
- `separate-chapter-state` (default `false`) stores the current chapter of a Quarto book independently from the scroll position inside that chapter, so a return visit can offer to reopen the previous chapter even if the user did not scroll.

## Limitations

- Only works with HTML-based output formats (`html`, `revealjs`, and `book`).
- Requires browser support for `localStorage`.
  Private browsing modes that throw on write are detected at startup and the extension disables itself silently with a single console warning.
- For regular pages, position is tracked per pathname.
  For books, position is tracked per book (all chapters share the same tracking by default).
- Project-type detection requires Quarto to populate `QUARTO_EXECUTE_INFO`, which it does for every supported render path.

## Example

Here is the source code for a minimal example: [example.qmd](example.qmd).

Output of `example.qmd`:

- [HTML](https://m.canouil.dev/quarto-remember/)
- [Reveal.js](https://m.canouil.dev/quarto-remember/example-revealjs.html)
