---
name: markdown
description: Markdown formatting conventions — heading/list/emphasis style, frontmatter, and link format (aligned with rumdl linter config)
---

## Formatting Rules

These match the rumdl linter config (`.rumdl.toml`). Run `rumdl <file>` to check.

### Headings

- **ATX style only** — use `## Heading`, not underline style (MD003)
- Start content at `##` level — no `#` headers in file body (Obsidian uses filename as title)

### Lists

- **Dash markers** — use `- item`, not `*` or `+` (MD004)

### Emphasis and Bold

- **Underscore for italic**: `_italic_`, not `*italic*` (MD049)
- **Asterisk for bold**: `**bold**`, not `__bold__` (MD050)

### Line Length

- Soft target of 120 characters for non-prose lines (code blocks, tables)
- Let editors handle visual wrapping for prose

## Frontmatter

- YAML fences (`---`) at the top of the file for structured properties
- Keep frontmatter minimal — omit empty fields rather than leaving them blank
- Common properties: `tags`, `aliases`

## Links

- Use **wikilinks** (`[[Note Name]]`) for internal vault links
- Aliases: `[[Note Name|display text]]`
- Heading links: `[[Note Name#Section]]`
- Standard markdown links (`[text](url)`) for external URLs only
