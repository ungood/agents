---
name: tldr
description: Look up concise command-line help using the tldr-pages project
---

## Overview

`tldr` displays simple help pages for command-line tools from the tldr-pages project.

More information: <https://github.com/tldr-pages/tldr/blob/main/CLIENT-SPECIFICATION.md#command-line-interface>

## Usage

- Print the tldr page for a specific command:

  ```text
  tldr command
  ```

- Print the tldr page for a specific subcommand:

  ```text
  tldr command subcommand
  ```

- Print the tldr page for a command from a specific platform:

  ```text
  tldr --platform android|cisco-ios|common|dos|freebsd|linux|netbsd|openbsd|osx|sunos|windows command
  ```

- Update the local cache of tldr pages:

  ```text
  tldr --update
  ```

- List all pages for the current platform and common:

  ```text
  tldr --list
  ```
