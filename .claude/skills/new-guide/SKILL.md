---
name: new-guide
description: Turn a piece of text OR a URL into a new styled HTML guide in this repo. Fetches/reads the source content, distills it into highlights + use cases + how-to steps, renders it as an HTML page matching the existing template, adds a card to index.html, then commits and pushes. Use when the user provides article text or a link and wants it added as a guide.
---

# new-guide

Convert raw content (pasted text or a URL) into a polished guide page that matches
this site's design, then publish it.

## Input

The user provides ONE of:
- A link/URL to an article or page, or
- A block of raw text/markdown.

If neither is clear, ask which one and for the content.

## Steps

1. **Get the source content.**
   - If given a URL, fetch it with the WebFetch tool. If fetch fails, ask the user to paste the text.
   - If given text, use it directly.

2. **Distill it.** Produce, in this order:
   - A short, specific **title**.
   - A 1–2 sentence **summary / big idea**.
   - **Highlights** organized for easy reading (tables where comparisons exist).
   - **Use cases** and **how-to** steps wherever the source describes a procedure.
   - Callouts for warnings/key insights.
   Keep it faithful to the source — distill and structure, don't invent facts.

3. **Render the HTML.** Copy the structure and class names from
   `guides/second-brain-obsidian-claude.html` exactly (same `<head>`, same CSS link
   `../css/style.css`, same header/footer, same callout/table/code-block markup and
   the copy-to-clipboard script). Only the body content changes.
   - Save to `guides/<kebab-case-slug>.html`.
   - Use semantic HTML: `<h1>`/`<h2>`, `<table>` wrapped in the scroll container,
     `<pre><code>` for commands, callout `<div>`s for ⚠️ / insights.

4. **Wire it into `index.html`.** Add one `<a class="card">…</a>` block to the card
   grid (copy an existing card, update title/description/href). Leave the dashed
   placeholder card last.

5. **Verify.** Open the new file's relative links resolve (css path `../css/style.css`)
   and that the card href matches the new filename.

6. **Publish.** Stage, commit, and push:
   ```bash
   git add -A
   git commit -m "Add guide: <title>"
   git push
   ```
   End git commit messages with the project's co-author trailer if configured.

7. **Report** the new file path, the card added, and the pushed commit. If GitHub
   Pages is enabled, give the live URL.

## Conventions
- Match the existing palette and typography via the shared `css/style.css` — never
  inline a different color scheme.
- Pure HTML/CSS + the existing vanilla copy-button JS. No frameworks, no build step.
- One guide = one HTML file in `guides/` + one card in `index.html`.
