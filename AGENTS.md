# AGENTS.md

## What this is

Personal static portfolio site — **HTML5 + CSS3 + vanilla JS only**. No framework, no build step, no backend, no database, no package manager. Dark theme, single page, responsive.

## Run / verify

There is no build or test command. Serve statically (avoids `file://` quirks with fonts/CORS):

```bash
python3 -m http.server 8080
# open http://localhost:8080
```

Or open `index.html` directly in a browser — relative paths (`css/`, `js/`, `resume.pdf`) work either way.

Manual checks only: no console errors, anchor nav scrolls + highlights, 375px→1440px no horizontal scroll, hamburger menu works, keyboard focus visible, `prefers-reduced-motion` disables reveal/scroll animation.

## Structure

```
index.html      # all sections (hero, about, skills, projects, education, contact)
css/style.css   # design tokens at top (:root), then base → sections → responsive
js/main.js      # header scroll state, mobile menu, IntersectionObserver reveal + active link
resume.pdf      # PLACEHOLDER — replace with real resume (same filename)
```

Section IDs for anchors: `#home #about #skills #projects #education #contact`.

## Gotchas

- **All content is placeholder** ("Alex Doe", sample projects, `alex@example.com`, `https://github.com/` links). Swap before deploying; search for `Alex Doe` / `alex@example.com`.
- **Asset paths are relative on purpose** — works on GitHub Pages subpaths, Netlify, or local file open. Don't switch to absolute `/...` paths.
- **Google Fonts** (Inter, JetBrains Mono) load from CDN — offline they fall back to system stack (defined in `--font-sans` / `--font-mono`).
- **Reveal animation**: `.reveal` starts at `opacity: 0`. If JS fails or an element is missed, content stays invisible — new animated elements must use the `reveal` class *and* be observed by `js/main.js`. `prefers-reduced-motion` forces everything visible.
- **Fixed header offset**: section anchors rely on `scroll-padding-top` in `html` (matches `--header-h`). Change both together.
- **Breakpoints**: 900px (about/skills stack), 720px (hamburger nav), 480px (full-width buttons).
- **Mobile menu** locks `body` scroll while open; closed on link click, Escape, and resize past 720px.
- Keep it dependency-free — no npm, no bundler, no framework without an explicit user request.
