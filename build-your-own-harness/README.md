# Build Your Own Harness

A lunch & learn series on building a GitHub Copilot harness for a real
codebase. It follows the August deck, *Engines & Harnesses* (`../index.html`).

**Open it:** double-click `index.html`, or serve the repo root and go to
`/build-your-own-harness/`. It reuses the reveal.js and fonts vendored in
`../vendor/`. Keys: `→` next section, `↓` deeper, `ESC` map, `S` speaker notes.

The slides carry only what has to be read. The talk track, sources and
caveats are in the speaker notes (`S`).

## Part 1 run of show

Sections run left to right. Each one is a column; go down for its slides.

| # | Section | Slides | Live in VS Code |
|---|---|---|---|
| 1 | Catch up | Recap table, changes since August, how the sessions work | |
| 2 | The contract | Map and territory, four kinds of knowing, the model's four, what the harness does, the board | Room fills the board |
| 3 | Anatomy | Prompt, memory, tools; what loads before your prompt; how to check; memory | Open Chat Debug View |
| 4 | `/init` | What it does, then **Wait** | Ask the repo owner what's off limits |
| 5 | Hooks first | Instructions vs hooks, no `git push`, protected paths, limits, other uses | `/create-hook`, test both hooks |
| 6 | Instructions | Review the draft, sections, Git conventions, writing rules, lifespan rule, which file, fix loop, personal files | Run `/init`, review, edit |
| 7 | Onboarding guide | The prompt, reading the work, prompt vs skill vs agent, the skill, staleness hook, cloud automation | Write ONBOARDING.md, add the skill |
| 8 | Narrow agents | Narrow vs broad, seven auditors, one auditor file, parallel sessions, spec-to-verify | Start 2 or 3 auditors |
| 9 | Close | Board again, what to dig into next | Room adds requests |

An hour fits sections 1 to 6 comfortably. Sections 7 and 8 are there if the
room moves fast, or for next time.

## The interactive bits

- **Quadrant board** (sections 2 and 9 share items): type and press Enter;
  click an item to remove it. **examples** shows dashed starter items for a
  quiet room; click one to add it.
- **Requests list** at the end.
- Saved in this browser's local storage only. Present from the browser you
  prepared in, and clear it (click items away) before the session.

## Prep checklist

- [ ] **Session Target.** Since VS Code 1.140 the default may be the
      Copilot harness. `/init` is documented for Local sessions; in a Copilot
      session use Chat: Open Customizations. Pick one in the dry run.
- [ ] **Node** on the presenting machine (the hook scripts use it).
- [ ] **Dry run the hooks** on a throwaway branch. Run the audit hook from
      `research/round3-hooks-context-memory.md` Q1 once to confirm the Local
      tool argument names, then ask the agent to `git push` and to open `.env`.
      In a Copilot session a crashing hook blocks every tool call.
- [ ] **Dry run `/init`** and note how long it takes.
- [ ] Have your personal principles file ready to show (section 6).
- [ ] For section 8: create `docs/audit/`, and set
      `"chat.tools.edits.autoApprove": { "**/*": false, "docs/audit/**": true }`.
- [ ] Clean terminal (no exported tokens). Clear the board.

## Keep it generic

This repo is public. Slides use made-up examples (`AuditLogger`,
`src/generated/`). Anything from the team's real repo stays on screen and in
the team's own branch.

## Adding a part

Add new sections after section 9, add a row to the deck log, and re-check any
Copilot setting against the live docs. They change monthly.

## Sources

`../research/round3-*.md` (fetched 2026-10-01) and
`../research/round2-vscode-copilot-setup.md`. The appendix slide maps each
section to its file.
