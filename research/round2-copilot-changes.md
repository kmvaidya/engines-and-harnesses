---
url: https://github.blog/changelog/2026-09-04-github-copilot-weekly-releases-august-31, https://github.blog/changelog/2026-09-02-content-exclusions-generally-available-in-copilot-app-and-cli, https://docs.github.com/en/copilot/concepts/context/content-exclusion, https://github.blog/changelog/2026-09-23-local-sandboxing-in-the-github-copilot-app, https://docs.github.com/en/copilot/how-tos/github-copilot-app/configure-local-sandboxing, https://docs.github.com/en/copilot/how-tos/use-copilot-agents/cloud-agent/customize-the-agent-firewall, https://docs.github.com/en/copilot/reference/ai-models/supported-models, https://docs.github.com/en/admin/data-residency/github-copilot-with-data-residency, https://ecorpit.com/github-copilot-september-2026-model-deprecations-migration-map/, https://github.blog/changelog/2026-07-31-upcoming-august-2026-model-deprecations-in-github-copilot, https://github.blog/changelog/2026-07-31-enterprise-teams-model-policy-targeting-in-public-preview/, https://github.blog/changelog/2026-07-29-default-model-enablement-for-copilot-business-and-enterprise/, https://github.blog/news-insights/company-news/github-copilot-is-moving-to-usage-based-billing/, https://docs.github.com/en/copilot/reference/copilot-billing/request-based-billing-legacy/model-multipliers-for-annual-plans, https://github.blog/changelog/2026-04-13-copilot-data-residency-in-us-eu-and-fedramp-compliance-now-available/, https://code.visualstudio.com/updates/v1_136, https://github.blog/changelog/2026-09-03-upcoming-deprecation-of-selected-github-copilot-models, https://github.blog/changelog/2026-09-18-upcoming-deprecation-of-selected-github-copilot-models-in-mid-october, https://github.blog/changelog/2026-08-24-copilot-harness-generally-available-in-copilot-for-jetbrains, https://github.blog/changelog/2026-09-09-enterprise-managed-permissions-for-github-copilot-agent-operations, https://github.blog/changelog/2026-08-12-agent-plugins-1-0-in-vs-code-copilot-cli-and-the-copilot-app, https://github.blog/changelog/2026-09-22-new-features-and-improvements-in-copilot-for-jetbrains, https://github.blog/changelog/2026-09-25-agentic-autofix-now-uses-copilot-memory, https://github.blog/changelog/2026-09-17-agentic-cli-customizations-now-in-the-usage-metrics-api, https://code.visualstudio.com/docs/agent-customization/custom-instructions, https://code.visualstudio.com/docs/agent-customization/prompt-files, https://code.visualstudio.com/docs/agent-customization/custom-agents, https://code.visualstudio.com/docs/agent-customization/hooks, https://code.visualstudio.com/docs/enterprise/manage-ai-settings, https://docs.github.com/en/copilot/reference/custom-instructions-support, https://docs.github.com/en/copilot/how-tos/use-copilot-agents/request-a-code-review/use-code-review, https://docs.github.com/en/copilot/reference/custom-agents-configuration, https://docs.github.com/en/copilot/reference/hooks-reference, https://docs.github.com/en/copilot/concepts/agents/about-agent-skills, https://docs.github.com/en/copilot/concepts/agents/copilot-memory, https://docs.github.com/en/enterprise-cloud@latest/copilot/reference/enterprise-administrators/enterprise-managed-settings, https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference, https://github.com/github/copilot-cli/releases, https://github.com/github/copilot-sdk/blob/main/CHANGELOG.md
fetched: 2026-09-30
---

# GitHub Copilot: what changed between Aug 12 and Sep 30, 2026

Round 2 delta file. Read it alongside the Track 1 files, which stay as the
Aug 12 record. Confidence tags (same scheme in every round-2 file):

- **[V]** passed a 3-agent adversarial check (2 of 3 refutes needed to kill)
- **[S]** spot-checked by hand against the live page on 2026-09-30
- **[P]** confirmed against the primary source on 2026-09-30
- **[E]** extracted with a quote from the named source, not cross-checked
- **[R]** refuted; do not use

**Coverage:** the first round-2 run returned nothing for custom
instructions, AGENTS.md, prompt files, custom agents, Agent Skills, hooks,
Copilot Memory, or the Copilot CLI/SDK. A follow-up pass on 2026-09-30
checked all of them against docs, changelogs and release notes: see §9 and
§10. Where §9 or §10 marks a round-1 statement [R], the `track1-*` file is
out of date on that point.

## 1. Content exclusions now reach the Copilot app and CLI [V]

