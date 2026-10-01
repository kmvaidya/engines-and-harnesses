---
url: https://code.visualstudio.com/docs/agents/concepts/customization, https://code.visualstudio.com/docs/agent-customization/overview, https://code.visualstudio.com/docs/agent-customization/prompt-files, https://code.visualstudio.com/docs/agent-customization/agent-skills, https://code.visualstudio.com/docs/agent-customization/custom-agents, https://code.visualstudio.com/docs/agent-customization/custom-instructions, https://code.visualstudio.com/docs/agent-customization/tool-sets, https://code.visualstudio.com/docs/agents/reference/tools-reference, https://code.visualstudio.com/docs/agents/reference/hooks-reference, https://code.visualstudio.com/docs/agents/run/subagents, https://code.visualstudio.com/docs/agents/concepts/agents, https://code.visualstudio.com/docs/agents/concepts/sessions, https://code.visualstudio.com/docs/agents/run/agent-harnesses, https://code.visualstudio.com/docs/agents/run/sessions/manage-sessions, https://code.visualstudio.com/docs/agents/run/approvals, https://code.visualstudio.com/docs/agents/run/review-code-edits, https://code.visualstudio.com/docs/agents/run/automations, https://code.visualstudio.com/docs/agents/guides/delegate-two-tasks, https://code.visualstudio.com/docs/agents/guides/customize-copilot-guide, https://code.visualstudio.com/docs/agents/best-practices, https://docs.github.com/en/copilot/concepts/agents/cloud-agent/about-automations, https://docs.github.com/en/copilot/how-tos/use-copilot-agents/cloud-agent/create-automations, https://docs.github.com/en/copilot/concepts/agents/about-github-agentic-workflows, https://docs.github.com/en/copilot/how-tos/github-agentic-workflows/creating-github-agentic-workflows, https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/add-custom-instructions/add-repository-instructions, https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/add-custom-instructions/add-personal-instructions, https://docs.github.com/en/copilot/how-tos/copilot-in-your-ide/customize-copilot/configure-custom-instructions/add-repository-instructions-in-your-ide, https://docs.github.com/en/copilot/reference/custom-instructions-support, https://docs.github.com/en/copilot/reference/custom-agents-configuration, https://docs.github.com/en/copilot/concepts/prompting/response-customization, https://docs.github.com/en/copilot/concepts/agents/code-review, https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/add-skills, https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions, https://docs.github.com/en/copilot/how-tos/copilot-cli/automate-copilot-cli/schedule-prompts, https://github.github.io/gh-aw/reference/safe-outputs-pull-requests/, https://github.github.io/gh-aw/reference/schedule-syntax/, https://github.github.io/gh-aw/reference/permissions/, https://github.github.io/gh-aw/reference/tools/, https://github.github.io/gh-aw/reference/copilot-cloud-agent/, https://github.blog/changelog/2026-06-02-schedule-and-automate-tasks-with-copilot-cloud-agent/, https://github.blog/changelog/2026-08-03-trigger-copilot-automations-with-comments/, https://github.blog/changelog/2026-09-10-github-copilot-weekly-releases-september-7/, https://agents.md/
fetched: 2026-10-01
---

# Round 3: prompt files vs skills vs agents, parallel agents, scheduled doc updates, instructions

Round 3 file. Tags: [P] confirmed against the primary source on 2026-10-01, [R] refuted.

Method: read the Markdown sources of the docs (microsoft/vscode-docs at commit
2026-09-30, `DateApproved: 9/30/2026`; github/docs `main`; github/gh-aw `main`,
latest release v0.89.21 of 2026-09-23), resolved GitHub's `{% data reusables %}`
includes, then spot-checked 25 distinctive phrases on the live rendered pages
(code.visualstudio.com, docs.github.com, github.github.io/gh-aw). All matched.
Session target names used below: **Local** (VS Code extension host, being
removed), **Copilot** (Agent Host, Copilot SDK harness), **Claude**, **Codex**,
**Cloud**.

---

## A. Prompt files vs skills vs custom agents

### 1. Definitions and the docs' own "which one" guidance [P]

VS Code has a decision page: "Understand agent customization", section
"Customization options at a glance"
(code.visualstudio.com/docs/agents/concepts/customization). The prompt-file,
skill and custom-agent pages all link to it as the "decision matrix".

