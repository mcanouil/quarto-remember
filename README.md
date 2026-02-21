# Remember Extension For Quarto

`remember` is an extension for Quarto to save and restore navigation position across page visits for HTML documents, Quarto books, and Reveal.js presentations.

## Installation

```bash
quarto add mcanouil/quarto-remember@1.1.0
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

The extension detects Quarto books by checking for both `.page-navigation` and `.nav-sidebar` elements.

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

## Limitations

- Only works with HTML-based output formats (`html`, `revealjs`, and `book`).
- Requires browser support for `localStorage` (not available in some private browsing modes).
- For regular pages, position is tracked per pathname. For books, position is tracked per book (all chapters share the same tracking).
- Book detection requires both `.page-navigation` and `.nav-sidebar` elements in the DOM.

## Example

Here is the source code for a minimal example: [example.qmd](example.qmd).

Output of `example.qmd`:

- [HTML](https://m.canouil.dev/quarto-remember/)
- [Reveal.js](https://m.canouil.dev/quarto-remember/example-revealjs.html)