- Week of Aug 31, 2026, GA for Business and Enterprise: "Copilot app and CLI
  now honor content exclusions, keeping sensitive code out of context across
  agentic workflows." (changelog 2026-09-02 and weekly release 2026-09-04)
- Gaps that remain, per the content-exclusion docs:
  - VS Code **Edit and Agent modes are still listed as unsupported**.
  - Exclusions do not apply to symlinks or to repos on remote filesystems.
  - The IDE may still pass indirect semantic information from excluded files.
- Round 1 (`track1-context.md`) only said exclusions filter indexed data before
  Chat. The agentic-surface coverage is new.

## 2. Local sandboxing in the Copilot app (public preview, Sep 23) [V]

- Limits what the agent can touch on the developer's machine: "helps reduce
  the potential impact of unintended commands by limiting access to files,
  network resources, and credentials on your machine ... Currently in public
  preview and subject to change."
- Policy is per project, in three areas:
  - **Filesystem:** extra read/write folders, read-only folders, denied folders.
  - **Network:** outbound internet and local network policies.
  - **Credentials:** Git HTTPS credentials and GitHub CLI authentication.
- Built on Microsoft MXC for macOS, Linux and Windows.
- **Off by default.** Turn it on per project ("Sandbox new sessions") or per
  session (`/sandbox on`).
- **Fails closed:** "If the operating system cannot enforce the policy, the
  sandboxed shell fails with an error."
- Does not cover cloud sandbox or remote-host sessions. The Copilot app and
  Copilot CLI sandbox settings are configured separately. Enterprise-managed
  settings can make the policy stricter.
- Round 1 (`track1-other-surfaces.md` §7) only saw "cloud and local sandboxes"
  as docs-nav entries. This is the first concrete, configurable version.

## 3. Cloud agent firewall: what it does not cover [V]

Not new, but round 1 (`track1-coding-agent.md`) did not record the limits.

- On by default, with a recommended allowlist also on by default (OS package
  repos, container registries, language package registries, CAs, Playwright
  hosts). Blocked requests appear as a warning in the PR body or a PR comment.
- "The firewall only applies to processes started by the agent via its Bash
  tool. It does not apply directly to Model Context Protocol (MCP) server
  processes or processes started in configured Copilot setup steps."
- "Sophisticated attacks may bypass the firewall ... should not be considered
  a comprehensive security solution." It only works inside the GitHub Actions
  appliance environment.
- [P] Configurable at org and repo level: "Organization-level and
  repository-level rules are combined." "By default, repository
  administrators can add their own entries to the firewall allowlist." A
  domain entry allows all subdomains (`packages.contoso.corp` admits
  `prod.packages.contoso.corp`); a URL entry allows only that scheme, host and
  path prefix. "Copilot code review also supports firewall configuration, at
  both the organization and repository level", set separately from the cloud
  agent's.
- **Implication for a bank:** MCP servers attached to the cloud agent need
  their own egress controls and trust review. The firewall does not cover them,
  and no primary GitHub source describes an egress control for MCP server
  processes on the cloud agent. What does exist is in
  `round2-agent-security-governance.md` §4.

## 4. Models: retirements and additions

**Retired Sep 1, 2026** [P]. GitHub changelog "Upcoming August 2026 model
deprecations in GitHub Copilot" (github.blog/changelog/2026-07-31-upcoming-august-2026-model-deprecations-in-github-copilot,
Jul 31, 2026; the title says August, the date given is "September 1st,
2026"). Scope: "all GitHub Copilot experiences (including Copilot Chat,
inline edits, ask and agent modes, and code completions)". Suggested
replacements: Gemini 3.1 Pro → Gemini 3.6 Flash; Opus 4.5 and 4.6 → Opus
4.7, 4.8 or 5; Sonnet 4.5 and 4.6 → Sonnet 5; Raptor Mini → MAI-Code-1-Flash.
The live supported-models page on 2026-09-30 [S] confirms five are gone:

| Model | Listed on Sep 30? |
|---|---|
| Gemini 3.1 Pro | No |
| Claude Opus 4.5 | No |
| Claude Opus 4.6 | No |
| Claude Sonnet 4.5 | No |
| Raptor mini | No |
| Claude Sonnet 4.6 | **Still listed**: "Claude Sonnet 4.6 will remain available to individual GitHub Copilot subscribers on annual plans so they retain a Sonnet offering." |

The docs page shows no retirement dates; the Sep 1 date comes from the
changelog.

**Two more rounds of retirements are already announced** [P]. Both apply
"across all GitHub Copilot experiences (including Copilot Chat, inline edits,
ask and agent modes, and code completions)".

