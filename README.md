# Guides

A personal collection of practical guides, published as a static website.

**🌐 Live site: https://naoralkobi.github.io/guides/**

This repo holds multiple standalone guides. Each guide is a single self-contained
HTML page; the landing page (`index.html`) lists them all as cards. No build step,
no frameworks — just HTML and CSS (plus a tiny bit of vanilla JS for copy-to-clipboard
buttons on code blocks).

## Structure

```
guides-site/
├── index.html                              # Landing page — lists all guides as cards
├── guides/
│   └── second-brain-obsidian-claude.html   # A full guide
├── css/
│   └── style.css                           # Shared stylesheet (used by every page)
└── README.md
```

## Adding a new guide

It's deliberately two small steps:

1. **Create the guide file.** Copy an existing guide from `guides/` (e.g.
   `second-brain-obsidian-claude.html`) to a new file in the same folder, give it a
   descriptive kebab-case name, and replace the content. The page already links to the
   shared stylesheet at `../css/style.css`, so it inherits the design automatically.
   Reuse the existing building blocks:
   - Headings: `<h2>` for sections, `<h3>` for steps (wrap a number in
     `<span class="step-num">1</span>` for the numbered badge).
   - Tables: wrap any `<table>` in `<div class="table-scroll">…</div>` so it scrolls on
     small screens.
   - Code blocks: use the `.code-block` markup — it gives you the styled frame, a label,
     and a working copy button (the JS at the bottom of the page wires it up).
   - Callouts: `<div class="callout warn">` for ⚠️ warnings,
     `<div class="callout insight">` for key insights.

2. **Add a card to `index.html`.** Inside `.card-grid`, copy the existing
   `<a class="card">…</a>` block, point its `href` at your new file, and update the tag,
   title, and description. (Keep or remove the dashed `.card.placeholder` as you like.)

That's it — no config to touch.

## Running locally

Just open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Publishing with GitHub Pages

1. Push this repo to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Pick your branch (e.g. `main`) and the `/ (root)` folder, then **Save**.

The site goes live at `https://<your-username>.github.io/<repo-name>/`. Because every
page uses relative links, it works the same locally, from the repo root, or under a
Pages subpath.
