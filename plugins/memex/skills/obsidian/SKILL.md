---
name: obsidian
description: Obsidian CLI reference — control the Obsidian app from the terminal for file operations, search, properties, tasks, and more
---

## Overview

Obsidian ships a built-in CLI (`obsidian`) that controls the running Obsidian app from the terminal. It requires Obsidian to be running — if it's not, the first command launches it.

Full docs: <https://help.obsidian.md/cli>

Run `obsidian help` or `obsidian help <command>` for inline reference.

## Syntax

```sh
obsidian <command> [param=value ...] [flags]
```

- **Parameters** take values: `name="My Note"` (quote values with spaces)
- **Flags** are boolean switches: `open`, `overwrite`, `newtab`
- Use `\n` for newlines and `\t` for tabs in content values
- Add `--copy` to any command to copy output to clipboard

### Targeting a vault

If CWD is inside a vault, that vault is used. Otherwise the active vault is used. Override with:

```sh
obsidian vault=memex <command>
```

### Targeting a file

Most commands accept `file` and `path`:

- `file=<name>` — resolves like wikilinks (name only, no path or extension needed)
- `path=<path>` — exact path from vault root, e.g. `50 Journal/2026/03-Mar/2026-03-08 Daily Journal.md`

If neither is given, commands default to the active file.

**The CLI does not accept positional arguments.** Always use named parameters:

```sh
obsidian open file="Notification Routing Plan"     # correct
obsidian open "Notification Routing Plan.md"       # WRONG — will error
```

## When to Use CLI vs. Direct File Operations

Most agent work should use direct file tools (Read, Write, Edit, Glob, Grep) — they're faster and don't require Obsidian to be running.

**Use the Obsidian CLI for:**

- `move` / `rename` — updates wikilinks across the vault (never use `mv`/`git mv`)
- `open` — show a note to the user in Obsidian
- `daily` — open or append to today's daily note
- `property:set` / `property:remove` — safely modify frontmatter properties
- `search` / `search:context` — Obsidian-native search (respects search operators)
- `tasks` / `task` — list and toggle tasks vault-wide
- `base:query` — query Bases views
- `backlinks` / `links` / `orphans` — link graph queries
- `tags` — vault-wide tag listing with counts
- `create` with `template=` — create a note from an Obsidian template

**Use direct file tools for:**

- Reading note content (Read tool — faster, gives line numbers)
- Writing or editing note content (Write/Edit tools)
- Finding files by name pattern (Glob tool)
- Searching file content by regex (Grep tool)

## Key Commands

### Files

```sh
obsidian open file="Note Name"              # open in Obsidian
obsidian open file="Note Name" newtab       # open in new tab
obsidian create name="Note" content="# Title\n\nBody"
obsidian create name="Note" template=Travel open  # from template
obsidian move file="Old Name" to="new/path.md"    # updates all links
obsidian rename file="Old Name" name="New Name"   # updates all links
obsidian delete file="Note"                       # moves to trash
obsidian read file="Note"                         # print contents
obsidian append file="Note" content="new line"
obsidian prepend file="Note" content="new line"
```

### Daily Notes

```sh
obsidian daily                              # open today's daily note
obsidian daily:path                         # get daily note path
obsidian daily:read                         # print daily note contents
obsidian daily:append content="- [ ] Task"  # append to daily note
```

### Search

```sh
obsidian search query="meeting notes"                 # file name matches
obsidian search query="meeting notes" total           # just the count
obsidian search:context query="TODO" format=json      # with line context
```

### Properties

```sh
obsidian properties file="Note"                          # list properties on a file
obsidian property:set file="Note" name=status value=active type=text
obsidian property:read file="Note" name=status
obsidian property:remove file="Note" name=status
```

### Tags

```sh
obsidian tags                              # list all tags
obsidian tags counts sort=count            # sorted by frequency
obsidian tag name=project verbose          # files with this tag
```

### Tasks

```sh
obsidian tasks todo                        # all incomplete tasks
obsidian tasks daily                       # tasks from daily note
obsidian tasks file="Note" verbose         # with file paths + line numbers
obsidian task ref="Recipe.md:8" toggle     # toggle a specific task
obsidian task daily line=3 done            # complete daily note task
```

### Links

```sh
obsidian backlinks file="Note"             # incoming links
obsidian links file="Note"                 # outgoing links
obsidian orphans                           # files with no incoming links
obsidian unresolved                        # broken links
```

### Bases

```sh
obsidian bases                             # list .base files
obsidian base:query file="Tasks" format=json
obsidian base:query file="Tasks" view="Active" format=csv
obsidian base:create file="Tasks" name="New Item" content="# New Item"
```

### Plugins

```sh
obsidian plugins filter=community versions  # list installed plugins
obsidian plugin:enable id=dataview
obsidian plugin:disable id=dataview
```

### Vault Info

```sh
obsidian vault                             # name, path, file/folder counts
obsidian files total                       # file count
obsidian files folder="20 Projects"        # list files in a folder
obsidian folders                           # list all folders
```

## Installed Plugins

### Obsidian Git

Automated git backup for the vault.

- **Auto-push interval:** 60 minutes
- **Auto-pull on boot:** enabled
- **Commit message format:** `vault backup: {{date}}` (`YYYY-MM-DD HH:mm:ss`)

The agent should not interfere with obsidian-git's commit cycle. Agent changes get picked up on the next auto-push. Manual `git commit` is fine for batch operations.

### Daily Notes Configuration

- **Format:** `YYYY/MM-MMM/YYYY-MM-DD Daily Journal`
- **Folder:** `50 Journal`
- **Template:** `40 Resources/Templates/daily-review`

Produces paths like: `50 Journal/2026/03-Mar/2026-03-08 Daily Journal.md`
