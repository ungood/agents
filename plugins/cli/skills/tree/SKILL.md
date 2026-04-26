---
name: tree
description: Show directory structure as a tree visualization
---

## Overview

`tree` shows the contents of directories in a tree format, making it easy to visualize directory structure and file hierarchy.

More information: <https://manned.org/tree>

## Usage

- Print files and directories up to `num` levels of depth (where 1 means the current directory):

  ```text
  tree -L num
  ```

- Print directories only:

  ```text
  tree -d
  ```

- Print hidden files too with colorization on:

  ```text
  tree -a -C
  ```

- Print the tree without indentation lines, showing the full path instead (use `-N` to not escape non-printable characters):

  ```text
  tree -i -f
  ```

- Print the size of each file and the cumulative size of each directory, in human-readable format:

  ```text
  tree -s -h --du
  ```

- Print files within the tree hierarchy, using a wildcard (glob) pattern, and pruning out directories that don't contain matching files:

  ```text
  tree -P '*.txt' --prune
  ```

- Print directories within the tree hierarchy, using the wildcard (glob) pattern, and pruning out directories that aren't ancestors of the wanted one:

  ```text
  tree -P directory_name --matchdirs --prune
  ```

- Print the tree ignoring the given directories:

  ```text
  tree -I 'directory_name1|directory_name2'
  ```
