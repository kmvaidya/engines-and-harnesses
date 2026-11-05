# The State of the Harness

A 40-minute talk on coding harnesses as of November 2026: what every coding
agent shares, where the makers disagree, what each says it is betting on, and
where the field is heading. It follows *Engines & Harnesses* (`../index.html`,
August) and *Build Your Own Harness* Part 1 (`../build-your-own-harness/`,
October).

The audience uses GitHub Copilot as its only approved tool. The talk covers
the whole field, closed and open source, so the room understands where Copilot
sits. It does not recommend other tools.

**Open it:** double-click `index.html`, or serve the repo root and go to
`/state-of-harnesses/`. It reuses reveal.js and the fonts in `../vendor/`.
Keys: `→` next section, `↓` deeper, `ESC` map, `S` speaker notes.

Slides carry only what the room has to read. The speaker notes (`S`) have
three parts per slide: the talk track (about 180 spoken words, roughly 75
seconds), a "Backup (do not read aloud)" paragraph with caveats and answers
for questions, and the research file behind each claim.

## Run of show

Sections run left to right; go down for each section's slides.

| # | Section | Minutes | What it covers |
|---|---|---|---|
| 1 | The loop | 4 | Every agent runs the same loop; most code lives around it; when the harness changes results and when it doesn't |
| 2 | The field | 5 | Four kinds of builder, how open each harness is, the 2026 sales and shutdowns, usage numbers and their limits |
| 3 | What they share | 5 | The same small toolbox, features copied within months, open standards at the edges, one harness behind many front ends |
| 4 | Where they split | 11.5 | How much harness, finding code, edit formats, system prompts, one agent or many, where safety lives, classifier miss rates, where the work happens |
| 5 | Philosophies | 5 | Model labs, platform owners, agent companies and open source, each in its own words next to something it shipped |
| 6 | Where it is heading | 4 | Four shifts in 2026 release notes, what vendors say comes next, a legacy-code benchmark |
| 7 | What it means for us | 3 | Where Copilot sits on each axis; findings that apply to any harness; questions |

About 38 minutes at 75 seconds a slide. Two slides are marked optional in
their notes (system prompts in section 4, vendor statements in section 6);
skipping both brings it to about 36. The appendix is never presented: it holds
the full comparison tables, deployment notes for a bank, the source map, and
claims not to repeat.

## Before presenting

- [ ] Everything was checked against sources on 4 and 5 November 2026. Product
      names and ownership changed monthly in 2026. If you present after
      December, re-check the field and direction sections (2 and 6) first.
- [ ] Read the notes on the loop-matters slide. The evidence on whether the
      harness changes results is mixed, and the notes say how far to push it.
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
