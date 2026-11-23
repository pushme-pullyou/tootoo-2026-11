# TooToo — AI Agent Instructions

This repo is the **published TooToo app**, not where TooToo is developed.

## The one rule

**Never hand-edit [`index.html`](index.html).** It is a generated build. From r2 on,
the component sources, assembler (`assemble.ps1`), tests and the `release` command live in
the rebuilt workshop, `g:\My Drive\2026-theo-github\pushme-pullyou-tootoo-next` (to be
published as `pushme-pullyou/dolittle`; see its `AGENTS.md`). Make every code change
there, and let its `release` command write this repo's `index.html`, `releases/rN/` and
`releases/latest.json`.

## What may be edited here

- `README.md`, `FORKING.md` — user-facing docs.
- `examples/` — sample content for the renderers.
- `favicon.ico`, `tootoo-screenshot.jpeg` — assets.
- This repo's own settings are the config block in `index.html` (between the
  `TOOTOO-CONFIG` markers). Each release carries it forward unchanged.

## Releases

`releases/rN/` folders hold frozen, runnable copies of earlier builds (`r1`, `r2`, …),
each matching a GitHub Release and tag of the same name. They are written only by the
workshop's `release` command. Never edit, move or delete one.

## Conventions

- Vanilla JavaScript, single file, static hosting, `file://` friendly — see the
  Constraints section of [`README.md`](README.md).
- README changelog entries are dated `YYYY-MM-DD`, newest first.
- History before 2026-10-31 is in the archive repo `pushme-pullyou/tootoo-2026-10`.
