---
url: https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions, https://code.visualstudio.com/docs/agent-customization/custom-instructions, https://docs.github.com/en/copilot/reference/custom-instructions-support, https://docs.github.com/en/copilot/concepts/prompting/response-customization
fetched: 2026-08-12
---

# Repo-wide custom instructions (`.github/copilot-instructions.md`)

## The file

- **Path:** `.github/copilot-instructions.md` (repository root `.github` folder).
- Natural-language Markdown. Docs: "whitespace between instructions is ignored."
- Instructions become "available for use by Copilot as soon as you save the file(s). Instructions are automatically added to requests."
  (Source: https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions)

## Size guidance / limits

- GitHub docs say repository-wide instructions should be **maximum ~2 pages** and "Instructions must not be task specific."
- No hard character limit documented on the repo-wide file (docs are silent on an exact byte/char cap).
  (Source: https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions)

## The full family of "custom instructions" (2026 taxonomy)

Per the concept page (https://docs.github.com/en/copilot/concepts/prompting/response-customization) there are now THREE tiers plus repo sub-variants:

1. **Personal instructions** — apply to all Copilot Chat conversations on github.com; set in personal settings; "Only supported for GitHub Copilot Chat on GitHub (not IDEs)". Copilot CLI additionally supports a personal file at `~/.copilot/copilot-instructions.md` (per the support-matrix reference page).
2. **Repository instructions** — three variants:
   - Repository-wide: `.github/copilot-instructions.md`
   - Path-specific: `NAME.instructions.md` files in `.github/instructions/`
   - Agent instructions: `AGENTS.md`, `CLAUDE.md`, or `GEMINI.md`
3. **Organization instructions** — set by org owners on github.com; requires Copilot Business/Enterprise; "Currently supported only for Copilot Chat, code review, and cloud agent on GitHub.com."

## Precedence (exact wording)

> "Personal instructions take the highest priority. Repository instructions come next, and then organization instructions are prioritized last."

Complete order given (highest → lowest): personal → repository path-specific → repository-wide → agent instructions (AGENTS.md etc.) → organization. BUT: **"All sets of relevant instructions are provided to Copilot"** — they are combined additively, precedence is weighting, not exclusion. Docs advise "try to avoid providing conflicting sets of instructions."
(Source: https://docs.github.com/en/copilot/concepts/prompting/response-customization)

## Where repo-wide instructions apply (support matrix)

From https://docs.github.com/en/copilot/reference/custom-instructions-support (reference page "Custom instructions support"):

| Surface | Repo-wide | Path-specific | AGENTS.md-family | Personal | Org |
|---|---|---|---|---|---|
| github.com Copilot Chat | yes | no | no | yes | yes |
| github.com **cloud agent** (formerly "coding agent") | yes | yes | AGENTS.md + CLAUDE.md + GEMINI.md | no | yes |
| github.com **code review** | yes | yes | AGENTS.md only | no | yes |
| VS Code Chat | yes | yes | AGENTS.md | no | (via `github.copilot.chat.organizationInstructions.enabled`) |
| VS Code code review | yes (only) | no | no | no | — |
| Visual Studio Chat | yes | yes | — | no | — |
| JetBrains Chat | yes | yes | — | yes | — |
| Eclipse Chat | yes only; code review: "Custom instructions are currently not supported" | | | | |
| Xcode Chat | yes | yes | — | — | — |
| Copilot CLI | yes | yes | agent instructions | `~/.copilot/copilot-instructions.md` | — |

(The matrix is reproduced from the fetched reference page; check the live page before slides — it changes.)

## Contradictions vs. 2024–2025 common knowledge

- **Code review DOES read `.github/copilot-instructions.md` AND path-specific instruction files now.** In 2024/early-2025 code review custom-instruction support was limited/preview; now repo-wide + path-specific + AGENTS.md + org instructions all apply to code review on github.com.
- **"Coding agent" is now called "cloud agent"** throughout the docs (see track1-coding-agent.md).
- **Personal instructions exist on github.com and outrank repo instructions** — many 2025-era decks claimed repo instructions were the top of the stack.
- Repo-wide instructions now support **all Copilot features** ("Repository-wide custom instructions support all Copilot features"), no longer chat-only.

## VS Code specifics (https://code.visualstudio.com/docs/agent-customization/custom-instructions)

- VS Code docs moved from `/docs/copilot/*` to **`/docs/agent-customization/custom-instructions`** (section renamed "Agent customization").
- Always-on instruction files VS Code loads: `.github/copilot-instructions.md`, `AGENTS.md` (root; nested experimental), `CLAUDE.md` (workspace root, `.claude/CLAUDE.md`, or `~/.claude/CLAUDE.md`).
- Settings:
  - `chat.useAgentsMdFile` — enable/disable AGENTS.md
  - `chat.useNestedAgentsMdFiles` — experimental nested AGENTS.md
  - `chat.useClaudeMdFile` — CLAUDE.md support
  - `github.copilot.chat.organizationInstructions.enabled` — org instructions in VS Code
  - `chat.useCustomizationsInParentRepositories` — monorepo/parent-repo discovery (parent folder must be trusted)
- Task-specific settings (`github.copilot.chat.reviewSelection.instructions`, `github.copilot.chat.commitMessageGeneration.instructions`, `github.copilot.chat.pullRequestDescriptionGeneration.instructions`) still exist for review-selection / commit-message / PR-description generation; the older code-/test-generation instruction settings are deprecated.
- User-level (cross-workspace) instruction files live under `~/.copilot/instructions/` (and `.claude/rules` as an alternative, which uses `paths:` instead of `applyTo:`); synced via Settings Sync ("Prompts and Instructions").

## Copy-paste snippets (verbatim from docs)

Referenced-instructions link syntax (VS Code):

```markdown
Apply the [general coding guidelines](./general-coding.instructions.md)
```

Tool reference inside instruction body (VS Code):

```
#tool:web/fetch
```
