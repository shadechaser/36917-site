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

Already done — site is live at `36917.me`. For reference:

1. Repo: `36917-site` (created under github.com/shadechaser/36917-site)
2. Pushed local `C:\Users\jerry\Documents\36917-site\` to it
3. Repo Settings → Pages → Source: `main` branch, `/ (root)`
4. `36917.me` pointed at GitHub Pages via a `CNAME` file in the repo + DNS records (A records + CNAME) set at Squarespace domain settings

GitHub's docs: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site

## Updating the Live Site

Once you've made changes locally — added a post, tweaked CSS, whatever — here's how to push them live:

**1. Check it locally first**
Run `start.bat`, look at `localhost:4000`, make sure it looks right.

**2. Push it up**

Open Command Prompt:

```
cd C:\Users\jerry\Documents\36917-site
```

```
git add .
```

```
git commit -m "describe what you changed"
```

```
git push
```

That's it. `git add .` stages every changed or new file in the whole folder — doesn't matter if it's 1 file or 20. `commit` saves a snapshot with your message. `push` sends it to GitHub, which automatically rebuilds and republishes the live site — usually live within a minute or two.

**Notes:**
- No need to run `git init`, `git remote add`, or `git branch -M main` again — those were one-time setup steps already done.
- If `git` ever comes back as "not recognized" in Command Prompt, close and reopen the Command Prompt window (fixes it 90% of the time), or check that `C:\Program Files\Git\cmd` is still in your system PATH.
- The commit message is just a note to your future self — worth being roughly accurate (e.g. `"add three new prose pieces, fix sidebar css"`) rather than always writing `"update"`.

## Reference

- `36917-locations.txt` — local reference file for site structure
- Chrome DevTools (Ctrl+Shift+M) for mobile preview testing
- VS Code, Alt+Z toggles word wrap
