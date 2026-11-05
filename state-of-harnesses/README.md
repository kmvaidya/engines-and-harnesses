# The State of the Harness

A 40-minute talk on coding harnesses as of November 2026, told from where
GitHub Copilot stands: what every coding agent shares, where the makers
disagree, what each says it is aiming for, and where the field is heading. It follows *Engines & Harnesses*
(`../index.html`, August) and *Build Your Own Harness* Part 1 (`../build-your-own-harness/`,
October).

The audience uses GitHub Copilot as its only approved tool, so Copilot is the
reference point throughout. Every comparison starts from what Copilot does, then
shows who does the opposite and what the evidence says. The talk covers the
whole field, closed and open source, so the room can place news about other
tools. It does not recommend other tools.

**Open it:** double-click `index.html`, or serve the repo root and go to
`/state-of-harnesses/`. It reuses reveal.js and the fonts in `../vendor/`.
Keys: `→` next section, `↓` deeper, `ESC` map, `S` speaker notes.

Slides carry only what the room has to read. The speaker notes (`S`) have
three parts per slide: the talk track (roughly 75 seconds, read aloud), an
**If asked** paragraph with caveats and answers for questions, and the
**Sources** behind each claim.

## Run of show

Sections run left to right; go down for each section's slides. Each topic
starts with the plain idea and then goes into detail.

| # | Section | Minutes | What it covers |
|---|---|---|---|
| | Title and plan | 1.5 | The seven questions the talk answers |
| 1 | What a harness is | 5 | Agent mode against autocomplete; the four places Copilot's agent runs, on one engine; the loop; Copilot's parts around it; when changing the harness changes results |
| 2 | Who builds harnesses | 5 | Four kinds of builder (Copilot's is a platform owner), how open each engine is, 2026 sales and shutdowns, usage |
| 3 | What they all share | 4 | The same few tools, features copied within months, the open file formats Copilot reads |
| 4 | Where they disagree | 11 | Six design choices on one overview slide, then one slide each: Copilot's choice first, then the opposite choice and the evidence |
| 5 | What each maker believes | 4.5 | Platform owners (Copilot's makers) first, then labs, agent companies and open source, each in its own words |
| 6 | Where it is heading | 3 | Agents that start without a prompt, the review bottleneck, a legacy-code benchmark |
| 7 | What to do | 4 | Questions for our platform team (sandbox, surfaces, models, retention, billing); five habits and how to do each in Copilot |

About 38 minutes. The appendix is never presented: it holds the full comparison
tables (Copilot first, or as a reference row), system prompts, deployment notes
for a bank, the source map, and claims not to repeat.

The deck was checked by three fresh-reader agents (a junior developer, a senior
architect and a QA lead from a mainframe background, none of them AI
specialists) and an AI-writing audit against `research/round4-ai-writing-patterns.md` §11.

## Before presenting

- [ ] Everything was checked against sources on 4 and 5 November 2026. Product
      names and ownership changed monthly in 2026. If you present after
      December, re-check the field and direction sections (2 and 6) first.
- [ ] Read the notes on the loop-matters slide. The evidence on whether the
      harness changes results is mixed, GitHub's "effective parity" result is
      GitHub testing itself, and the notes say how far to push it.
- [ ] A few quotes come from auto-captioned talks; their notes say so. Listen
      to the timestamp before quoting them word for word.
- [ ] The appendix deployment tables are reference notes from public vendor
      docs, not an evaluation. Say so if someone screenshots them.

## Sources

Every perishable claim traces to `../research/round5-*.md` (fetched 4 and 5
November 2026). Start with `round5-synthesis.md`. Each research file ends with
a verification pass from a separate fact-checker, which overrides the body.
The appendix slide "sources" maps each section to its files, and the deck was
written against the house writing rules in `round4-ai-writing-patterns.md` §11.
