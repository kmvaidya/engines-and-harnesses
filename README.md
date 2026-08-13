# Engines & Harnesses

An interactive web presentation on AI engineering — how language models actually
work, and how to build the machine around them. From neurons to harnesses.

**Live deck:** open `index.html`. That's it — no build step, no dependencies,
everything (reveal.js, fonts) is vendored. It works from a double-click
(`file://`), from any static server, and from GitHub Pages.

## The spine

The model is the **engine**; everything around it is the **harness**. Out of the
box, Copilot is a rental car; configured, it's your car; engineered, it's a fleet
vehicle spec'd for one job. And the harness must be matched to the engine: as
engines get better, the *compensation* layer of the harness shrinks while the
*capability* layer grows — Anthropic deleting 80% of Claude Code's system prompt
for Claude 5-generation models (verified, cited on the slide) is the receipt.

## Driving it

| Key | Does |
|---|---|
| `→` / `←` | next / previous act (horizontal = the 12 acts) |
| `↓` / `↑` | optional depth within an act (vertical = skippable) |
| `ESC` | overview map of the whole deck |
| `S` | speaker view — notes + timer (allow the popup) |
| `F` | fullscreen |

Every act stands alone; jump anywhere. Speaker notes carry "if short on time,
skip to X" at the load-bearing junctions.

### Suggested cuts

- **30 minutes:** Title → Act 2 (Tokens, with the live demos) → Act 3 (Scale) →
  The Turn → Act 6 (Harness: map, instructions file, before/after) → Act 9 ladder.
- **60 minutes:** the above, plus Act 1 (History), Act 4 (Thinking tokens),
  Act 7 (Context engineering + the generation shift), and the Kahoot.
- The appendix column is never presented; it's for readers of the site.

### Live demos

All embedded demos (Transformer Explainer, Tiktokenizer, TensorFlow Playground,
bbycroft's LLM visualization) were probed and embed cleanly in iframes
(`research/track3-demo-embeds.md`). Every embed has an "open in new tab" bar —
use it if the venue projector or network misbehaves. Demos need network; the
deck itself does not.

## Serving locally

Any static server works, e.g.:

```sh
python -m http.server 8000
# then http://localhost:8000
```

(Only needed if your browser blocks the speaker-view popup on `file://` —
otherwise double-clicking `index.html` is fine.)

## PDF fallback (offline insurance)

Open in Chrome/Edge:

```
http://localhost:8000/?print-pdf
```

then `Ctrl+P` → Save as PDF, "Background graphics" ON, margins None. Iframes are
hidden in print; each demo slide keeps its title/description/URL card.

## Deploying to GitHub Pages

```sh
git remote add origin https://github.com/<you>/<repo>.git
git push -u origin main
```

Then on github.com: **Settings → Pages → Deploy from a branch → `main` / `(root)`**.
The deck appears at `https://<you>.github.io/<repo>/`. Nothing to configure —
the site is static files at the repo root.

## What's in the repo

```
index.html            the whole deck (slides + speaker notes)
css/theme.css         custom dark theme ("shop manual" — amber engine, teal harness)
vendor/               reveal.js 5.2.1 + plugins + fonts, vendored for offline
research/             38 sourced research files + INDEX.md — the bibliography;
                      every perishable fact on a slide traces here (fetched 2026-08-12)
kahoot-questions.md   8 draft quiz questions, gimme → spicy
BLINDSPOTS.md         pre-build blind-spot pass on the brief, with the calls made
ASSUMPTIONS.md        decisions made without asking, logged
```

## Updating it later

The Copilot surface moves monthly. The deck flags perishable facts with "as of
August 2026"; to refresh, re-run the research sweep (the files in `research/`
carry their source URLs), update the affected slides, and bump the date on the
title slide. The engine-side acts (1–5) age slowly; Acts 6–8 are the ones to
re-check.

---

Deck by **Kay** · August 2026 · researched and assembled with Claude (Fable 5).
Fork it, gut it, present your own version — that's what it's for.