| Retires | Model | Suggested replacement | Source |
|---|---|---|---|
| Oct 2, 2026 | Claude Opus 4.7 | Claude Opus 5 | github.blog/changelog/2026-09-03-upcoming-deprecation-of-selected-github-copilot-models |
| Oct 2, 2026 | Gemini 3.5 Flash, Gemini 3.6 Flash | Gemini 3.8 Flash | same |
| Oct 2, 2026 | Kimi K2.7 Code | Kimi K3 | same |
| Oct 19, 2026 | GPT-5.5, GPT-5.4 | GPT-5.6 Sol | github.blog/changelog/2026-09-18-upcoming-deprecation-of-selected-github-copilot-models-in-mid-october |
| Oct 19, 2026 | GPT-5.4 mini, GPT-5 mini | GPT-5.6 Luna | same |
| Oct 19, 2026 | Gemini 3.7 Flash | Gemini 3.8 Flash | same |
| Oct 19, 2026 | Grok 4.5 | Grok 4.6 | same |

For Oct 19: "Under default model enablement, the suggested alternatives are
automatically enabled for Copilot Enterprise and Copilot Business customers
unless an administrator has turned off the global default or explicitly
disabled the model."

**Impact on data residency (§6):** Opus 4.7, Gemini 3.5 Flash, GPT-5 mini,
GPT-5.4, GPT-5.4 mini and GPT-5.5 are on the EU compliant list today; Gemini
3.5 Flash's replacement (3.8 Flash) is on neither list. Unless GitHub adds the
replacements to the compliant lists, a residency-enforcing EU enterprise loses
six models by Oct 19 and keeps no Gemini model. The Opus 4.7 retirement also
changes §5's multiplier example.

**Current list (supported-models page, 2026-09-30)** [S], all shown as GA:

- **OpenAI:** GPT-5 mini, GPT-5.3-Codex, GPT-5.4, GPT-5.4 mini, GPT-5.4 nano,
  GPT-5.5, GPT-5.6 Luna/Sol/Terra, **GPT-6 Astra, GPT-6 Luna/Sol, GPT-6.1 Sol**
- **Anthropic:** Claude Fable 5, **Fable 5.1**, Haiku 4.5, Opus 4.7, Opus 4.8,
  Opus 4.8 (fast mode, preview), Opus 5, **Opus 5.5**, Sonnet 4.6, Sonnet 5,
  **Sonnet 5.5**
- **Google:** Gemini 3.5 Flash, 3.6 Flash, **3.7 Flash, 3.8 Flash**
- **Other:** **MAI-Code-1.1-Flash** (Microsoft), Kimi K2.7 Code, Kimi K3,
  Grok 4.5, **4.6, 4.7**

Bold = not in round 1's `track1-models.md` list. The page summary came through
a fetch tool, so treat GA status per model as approximate and check the page
before quoting a specific one on a slide.

- [P] "Claude Fable 5.1 is available to Copilot Pro+, Max, Business, and
  Enterprise users." "Gemini 3.8 Flash is rolling out to Copilot Pro, Pro+,
  Max, Business, and Enterprise users." (weekly release changelog, Sep 4,
  2026, "GitHub Copilot weekly releases — August 31")
- [P] Jul 31, 2026, enterprise-teams model policy targeting, public preview
  (github.blog/changelog/2026-07-31-enterprise-teams-model-policy-targeting-in-public-preview/):
  admins "set a baseline of models for the entire enterprise and then grant
  additional models to specific enterprise teams". Model states are Enabled,
  Disabled and Optional. GitHub frames it as tailoring "by job role or early
  experimentation by frontier teams"; round 2's "restrict expensive models"
  was our inference, not GitHub's wording. Enterprise customers with Copilot
  Business or Enterprise; most got the opt-in on Aug 3.
- [P] Jul 29, 2026, default model enablement for Business and Enterprise
  (github.blog/changelog/2026-07-29-default-model-enablement-for-copilot-business-and-enterprise/):
  generally available models are on by default with a single opt-out policy,
  effective Aug 26. **Relevant to a bank:** "Open-weight models (e.g.,
  DeepSeek, Kimi K2.7) and models not covered by GitHub's data retention
  agreement (e.g., Fable 5) are excluded from default enablement regardless of
  your policy." A related "Global model policy generally available" changelog
  followed on Aug 26.

## 5. Billing [P]

- Primary: "GitHub Copilot is moving to usage-based billing"
  (github.blog/news-insights/company-news/github-copilot-is-moving-to-usage-based-billing/,
  Apr 27, 2026). "Starting June 1, premium request units (PRUs) will be
  replaced by GitHub AI Credits."