Questions it tells you to ask: "Should it apply automatically, or only when you
request it?", "Are you providing guidance, defining a workflow, adding a
capability, or enforcing an action?", "Should the model decide when to use it?"

| Need (verbatim) | Use | Example (verbatim) | Activation (verbatim) |
|---|---|---|---|
| Teach the agent a workflow with supporting resources | Agent skills | Create a service from instructions, template files, and a setup script | The agent loads the skill when the task matches, or you invoke it directly |
| Run a saved task on demand | Prompt files | Scaffold a React component | You invoke the prompt as a slash command |
| Use a specialized role and tool configuration | Custom agents | Review code with read-only tools | You select the agent, use it as a subagent, or another agent delegates to it |

Definitions (verbatim):
- Prompt files: "Prompt files, also known as slash commands, let you simplify
  prompting for common tasks by encoding them as standalone Markdown files that
  you can invoke directly in chat." (.../agent-customization/prompt-files)
- Skills: "Agent Skills are folders of instructions, scripts, and resources
  that AI agents can load when relevant to perform specialized tasks. Agent
  Skills is an open standard that works across multiple AI agents"
  (.../agent-customization/agent-skills). GitHub: "Agent skills are folders of
  instructions, scripts, and resources that Copilot can load when relevant to
  improve its performance in specialized tasks."
- Custom agents: "Custom agents combine instructions, tools, and an optional
  language model into a reusable configuration for a specific role, such as
  planning or code review." (.../agent-customization/custom-agents)

Starting advice: "Start with instructions when your main goal is to stop
repeating project context. Add other customization types when you identify a
recurring task, specialized role, missing capability, or action that must
always run." And: "Customization types are building blocks rather than
mutually exclusive alternatives." (concepts/customization)

Instructions are not enforcement: "adding a rule to an instructions file is not
equivalent to enforcing that rule with a hook." (concepts/customization)

