---
name: people
description: Create, update, and manage people files in the vault's 40 Resources/People/ directory
---

## Overview

People files live in `40 Resources/People/`. Each file represents a person and contains structured properties plus freeform notes (meeting notes, observations, etc.).

## File Conventions

### Filename

Use the person's **preferred name** — the name they go by day-to-day:

- Full preferred name: `Sébastien Laporte.md`, `Michael Darwish.md`
- Nickname-based if that's what everyone uses: `MG.md`, `GG.md`

### Structure

Every people file follows this layout:

```markdown
# Preferred Name

**Full Name:** Legal / formal name (only if different from header)
**Nickname:** Short name or initials (only if commonly used)
**Email:** user@example.com
**Role:** Job title
**Team:** Primary team name
**Team Role:** manager | technical_lead | product_lead | product_designer | qa | member | honorary_member
**Manager:** [[Manager Name]]
**Location:** City or City, Country
**Status:** Met | Scheduled | Pending | Not started

## Notes

Freeform content: meeting notes (dated with ### headings), observations, context, etc.
```

### Property rules

- Omit any property that has no value — don't include empty fields.
- **Manager** should be an Obsidian wikilink: `[[Name]]`
- **Team** is the team name. If someone is on multiple teams, list the primary one and mention others in notes.
- **Team Role** indicates their role within the team structure (manager, tech lead, etc.), not their job title.
- **Status** tracks your relationship: `Met` (had a 1:1), `Scheduled` (meeting booked), `Pending` (intend to meet), `Not started` (no plans yet).

## Key Patterns

### Creating a new person file

1. Use their preferred name as the filename.
2. Populate all available properties.
3. Set Status to `Not started` unless specified otherwise.

### After a meeting

Add a dated section under `## Notes`:

```markdown
### January 15, 2026

- Key discussion points
- Action items
- Observations
```

## Troubleshooting

- **Person not in any directory**: Create the file manually with whatever info is available.
- **Duplicate people across teams**: Some people appear on multiple teams. Use their primary team for the Team property.