- Users who run out **no longer fall back automatically to a cheaper model**:
  "Fallback experiences will no longer be available ... Under the new model,
  usage will instead be governed by available credits." Admins can "set
  budgets at the enterprise, cost center, and user levels". Note: the docs
  page `copilot/concepts/billing/copilot-requests` still carries the legacy
  fallback text; the blog is authoritative for the change.
- On legacy annual plans (Pro and Pro+ "staying on annual plans under
  request-based billing"), premium-request multipliers still apply. Live
  multiplier page (docs.github.com/en/copilot/reference/copilot-billing/request-based-billing-legacy/model-multipliers-for-annual-plans):
  Opus 4.7 27, Opus 4.8 27, Sonnet 4.6 9, GPT-5.5 57, Haiku 4.5 0.33.
  [R] "Opus 4.5 was 15x" can no longer be checked: the live table dropped Opus
  4.5 after retirement and only a search snippet of the old page shows it. Do
  not put the 15x figure on a slide.

## 6. Data residency [S]

Not new, but not covered in round 1.

- Copilot with data residency (GHE.com) is available only in the **United
  States** and **European Union**. When enforced, all Copilot requests go to
  model endpoints in the enterprise's region; code, prompts and responses stay
  in region during inference, and Copilot logs and telemetry are stored in
  region-appropriate storage.
- Enforced by the policy "Restrict Copilot to data residency compliant
  models", **disabled by default**.
- Preview features are not covered until GA: they "will be supported with
  compliant model alternatives at the time of their GA release."
- **10% surcharge** on AI credits for requests under enforcement.
- Compliant models (live page, 2026-09-30):
  - **US (9):** GPT-4o mini, GPT-4o, GPT-4.1, GPT-5.2, GPT-5.3-Codex, Claude
    Haiku 4.5, Claude Sonnet 5, Claude Opus 4.8, Claude Opus 5
  - **EU (19):** GPT-4o mini, GPT-4.1, GPT-5 mini, GPT-5.2, GPT-5.3-Codex,
    GPT-5.4, GPT-5.4 mini, GPT-5.4 nano, GPT-5.5, GPT-5.6 Luna/Sol/Terra, GPT-6
    Astra, Claude Haiku 4.5, Opus 4.7, Opus 4.8, Opus 5, Sonnet 5, Gemini 3.5
    Flash
- Note: Fable 5.x, Opus 5.5 and Sonnet 5.5 are **not** on either compliant
  list. A bank that enforces residency cannot use them.
- [P] "Generally, any Copilot extension or CLI version released in 2025 or
  later includes the necessary policy enforcement capabilities."
- [P] **Agent sessions are covered**, not only chat and completions. The docs
  say "All generally available Copilot features work with this enforcement";
  the Apr 13, 2026 changelog
  (github.blog/changelog/2026-04-13-copilot-data-residency-in-us-eu-and-fedramp-compliance-now-available/)
  lists them: "agent mode, inline suggestions, chat, Copilot cloud agent,
  code review, pull request summaries, and Copilot CLI."

## 7. Other items from the Aug 31 weekly release [P]

Primary: VS Code 1.136 release notes (code.visualstudio.com/updates/v1_136,
Sep 2, 2026).

- **"Agent merge (Preview)"**: "It asks an agent to address review feedback,
  fix failed checks and merge conflicts, and rerun workflows." Setting
  `chat.agentMerge.enabled`. Labelled Preview, not "public preview".
- **"Multi-root workspaces in editor window (Experimental)"**: "Copilot and
  Claude agent sessions in the editor window Chat view support multi-root
  workspaces. This capability is currently scoped to the editor window."
  Round 2's "every folder in a workspace" overstated it; "agent hooks remain
  scoped to a single workspace folder".
- **[P] Copilot harness GA in JetBrains.** The adversarial check first
  refuted this 0-3; the primary source shows it is true.
  "Copilot harness generally available in Copilot for JetBrains"
  (github.blog/changelog/2026-08-24-copilot-harness-generally-available-in-copilot-for-jetbrains,
  Aug 24, 2026): "Copilot harness is now generally available, providing
  faster feature delivery and better code quality." The Aug 31 weekly release
  repeats it. Only the timing in the original claim was off (announced Aug
  24, not the week of Aug 31). The earlier refutation is a reminder that the
  3-agent check can be wrong in both directions.

## 8. Enterprise governance baseline (GA Feb 26, 2026) [V]

Not new since August; recorded here because round 1 only listed it as docs nav.
Full detail is in `round2-agent-security-governance.md` §4.

## 9. Instructions, AGENTS.md, prompt files and custom agents (Aug 12 to Sep 30) [P]

Method: every Copilot changelog entry from Aug 12 to Sep 30 (including six
weekly roundups), VS Code release notes 1.133 to 1.140 (now weekly; 1.140
shipped Sep 30), the live docs, and a diff of the github/docs and
microsoft/vscode-docs sources against their Aug 12 state. **No changelog entry
announces a change to instruction files, AGENTS.md or prompt files. Most
changes below appear only in the docs**, so they are easy to miss.

The main theme: VS Code now runs different "agent harnesses". Its own Local
agent is one; Agent Host sessions run Copilot, Claude or Codex, each with its
own file discovery rules. Much of round 1's VS Code detail now applies to the
Local agent only, and "the Local agent will be removed in a future release".

### 9.1 Repo, personal and org custom instructions

- GitHub docs: no substantive change. Precedence is still personal, then
  path-specific, then repository-wide, then agent instructions, then
  organization, and "all sets of relevant instructions are provided to
  Copilot" (docs.github.com/en/copilot/concepts/prompting/response-customization).
- **VS Code dropped its precedence list** (1.139 docs, Sep 23): "Applicable
  instruction sources are additive. Do not depend on a file order or
  precedence rule to resolve conflicts because discovery and merge behavior
  can differ by harness." For slides: say "avoid conflicting instructions",
  not "personal beats repo beats org".
- **Instruction files depend on the harness**: "Agent Host sessions use the
  discovery rules and file formats of the selected harness." Copilot reads
  `.github/copilot-instructions.md` or `AGENTS.md`; Claude reads `CLAUDE.md`
  and `.claude/rules`; Codex reads `AGENTS.md`; the Local agent reads all
  three (code.visualstudio.com/docs/agent-customization/custom-instructions).
- [R] Round 1 said user instruction files sync through Settings Sync. Now:
  "User instructions in Agent Host folders, such as `~/.copilot/instructions`
  and `~/.claude/rules`, do not roam through Settings Sync."
- Organization-managed custom instructions and org/enterprise skills now work
  in JetBrains (changelog 2026-09-22). The docs support matrix has not caught
  up.
- Copilot CLI personal instructions also accept
  `~/.copilot/instructions/**/*.instructions.md` (already true on Aug 12;
  round 1 missed it).
- **Copilot CLI subagents do not get repo instructions by default.** A custom
  agent spawned as a subagent "doesn't receive repository instruction files
  (`copilot-instructions.md`, `AGENTS.md`, `CLAUDE.md`) by default. Set
  `include-custom-instructions: true` in its frontmatter to opt in." (CLI
  reference, added Sep 21.) A bank that puts policy in `AGENTS.md` should know
  subagents skip it.

