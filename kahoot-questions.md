# Kahoot — 11 questions, all harness engineering, scenario-first

Redesigned 2026-08-13: instead of "did you read the slides", each question is a
situation a real Copilot user hits, and the correct answer is the optimal
harness-engineering move. Mix: 5 medium, 6 hard. Q11 is the one pure knowledge
question. Traps where the obvious answer is wrong are marked 🪤.

Kahoot limits: question ≤ 120 chars, answers ≤ 75 chars — all fit. Correct
answer marked ✔, spread across the four slots. Timer: 30s everywhere (scenarios
need reading time); 20s is fine for Q7 and Q11.

Every answer is verified against `/research/` (fetched 2026-08-12). The
rationale line under each question is for the host, not for Kahoot.

---

**1. Copilot keeps writing npm commands and untyped JS in your strict pnpm TypeScript repo. One fix for the whole team goes where?** *(medium)*

- Each dev adds it to their personal instructions
- ✔ .github/copilot-instructions.md, committed to the repo
- Paste the rules at the start of every chat
- Fine-tune a custom model on the codebase

*Why: repo-wide instructions are auto-added to every request for everyone with the repo, the moment the file is saved. Personal instructions fix one person; pasting fixes one chat. (track1-repo-custom-instructions.md)*

**2. Half your team uses Copilot, half Claude Code, one holdout uses Cursor. The ONE instructions file they all read?** *(medium)*

- ✔ AGENTS.md
- .github/copilot-instructions.md
- README.md
- One file per tool, kept in sync by hand

*Why: AGENTS.md is the emerging cross-tool standard; Copilot, Claude Code, Codex, Cursor and Gemini all read it, so the harness investment survives changing tools. (track1-agents-md.md)*

**3. Your migration rules leak into answers about React code. How do you scope them to just the migrations folder?** *(medium)*

- Split the frontend into its own repo
- Add "only applies to migrations" to the repo-wide file
- ✔ A .instructions.md file with an applyTo glob
- Name the folder in every prompt

*Why: path-specific files in .github/instructions/ take an applyTo glob (comma-separated inside one string, e.g. "prisma/migrations/&#42;&#42;") and only ride along for matching files. Repo-wide instructions always apply, whatever caveat you write into them. (track1-path-specific-instructions.md)*

**4. The cloud agent should follow your style rules, but code review nitpicks them on every PR. The precision knob?** *(hard)*

- ✔ excludeAgent: "code-review" in that file's frontmatter
- Delete the style rules and trust reviewers
- Turn off Copilot code review for the repo
- Keep two copies of the repo with different rules

*Why: the excludeAgent frontmatter key (new in 2026) opts one instructions file out of "code-review" or "cloud-agent" while the other surface keeps it. (track1-path-specific-instructions.md)*

**5. Your team has 30 playbooks: deploys, migrations, browser tests. Loading them all would flood the context window. The fix?** *(hard)*

- One giant AGENTS.md holding all 30
- Pick a model with a bigger context window
- Paste the right playbook into chat each time
- ✔ Skills: name+description in context, body loads when needed

*Why: progressive disclosure. A skill costs a one-line description until its moment comes, so you can install many and pay for none until they fire. The giant file and the bigger window both still spend tokens on all 30 every request. (track1-agent-skills.md)*

**6. Compliance says the agent must NEVER force-push. "It usually obeys the rule" won't fly. What do you reach for?** *(hard)*

- An ALL-CAPS rule in copilot-instructions.md
- ✔ A preToolUse hook that returns deny
- A warning paragraph in AGENTS.md
- Asking for confirmation in every prompt

*Why: instructions persuade a probabilistic model; a hook is plain code that gates the tool call before it runs, and a preToolUse guard that errors fails closed. Deterministic, auditable, not a matter of model mood. (track1-hooks.md)*

**7. Your Planner custom agent must never edit code, and it never does. What actually guarantees that?** *(hard, 🪤)*

- The "Do NOT edit code" line in its prompt
- A script that reverts its edits afterward
- ✔ Its tools list simply has no edit tool
- Its temperature is set to zero

*Why: safety by construction. The .agent.md tools list is the guardrail; the agent can't use a capability it was never handed. The prompt line is politeness, not enforcement. (track1-custom-agents.md)*

**8. A teammate hitched 9 MCP servers "just in case". Chat got pricier and dumber before any tool was even used. Why?** *(medium)*

- ✔ Every tool description spends context on every request
- The servers burn CPU in the background
- Each server adds network round-trips
- MCP bills per connected server

*Why: every connected server's tool definitions sit in the context window whether used or not, thinning attention and raising cost. Anthropic's fix for the extreme case cut one workflow from 150K tokens to 2K. Hitch only the trailers you're towing. (track2-anthropic-code-execution-mcp.md)*

**9. You assign an issue to the cloud agent. Its PR admits tests failed: dependencies never installed in its sandbox. The fix?** *(hard)*

- Write "run pnpm install first" in the issue
- List the dependencies in AGENTS.md
- Retry until a run gets lucky
- ✔ A copilot-setup-steps.yml workflow pre-installs them

*Why: .github/workflows/copilot-setup-steps.yml (on the default branch, exact job name copilot-setup-steps) provisions the Actions sandbox before the agent starts. Instructions ask; setup steps guarantee. (track1-coding-agent.md)*

**10. The cloud agent's PR carries a warning: a request to your private package registry was blocked. The right fix?** *(hard, 🪤)*

- Disable the agent firewall
- ✔ Add the registry domain to the firewall allowlist
- Mirror the packages to public npm
- Retry the task; it's probably a flake

*Why: the blocked-request warning names the address and command; the Internet access settings take custom domain or URL entries. Disabling the firewall "works" but the docs' own warning applies: it opens exfiltration risk for every future run. (track1-coding-agent.md)*

**11. Anthropic cut 80% of Claude Code's system prompt for Claude 5 models. Effect on their coding evals?** *(medium, knowledge)*

- A small, acceptable quality drop
- Big cost win, small quality loss
- ✔ No measurable loss
- It only worked after adding examples

*Why: "we removed over 80% of Claude Code's system prompt — and saw no measurable loss on our coding evaluations" (Thariq Shihipar, claude.com/blog, Jul 24 2026). The thesis in one number: as engines improve, compensation scaffolding comes out. (track2-thin-harness-evidence.md)*

---

Setup: kahoot.com → Create → 11 questions is comfortable to enter by hand in
one sitting (the spreadsheet import stops being worth it at this size). Strip
the *(difficulty)* tags and Why lines; they're host notes. Correct answers land
in slots 1/2/3/4 fairly evenly as written. Grab the join QR from the lobby
screen and drop it into the placeholder box on the Kahoot slide.
