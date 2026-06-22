# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A static website hosting a personal collection of standalone HTML guides. No build step,
no framework, no dependencies — just hand-written HTML, one shared CSS file, and a small
inline vanilla-JS snippet for copy-to-clipboard buttons. Published via GitHub Pages at
https://naoralkobi.github.io/guides/.

## Run / preview

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

Or just open `index.html` directly in a browser. There are no tests, linters, or build commands.

## Architecture

- `index.html` — landing page. A `.card-grid` of `<a class="card">` blocks, one per guide,
  plus a trailing dashed `.card.placeholder`.
- `guides/<slug>.html` — each guide is a fully self-contained page. All guides share the
  same `<head>`, header, footer, and copy-to-clipboard `<script>`; only the body content
  differs. Filenames are descriptive kebab-case.
- `css/style.css` — the single source of design truth. Every page links it via
  `../css/style.css` (relative paths keep the site working locally and under the Pages
  subpath). Never inline styles or add a second stylesheet — reuse existing classes.

`guides/second-brain-obsidian-claude.html` is the canonical template. New guides should be
copied from it so they inherit the exact `<head>`, palette, and markup.

## Markup conventions (reuse, don't reinvent)

- Sections: `<h2>`; steps: `<h3>` with a numbered badge `<span class="step-num">1</span>`.
- Tables: always wrap in `<div class="table-scroll">…</div>` so they scroll on mobile.
- Code: use the `.code-block` markup (`.code-head` / `.code-label` / `.copy-btn`) — the
  bottom-of-page script wires up the copy button automatically.
- Callouts: `<div class="callout warn">` for ⚠️ warnings, `<div class="callout insight">`
  for key insights.

## Adding a guide

The `new-guide` skill (`.claude/skills/new-guide/`) automates the full flow: distill source
text/URL → render an HTML page from the template → add a card to `index.html` → commit & push.
Prefer it over doing the steps by hand. Manually, the two steps are: create
`guides/<slug>.html` from the template, then add a matching `<a class="card">` to the
`.card-grid` in `index.html` (keep the placeholder card last).