### 9.2 Path-specific instructions

- GitHub side: no change. `applyTo` takes comma-separated globs in one
  string; `excludeAgent` accepts `"code-review"` or `"cloud-agent"`; on
  GitHub.com path-specific files still apply only to the cloud agent and code
  review.
- [R] `chat.instructionsFilesLocations` "is deprecated and only used by the
  Local agent" (1.137 docs, Sep 8-9). A "Migrate Location Settings" flow
  exists, off by default.
- Supported folders per harness: Copilot uses `.github/instructions` and
  `~/.copilot/instructions`; Claude uses `.claude/rules` and `~/.claude/rules`.
  Frontmatter unchanged (`name`, `description`, `applyTo`).

### 9.3 AGENTS.md

- Cloud agent: no change. "the nearest `AGENTS.md` file in the directory tree
  will take precedence"; a single root `CLAUDE.md` or `GEMINI.md` is the
  alternative.
- [R] **Code review now reads more files.** Round 1 said "AGENTS.md only".
  Now: "Copilot code review also reads custom instructions from `CLAUDE.md`,
  `GEMINI.md`, and `REVIEW.md` files in your repository, if they exist."
  `REVIEW.md` is documented nowhere else. Added Sep 2, no changelog. The
  support matrix still says AGENTS.md only, so GitHub's own docs disagree.
- **For a bank** (not new): code review reads instructions from the PR's head
  branch, so a PR author can change the review instructions inside their own
  PR (docs.github.com/en/copilot/how-tos/use-copilot-agents/request-a-code-review/use-code-review).
- VS Code nested AGENTS.md is still experimental and off by default
  (`chat.useNestedAgentsMdFiles`).

### 9.4 Prompt files

- [R] **Prompt files are deprecated in VS Code.** "Prompt files are
  deprecated for Agent Host sessions and aren't loaded by Agent Host. They
  continue to work with the Local agent for now, but the Local agent will be
  removed in a future release. Use prompt file migration to convert existing
  prompts to agent skills. This experimental migration is enabled by
  default." (`chat.customizations.promptMigration.enabled` now defaults to
  `true`.) Round 1 called them "being superseded" with migration opt-in.
