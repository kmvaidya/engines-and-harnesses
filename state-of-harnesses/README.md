# The State of the Harness

A 40-minute talk on coding harnesses as of November 2026, told from where
GitHub Copilot stands: what every coding agent shares, where the makers
disagree, what each says it is aiming for, and where the field is heading. It follows *Engines & Harnesses*
(`../index.html`, August) and *Build Your Own Harness* Part 1 (`../build-your-own-harness/`,
October).

The audience uses GitHub Copilot as its only approved tool, so Copilot is the
reference point throughout: it is the first column of every table and the blue
name on every slide. Comparisons show the whole field, though, not Copilot against
everyone else: each design question shows the camps builders fall into, who is in
each and why, and where Copilot sits among them. The talk covers the
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
| 1 | What a harness is | 7 | Agent mode against autocomplete; where Copilot's agent runs, on one engine; the loop, with a click-through **demo** of one session; Copilot's parts; a **demo** of working space filling and being summarised; when changing the harness changes results |
| 2 | Who builds harnesses | 4 | Four kinds of builder, how open each engine is, usage |
| 3 | What they all share | 3 | The same few tools; the open file formats Copilot reads |
| 4 | Where they disagree | 13 | One table of seven products against seven questions, then one slide per question showing the camps, with **demos** for search, edit formats (find and replace failing on an ambiguous match) and safety layers; which AI approvers have published error rates |
| 5 | What each maker believes | 6.5 | Maker cards from each maker's own documentation (belief, quote, what it built, where words and product don't match): platform owners (Copilot's makers) first, then labs, agent companies and open source; then where they agree and the two questions that split them |
| 6 | Where it is heading | 3.5 | A 2026 timeline of five trends across the whole field, with Copilot's releases marked; a legacy-code benchmark |
| 7 | What to do | 5 | Questions for our platform team; five habits; what evidence is solid and what is weak |

About 43 minutes with the in-deck demos. To bring it to 40, take the phil-sum slide in a sentence and skip the search demo. Two **optional live embeds** add about a
minute each: the SWE-bench "Bash Only" leaderboard (section 1) and the agents.md site
(section 3). They need internet access; skip them if the room's network blocks them.

**Demos.** The step-through and working-space slides advance with the normal
next key (they use fragments). The search, edit and safety widgets are clicked
on the slide; their data lives in `js/demos.js` and runs offline. Each is
labelled as an illustration on screen. Bank-specific answers to the
platform-team slide are deliberately not in this repo.

The appendix is never presented: it holds the full comparison tables (Copilot
first, or as a reference row), system prompts, 2026 sales and shutdowns,
features copied between tools, deployment notes for a bank, the source map,
and claims not to repeat.

Sections 4 to 6 were rebuilt on 5 November after Kay's third review (they read as
Copilot against everyone, and the philosophies were not grounded in the makers' own
docs). The deck was checked by three fresh-reader agents (a junior developer, a senior
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

Every perishable claim traces to `../research/round5-*.md` (fetched 4 November
2026) or `../research/round6-*.md` (checked against live pages 5 November 2026;
round 6 wins where they conflict). Start with `round5-synthesis.md`; section 5's
maker cards come from `round6-philosophy-sources.md`. Each research file ends with
a verification pass from a separate fact-checker, which overrides the body.
The appendix slide "sources" maps each section to its files, and the deck was
written against the house writing rules in `round4-ai-writing-patterns.md` §11.
