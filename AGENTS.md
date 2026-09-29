# VSDTL IDE

## Overview
Single-file static HTML app (`index.html`) — a mini IDE for a custom DSL called VSDTL.
No build step, no dependencies, no backend. Served as a static file.

## Running
```
docker compose -f docker-compose.base44.yml up -d
```
Serves on port 3000 via nginx (custom `nginx.conf` runs as root to handle bind-mount permissions).

## Architecture
- **Editor**: textarea overlay with a `<pre>` highlight layer behind it for syntax coloring
- **Runner**: parses `@table = [...]` definitions and `Display(#table)` statements line-by-line
- **Command prompt**: supports `Insert(table)`, `Add(table,"val")`, `Display(#table)`

## DSL Syntax
- `@name = [JSON array]` — define a table
- `Display(#name)` — print table contents to output
- `Insert(name)` — create empty table (command prompt only)
- `Add(name,"val1","val2")` — append values to a table (command prompt only)

## Key Implementation Notes
- Syntax highlighter escapes HTML (`&`, `<`, `>`) before injecting into `innerHTML`
- Quoted strings are tracked as a single token (not split on `"` delimiter)
- Scroll sync covers both `scrollTop` and `scrollLeft`
- Table name regexes escape special chars to avoid false matches
- No live-reload dev server (static file); call `reload_preview` after edits
