# AGENTS.md

## Project Overview
Single-file static web app ("VSDTL IDE") — a self-contained `index.html` with inline CSS and vanilla JS. No backend, no build step, no dependencies, no framework.

## Running
- Served by `nginx:alpine` via `docker-compose.base44.yml`, mapping `index.html` into the container on port 3000.
- Start: `docker compose -f docker-compose.base44.yml up -d`
- No external credentials or secrets required.

## Editing
- All code lives in `index.html`. Edits are reflected on page refresh (no live-reload dev server); call `reload_preview` after changes.
