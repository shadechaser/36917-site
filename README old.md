# 36917.me — Jekyll Site

Personal literary and creative site by Jerry Mesner, hosted on GitHub Pages. Replaces the old Squarespace site.

The name comes from numerology — 369 as a life number, 17 as a favorite number.

## Design: "The Notebook"

Sparse, literary, minimal color. Near-black ink on warm off-white paper.

- **Body / literary content:** EB Garamond
- **UI chrome, dates, metadata:** DM Mono
- Colors (in `assets/css/main.css`): ink `#111110`, rules `#b8b6b0`, mid-tone `#4a4a47`, accent `#333331`
- Mobile font bumps kick in under 600px width

## Setup

```
cd C:\Users\jerry\Documents\36917-site
bundle exec jekyll serve
```

Or just run `start.bat`. Visit `http://localhost:4000`.

Stack: Jekyll ~4.3, Liquid 4.0.4, kramdown, jekyll-paginate. Ruby lives at `C:\Ruby40-x64`.

`_config.yml` has `kramdown hard_wrap: true` set — if you change this, you need a **full restart** of `start.bat` for it to take effect (not just a page refresh).

## Site Structure

**Writing collections:**
- Prose → `_posts/` (also the main index at `index.html`)
- Haiku → `_haiku/`
- Lyrics → `_lyrics/`
- Yearly Christmas prose → `_xmas/`
- Eulogies → `_eulogies/`

**Making categories:**
- Music → `music.html`
- Art → `art.html` — auto-generates a gallery grid from every image dropped into `assets/images/art/` via a `site.static_files` Liquid loop, with an EB Garamond lightbox. **No HTML edits needed** — just add images (lowercase, hyphen-separated names, optional numeric prefix to control order).

**Standalone:**
- `/it-could-only-ever-be-this/` — a self-contained interactive HTML piece, linked from the hero mandala and the footer.

### Adding a post

Create a file in the right collection folder, named `YYYY-MM-DD-post-slug.md`:

```yaml
---
title: "Your Post Title"
date: 2026-01-01
layout: post
category: prose
---

Your content here in Markdown.
```

**For poems/verse:** add `style: verse` to the front matter. This triggers JS in `_layouts/post.html` that wraps each line in a `.vline` span with a hanging indent — so a line that wraps because the browser forced it reads differently from an intentional line break. All 211 existing posts already have this set.

## Key Files — "Where Shit Goes"

| File path | What's there |
|---|---|
| `_includes/hero.html` | Sitewide hero tagline ("welcome to 36917 — a delta of the Great River.") + animated mandala SVG (207px), links to `/it-could-only-ever-be-this/` |
| `_includes/header.html` | Two-tier grouped nav (WRITING / MAKING labels with rules, vertical dividers). Mandala does **not** live here — it's in `hero.html`. |
| `_includes/footer.html` | Holds "about," "contact," and an italic link to "it could only ever be this." The duplicate mandala-page link was removed from here. |
| `_includes/sidebar.html` | Collapsible tree nav; expand/collapse state persists via `sessionStorage`. **The `.page-layout` CSS lives here, not in `main.css`** — easy to forget. |
| `_layouts/post.html` | Verse/poetry line-wrap fix (see `style: verse` above) |
| `assets/css/main.css` | Main stylesheet (renamed from `.scss` — plain CSS now, no Sass build step) |
| `_config.yml` | Site config; `hard_wrap: true` for kramdown |
| `index.html` | Prose landing page; has an `intro:` front matter field. **Known bug:** YAML double-quote issue — fix is to wrap the outer string in single quotes instead. |
| `pages/lyrics.html`, `pages/eulogies.html` | Have `intro:` front matter added; actual intro text still pending |
| `art.html` | Auto-gallery, see above |
| `it-could-only-ever-be-this/index.html` | Standalone interactive piece, clean URL |

### Structural notes
- The `.page-layout` two-column layout caps usable content width at ~740px. True no-wrap for very long lines isn't possible without hiding the sidebar.
- GitHub Pages runs the JS embedded in Jekyll layouts fine — no build step needed for that.

## Known Issues / Outstanding Work

- [ ] **GitHub Pages deploy** — repo `36917-site` created, Git installed/configured, push sequence prepared but not yet executed. Domain is `36917.me`.
- [ ] **Mandala at 207px** — needs checking on narrow/mobile screens for wrapping issues.
- [ ] **Audio** — ~700MB of audio content to integrate. archive.org chosen as host (free, no cap, direct MP3 linking, no bandwidth throttling — beats Dropbox). Still need to build a reusable `_includes/audio-player.html` include.
- [ ] **Six duplicate post filenames** need resolving:
  - In `_posts/`: `thanks-god`, `compassion`, `all-shall-be-well`, `gibbous-blessing`
  - In `_lyrics/`: `sleep-easy`, `i-dont-know-you`
- [ ] **YAML quote bug** in `index.html` front matter (see above)

## Deploying to GitHub Pages

1. Repo: `36917-site` (already created)
2. Push local `C:\Users\jerry\Documents\36917-site\` to it
3. Repo Settings → Pages → Source: branch + root
4. Point `36917.me` at GitHub Pages via CNAME + DNS

GitHub's docs: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site

## Reference

- `36917-locations.txt` — local reference file for site structure
- Chrome DevTools (Ctrl+Shift+M) for mobile preview testing
- VS Code, Alt+Z toggles word wrap
