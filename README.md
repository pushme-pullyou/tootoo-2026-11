# TooToo

[![Live Demo](https://img.shields.io/badge/demo-live-success)](https://pushme-pullyou.github.io/tootoo/)
[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)
[![Single File](https://img.shields.io/badge/single--file-vanilla%20JS-orange)](index.html)

**Navigate any GitHub repo in your browser. Zero install. Single HTML file.**

![TooToo screenshot](tootoo-screenshot.jpeg)

## Try it

| Try | What it demos |
| --- | --- |
| [octocat/hello-world](https://pushme-pullyou.github.io/tootoo/?owner=octocat&repo=hello-world) | Tiny repo — see the basic UI in two seconds |
| [facebook/react @ React README](https://pushme-pullyou.github.io/tootoo/?owner=facebook&repo=react#packages/react/README.md) | Big repo, deep-linked to a specific file |
| [openai/openai-cookbook](https://pushme-pullyou.github.io/tootoo/?owner=openai&repo=openai-cookbook) | Markdown-heavy repo |
| [torvalds/linux @ master](https://pushme-pullyou.github.io/tootoo/?owner=torvalds&repo=linux&branch=master) | Too large — over GitHub's 100,000-file / 7 MB tree limit, so it shows the "too large" notice |
| [kubernetes/kubernetes @ master](https://pushme-pullyou.github.io/tootoo/?owner=kubernetes&repo=kubernetes&branch=master) | 30,000+ files — the full tree loads and filters |

## [Examples](examples/)

The [`examples/`](examples/) folder has sample content for every renderer. A few worth a click:

* [`docs/formatting-showcase.md`](examples/docs/formatting-showcase.md) — Markdown headings, lists, code, and links
* [`svg/diagram.svg`](examples/svg/diagram.svg) — inline SVG with a raw-source toggle
* [`images/the-scream.jpg`](examples/images/the-scream.jpg) — image viewer
* [`data/us-county-state-latlon-pop.csv`](examples/data/us-county-state-latlon-pop.csv) — CSV table
* [`pdf/sample.pdf`](examples/pdf/sample.pdf) — PDF viewer
* [`html/sample-page.html`](examples/html/sample-page.html) — HTML preview
* [`code/code-sample.js`](examples/code/code-sample.js) — syntax-highlighted code
* [`audio/sample.wav`](examples/audio/sample.wav) — audio player
* [`video/pano.mp4`](examples/video/pano.mp4) — video player

## Why TooToo?

* **Instant cross-tree filter.** Type a few letters, see every matching path. GitHub's web UI only filters the current folder.
* **Sticky sidebar, sticky breadcrumbs.** Scroll a long file without losing context.
* **Built for phones too.** A−/A+ buttons resize everything; the sidebar collapses to a sensible width on narrow screens; dark mode is one tap.
* **Works on a local checkout.** Open `index.html` from disk, pick a cloned repo's folder, and TooToo reads the files straight from disk, unpushed edits included — no API quota burn.
* **Drag-and-drop friendly.** One file. Copy it into any repo, push, enable Pages, done.

## Features

* **Single file** — one `index.html` with HTML, CSS, and JS inline
* **Local folders** — on `file://`, open a folder (or reopen the last one); its `.git/config` names the GitHub repo
* **Auto-detect** — the repo comes from `?owner=&repo=`, the config block, or the `*.github.io` address
* **File tree** — sidebar with collapsible folders, filter input, keyboard navigation; blog folders sort newest first
* **Content viewer** — Markdown (rendered via marked), syntax-highlighted code, images, audio, video, PDF, CSV tables, HTML pages
* **Dark mode** — toggle with persisted preference
* **Resizable sidebar** — drag to resize, width saved across visits
* **Collapsible sidebar** — toggle with the header button or Ctrl/⌘ B, state persisted
* **Font size controls** — A−/A+ buttons, helpful on phones
* **GitHub token support** — optional PAT for private repos and higher rate limits (5,000/hr vs 60/hr)
* **File text cache** — the last 50 files read stay in memory, to save API calls
* **Hash routing** — deep-link to any file or heading via `#path/to/file#anchor`
* **Copy / New Tab / Download** — copy raw text, open a file in a new tab, or save it to disk
* **Rendered ↔ Raw toggle** — for Markdown, HTML, CSV and SVG files; preference saved per file type
* **HTML previews** — pages run in a frame, at their published or local URL when there is one. The frame isn't sandboxed: open only HTML you trust
* **Update notice** — tells the maintainer, at most once a day, when a newer release exists, and downloads it with their settings already in it

## Quick Start

**On GitHub Pages** — visit the [live URL](https://pushme-pullyou.github.io/tootoo/) above, adding `?owner=…&repo=…` for any public repo.

**Your own install** — download `index.html` from the [latest release](https://github.com/pushme-pullyou/tootoo/releases/latest) and put it in your repo:

* **Opened from disk** (`file://`), it offers **📂 Open folder**: pick the cloned repo, and it reads the files from disk. Next time, **Reopen** brings the same folder back. **Browse GitHub instead** reads the repo from GitHub.
* **On your Pages site** (`<you>.github.io/<repo>/`), it browses that repo with no settings at all.

## Settings: the config block

Everything an install changes lives in one marked block near the top of `index.html`:

```html
<!-- TOOTOO-CONFIG-START: your settings. Updates carry this block forward unchanged. -->
<script>
window.TOOTOO_CONFIG = {
  appName: 'Pages',
  themeColor: '#3a8856',
  // …every other key is listed there, commented out, with a short note
};
</script>
<!-- TOOTOO-CONFIG-END -->
```

A missing key uses the default, and a key the app doesn't know is ignored (About lists them). The keys: `owner`, `repo`, `branch`, `appName`, `subtitle`, `themeColor`, `headingFontUrl`, `headingFont`, `faviconFile`, `sourceRepoUrl`, `homeUrl`, `storagePrefix`, `hiddenFolders`, `hiddenFiles`, `hideDatedBackups`, `autoOpenFolderReadme`, `rightsText`, `rightsOwners`, `checkForUpdates`, `updateUrl`. Give each install its own `storagePrefix`.

## Updating an install

Releases are numbered (`r1`, `r2`, …) and frozen once cut; [`releases/latest.json`](releases/latest.json) names the newest. Nothing is pushed to installs: each one updates when its maintainer chooses.

1. Open your install from disk (or with a GitHub token saved). When a newer release exists, it shows **rN available**.
2. Click **⬇ Download updated index.html**: the new release with your config block already in it.
3. Rename the old `index.html` to `index.bak` (always hidden from the tree), put the download in its place, then commit and publish.

By hand, it's the same: download the new release, and copy your old file's block, from `TOOTOO-CONFIG-START` to `TOOTOO-CONFIG-END`, over the new one's.

**From r1:** r1 has no update notice, and kept its settings in a separate `tootoo.config.js`. Paste that file's contents between r2's markers (inside the `<script>`), then delete `tootoo.config.js`. Retired keys, such as `faviconLetters`, `faviconColor` and `preferPagesUrls`, are ignored.

## Browser storage

Settings are saved per page (`<prefix>:<pathname>:<name>`), so two installs on one site keep their own: `darkMode`, `fontSize`, `sidebarWidth`, `sidebarHidden`, and `raw:<ext>` (Raw ↔ Rendered per file type). The GitHub token is `<prefix>:githubToken`, and the last update check is `<prefix>:update`. The last opened folder is remembered in IndexedDB (`tootoo`), per page. Clear them in DevTools → Application.

## Constraints

* Vanilla JavaScript — no frameworks, no build tools, no Node.js
* ES2020+ — `const`/`let`, arrow functions, template literals, async/await
* Static hosting only — GitHub Pages or open from `file://`
* External CDN deps, pinned: marked and DOMPurify at startup; highlight.js only when code is shown

## Where development happens

This repo carries the **finished app** and its releases, nothing else. `index.html` and `releases/rN/` are **generated builds** — never hand-edited. The component sources, assembler and tests live in the Dolittle workshop. From r2 on they come from its rebuild, which will be published as [pushme-pullyou/dolittle](https://github.com/pushme-pullyou/dolittle) (until then, that link shows the r1 workshop). Releases are published here; nothing is pushed to installs.

Earlier history — the 2026-04 → 2026-10 development record, prompts, and snapshots — is preserved intact in the [tootoo-2026-10](https://github.com/pushme-pullyou/tootoo-2026-10) archive repo.

## Project Structure

```text
index.html                    ← the latest release, with this repo's own config block (GENERATED — do not hand-edit)
releases/rN/index.html        ← each release, frozen once cut
releases/latest.json          ← names the latest release, for the update notice
favicon.ico                   ← the TT mark
README.md                     ← user-facing docs (this file)
FORKING.md                    ← architecture + recipes for forkers (describes r1)
examples/                     ← sample content for every renderer (with index README)
```

## License

MIT — Copyright pushme-pullyou. See [`LICENSE`](LICENSE).

## Releases

- [r2](https://pushme-pullyou.github.io/tootoo/releases/r2/) — 2026-11-22 — The rebuild: settings in a config block inside `index.html` (no more `tootoo.config.js`), local folders on `file://`, the update notice, PDF / CSV / HTML loaders fetched on demand. Retired: `faviconLetters`, `faviconColor`, `preferPagesUrls`, spreadsheets, the self-test and the repo form
- [r1](https://pushme-pullyou.github.io/tootoo/releases/r1/) — 2026-11-21 — First numbered release: the 2026-11-02 build (HTML previews run scripts, `faviconFile`, dated backups hidden by default)

## Change Log

* 2026-11-22 — Release r2, the rebuild. `index.html` is now r2, with this repo's settings in its config block; `tootoo.config.js` is gone. r1 stays at [`releases/r1/`](releases/r1/). README updated for the config block, updates, and storage. A GitHub token saved in r1 must be saved again once.
* 2026-11-02 — HTML/HTM previews now run scripts without a sandbox and load actual local or published Pages URLs when available, preserving config/assets and repository detection. Embedded app copies avoid recursive self-previews, and root-site `/index.html` detects the correct repository. Only open trusted HTML. Dated backups are hidden by default (`hideDatedBackups: false` shows them). Added `faviconFile` for supplied icon files or URLs; unset means no app icon marks. Removed fallback icon generation.
* 2026-11-01 — Sidebar: a floating go-to-top button appears when the panel overflows. README-prefixed files, including descriptive names and dated backups, now appear first among each folder's files.
* 2026-11-01 — Sidebar: a branch that doesn't exist now says so, instead of being reported as a private repo with a token prompt. The file count resets when a tree fails to load, and Left Arrow while filtering no longer strands keyboard focus.
* 2026-11-01 — github.io links: TooToo now remembers which repos have a GitHub Pages site. It learns this from the repo lookup it already makes, with no extra requests. The owner and repo title links, New Tab, and HTML previews then use the github.io site when one exists and fall back to github.com or raw files when it doesn't. The header links update as soon as this is known.
* 2026-11-01 — Header: the brand icon now always goes back to the start (this page, no `?owner=…` or `#file`); on narrow screens the right-hand buttons slide over the subtitle and move to a second row only when they'd cover owner / repo. `headingFontUrl` now also accepts a `.ttf` / `.woff2` font file, not just a Google Fonts stylesheet. Fixed a token save that could fail silently.
* 2026-10-31 — Fresh start: this repo is now just the finished app — `index.html`, its config, and the `examples/` content. Development (component sources, assembler, pipeline, tests) moved to the [Dolittle workshop](https://github.com/pushme-pullyou/dolittle); the previous repo, with the full 2026-04 → 2026-10 changelog and archives, lives on as [tootoo-2026-10](https://github.com/pushme-pullyou/tootoo-2026-10)