GitHub's skills-vs-instructions line: "We recommend using **custom
instructions** for simple instructions relevant to almost every task (for
example information about your repository's coding standards), and **skills**
for more detailed instructions that Copilot should only access when relevant."
(docs.github.com/.../customize-cloud-agent/add-skills)

### 2. Status and capabilities [P]

- **Prompt files deprecated for Agent Host, still work in Local.** Current
  wording, identical on the prompt-files page and the overview migration
  section: "Prompt files are deprecated for Agent Host sessions and aren't
  loaded by Agent Host. They continue to work with the Local agent for now, but
  the Local agent will be removed in a future release. Use prompt file
  migration to convert existing prompts to agent skills. This experimental
  migration is enabled by default." Setting:
  `chat.customizations.promptMigration.enabled`: `true`. Confirms round 2 §9.4.
- Custom-agents page repeats it: "Agent Host sessions don't load prompt files."
- GitHub docs (response-customization, VS Code/VS/JetBrains tabs) still
  describe prompt files with no deprecation note. JetBrains: the support
  reference says its Customizations editor lets you "manage reusable skills and
  prompt files". **Doc disagreement:** VS Code deprecates, GitHub docs do not.
- **Skills as /name: yes.** "Skills are available as slash commands in chat,
  alongside prompt files. Type `/` in the chat input field to see a list of
  available skills and prompts". Example: "`/webapp-testing for the login
  page`". Hide from `/` with `user-invocable: false`; make slash-only with
  `disable-model-invocation: true`.
- **Skills can bundle scripts/templates: yes.** VS Code: "Optionally, add
  scripts, examples, or other resources to your skill's directory." Note: "Make
  sure to reference any additional files in your `SKILL.md` for them to be
  picked up by the agent. Use Markdown links or `#file:` references with paths
  relative to the `SKILL.md` file". Also "If a file isn't referenced in the
  instructions, it won't be loaded."
- **Doc disagreement on skill resources:** GitHub says "When a skill is
  invoked, Copilot automatically discovers all of the files in the skill's
  directory and makes them available alongside the skill's instructions."
  VS Code says unreferenced files are not loaded. Safe rule for slides:
  reference every bundled file from `SKILL.md`.
- Skill frontmatter differs by product. VS Code documents `name`,
  `description` (required), `argument-hint`, `user-invocable`,
  `disable-model-invocation`, `context: fork` (experimental). GitHub documents
  `name`, `description`, `license`, `allowed-tools` (not in VS Code docs).
  `name` "Must match the parent directory name. Maximum 64 characters. Names
  with invalid characters cause the skill to silently fail to load."

### 3. Minimal examples (only documented fields) [P for fields; files are ours]

(a) `.github/skills/update-onboarding-doc/SKILL.md`

```markdown
---
name: update-onboarding-doc
description: Updates ONBOARDING.md to match recent repository changes. Use when asked to refresh or check the onboarding guide after merges, new setup steps, renamed commands, or new environment variables.
argument-hint: "[git ref or date to start from, default 14 days ago]"
---

# Update ONBOARDING.md from recent changes

1. List recent changes: run `git log --since="14 days ago" --name-status --no-merges`
   (or use the ref or date the user gave). Focus on build files, setup scripts,
   CI workflows, `.env.example` and top-level docs.
2. Read `ONBOARDING.md` at the repository root and the
   [section checklist](./checklist.md).
3. For each change a new joiner would hit (new prerequisite, renamed command,
   new environment variable, removed step), update the matching section.
   Keep the existing headings and tone.
4. Edit only `ONBOARDING.md`. Do not change code or other docs.
5. Update the "Last reviewed" line with today's date and the commit range.
6. Reply with one line per edit and the commit that caused it. If nothing
   relevant changed, say so and make no edits.
```

Folder: `SKILL.md` plus `checklist.md` (referenced from the body, as VS Code
requires). `argument-hint` is VS Code-only; drop it for a strictly portable
file. `name` matches the folder name.

(b) `.github/prompts/update-onboarding-doc.prompt.md` (Local agent only)

```markdown
---
name: update-onboarding-doc
description: Update ONBOARDING.md from recent repository changes
argument-hint: "since=<git ref or date>"
agent: agent
tools: ['read', 'search', 'edit', 'execute']
---
Update `ONBOARDING.md` so it matches changes since ${input:since:14 days ago}.

1. Run `git log --since="${input:since:14 days ago}" --name-status --no-merges`.
2. Read `ONBOARDING.md` and [our docs style guide](../instructions/docs.instructions.md).
3. Update only the sections a new joiner would be affected by. Edit no other file.
4. Summarize each edit and the commit that caused it.
```

Fields used are all in the prompt-file table: `description`, `name`,
`argument-hint`, `agent`, `model` (omitted), `tools`. `${input:name:placeholder}`
is documented as a convention "Most language models understand"; it is not a
guaranteed variable. Tool sets `read`, `search`, `edit`, `execute` are from the
tools reference. Because prompt files are not loaded on Agent Host, ship the
skill, not the prompt file, for the Copilot target.

### 4. Custom agents (.agent.md) [P]

VS Code frontmatter fields today (custom-agents page, verbatim names):
`description`, `name`, `argument-hint`, `tools`, `agents`, `model` (string or
prioritized array), `user-invocable`, `disable-model-invocation`, `infer`
("**Deprecated.**"), `target` (`vscode` or `github-copilot`), `mcp-servers`
(for `target: github-copilot`), `handoffs` (`label`, `agent`, `prompt`,
`send`, `model`), `hooks` (Preview). Hooks: "Hooks defined here only run in the
Local harness when this agent is active". `agents` note: "If you specify
`agents`, ensure the `agent` tool is included in the `tools` property."

GitHub reference (custom-agents-configuration): `name`, `description`
(**Required**), `target` ("If unset, defaults to both environments"), `tools`,
`model` (string), `disable-model-invocation`, `user-invocable`, `infer`
(retired), `mcp-servers`, `metadata`. Body max: "The prompt can be a maximum of
30,000 characters." `argument-hint` and `handoffs` "are currently not supported
for Copilot cloud agent on GitHub.com. They are ignored to ensure
compatibility." "All unrecognized tool names are ignored".

Tool names, read-only (VS Code tools reference): tool sets `read` ("Read
workspace files and execution output"), `search` ("Search the workspace"),
`web` ("Access web content"). Individual: `read/readFile`, `read/problems`,
`read/terminalLastCommand`, `search/changes`, `search/codebase`,
`search/fileSearch`, `search/listDirectory`, `search/textSearch`,
`search/usages`, `web/fetch`, `githubRepo`, `githubTextSearch`.
Editing: tool set `edit` ("Modify workspace files and notebooks"),
`edit/createDirectory`, `edit/createFile`, `edit/editFiles`,
`edit/editNotebook`. Running: `execute`, `execute/runInTerminal`.
Delegation: `agent`, `agent/runSubagent`.
- [R] Round 1 cited `read/file`. The reference lists `#read/readFile`; there is
  no `read/file`.
- GitHub aliases (case-insensitive) for portable files: `execute`, `read`,
  `edit`, `search`, `agent`, `web`, `todo`. So `tools: ['read', 'search']` is
  valid in both VS Code and on github.com. `web` and `todo` are "Currently not
  applicable for Copilot cloud agent".

**Write to only one file: not possible through tool scoping.** No documented
tool or frontmatter field takes a path. `edit` is all-or-nothing. Documented
partial controls:
1. `handoffs` to an editing agent with a pre-filled prompt (human clicks it).
2. Sensitive-file approval: `chat.tools.edits.autoApprove` glob map ("To
   require confirmation before specific files are edited, configure
   sensitive-file approval"). This asks, it does not block.
3. Local only: an agent-scoped `PreToolUse` hook can return
   `permissionDecision: "deny"`. But the hook input documents `tool_input` only
   as "Arguments for the tool call", so the file-path field of edit tools is
   undocumented. Test before relying on it.

Minimal read-only auditor with a one-file save step (VS Code; the handoff is
ignored on github.com):

```markdown
---
name: Auditor
description: Audit the codebase for security and convention issues and report findings without editing files
tools: ['read', 'search']
handoffs:
  - label: Save report to docs/AUDIT.md
    agent: agent
    prompt: Write the audit findings above to docs/AUDIT.md. Do not edit any other file.
    send: false
---
Review the requested scope using read-only tools. Report each finding with
file path, line, severity and a suggested fix. Do not propose edits to files.
```

The Auditor itself cannot edit. The save happens in the built-in Agent after a
human click (`send: false`), and nothing technically stops that agent touching
other files. Pair it with `chat.tools.edits.autoApprove: {"**/*": false,
"docs/AUDIT.md": true}` if you want a prompt on any other edit. The docs'
security advice: "For security-sensitive workflows, create agents with
read-only tools to prevent unintended modifications."

---

## B. Running agents in parallel in VS Code [P]

### 5. Ways to run several agents at once

- **Sessions in parallel.** "Sessions are independent, can run in parallel,
  and are shared across the Chat view and the Agents window."
  (concepts/agents). Best practices: "You can have multiple sessions running
  at once, across local, background, and cloud environments, and switch
  between them via the sessions list". Agents window: to start one in the
  background, "press `Alt+Enter` or hold `Alt` and select **Send**".
  `chat.viewSessions.enabled` (default `true`): "Show the agent sessions list
  in the Chat view." The docs now say "sessions list"; no page calls it an
  "Agent Sessions view".
- **Peer chats inside one session** (Agent Host, Copilot and Claude): "Running
  several chats in one session lets you work on related tasks against the same
  codebase at the same time".
- **Subagents.** Local uses `runSubagent` (`agent/runSubagent`); the Copilot
  harness "uses the Copilot SDK to manage delegation". Parallelism is
  conditional: "independent subtasks can run in parallel when the harness
  supports concurrent subagents" (concepts/agents). The Local tab does not say
  Local subagents run concurrently; its example is "Use two subagents to
  review the current changes". Local limits: "Each Local invocation is
  stateless", nesting off by default
  (`chat.subagents.allowInvocationsFromSubagents`), "maximum depth of five".
  Restrict with `agents: [...]`.
- **Agent-driven orchestration** (Agent Host): agents can "Create a new session
  for a sub-task, or create a new chat in an existing session" and "Send a
  message to another session". "Sending a message to another session always
  requires your confirmation."
- **Copilot CLI in VS Code:** "enter `copilot` in an integrated terminal.
  VS Code adds the session to the sessions list." VS Code "can also discover
  supported local sessions created in Copilot CLI, the GitHub Copilot app,
  Claude Code, and Codex."
- **Worktree sessions** (Agents window only: "The code isolation option
  (worktree or folder) is only available in Agents window"). Use **New
  Worktree** for "Parallel tasks that should not modify your active
  workspace".
- **Cloud delegation:** Session Target **Cloud** runs remotely and "opens a
  pull request for review"; "In a Copilot session, enter `/delegate` to
  continue the task in the cloud." Claude and Codex cloud agents "are
  currently in preview".
- **Local automations** (VS Code 1.137, public preview per changelog
  2026-09-10): saved prompt plus schedule; "An automation runs one session at
  a time."

### Worktree safety (confirms round 2)

- "Worktree sessions use **Allow all**, so choose **Folder** when you want
  manual approval prompts. A worktree isolates code changes but isn't a
  security boundary." (run/agent-harnesses)
- For the Copilot harness: "**Worktree**: the permission level is **Allow
  all** and can't be changed." Approvals page: "worktree sessions always use
  **Allow all**."
- "It does not restrict commands, network access, or access to files outside
  the worktree. Use agent sandboxing for operating system-level file system and
  network restrictions." (concepts/agent-harnesses)
- Implication for slides: choosing a worktree to run things in parallel
  silently turns off approval prompts. Enterprise `ask`/`deny` managed rules
  still apply (round 2 §10.1).

### Two agents, same file

- "Both chats can edit the same files." "Separate conversations don't
  guarantee separate files. If two chats or sessions use the same folder or
  worktree, their edits affect the same files." (concepts/sessions)
- "a fork of a Copilot worktree session continues to use the original
  worktree."
- Agent Host edits have no pending state: "the agent applies and saves edits
  directly in the session's folder or isolated Git worktree."
- With separate worktrees: "Each task has its own working files and branch.
  Integration can still produce conflicts." and "Separate worktrees can still
  share ports, databases, and other external resources."
- Locking, merge or last-writer behaviour for concurrent edits to one file:
  **not found**.

---

## C. Automating a recurring doc update on GitHub

### 6a. Copilot cloud agent automations [P]

- "With automations, you can set up Copilot cloud agent to run automatically,
  either on a schedule or in response to an event in a repository."
- Triggers in the docs: "On a schedule ... hourly, daily, or weekly", "When an
  issue is created", "When a pull request is opened", "When a pull request is
  synchronized". [R] Round 1 listed only schedule and issue-created.
- **Doc/changelog disagreement:** changelog 2026-08-03 "Trigger Copilot
  automations with comments": "run when an issue comment or pull request
  comment is created". The docs trigger list does not include comments.
- Configure name, prompt, triggers, model, tools ("such as pushing changes,
  updating issue labels, or creating a pull request"). "Selecting tools is the
  main way you control the scope". "can only take action in the single
  repository it is scoped to."
- Availability: "The repository must be **private or internal**." Plans: Pro,
  Pro+, Max, Business, Enterprise. Write access needed to create.
- Governance facts worth a slide: automations "are not committed to Git, so
  they are not versioned alongside your code or managed through pull
  requests"; "private to the user who created it. Other people, including
  repository administrators, can't see your automations", but the sessions are
  visible; PRs are "attributed to the user who created the automation ... they
  can't approve those pull requests"; events from users without write access
  are ignored by default; billing goes to the creator.
- Release status: the docs and the 2026-06-02 launch changelog carry no
  preview label. Not stated.
- For a recurring ONBOARDING.md refresh this works: schedule weekly, prompt =
  the skill steps, tools = push + create PR. The skill in §3 is inherited
  ("Agent skills" are listed under "Configuration inherited from the
  repository").

### 6b. GitHub Agentic Workflows (gh-aw) [P]

- Status: "GitHub Agentic Workflows are in public preview and subject to
  change." Unchanged since round 2.
- Files: "a markdown file in `.github/workflows/`", compiled with
  `gh aw compile` to a `.lock.yml`; commit both.
- Engine: "`copilot` is the default; `claude`, `codex`, and `gemini` are also
  supported". Copilot engine in an org repo: put `copilot-requests: write`
  under `permissions` to bill the org via `GITHUB_TOKEN`.
- Security model (verbatim): "**Read-only by default**: Workflows have
  read-only repository permissions unless you explicitly grant more." "**Safe
  outputs**: Write operations (such as creating issues, adding comments, or
  opening pull requests) are only allowed through validated `safe-outputs`
  declared in the frontmatter." "**Threat detection**: Proposed outputs are
  scanned for suspicious or unsafe changes before write actions are applied."
  `max-ai-credits` default cap "1,000 AIC per run".
- `create-pull-request` safe output (gh-aw reference): `draft` "default: true"
  and "`draft` is a **policy**, not a default, so the agent cannot override it
  at runtime." `allowed-files` "acts as an **exclusive allowlist**: every file
  touched by the patch must match at least one pattern". Example in docs:
  `allowed-files: - .github/aw/instructions.md  # only this one file may be
  modified`. **This is the one-file write restriction that VS Code agents
  lack.**
- Protected files are refused or flagged by default (`protected-files`
  default `request-review`: "Create the pull request and submit a
  `REQUEST_CHANGES` review listing the protected files"). Includes `AGENTS.md`
  (Copilot engine), `.github/`, any top-level dot folder, dependency manifests.
- **Internal inconsistency on the gh-aw page:** the summary says protected
  files include "common top-level documentation such as `README.md`,
  `CONTRIBUTING.md`, `SECURITY.md`, and `CODE_OF_CONDUCT.md`"; the detailed
  "Protected Files" table later on the same page lists four categories without
  README. Whether a root `ONBOARDING.md` is protected is not stated. Under the
  default policy the PR still opens, with a change-request review.
- Schedule: fuzzy schedules "(recommended)"; "Use `on: daily` as shorthand,
  which automatically expands to include both schedule and
  `workflow_dispatch`". `weekly on monday` is a documented pattern.
- Tools: `edit:` "Allows file editing in the GitHub Actions workspace";
  `bash:` with a list restricts commands, "Use wildcards like `git:*`".
- Verbatim docs example (weekly issue report) is in track1-other-surfaces.md.
- gh-aw can also start the cloud agent: safe outputs `create-agent-session`
  and `assign-to-agent` ("Both safe outputs require a fine-grained PAT").

Minimal workflow for the doc refresh (assembled from documented fields;
compile-test before showing):

```markdown
---
on: weekly on monday

permissions:
  contents: read
  copilot-requests: write

network: defaults

tools:
  edit:
  bash: ["git:*"]

safe-outputs:
  create-pull-request:
    title-prefix: "[onboarding] "
    labels: [documentation]
    allowed-files:
      - ONBOARDING.md
---

# Refresh ONBOARDING.md

Review commits merged in the last 7 days. Update ONBOARDING.md so new joiners
get correct prerequisites, setup commands and environment variables. Change
only ONBOARDING.md. If nothing relevant changed, make no changes.
```

Single-line `on: weekly on monday` is the form used in GitHub's own docs
example; whether it also adds `workflow_dispatch` like `on: daily` is not
stated. The PR opens as a draft by default.

### 6c. Other schedulers (for completeness) [P]

- VS Code automations (Agents window, `chat.automations.enabled`, "off by
  default on Stable"): run on your machine; "Keep the machine that runs the
  automation awake". Export as `.automation.md`, which "doesn't include the
  workspace, provider, model, permissions".
- Copilot CLI `/every` and `/after`: experimental, "the schedules fire only
  while the session in which they were created is running."

---

## D. Instructions

### 7. What to put in repository instructions [P]

- VS Code, `copilot-instructions.md` "for: Coding style and naming
  conventions ... Technology stack declarations and preferred libraries ...
  Architectural patterns to follow or avoid ... Security requirements and error
  handling approaches ... Documentation standards."
- VS Code guide, review checklist: "**Architecture** ... **Commands**: include
  the correct build, test, lint, and formatting commands ... **Technology
  choices** ... **Conventions** ... **Definition of done**: state which
  validations the agent should run before completing a task." Tip: "Project
  instructions are most useful when they document decisions the agent cannot
  reliably infer from the code alone. Avoid generic advice".
- VS Code writing tips: "Keep your instructions short and self-contained",
  "Include the reasoning behind rules", "Show preferred and avoided patterns
  with concrete code examples", "Focus on non-obvious rules. Skip conventions
  that standard linters or formatters already enforce."
- VS Code official example file (verbatim):

```markdown
# Project instructions

## Architecture

* Add HTTP handlers under `src/api/routes`.
* Keep database access in `src/repositories` so handlers remain independently testable.

## Validation

* Run `npm test -- <changed-package>` after changing application code.
* Add or update tests for every behavior change.
```

- GitHub "Writing effective custom instructions": "short, self-contained
  statements"; "Because the instructions are sent with every chat message, they
  should be broadly applicable"; start with project overview, coding standards,
  and tools/libraries with versions. Its example has sections "Project
  Overview", "Libraries and Frameworks", "Coding Standards", "UI guidelines".
  It warns these "may not have the intended results": references to external
  style guides, forced answer style, length limits.
- Length: the only number is inside GitHub's "onboard this repository" prompt:
  "Instructions must be no longer than 2 pages." and "Instructions must not be
  task specific." It is guidance to the generating agent, not a product limit.
  No hard size limit found for repo instructions. (Custom agent bodies: 30,000
  characters.)
- More official examples: docs.github.com/en/copilot/tutorials/customization-library/custom-instructions.

### 8. AGENTS.md vs .github/copilot-instructions.md [P]

Documented guidance on which to use (GitHub, code-review concept page, table
"Choosing between custom instructions, AGENTS.md, and skills"): "Use
`.github/copilot-instructions.md` for repository-wide rules specific to
Copilot, use path-specific `*.instructions.md` files ... for rules that apply
only to certain files or directories, use `AGENTS.md` for standing rules you
want to share across AI tools and agents, and use skills for task-specific
workflows". Rules column: copilot-instructions "Copilot, always know this for
this repository"; AGENTS.md "Any agent, always know this".

VS Code: "`AGENTS.md` is not specific to Codex. It is a cross-agent format".
Use it when "You work with multiple compatible AI coding agents and want to
share one set of instructions" or want "subfolder-level instructions". "If
your team uses multiple harnesses, use a shared format that they all support
when possible."

agents.md site: "A simple, open format for guiding coding agents"; "README.md
files are for humans"; nested: "Agents automatically read the nearest file in
the directory tree, so the closest one takes precedence"; "Popular choices:"
followed by a list: "Project overview", "Build and test commands", "Code style
guidelines", "Testing instructions", "Security considerations"; "stewarded by the Agentic AI
Foundation under the Linux Foundation." Copilot is in its supporter list.

Which surface reads which:

| Surface | copilot-instructions.md | AGENTS.md | CLAUDE.md / GEMINI.md | Source |
|---|---|---|---|---|
| VS Code, Copilot target | yes ("or `AGENTS.md`") | yes | not listed | VS Code custom-instructions |
| VS Code, Local | yes (`github.copilot.chat.codeGeneration.useInstructionFiles`) | yes (`chat.useAgentsMdFile`) | CLAUDE.md yes (`chat.useClaudeMdFile`) | same |
| VS Code, Claude target | no | no | CLAUDE.md, `.claude/rules` | same |
| Cloud agent | yes | yes, nearest wins | both | GitHub support matrix |
| Code review (github.com) | yes | yes | matrix: AGENTS.md only; reusable: also CLAUDE.md, GEMINI.md, REVIEW.md | see flag below |
| Copilot CLI | yes | yes | both, plus `.claude/CLAUDE.md` | CLI how-to |
| JetBrains Chat | yes | not in matrix | not in matrix | GitHub support matrix |

- Nested AGENTS.md: GitHub "the nearest `AGENTS.md` file in the directory tree
  will take precedence". VS Code Local: nested files off by default
  (`chat.useNestedAgentsMdFiles`); "For Agent Host sessions, follow the
  selected harness's working-folder and nested-instruction rules." CLI:
  discovered in "the repository root, the current working directory,
  intermediate directories between them, and any directories nested in the
  path of a file it is working on".
- **Flag 1:** GitHub's code-review table says AGENTS.md is "read from
  repository root", while its other pages say nearest-in-tree.
- **Flag 2 (still open from round 2):** the code-review reusable says "Copilot
  code review also reads custom instructions from `CLAUDE.md`, `GEMINI.md`,
  and `REVIEW.md` files", but the support matrix still lists "AGENTS.md" only.
- **Flag 3:** the GitHub IDE how-to links VS Code nested AGENTS.md to the old
  `/docs/copilot/customization/...` URL.

### 9. Personal instructions [P]

- VS Code Copilot target: "For personal, always-on instructions in Copilot
  Agent Host sessions, use `~/.copilot/copilot-instructions.md`." Personal
  targeted files: `~/.copilot/instructions` ("Agent Host user, Copilot
  format"). Claude target: `~/.claude/rules`, `~/.claude/CLAUDE.md`.
- VS Code Local: user instructions live in "VS Code profile storage" and "can
  roam through Settings Sync". Agent Host folders "do not roam through Settings
  Sync". Migration: "Migrate User Data Customizations"
  (`chat.customizations.userDataMigration.enabled`, default `false`).
- In the editor: Agent Customizations editor, **Instructions**, "From the
  **New** dropdown, select a workspace or user instruction." Scope
  definition: "User customizations are specific to you and are not committed
  to the project."
- Copilot CLI: `$HOME/.copilot/copilot-instructions.md` and
  `$HOME/.copilot/instructions/**/*.instructions.md` (moves with `COPILOT_HOME`).
- github.com: personal instructions in Copilot Chat ("click your profile
  picture. Then click **Personal instructions**"); they apply "to every
  conversation you have on the GitHub website". The support matrix lists
  personal instructions for github.com Chat and JetBrains Chat only, not for
  the cloud agent or code review.
- JetBrains: "a locally stored `global-copilot-instructions.md` file" at
  `~/.config/github-copilot/intellij/` (macOS) or
  `C:\Users\YOUR-USERNAME\AppData\Local\github-copilot\intellij\` (Windows).
- **Git-ignored personal file inside the repo** (for example
  `.github/instructions/me.instructions.md` plus `.gitignore`): whether VS Code
  loads git-ignored instruction files is **not found** in any doc. The only
  documented local-only repo file is `CLAUDE.local.md` ("for local-only
  instructions (not committed to version control)"), Local agent only. Related
  documented fact: worktree sessions omit ignored files ("Git-ignored files,
  such as `.env` files and installed dependencies, are also absent by
  default"), so such a file would be missing in worktree sessions unless
  copied with `git.worktreeIncludeFiles`. It would also never reach the cloud
  agent or code review, which work from the pushed repository (inference).
  Recommend the user-level folders above instead.
- Precedence: VS Code "Applicable instruction sources are additive. Do not
  depend on a file order or precedence rule to resolve conflicts because
  discovery and merge behavior can differ by harness." Copilot CLI: "does not
  define a general precedence order between these files. Avoid conflicting
  instructions." GitHub.com: "Personal instructions take the highest priority.
  Repository instructions come next, and then organization instructions are
  prioritized last. However, all sets of relevant instructions are provided to
  Copilot." **Disagreement:** GitHub.com publishes an order, VS Code and the
  CLI say there is none.

### 10. `*.instructions.md` frontmatter [P]

- VS Code (all optional): `name` ("Display name shown in the UI. Defaults to
  the file name."), `description` ("Describes the tasks for which the file is
  relevant. Include it for on-demand discovery."), `applyTo` ("Glob pattern
  that automatically applies the instructions to matching files, relative to
  the workspace root. Use `**` to match all files."). "If you omit both
  `description` and `applyTo`, attach the file manually".
- VS Code does **not** document `excludeAgent`. That field is GitHub-only:
  "add the `excludeAgent` keyword ... Use either `"code-review"` or
  `"cloud-agent"`."
- GitHub `applyTo` takes comma-separated globs in one string:
  `applyTo: "**/*.ts,**/*.tsx"`.
- Claude rules (`.claude/rules`) use `paths` (array) instead of `applyTo`,
  "defaults to `**` when omitted".
- Locations: `.github/instructions` (searched recursively) and
  `~/.copilot/instructions` for the Copilot target.
  `chat.instructionsFilesLocations` "is deprecated and only used by the Local
  agent".
