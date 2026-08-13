# Assumptions log

Running log of decisions made without asking. Newest at the bottom.

- **2026-08-12** — No skill named `frontend-design` exists in this environment. The
  closest is `artifact-design` (targets claude.ai Artifacts). I load it for its
  design fundamentals and hand-build the reveal.js theme; the deck is a custom
  dark theme, not a stock reveal template.
- **2026-08-12** — reveal.js is **vendored** into `vendor/` (no CDN) so the deck
  opens by double-click with no network and survives a locked-down venue. Fonts
  (Inter Variable, JetBrains Mono Variable) vendored too, same reason. No build
  step: the site is plain files, served from repo root.
- **2026-08-12** — Deck language is English; single `index.html` carries all
  slides inline (reveal's external-markdown loading breaks over `file://`).
- **2026-08-12** — Attribution: deck footer/title uses **Kay** (from git identity;
  the brief says "my name on it" but never states the name). It's one marked line
  in `index.html` to change.
- **2026-08-12** — I commit locally but do **not** create a GitHub repo or push:
  publishing under the user's account is theirs to trigger. README has the exact
  commands to go from this repo to a live GitHub Pages URL.
- **2026-08-12** — Site serves from the repo **root** (GitHub Pages "deploy from
  branch, / root"), so `index.html`, `vendor/`, `css/` live at top level next to
  the docs files. Research and meta files are part of the public artifact — the
  brief says fully public from commit one, and they're presentable.
- **2026-08-12** — "Roughly two hours" is treated as a soft budget for *my* work;
  research agents run in parallel and don't count against writing time.
- **2026-08-12** — Correction to the brief: Papyan's MAT1510 is a *graduate
  theory* course and links **no** interactive demos (verified against the raw
  HTML of all five year pages). So the history act embeds the classic demos
  directly (TensorFlow Playground etc.) and uses the course differently — its
  2021→2025 syllabus drift as a "watch the field move" slide, plus its framing
  and public slide decks as the act's reference. See research/track3-papyan-course.md.