- Not announced: the 1.137 release notes list "None" under deprecated
  features, and no changelog mentions it. GitHub docs still describe prompt
  files as public preview with no deprecation note.
- Frontmatter unchanged. Prompt bodies can now reference `#file:` and `~/`
  paths (Sep 17).

### 9.5 Custom agents (.agent.md)

- **The VS Code docs example still names retired models**:
  `model: ['Claude Opus 4.5', 'GPT-5.2']`, and `handoffs.model` gives
  `Claude Sonnet 4.5 (copilot)`. Do not copy them onto a slide. GitHub's own
  reference has no model example and documents `model` as a single string.
- Frontmatter fields unchanged. Agent-scoped `hooks` now "only run in the
  Local harness when this agent is active" (Sep 21).
- [R] `chat.agentFilesLocations` and `chat.modeFilesLocations` "are
  deprecated and only used by the Local agent".
- [R] `/create-agent` and similar shortcuts "aren't available in Agent Host
  sessions, such as Copilot". The eye-icon hide control is gone; use
  `user-invocable: false`.
- User-level agents can also live in `~/.claude/agents`.
- Cloud agent ignores `argument-hint` and `handoffs`: they "are currently not
  supported for Copilot cloud agent on GitHub.com. They are ignored to ensure
  compatibility." (Not new; round 1 missed it.)
- Org and enterprise agents now appear in Visual Studio (changelog Aug 28)
  and the Copilot app (docs, Sep 4). Org agents live in the org's `.github`
  or `.github-private` repo; enterprise agents in a designated
  `.github-private` repo (round 1 named only `.github-private`).
- **Copilot CLI-only fields:** `models` (priority list), `modelPolicy`
  (`"required"` makes the agent refuse to run rather than substitute another
  model; default `"preferred"`), `reasoningEffort`. For a bank pinning a
  residency-compliant model, `modelPolicy: "required"` is the relevant knob.
- CLI precedence corrected Sep 30: "If personal and repository custom agents
  have the same ID, the personal agent is used." Org and enterprise agents
  rank lowest. IDs come from the file path (`agents/team/reviewer.agent.md`
  becomes `team--reviewer`).
- Docs lag: the CLI built-in agents still list `claude-sonnet-4.6` as default
  for `code-review`, `general-purpose` and `security-review`.
- Governance: the usage metrics API now reports CLI "Skills, Custom agents,
  Model Context Protocol (MCP) servers, Slash commands, Plugins" per user and
  in aggregate (changelog 2026-09-17).
- Unconfirmed: VS Code 1.136 release notes credit a PR "Support reasoning
  effort in custom agent files"; the VS Code docs do not list the field yet.

### 9.6 Link changes

On Sep 30 GitHub moved the IDE how-to pages under
`/copilot/how-tos/copilot-in-your-ide/...` (e.g. custom instructions:
`.../customize-copilot/configure-custom-instructions/add-repository-instructions-in-your-ide`;
custom agents: `.../use-copilot-agents/use-custom-agents`). Re-check slide
links.

## 10. Skills, hooks, Memory, CLI and SDK (Aug 12 to Sep 30) [P]

Checked against GitHub docs, every changelog entry Aug 12 to Sep 30, VS Code
release notes 1.134 to 1.140, and the github/copilot-cli (v1.0.80 to v1.0.90),
github/copilot-sdk and github/gh-aw releases. Items marked "not in round 1;
could not date" are on the live page but no changelog dates them, so do not
read them as changes after Aug 12.

### 10.1 Enterprise-managed permissions (GA Sep 9): the biggest change

- "Enterprise managed permissions for GitHub Copilot agent operations"
  (github.blog/changelog/2026-09-09-enterprise-managed-permissions-for-github-copilot-agent-operations).
  Admins "centrally control which agent operations are blocked, require human
  approval, or can proceed without a prompt" for shell commands, file reads
  and edits, and network domains. "Managed restrictions can't be weakened by
  user or workspace settings, auto-approval, or previously saved approvals."
  Applies to the Copilot app, the CLI and VS Code Agent Host sessions.
- Rules: deny > ask > allow. "The effective allowlist is the intersection of
  all sources that declare one, not the union." "A managed `ask` rule can't
  be satisfied by bypass mode (also known as allow-all or YOLO mode), an
  auto-approval setting, a hook or other approval shortcut, or a grant
  persisted from an earlier approval." Selectors: `Shell(...)`, `Read(...)`,
  `Edit(...)`, `Domain(...)`.
