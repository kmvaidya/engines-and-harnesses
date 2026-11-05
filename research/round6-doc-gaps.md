---
fetched: 2026-11-05
purpose: Round 6. Fill items the State of the Harness deck marked "not documented" or "research doesn't say". Each quote read on the live vendor page on 2026-11-05 unless tagged otherwise.
---

# Documentation gaps: what the vendors actually say (checked 2026-11-05)

Method. Each page was downloaded today with curl (or via the GitHub API for repo files and commit dates), its text extracted, and quotes copied from the extracted text. Tags:

- **[P]** read on the live primary page today (vendor docs, changelog, blog, repo, or the vendor's own post).
- **[P\*]** seen only through a summariser or search snippet.
- **[S]** secondary source.
- **[O]** my inference. It is not a quote.

Dates: changelog and blog dates are the publication dates. For docs pages I give the last commit date from the public docs repos (`github/docs`, `microsoft/vscode-docs`) where I could get it. Otherwise "live Nov 5".


---

## Summary table

| # | Item | Status |
|---|---|---|
| 1 | Copilot assisted permissions | **Mostly filled.** Judge model: "Copilot selects", not named. Defaults, admin controls and failure behaviour are documented. **Accuracy and miss rate: still undocumented.** |
| 2 | CLI "semantic code search by default for online sessions" | **Partly filled.** "Online session" is never defined (my inference: not `COPILOT_OFFLINE`). GHES: not available (documented for VS Code; implied for CLI). GHE.com: not stated for the CLI. |
| 3 | Code review Max | **Filled** |
| 4 | Rubber duck | **Filled.** CLI, app, VS Code (Copilot harness, experimental) and cloud agent on github.com. Pairing is "complementary model"; only Claude→GPT-5.4 was ever named. |
| 5 | Dynamic workflows and /fleet | **Filled**, with limits. Two docs disagree on the default subagent depth and concurrency. |
| 6 | Copilot harness system prompt, edit mapping, tool list | **Partly filled.** CLI tool list and system-prompt **section names** are documented. Prompt **text**, and which model gets `edit` vs `apply_patch`, are **still undocumented**. |
| 7 | Copilot local sandbox | **Filled.** Off by default. VS Code uses it in Copilot-harness (Agent Host) sessions. Windows 10 is never named; the docs require Windows 11 25H2/26H1 builds. |
| 8 | Factory Legacy-Bench | **Filled.** The Sep 24 snapshot ran on the Droid harness at default effort (per the Fireworks card). The full set is 100 tasks. The COBOL payroll example details are documented. |
| 9 | Edit formats | **Antigravity filled** (full argument list). **Kiro filled** (operations). **Devin and Amp: tool names only.** **Cursor: hook and stream schemas only.** The model-facing schema is still undocumented for Cursor, Devin and Amp. |
| 10 | AI-approver error rates | **Codex filled** (Apr 30, 2026). **Cursor filled** ("97% accurate", Jun 11, 2026). **Antigravity Auto: still undocumented.** |
| 11 | Why GitHub keeps the runtime closed | **Still undocumented** |

---

## 1. Copilot assisted permissions (GA Oct 26, 2026)

**Plain English.** A language model reviews each eligible permission request: run a command, touch a path, or fetch a URL. If it is confident the request is safe, the request runs without asking you. Otherwise you get the normal prompt. In autopilot or non-interactive runs, an unapproved request is denied instead, and the explanation goes back to the agent.

- **Judge model.** GitHub does not name it. "Copilot selects" the model. It can differ from your chat model and falls back to your session model. With BYOK, the judge is your session model.
- **Inputs.** The docs say only that the judge weighs the request against "the authority you gave for the task". Changelogs say it receives "visible shell code", including some nested `bash -c` and PowerShell. No document gives the full input. For example, it is not stated whether the judge sees the transcript.
- **Default.** Manual approval is the default in VS Code. The CLI docs say: "If neither you nor your administrator has configured a default, new sessions can start in manual or assisted mode." So the CLI default is not fixed. CLI 1.0.104 (Oct 27) removed the experimental flag.
- **Admin controls.**
  - Disable Assisted.
  - Block Allow All while keeping Assisted.
  - Set the default mode.
- **Accuracy.** No accuracy, miss or false-positive rate is published.

**Verbatim quotes**

- "Assisted permissions are now generally available in GitHub Copilot CLI, GitHub Copilot app, and Visual Studio Code. When Copilot requests permission to run a command, access a file system path, or open a URL, a large language model evaluates the request. Requests classified as clearly safe automatically proceed. Other requests require your approval." Also: "you can use enterprise-managed settings to block Allow All while keeping Assisted available or disable Assisted separately. You can also choose the default permission mode for new sessions... If the default is unavailable or prohibited by policy, the session starts with manual approval." From https://github.blog/changelog/2026-10-26-github-copilot-assisted-permissions-generally-available, Oct 26, 2026. **[P]**
- From https://docs.github.com/en/copilot/concepts/customizations/allowing-safe-commands (last commit Oct 27, 2026) **[P]**:
  - "Copilot selects the model used for the safety review, which can differ from the model you selected for your conversation. If the selected review model is unavailable, the review can use your session's active model instead. If you use your own model provider, the review uses your session's active model."
  - "When you enable assisted permissions, existing rules and human approvals are evaluated before a model review. For eligible requests that aren't already resolved—whether to run a command, access a path, or fetch a URL—the model assesses whether the action is safe and within the authority you gave for the task."
  - "In Copilot CLI, enterprise ask rules for shell commands, file reads, file writes, and URLs can be satisfied by model approval when the request is eligible for review. This means those rules do not always result in a prompt for your confirmation. Enterprise deny rules still apply."
  - "Assisted permissions does not review other tool calls that enterprise rules require you to approve, or requests to bypass local sandboxing."
  - "If a safety review is unavailable or cannot evaluate a request, the request follows the session's normal permission handling."
  - "In autopilot mode and non-interactive runs, requests that still require your approval are denied instead. When the safety review requires approval, its explanation is passed back to Copilot so it can try a different approach."
  - "The model can make mistakes and approve dangerous or unintended actions. This feature is not a substitute for sandboxing or access restrictions."
  - "If neither you nor your administrator has configured a default, new sessions can start in manual or assisted mode. Use /permissions show to check."
  - "Tool permission controls are not available for cloud sessions."
  - On `--assisted-approval`: "When successfully enabled, --assisted-approval takes precedence over --allow-all-tools, but it does not change --allow-all-paths or --allow-all-urls." Also: "If assisted permissions can't be turned on... It does not cancel a separate --allow-all-tools option that you supplied, so tool requests may still be approved without a safety review."
  - Admin keys: "permissions.disableBypassPermissionsMode: "disable"" and "permissions.disableAssistedPermissionsMode: true".
- From https://github.com/microsoft/vscode-docs/blob/main/docs/agents/run/approvals.md (last commit Nov 4, 2026) **[P]**:
  - "| **Manual permissions** (default) | Uses your tool, URL, and terminal approval settings..."
  - "| **Assisted permissions** | Uses an LLM judge to assess each tool call. Calls that the judge does not approve require your confirmation. |"
  - "This option isn't available for Local harness sessions."
  - "The model-based risk assessment can make mistakes. The first time you select this level, a warning dialog asks you to confirm."
- VS Code 1.144 release notes (Oct 28, 2026): "the agent performs an LLM-based risk assessment for each tool call and automatically approves low-risk calls. When a call is deemed higher risk or if the risk cannot be determined, the tool call still requires explicit user approval... Assisted permissions require Folder isolation and might be restricted by your organization." From https://code.visualstudio.com/updates/v1_144 **[P]**
- From VS Code `docs/enterprise/manage-ai-settings.md` **[P]**: "`permissions.defaultMode` | Sets the initial permission level. Supported values are `"manual"`, `"assisted"`, and `"allow-all"`." Also: "For Copilot harness sessions, a tool marked `false` removes **Allow all**... It does not require confirmation for each call to that tool, so **Assisted permissions** and saved session approvals can still approve it." The second quote is about `ChatToolsEligibleForAutoApproval`.
- Application card, https://docs.github.com/en/copilot/responsible-use/agents **[P]**: "Model review does not guarantee that an action is safe."
- CLI changelog, https://raw.githubusercontent.com/github/copilot-cli/main/changelog.md **[P]**:
  - 1.0.94 (Oct 8): "Assisted permissions send visible shell code to the permission judge instead of requiring unnecessary manual approval." Also: "Managed policy can disable Assisted Permissions and keep sessions in Manual Approval mode."
  - 1.0.96 (Oct 12): "Timeline now shows whether you, Assisted Permissions, policy, or unattended fallback made each permission decision."
  - 1.0.100 (Oct 19): "Enterprise-managed ask permissions in Assisted mode now allow safe actions without unnecessary confirmation prompts."
  - 1.0.101 (Oct 20): "Add assistedApprovalInstructions setting to guide Assisted Permissions confirmation decisions." Also: "Extension capability requests use explicit approval instead of the Assisted judge."
  - 1.0.104 (Oct 27): "Assisted Permissions are available without enabling experimental mode."

**Conflict for a bank to note.** Two GitHub docs pages read differently on managed ask rules:

- The managed-settings reference says of `disableBypassPermissionsMode`: "Managed deny and ask rules continue to apply." From https://docs.github.com/en/copilot/reference/enterprise-administrators/enterprise-managed-settings **[P]**.
- The assisted-permissions page says ask rules "can be satisfied by model approval".
- VS Code 1.142 (Oct 14) said: "Assisted Permissions is not currently compatible with permissions.{allow,ask,deny}... please set "disableAssistedPermissionsMode": true." 1.143 then says: "Assisted permissions no longer prompt again for eligible managed tool requests they approve."

[O] Under Assisted mode, a managed **ask** rule no longer guarantees that a human sees the prompt. Only **deny** is a hard stop.

**Accuracy: still undocumented.** Places searched:

- the GA changelog
- the docs page above
- the application card (its false-positive text is about code review)
- VS Code docs and 1.142 to 1.145 notes
- the CLI changelog
- web search for evaluation numbers

GCN [S] and a DEV post [S] also say that no rule set and no override rate are published (https://gcn.com/github-copilot-lets-approve-own-terminal/22898/).

---

## 2. CLI v1.0.100 (Oct 19): "Enable semantic code search by default for online sessions"

**Plain English.** The changelog line is real (1.0.100, dated 2026-10-19). No GitHub page defines "online session". The only documented opposite is CLI **offline mode** (`COPILOT_OFFLINE=true`), which stops all contact with GitHub's servers. [O] So "online" most likely means "not in offline mode", that is, signed in and talking to GitHub, where the server-side index lives. That reading is mine, not GitHub's.

- **GHES.** VS Code docs say remote indexing "is not supported for GitHub Enterprise Server". The CLI-on-GHES page (technical preview) does not list semantic search. It says that anything needing GitHub cloud services is unavailable in the GHES offline configuration. [O] So semantic search is not available for GHES repos.
- **GHE.com (data residency).**
  - VS Code says remote indexing works for "GitHub.com or GitHub Enterprise Cloud". GHE.com is not named either way.
  - External ingest (indexing non-GitHub repos) is explicitly "not available on GHE.com or GitHub Enterprise Server".
  - The data-residency page says "All generally available Copilot features work with this enforcement". That page is about model routing, not indexing.
  - No page says whether the CLI's semantic search works for GHE.com repos. **Still undocumented** for the CLI on GHE.com.

**Verbatim quotes**

- Changelog: "## 1.0.100 - 2026-10-19 ... - Enable semantic code search by default for online sessions." From https://raw.githubusercontent.com/github/copilot-cli/main/changelog.md **[P]**
- "Remote indexing works for repositories hosted on GitHub.com or GitHub Enterprise Cloud. It is not supported for GitHub Enterprise Server." Also: "External ingest is available on github.com, but not on GHE.com or GitHub Enterprise Server." From https://code.visualstudio.com/docs/agents/reference/workspace-context.md, live Nov 5. **[P]**
- From https://docs.github.com/en/copilot/concepts/prompting-and-context/repository-indexing **[P]**:
  - "Once an index has been created for a repository, it can be used by: Copilot Chat in GitHub and Visual Studio Code; Copilot cloud agent." The CLI is not listed.
  - "This feature is only available on GitHub.com. It is not available on GHE.com or GitHub Enterprise Server." This refers to semantic indexing for non-GitHub repositories.
- From `content/copilot/copilot-on-ghes/set-up-copilot-cli.md`, github/docs, last commit Oct 28, 2026 **[P]**:
  - "> This feature is in technical preview"
  - "In general, any capability that relies on connectivity to GitHub cloud services is not available in the GitHub Enterprise Server offline configuration."
  - The capability table lists "GitHub MCP server tools ... Not available" and "Web search and web fetch ... Not available". Semantic search is not listed.
- "If you set the `COPILOT_OFFLINE` environment variable to `true`, Copilot CLI runs without contacting GitHub's servers." From `content/copilot/how-tos/copilot-cli/set-up-copilot-cli/authenticate-copilot-cli.md` **[P]**
- "All generally available Copilot features work with this enforcement." From `data/reusables/copilot/model-compliance/supported-features.md` (last commit Sep 15, 2026), included on https://docs.github.com/en/admin/data-residency/github-copilot-with-data-residency **[P]**
- Universe changelog (Oct 28): "Semantic search can also find code by what it does... Copilot can search across repositories in your organization." From https://github.blog/changelog/2026-10-28-github-intelligence-puts-your-code-context-and-history-to-work **[P]**. It gives no host or residency caveats.

**Places searched for "online session":**

- the CLI command reference
- the CLI config reference
- About Copilot CLI
- the full CLI changelog (the phrase appears once)
- github/docs code search for "online session" (no Copilot hit)
- github/docs code search for "semantic code search"

---

## 3. Copilot code review "Max" (public preview, Oct 28, 2026)

**Plain English.** Max is the third review effort level, above Lite and Balanced (Balanced is the default). It runs several independent review agents on models from different providers. An aggregation agent then reconciles their findings into one review. It is slower and costs more: about $10 per review on average, against $1.50 for Balanced and $0.25 for Lite. Admins can cap the highest level allowed. Copilot approvals, which count toward required reviews, went GA on the same day and are off by default.

**Verbatim quotes**

- From https://github.blog/changelog/2026-10-28-copilot-code-review-merge-with-confidence-with-max-and-approvals, Oct 28, 2026 **[P]**:
  - "It joins Lite and Balanced as a third review effort level and runs several independent review agents across models from different providers. Each model has its own strengths and blind spots, so combining them helps catch issues a single model might miss. An aggregation agent then reconciles their findings, resolves disagreements, and double-checks accuracy before combining everything into a single review."
  - "Because Max does more work on each review, it takes longer and uses more AI credits than Lite or Balanced."
  - "Enterprise, organization, and repository admins can optionally set a maximum review effort level to decide where Max is available."
  - "Approvals are off by default."
- From https://docs.github.com/en/copilot/concepts/agent-capabilities/agent-powered-workflows-and-operations/code-review (last commit Nov 5, 2026) **[P]**:
  - "Lite: Standard review. Provides fast, targeted feedback on common issues..."
  - "Balanced: Routes pull requests to a higher-reasoning model for longer analysis... (default)."
  - "Max: The highest-effort review. Uses multiple high-reasoning models for the most intensive review of pull requests that require the most scrutiny."
  - "Max review effort level is currently in public preview and subject to change."
  - "On average, a review costs an estimated $0.25 USD with Lite, $1.50 USD with Balanced, and $10 USD with Max."
  - Range table: "Max $1.50 USD to $25 USD"
  - "GitHub's built-in default, which is Balanced."
  - "Model switching is not supported... Copilot code review may use models that are not enabled on your organization's "Models" settings page."

The last point matters for a bank. [O] Code review, including Max, can use models your org has not enabled in its Models settings.

---

## 4. Copilot "rubber duck" critic

**Plain English.** Rubber duck is a read-only critic agent that runs on a model from a different family to your session model.

**Where it is available:**

- Copilot CLI
- Copilot app
- VS Code, in Copilot-harness sessions only, marked experimental
- the cloud agent on github.com: the how-to lists `/rubber-duck` as a slash command

**When it runs.** It runs only when you ask, unless you turn on proactive invocation (`subagents.agents["rubber-duck"].autoInvoke`, default `false`). The VS Code doc says the harness "might consult Rubber Duck automatically".

**Pairing.** The docs say "complementary model" and give one example: a Claude session may get a GPT critic. The April 6 blog named the only concrete pairing: Claude orchestrator with GPT-5.4 as the duck. CLI 1.0.87 (Sep 21) enabled it "for every model family". No current page lists which model pairs with which. VS Code requires a Claude or GPT main model.

**Verbatim quotes**

- From https://docs.github.com/en/copilot/concepts/agent-capabilities/choosing-and-delegating-agent-work/getting-a-second-opinion, live Nov 5 **[P]**:
  - "Rubber duck is a built-in agent available in GitHub Copilot CLI and the GitHub Copilot app."
  - "it deliberately runs on a different AI model from the one driving your session. Copilot picks a critic model that contrasts with the current session model. For example, if you have chosen to use a Claude model for your session, the rubber duck agent may use a GPT model as the critic. Copilot only uses the rubber duck agent if a suitable model is available."
  - "By default, the rubber duck agent is not automatically invoked."
  - "The rubber duck agent has read-only access to your codebase via the standard exploration tools."
- From VS Code `docs/agents/run/review-code-edits.md` (last commit Nov 4, 2026) **[P]**:
  - "`feature(rubber-duck)`. In a Copilot harness session, Rubber Duck uses a complementary model to review plans, code, and tests..."
  - "The harness might consult Rubber Duck automatically during non-trivial work."
  - "Rubber Duck requires a Claude or GPT model in the main session and an available complementary model."
  - `build/feature-lifecycle.json`: `"rubber-duck": { "label": "Rubber Duck", "state": "experimental" }`
- Cloud agent: "You can also use slash commands in your prompt to perform specific actions, such as `/rubber-duck` to get an second opinion". From `content/copilot/how-tos/use-copilot-agents/cloud-agent/use-cloud-agent-on-github.md`, github/docs, last commit Oct 28, 2026 **[P]**
- From the blog https://github.blog/ai-and-ml/github-copilot/github-copilot-cli-combines-model-families-for-a-second-opinion/, Apr 6, 2026 **[P]**:
  - "When you've selected a Claude model from the model picker to use as your orchestrator, Rubber Duck will be GPT-5.4."
  - "we are enabling Rubber Duck for all Claude family models (Opus, Sonnet, and Haiku)... We are already exploring other model families for the Rubber Duck to pair with GPT-5.4 as the orchestrator."
- CLI changelog **[P]**:
  - 1.0.58 (Jun 2): "Rubber Duck is now enabled by default"
  - 1.0.64 (Jun 23): "a complementary model strategy that picks an opposite-family model"
  - 1.0.87 (Sep 21): "Enable the rubber-duck agent for every model family and for low-cost-tier session models"
  - 1.0.85 (Sep 16): "The `/rubber-duck` command is hidden after a model refresh removes its compatible critic"
- Config reference: "subagents.agents["rubber-duck"].autoInvoke boolean false". From https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-config-dir-reference **[P]**

**Still undocumented:** the current per-family pairing table (which critic for GPT, Gemini or Grok sessions).

---

## 5. Dynamic workflows (public preview, Oct 1, 2026) and /fleet

**Plain English.**

- **/fleet** asks Copilot to split a task across parallel subagents. Copilot decides how to divide the work each time.
- **A dynamic workflow** is a program, held in a Copilot extension, that fixes the steps, the conditions and the handoffs to agents. It can be rerun, paused and resumed.

Availability:

- Dynamic workflows run in the CLI (requires `--experimental` or `/experimental on`), the Copilot app and the SDK. Not VS Code or the cloud agent.
- They are not available to Pro and Pro+ users on legacy annual request-based plans.
- `/workflows` needs a token-based-billing plan.

**Documented limits**

- **Dynamic workflows.** You can cap four things: concurrent agents, total agents, active running time, and approximate AI credits. The credit cap is "not a hard ceiling".
- **Permissions.** Workflow subagents inherit the session's grants. `copilot workflow run` shows no approval prompts.
- **/fleet.**
  - No fleet-specific limit is documented. It falls under the general subagent limits: depth 6 by default (maximum 256), and concurrency set by plan (Business 16, Enterprise 32).
  - Only usage-based-billing users can override these limits.
  - `--fleet` cannot be combined with `--acp`.
  - The SDK binding is experimental.

**Verbatim quotes**

- From https://github.blog/changelog/2026-10-01-dynamic-workflows-in-copilot-cli-and-the-copilot-app, Oct 1, 2026 **[P]**:
  - "A dynamic workflow is a program that defines how a task is carried out."
  - "The program itself lives inside a GitHub Copilot extension."
  - "Unlike /fleet, where Copilot delegates work to subagents and coordinates their work in parallel, a dynamic workflow carries out a process defined in code."
  - "In the latest version of Copilot CLI, enable experimental features by running the CLI with the --experimental command-line option."
- From https://docs.github.com/en/copilot/concepts/agent-capabilities/agent-powered-workflows-and-operations/dynamic-workflows, live Nov 5 **[P]**:
  - "Dynamic workflows are available in the Copilot app, Copilot CLI, and Copilot SDK. They are available to users on all Copilot plans except Copilot Pro and Copilot Pro+ subscribers on existing annual plans who remain on legacy premium request-based billing."
  - "/fleet encourages Copilot to delegate work to subagents and coordinate their work in parallel. Copilot decides how to break down the task each time." Also: "A dynamic workflow carries out a process defined in code."
  - Limits: "The maximum number of workflow-owned agents that can be active at the same time. The maximum number of workflow-owned agents that can be launched, in total... The maximum active running time... The approximate maximum number of AI credits."
  - "Usage is reported after it occurs, so work already underway can take the total past the limit. This is an approximate maximum, not a hard ceiling."
  - Settings keys: "workflows.defaultLimits.maxConcurrentSubagents, workflows.defaultLimits.maxTotalSubagents, workflows.defaultLimits.timeoutSeconds, workflows.defaultLimits.maxAiCredits"
  - "A dynamic workflow's subagents use the CLI's permission system and inherit the permission grants of the session that started them."
  - "An extension can also run its own code directly, outside these permission prompts."
- From https://docs.github.com/en/copilot/how-tos/use-copilot-agents/use-dynamic-workflows **[P]**: "To use dynamic workflows in Copilot CLI, you must enable experimental features by running the CLI with the --experimental command-line option."
- From the CLI command reference, https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference (last commit Nov 3, 2026) **[P]**:
  - "/workflows Observe workflow runs, phases, agents, and progress. Requires a token-based-billing plan."
  - "[copilot workflow run] does not display permission approval prompts."
  - Subagent limits: "The CLI enforces depth and concurrency limits to prevent runaway agent spawning. | Max depth 6 256 | Max concurrent plan-based 32"
  - Concurrency by plan: "Free / Education 2 | Pro / Pro+ 4 | Max 8 | Business 16 | Enterprise 32 | Usage-based billing 32"
  - "When the limit is reached, new subagent requests are rejected until an active agent completes."
  - "These settings are ignored for plans that don't use usage-based billing."
- From https://docs.github.com/en/copilot/how-tos/copilot-cli/use-copilot-cli/speed-up-task-completion **[P]**: "The --fleet option is not supported in ACP server mode."
- From the SDK, https://docs.github.com/en/copilot/how-tos/copilot-sdk/features/fleet-mode **[P]**:
  - "Fleet mode is ... "the runtime's built-in pattern for dispatching multiple sub-agents in parallel via the task tool, with SQL todos as the shared coordination state.""
  - "Fleet mode is exposed through generated session RPC bindings and is marked experimental in several SDKs."

**Internal inconsistency.** The same command-reference page lists environment variables with different defaults:

- "COPILOT_SUBAGENT_MAX_CONCURRENT Maximum concurrent subagents per session (default: 32, range: 1 – 256)"
- "COPILOT_SUBAGENT_MAX_DEPTH ... (default: 4, range: 1 – 128)"

The limits table gives depth 6 (maximum 256) and plan-based concurrency (maximum 32). [O] Quote the table, and note that GitHub's own page disagrees with itself.

---

## 6. Copilot harness (closed): system prompt, edit tool mapping, tool list

**Plain English.**

- **Tool list.**
  - The CLI's built-in tool list is documented.
  - VS Code does not publish a list for Copilot-harness sessions. It points you to the Tools tab and warns that Local-harness tool names do not map to it.
- **System prompt.** The section names are documented through the `systemMessage` customize mode: `preamble`, `tone`, `tool_efficiency`, `environment_context`, `code_change_rules`, `guidelines`, `safety`, `custom_instructions`, `runtime_instructions`, `last_instructions`. The text of those sections is not published.
- **Edit tool per model.** The docs say only "apply_patch ... used by some models instead of edit / create". A Dec 2025 changelog line says "Add apply_patch toolchain for OpenAI Codex models". The current mapping for the closed runtime is not published. The open Local harness source maps it, but that is a different runtime.

**Verbatim quotes**

- From the CLI command reference, https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference (last commit Nov 3, 2026) **[P]**:
  - Shell tools: "bash / powershell Execute commands; list_bash / list_powershell; read_bash / read_powershell; stop_bash / stop_powershell; write_bash / write_powershell"
  - File tools: "apply_patch Apply patches (used by some models instead of edit / create); create Create new files; edit Edit files via string replacement; view Read files or directories"
  - Agent tools: "list_agents; read_agent; task Run subagents; write_agent"
  - Other tools: "ask_user; glob; grep (or rg); skill; web_fetch"
- From the config reference, https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-config-dir-reference **[P]**:
  - "Replacing or removing built-in instructions can change the CLI's tool use and other expected behavior."
  - Section table: "preamble Section The assistant's introductory identity instructions. | tone | tool_efficiency | environment_context | code_change_rules Section Guidance for making code changes. | guidelines | safety Section Safety guidance and environment limitations. | custom_instructions | runtime_instructions | last_instructions"
- CLI changelog 0.0.366 (Dec 3, 2025): "Add apply_patch toolchain for OpenAI Codex models". CLI changelog 1.0.7 (Mar 17, 2026): "Add "customize" mode to system message config for section-level system prompt overrides". **[P]**
- From VS Code `docs/agents/reference/tools-reference.md` **[P]**:
  - "The following tables use Local harness tool reference names. Do not assume that these identifiers map directly to Copilot harness tools. In a Copilot session, use the **Tools** tab."
  - From `docs/agents/run/tools.md`: "The **Copilot** group lists the harness's built-in tools. These tools run in the Copilot runtime and are read-only in the **Tools** tab."
- From VS Code `docs/agents/run/agent-harnesses.md` **[P]**: "The shared SDK runtime also does not imply identical tools, models, permissions, or customizations across products."
- The Rust-port blog describes the prompt order only: "GitHub Copilot shapes the agent loop specifically to preserve a long and stable prefix (the system prompt, then the tool definitions, then the accumulated conversation)". From https://github.blog/ai-and-ml/generative-ai/migrating-the-github-copilot-runtime-to-rust-using-copilot/ **[P]**

**Still undocumented:**

- system prompt text
- per-model prompt variants
- which models get `edit` vs `apply_patch` in the closed runtime
- a tool list for VS Code Copilot-harness, app and cloud sessions

Places searched:

- the CLI reference and config reference
- the CLI changelog
- VS Code docs: tools reference, tools, agent harnesses
- the harness evaluation blog (Jun 25)
- the Rust-port blog
- the Microsoft Copilot harness post (Oct 28)

---

## 7. Copilot local sandbox

**Plain English.**

- **Default.** Off by default in the CLI, the app and VS Code.
- **VS Code.** Yes, VS Code agent sessions use it: Copilot-harness (Agent Host) sessions, setting `chat.agent.sandbox.enabled`, default `off`. In VS Code, Windows support is marked **Experimental**. The Local harness sandboxes terminal commands on macOS and Linux only; its Windows sandboxing was deprecated in 1.142.
- **When enabled, the defaults are:**
  - write access to the working directory and temp
  - outbound internet on
  - local network off
  - Git and gh credentials proxied
  - dev-tool paths readable
  - MCP and LSP servers sandboxed
  - bypass prompts allowed
- **Built-in file tools** are checked in software on a "best-effort basis". The OS never sees them.
- **Windows 10** is not named anywhere. The documented requirement is Windows 11 25H2 with KB5124010+ or 26H1 with KB5124006+, with the BaseContainer tier.
- **Unsupported host.** The CLI turns the sandbox off for the session with a notice. If managed settings set `failIfUnavailable: true`, model and tool execution is blocked instead. In the app, sandboxed commands fail. [O] Windows 10 is an unsupported host.

**Verbatim quotes**

- "Local sandboxing for GitHub Copilot is now generally available in GitHub Copilot CLI, the GitHub Copilot app, and VS Code sessions using Agent Host." Also: "Local sandboxing is powered by Microsoft eXecution Container (MXC)". From https://github.blog/changelog/2026-10-07-local-sandboxing-for-github-copilot-now-generally-available, Oct 7, 2026 **[P]**
- From https://docs.github.com/en/copilot/concepts/security-governance-and-network-settings/about-cloud-and-local-sandboxes **[P]**:
  - "Local sandboxing is turned off by default. Until you enable it, the shell commands that Copilot runs execute directly on your machine with the same access as your user account."
  - "the built-in tools are coded to check the sandbox policy themselves and honor your configured settings on a best-effort basis."
  - "Local sandboxing is available on macOS, on Linux, and on recent Windows 11 builds."
  - "If your host cannot support a requested feature, Copilot CLI reports the requirement instead of running the command with weaker restrictions."
  - "On Windows, the sandbox relies on programs honoring the proxy settings. As a result, these controls do not provide the same protection against direct connections as on macOS and Linux."
  - "In Copilot CLI, a saved user preference to enable sandboxing is turned off for the current session if the host does not support it. A notice explains that shell commands and services will run without a sandbox."
  - "When effective managed settings set both sandbox.enabled and sandbox.failIfUnavailable to true, the CLI blocks model requests and tool execution for the session if it cannot enforce sandboxing."
- From https://docs.github.com/en/copilot/how-tos/cloud-and-local-sandboxes/using-local-sandboxing **[P]**:
  - "Local sandboxing on Windows requires Windows 11 version 25H2 with update KB5124010 or later, or Windows 11 version 26H1 with update KB5124006 or later, with support for the BaseContainer tier of the ProcessContainer backend."
  - "Outbound internet access is on by default. Local network access is off."
  - "Bypass requests are enabled by default."
- From VS Code `docs/agents/run/agent-sandboxing.md` (last commit Nov 4, 2026) **[P]**:
  - "The `setting(chat.agent.sandbox.enabled)` setting controls sandboxing on all supported platforms. It accepts `off` or `on` and defaults to `off`."
  - "| Windows | Windows 11 with BaseContainer and the required OS capabilities."
  - "Windows support is Experimental."
  - "Sandbox device policies don't enforce these controls for Copilot harness sessions. Administrators should use Copilot managed settings to require sandboxing."
  - "The Local harness sandboxes terminal commands on macOS and Linux only."
  - "Built-in tools that don't start operating system processes use their own permission checks."
- VS Code 1.142 (Oct 14): "Windows sandboxing for terminal commands in Local agent sessions has been deprecated. For sandboxed command execution on Windows, use an Agent Host session." **[P]**

**Conflict.** CLI changelog 1.0.100 (Oct 19) says: "Sandbox allows local network access by default so commands can reach localhost and private-network services." **[P]** Both the GitHub how-to ("Local network access is off") and VS Code (`allowLocalNetwork` "defaults to `false`") say the opposite. [O] Treat the docs as current, but test it.

**Windows 10: still undocumented by name.** Places searched:

- the three GitHub sandbox pages
- the VS Code sandboxing doc
- the aka.ms Windows-support link, which goes to KB5124010 and does not mention sandboxing
- github/docs and vscode-docs code search for "Windows 10" with sandbox

---

## 8. Factory Legacy-Bench (Sep 24, 2026)

**Plain English.**

- **Harness.** The Sep 24 post does not name the harness or the task count. The Fireworks Specialized Intelligence Index card (updated Nov 4, 2026) does. It says Factory's own run "used the Factory Droid harness at each model's default reasoning effort". Fireworks' separate rerun used Harbor terminus-2 on the full **100-task** set.
- **Task count.** The repo README and the April 1 launch post say "hundreds of tasks", with 10 public samples. [O] The "100-task set" may be the evaluation subset. The sources do not reconcile the two numbers.
- **The COBOL payroll example** comes from the April 1 launch post, with more detail than the Sep 24 version: a health deduction of $275 instead of $125, the error cascades into wrong totals, and 24 of 29 tests still pass. Neither post names which model or agent produced it.
- **April leaderboard (12 model-agent pairs).** It compared Droid against Codex CLI, Gemini CLI, Claude Code and Cursor. The April post says Droid beats each vendor's own agent on the same model.

**Verbatim quotes**

- From https://factory.com/news/legacy-bench-specialized-intelligence-index, Sep 24, 2026 **[P]**:
  - "Ten representative tasks are available on GitHub in the Harbor format. The full benchmark is used for evaluation."
  - "The latest evaluation snapshot prepared for the Specialized Intelligence Index produced the following results: GPT-5.6 Sol 60.0% $0.44 2m 43s; Claude Opus 5 52.0%; GPT-6 Astra 51.0%; DeepSeek V4.1 Flash 49.0%; Kimi K3 44.0%; GLM 5.3 23.0%"
  - "In a COBOL payroll task, the program compiled and passed 24 of 29 tests, but calculated a $275 health deduction instead of $125. The output looked plausible, and the model reported success."
  - The post does not name a harness.
- From https://fireworks.ai/specialized-intelligence-index/benchmarks/code-generation/legacy-bench, "Last updated Nov 4, 2026" **[P]** (from the page's embedded card data):
  - "TASK SET", "100 tasks · COBOL, Java 7, BASIC, C89, Fortran, Assembly · ten public samples"
  - "HARNESS", "Harbor terminus-2 on E2B · max reasoning effort · reasoning history preserved"
  - "These results are not comparable with Factory's own run, which used the Factory Droid harness at each model's default reasoning effort; harness, effort, and timeouts all differ."
- From https://factory.com/news/legacy-bench (redirected from factory.ai), "Leo Tchourakov, Abhay Singhal, Eno Reyes - April 1, 2026" **[P]**:
  - "Legacy-Bench consists of hundreds of tasks spanning six legacy language families"
  - "Overall pass rates range from 16.9% to 42.5% across the 12 model-agent combinations we evaluated."
  - "In one payroll processing task, the agent calculates a health deduction as $275 instead of $125, and the error cascades into wrong totals. 24 of 29 tests still pass. The agent sees no signal that anything is wrong and moves on."
  - "Of the 44 tasks that no model solves, 31 are COBOL"
  - "In 97% of failures, the agent believes it has solved the task."
  - "On the same underlying model, Droid consistently outperforms the model provider's own agent"
  - "Evaluation uses a single-pass methodology."
  - Chart `overall-results-30a65e.png` **[P]**, which I read as an image: Droid/gpt-5.3-codex 42.5%; Droid/gpt-5.4 40.7%; Codex CLI/gpt-5.4 40.1%; Codex CLI/gpt-5.3-codex 39.4%; Droid/gemini-3.1-pro 38.7%; Gemini CLI/gemini-3.1-pro 36.0%; Droid/claude-opus-4.6 34.6%; Claude Code/claude-opus-4.6 33.0%; Droid/glm-5 32.2%; Cursor/composer-2 31.0%; Droid/gemini-3-flash 27.2%; Droid/kimi-k2.5 16.9%.
- Repo https://github.com/Factory-AI/legacy-bench (Apache-2.0, created Apr 2, 2026) **[P]**: "This repository contains ten representative public sample tasks." Language mix: "COBOL 46% | Java 7 32% | BASIC 6% | C89 5% | Fortran 5% | Assembly 5%".

[O] **Slide caveat.** The Sep 24 numbers (Droid, default effort) and the Fireworks board (terminus-2, max effort, where Claude Opus 5.5 scores 62.0) disagree on rankings. They are different harness runs, so do not mix them on one chart. This is itself a harness-effect example.

---

## 9. Edit formats marked undocumented

### Antigravity: filled [P]

From https://antigravity.google/docs/hooks, "Supported tools" section (last-modified Nov 5, 2026):

- "write_to_file : Create new files. Arguments : TargetFile , Overwrite , CodeContent , Description , IsArtifact (optional), ArtifactMetadata (optional)"
- "replace_file_content : Edit a single contiguous block of text in a file. Arguments : TargetFile , Instruction , Description , AllowMultiple , TargetContent , ReplacementContent , StartLine , EndLine , TargetLintErrorIds (optional)"
- "multi_replace_file_content : Make multiple, non-contiguous edits to the same file. Arguments : TargetFile , Instruction , Description , ReplacementChunks (array of chunks), TargetLintErrorIds (optional), ArtifactMetadata (optional)"

[O] This is string replacement (target text and replacement text) bounded by a line range, plus an `Instruction` field, as in Gemini CLI's `replace`.

### Kiro: filled, for operations [P]

From https://kiro.dev/docs/tools.md (last-modified Nov 4, 2026):

- "| `fs_write` | Create or overwrite a file. CLI 2.x name: `write` |"
- "| `fs_append` | Append content to the end of an existing file |"
- "| `str_replace` | Replace exact text in a file (targeted edits) |"
- "| `delete_file` | Delete a file |"
- The `write` category maps to "fs_write, fs_append, str_replace, delete_file, code".

The older CLI 2.x page (https://kiro.dev/docs/reference/built-in-tools) still says only "Tool name : write ... Aliases : fs_write , fsWrite ... Tool for creating and editing files". Parameter names are not given on either page.

### Devin CLI (Cognition): tool names only [P]

- From https://docs.devin.ai/cli/extensibility/hooks/lifecycle-hooks.md (last-modified Nov 5, 2026):
  - "| File operations | `read`, `write`, `edit`, `apply_patch`, `notebook_read`, `notebook_edit` |"
  - "The exact tool names available can vary by CLI mode, model, and enabled integrations."
- From https://docs.devin.ai/cli/reference/permissions.md: "Direct file edits via the `edit` and `write` tools still prompt. These tools run inside the CLI process rather than inside the sandbox."

[O] Having both `edit` and `apply_patch`, varying "by ... model", suggests the same split as Copilot and OpenCode. **Still undocumented:** parameters, which model gets which tool, and Cloud Devin's tools.

### Amp: tool names only [P]

- Plugin docs, https://ampcode.com/docs/markdown/customize/plugins (lastModified 2026-10-29): "const EDIT_TOOLS = ['edit_file', 'create_file', 'apply_patch']"
- Tools page, https://ampcode.com/docs/markdown/tools (lastModified 2026-10-23): "You can see Amp's builtin tools by running `amp tools list` in the CLI."

**Still undocumented:** parameters.

### Cursor: no model-facing schema; adjacent schemas documented [P]

- Hooks, https://cursor.com/docs/hooks.md, `afterFileEdit` input: "{ "file_path": "<absolute path>", "edits": [{ "old_string": "<search>", "new_string": "<replace>" }] }"
- CLI stream, https://cursor.com/docs/cli/reference/output-format.md: "`tool_call.writeToolCall.args` contains `{ "path": "file.txt", "fileText": "content...", "toolCallId": "id" }`"
- SDK, https://cursor.com/docs/sdk/typescript.md: "`ToolCall` is a discriminated union over every built-in tool (shell, edit, read, write, glob, grep, ls, semSearch, mcp, task, and others). Its shape is internal-facing"

[O] Edits reach hooks as search/replace pairs. That does not show what the model emits, or whether an apply model sits in between. **Still undocumented.**

Places searched for the Cursor, Devin and Amp model-facing schemas:

- vendor tool reference pages
- hooks docs
- SDK docs
- CLI output-format docs
- llms.txt indexes

No vendor-published system prompt or tool schema was found.

---

## 10. AI-approver error rates

### Codex auto-review: published Apr 30, 2026 (before mid-2026, but missing from our files) [P]

OpenAI Alignment blog, "Auto-review of agent actions without synchronous human oversight", https://alignment.openai.com/auto-review/, Apr 30, 2026 (Trębacz, Arnesen, Matthews, Hurd, Park, Lin, Gershenson):

**Usability (OpenAI's internal traffic):**

- "Codex sessions stop for human approval roughly 200x less often than in manual approval mode"
- "Auto-approval Rate On Escalated Actions ... 99.1%"
- "Effective Approval Rate On All Actions ... 99.93%"

**Safety (synthetic test sets; miss rate = 100% minus recall):**

- "Overeagerness Recall ... 90.3%"
- "Prompt Injection Recall ... 99.3%"
- "MonitoringBench [Hard] Recall ... 96.1%"
- Footnote: "When measured among all the categories, including destructive deletions and data tampering, the score drops to 90.2%."

**Method:**

- "We evaluate usability by looking at acceptance rates on internal traffic... March 2026."
- "We evaluate safety on synthetically augmented datasets."

**Cautions:**

- "Auto-review should not be treated as a guarantee of security. During automated and human red-teaming, we identified cases where Auto-review could be misled into approving commands without user approval."
- "it should not be understood as a mechanism for protecting against model scheming."

**Docs.** https://learn.chatgpt.com/docs/sandboxing/auto-review **[P]**: "The reviewer sees a compact transcript plus the exact approval request... Hidden assistant reasoning is not included." Also: "Auto-review interrupts the turn after 3 consecutive denials or 10 denials within a rolling window of the last 50 reviews in the same turn."

**Later coverage.** [S] CellCog (Oct 6, 2026) repeats these figures and says auto-review became free on Oct 6. I found no newer OpenAI numbers.

### Cursor auto-review: published Jun 11, 2026 [P]

- Cursor on X, https://x.com/cursor_ai/status/2065137803084857845, 2026-06-11T18:23Z (read via X's syndication API): "Auto-review is now the default for all new users. A classifier subagent reviews actions in context before deciding whether to allow, block, or ask for approval. Our evals show it's 97% accurate, with most misses near ambiguous edges."
- Blog "Governing agent autonomy with Auto-review", David Gomes and Travis McPeak, Jun 11, 2026, https://cursor.com/blog/auto-review **[P]**:
  - "We started with roughly 12 hours of internal developer sessions, then cut that down and deduplicated common actions into 6,122 labeled rows."
  - "it currently blocks around 4% of actions"
  - "only about 7% of total chats in Auto-review mode lead to at least one interruption."
  - The blog itself does not state the 97% figure, and it does not split misses into false allows and false blocks.
- Docs, https://cursor.com/docs/agent/security/run-modes.md **[P]**:
  - "Today it uses Gemini 3.5 Flash Lite, with Haiku as the fallback."
  - "The classifier can make mistakes. It can allow a call you would have blocked, or block a call you would have allowed."

### Antigravity Auto: still undocumented

The docs describe the mechanism only, with no rates. https://antigravity.google/docs/permissions **[P]**:

- "When a command needs to run outside the sandbox, Antigravity automatically evaluates it so safe, reversible commands run without prompting, while risky or irreversible commands still ask for your approval."
- "It isn't currently available for business or enterprise accounts, including Antigravity in Gemini Enterprise."

The changelog, https://antigravity.google/docs/changelog **[P]**, says commands are "first reviewed by a separate agent" and mentions timeout tuning. It gives no accuracy figures.

Places searched:

- docs: permissions, sandbox, CLI permissions
- the changelog
- the blog index (about 30 posts)
- web search

---

## 11. Published rationale for keeping the Copilot runtime closed

**Still undocumented.** The only stated pitch is managed service: Microsoft runs it so you don't have to.

- From the Microsoft blog, https://blogs.microsoft.com/blog/2026/10/28/introducing-the-microsoft-copilot-harness-unlocking-the-potential-of-truly-multi-model-agentic-work/, Oct 28, 2026 **[P\*]** (read via WebFetch summariser; curl was blocked):
  - "With the Copilot harness, Microsoft runs the agent loop and sandbox, with governance and optimization built in from day one."
  - "Now, you can build on the same harness Microsoft and GitHub ship in our own products, and you don't have to maintain it."
  - The summariser found no sentence on open source or licensing.
- github/copilot-cli issue #83 "Open Source?" is still open (GitHub API, today). It has 4 comments, all `author_association: NONE`, last updated Apr 23, 2026. **[P]**
  - #1079 "Source Code" was closed as a duplicate on Apr 6, 2026.
  - #3241 was closed as a duplicate on Oct 26, 2026, with no reasoning given.
  - #2294 "License clarification: packaging GitHub Copilot CLI in Linux distro repos" (Mar 25, 2026) is open with no staff reply.

Places searched:

- the copilot-cli issue tracker (search "open source")
- the Microsoft harness post
- the Rust-port blog
- the SDK README (per round 5 PA, re-checked by absence)
- web search for statements by GitHub or Microsoft leaders
