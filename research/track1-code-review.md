---
url: https://docs.github.com/en/copilot/concepts/agents/code-review
fetched: 2026-08-12
---

# Copilot code review (2026 state)

## Requesting reviews

- **Manual:** add Copilot as a reviewer on a PR. **Re-review:** click the sync button next to Copilot's name in the Reviewers menu.
- **Automatic:** enable per-user (Pro/Pro+ own PRs), per-repo (owner), or org-wide. Triggers: "When you create a pull request as an 'Open' pull request" or "The first time you switch a 'Draft' pull request to 'Open'"; options for "Every time you push a new commit" and reviewing drafts.
- Platforms: github.com, GitHub CLI, GitHub Mobile, VS Code, Visual Studio, Xcode, JetBrains, **Azure DevOps (public preview)**.

## NEW: Review effort levels (not in 2024-2025)

- **Lite (default):** "Provides fast, targeted feedback on common issues such as bugs, security vulnerabilities, and style inconsistencies."
- **Balanced:** routes to "a higher-reasoning model for longer analysis of complex logic, security-sensitive code, and cross-service changes."

## NEW: Cost is in AI credits (dollar-denominated), not premium requests

Verbatim: "A review typically consumes an estimated $0.05 USD to $1 USD worth of AI credits with 'Lite' effort, and $0.25 USD to $5 USD worth of AI credits with 'Balanced' effort." Plus GitHub Actions minutes "for agentic capabilities (context gathering)".

Attribution: "If a repository is configured to automatically request a code review from Copilot for all new pull requests, the AI credits consumption is attributed to the pull request author."

**Members WITHOUT a Copilot license can get code review** if the org enables two policies: "AI credits paid usage" and "Allow members without a Copilot license to use Copilot code review".

## Customization — code review reads (answering the key question: YES)

1. **`.github/copilot-instructions.md`** — "Repository-wide, always-on rules for Copilot"
2. **`.github/instructions/**/*.instructions.md`** path-specific files (opt-out per file with `excludeAgent: "code-review"`)
3. **`AGENTS.md`** — "Always-on rules shared across AI agents" (AGENTS.md only; CLAUDE.md/GEMINI.md not honored by code review per the support matrix)
4. **Organization-level instructions**
5. **Agent Skills** — "Copilot code review can automatically use relevant skills when reviewing a pull request"
6. **MCP servers** — "Copilot code review can use MCP servers to pull context directly into the review"; GitHub + Playwright MCP servers "enabled by default"
7. **Copilot Memory** — Pro/Pro+/Max users; stores "useful details it has learned about a repository"

(That list is a headline: code review is now a fully customizable agent — instructions + skills + MCP + memory.)

## Languages / exclusions / limits

- "Copilot reviews your code written in any language" (2024-era supported-language list is obsolete).
- Excluded files: "Dependency management files, such as package.json and Gemfile.lock," log files, SVG files. Full list: reference page "Files excluded from code review" (see docs nav).
- Docs are silent on a max-file count on this page.
- Caveat verbatim: "Copilot is not guaranteed to spot all problems or issues in a pull request. Sometimes it will make mistakes. Always validate Copilot's feedback carefully."

## Plan availability

- All paid plans; Business/Enterprise get full org features; Pro/Pro+ can auto-review their own PRs.
- Note the new plan names appearing in docs: Free, Pro, Pro+, **Max**, Business, Enterprise (Max is new; see track1-models.md).

## Related tutorial pages (for deeper dives)

- "Custom instructions for reviews": https://docs.github.com/en/copilot/tutorials/customization-library (customization library)
- Automatic code review setup how-to (docs nav: "Automatic code review setup")
- VS Code side: code review honors repo-wide instructions only (per support matrix; see track1-repo-custom-instructions.md).