- **Not on the cloud agent or JetBrains** (JetBrains supports only
  `disableBypassPermissionsMode`).
- Sep 25: an in-product validator checks `copilot/managed-settings.json` and
  `copilot/team-mappings.json` in `.github-private`.
- JetBrains got managed plugins, MCP allow/deny, OpenTelemetry and
  `disableBypassPermissionsMode` (Aug 18), and managed sandbox policies in
  public preview (Sep 8). The docs key table still says sandbox is not
  supported in JetBrains.

### 10.2 Agent Skills

- Core format, locations and surfaces: no change (`.github/skills`,
  `.claude/skills`, `.agents/skills`; `~/.copilot/skills`, `~/.agents/skills`).
- Org and enterprise skills now work in JetBrains (changelog Sep 22). No docs
  page explains where org skills live; treat as JetBrains-only and
  undocumented.
- `allowed-tools` and `license` frontmatter are documented for cloud agent and
  CLI skills (not in round 1; could not date). Warning: "Pre-approving `shell`
  or `bash` removes the confirmation step for running terminal commands and
  can allow attacker-controlled skills or prompt injections to execute
  arbitrary commands in your environment."
- `gh skill` (public preview, GitHub CLI 2.90.0+): `search`, `preview`,
  `install` (with `@TAG`/`@SHA` and `--pin`), `update`, `publish`. Provenance
  "is written into the skill's `SKILL.md` frontmatter, including the source
  repository, ref, and tree SHA." "Skills are not verified by GitHub and may
  contain prompt injections, hidden instructions, or malicious scripts."
- Code review uses a skill reliably if it has "a review-focused skill
  directory name such as `code-review`."
- VS Code `name` rule tightened: "Do not use slashes, colons, dots, or
  namespace prefixes. Must match the parent directory name. Maximum 64
  characters."
- CLI: new `copilot skill add|list|remove|enable|disable`; `copilot plugins
  install --skill` replaced in v1.0.85 (Sep 16).
- Usage metrics API reports skills, plugins, custom agents, MCP and slash
  commands (Sep 17), but "customer-defined names are not shown", so it is not
  a skill audit trail.

### 10.3 Hooks

- Event list unchanged: 14 events. Cloud agent subset unchanged: 12 fire (not
  `notification` or `permissionRequest`), `"ask"` is treated as `"deny"`,
  only `.github/hooks/*.json` is read
  (docs.github.com/en/copilot/reference/hooks-reference).
- Decision fields and exit codes unchanged. **Now spelled out: timeouts fail
  open**, "for every event, including `preToolUse` and admin-deployed policy
  hooks." HTTP `preToolUse` hooks also fail open on "a network error,
  timeout, or non-2xx response". A slow policy hook lets the call through.
  Pair hooks with managed deny rules (§10.1).
- Policy hooks can come from the Windows Registry
  (`HKLM\Software\Policies\GitHub\Copilot`); POSIX policy files "must be
  owned by root and must not be group- or world-writable"; they run
  "regardless of folder trust state"; "Policy hooks are not supported under
  Copilot cloud agent." (Not in round 1; could not date.)
- Also on the live page (could not date): `exec` + `args` hooks without a
  shell; HTTP hooks must use `https://` for permission events; a hook `allow`
  cannot pre-approve leaving the sandbox, "Only `deny` still propagates";
  "After 8 consecutive `block` continuations, the CLI overrides the hook and
  ends the turn anyway"; PascalCase `PreToolUse` hooks use Claude Code matcher
  semantics.
- CLI releases: v1.0.81 (Aug 27) passes OpenTelemetry trace context to hooks.
  **v1.0.85 (Sep 16) security fix:** "The `allowManagedHooksOnly` policy now
  also blocks extension-registered `preToolUse`, `postToolUse` and
  `postToolUseFailure` callbacks, which previously bypassed the managed-only
  lockdown".
- VS Code: `allowManagedHooksOnly` and `strictPluginOnlyCustomization` are
  managed settings (since 1.132). `allowManagedHooksOnly` is missing from
  GitHub's own managed-settings key table.
- [R] Round 1 treated VS Code hooks as one Preview feature. Now: "The VS Code
  hooks experience is in Preview. Individual provider implementations might
  have a different lifecycle status. For example, hooks in the Copilot SDK
  are generally available." The Local harness fires only 8 events and
  "ignores matcher values".
- [R] Round 1 said VS Code "additionally" reads `.claude/settings.json`. The
  CLI reads it too: "Cross-tool `.claude/settings.json` and
  `.claude/settings.local.json` files in the repository are also read."
