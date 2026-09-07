# dcsoto.github.io — applying the new visual identity

Everything here layers on top of your existing Beautiful Jekyll fork. No theme files
(`_layouts/`, `_includes/nav.html`, `assets/css/main.css`) need to be edited, so future
Beautiful Jekyll updates stay painless.

## Step 2 — copy the new files

Copy `assets/css/dcsoto-theme.css` and `_includes/head-extra.html` into the same paths in your repo.

## Step 3 — landing page

Replace `index.html` with the one in this folder. It uses `layout: base` (nav + footer, no
banner) and pulls posts from `site.posts`: the newest post becomes the **Latest** card, the
next four become the **From the blog** bars.

- Edit the four topic labels in the `<nav class="dc-topics">` block if you want different ones.
- Intro paragraph and eyebrow text live in plain HTML at the top of the file.

## Step 6 — pages that need no markup changes

`aboutme.md`, `research.md`, `resources.md`, `press.html`, `blog.html`, `tags.html` and all
posts pick up the new look automatically: cream background, condensed uppercase titles,
Lora body, mono labels, card-style post previews, dark code blocks with a blue offset shadow,
hard-shadow images, pink drop cap on the first paragraph of every post.

Optional upgrades (classes already exist in the CSS):

- **Pink drop cap on a page** (about, research): start the first paragraph with
  `<span class="dc-dropcap">I</span> am a researcher…`
- **Step headings in tutorials**: `## <em>Step 1</em> Generate a FASTA file` — the `<em>` turns blue.
- **Note box**: `<div class="dc-note"><span class="dc-mono">Note</span><span>…</span></div>`
- **Stamp**: `<span class="dc-stamp">Coming soon!</span>`
- **Resources as cards**:
  ```html
  <div class="res-grid">
    <a class="res-card" href="/single-cell-tools"><strong>My favorite single-cell tools</strong><span>A curated list of tools for scRNA-seq and scATAC-seq data processing.</span></a>
  </div>
  ```
- **Press rows** (replace the table): one link per item, colour the type tag with `dc-bg-blue` / `dc-bg-pink` / `dc-bg-mustard` / `dc-bg-ink`:
  ```html
  <div class="press-list">
    <a class="press-item" href="…"><span class="press-date">2025.07.21</span><span class="press-type dc-bg-blue">University press</span><span><span class="press-title">Finding Human Brain Genes in Duplicated DNA</span><span class="press-outlet">UC Davis College of Biological Sciences</span></span><span class="press-source">UC Davis News ↗</span></a>
  </div>
  ```

## Palette & type (for anything you add later)

- Cream `#f3efe4` · card `#f8f4eb` · ink `#23201c` · body `#3a332b` · muted `#5c5346` · rule `#cfc6b2`
- Blue `#3b6fcf` (accent) · Pink `#e8517a` (drop caps, tags) · Mustard `#e9a93a`
- Display: Bebas Neue · Body: Lora · Labels/code: IBM Plex Mono
- Signature details: 2px ink borders, hard offset shadows (`4px 4px 0`), double-rule "stamp" boxes, mono uppercase eyebrows.

## Checking locally

`bundle exec jekyll serve` then open <http://localhost:4000>. If a Beautiful Jekyll class
name in your version differs from what the CSS targets (the CSS is written for Beautiful
Jekyll 6.x), inspect the element and adjust the selector in `dcsoto-theme.css`.