- The hooks concept page is stale (8 events, no policy hooks). Use the
  reference page.

### 10.4 Copilot Memory

- Still public preview. 28-day expiry, but "The 28-day timer may reset
  whenever Copilot successfully validates and uses an entry."
- [R] Round 1 listed cloud agent, code review and CLI. Now also **agentic
  autofix**, which "stores the fix pattern as a memory for future use" (Sep
  25). JetBrains support was announced Aug 13; the concept page does not list
  it yet.
- Governance (could not date): repository facts are created only "in
  response to actions by users with write access"; "Preferences are owned by
  the billing entity"; "Facts can also be captured from pull requests that
  were closed without merging."
- Admin: JSONL export of preferences ("limited to 10 per hour"); audit events
  when an admin exports or deletes memories and when a user opts out.
- **Do not confuse with chat retention:** from no earlier than Sep 28,
  github.com Chat, Mobile Chat and cloud agent "chat data will be retained for
  the life of the account instead of 28 days" (changelog Aug 28).

### 10.5 Copilot Spaces

- No change since Aug 12. Gap (could not date): "the system does not block
  the creation of a space under an organization that has not configured
  Spaces, or has Spaces disabled."

### 10.6 Copilot CLI

- v1.0.79 (Aug 10) to v1.0.90 (Sep 30). A native Rust runtime now sits under
  the TypeScript interface.
- New: `/tasks`, `/rewind`, `--plan` with `--mode autopilot`, `defaultMode`
  and `defaultPermissionMode`, `/config`, `forceLoginOrgs` ("Enterprise admins
  can pin sign-in to approved GitHub organizations"),
  `include-custom-instructions`, Claude Code `.claude/rules` as instructions
  (v1.0.89), HydraFusion multi-model routing (experimental).
- Breaking: v1.0.81 "Removed `/plugins`"; v1.0.85 changed
  `copilot plugins list --json`.
- **Policy fixes a bank should require:** v1.0.81 "forceRemoteSettingsRefresh
  now fails closed"; v1.0.83 enterprise-denied MCP servers "can no longer
  start before the managed allow/deny policy resolves"; v1.0.88 (Sep 22)
  managed settings now apply in ACP mode, AHP hosts and `--server` sessions,
  which "previously ran with no managed MCP, permission, or plugin policy".
  **Minimum version for policy enforcement: v1.0.88.**
- Sandbox still "Only available in experimental mode". Managed `sandbox` key:
  `enabled`, `failIfUnavailable`, `allowBypass: false`. Linux needs
  `slirp4netns`, `nsenter` and iptables tools on PATH (v1.0.83). VS Code 1.135
  (Aug 26) rolled its Local-harness sandbox back to opt-in.

### 10.7 Copilot SDK

- GA, semantic versioning, six languages: "Python, TypeScript, Go, .NET,
  Java, and Rust" (GA came in June, before this window). v1.0.11 to v1.0.16.
- v1.0.13 (Sep 4): `managedSettings` "injects an enterprise permissions
  policy at session startup"; it "is not persisted with the session, so it
  must be re-supplied on resume to remain in effect". Also rotating
  session-scoped GitHub credentials and `sandbox.allowBypass`.
- v1.0.14 (Sep 16): typed message provenance "distinguishing human `user`
  input, internal `system` injections, and identified `agent-` senders, so
  recipients can reliably tell agent input from human authorization".
- VS Code's Agent Host Copilot agent "is powered by the Copilot SDK" (1.134);
  1.140 says the Copilot harness "might already be the default selection".

### 10.8 Plugins

- **Agent Plugins 1.0, GA Aug 12**: "packages agent skills and MCP servers
  into one installable plugin", GA "in VS Code, Copilot CLI, the GitHub
  Copilot SDK, and the GitHub Copilot app, on all Copilot plans". Governed by
  `enabledPlugins`, `extraKnownMarketplaces` and `strictKnownMarketplaces` in
  managed settings; `autoUpdate` for marketplaces (Aug 26).
- CLI v1.0.87: "Empty strictKnownMarketplaces allowlists now hide and block
  built-in plugin marketplaces."
- Docs conflict: the plugins page says the cloud agent installs plugins from
  `.github/copilot/settings.json`; the hooks reference says "Cloud agent does
  not load `settings.json`". Test before relying on plugin hooks in the cloud
  agent.

### 10.9 Agentic Workflows

- No change: public preview; `engine` accepts `copilot` (default), `claude`,
  `codex`, `gemini`. The gh-aw reference also lists `pi` (since June).
  Outputs "are scanned for suspicious or unsafe changes before write actions
  are applied." Billing: "`1 AIC = $0.01 USD`".
