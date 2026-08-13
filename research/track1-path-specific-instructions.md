---
url: https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions, https://code.visualstudio.com/docs/agent-customization/custom-instructions
fetched: 2026-08-12
---

# Path-specific instructions (`.github/instructions/*.instructions.md`)

## File naming and location

- **GitHub side:** files live in **`.github/instructions/`** (subdirectories allowed) and MUST be named **`NAME.instructions.md`** (must end with `.instructions.md`).
- **VS Code side:** default workspace location `.github/instructions/`; extra locations configurable via `chat.instructionsFilesLocations`. User-level location: `~/.copilot/instructions/`.
  (Sources: https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions ; https://code.visualstudio.com/docs/agent-customization/custom-instructions)

## Frontmatter — exact syntax

GitHub docs (verbatim):

```markdown
---
applyTo: "app/models/**/*.rb"
---
```

Multiple glob patterns are **comma-separated inside one string**:

```markdown
---
applyTo: "**/*.ts,**/*.tsx"
---
```

**NEW (not in 2024-2025 docs): `excludeAgent` frontmatter key** — lets one instructions file opt out of a surface:

```markdown
---
applyTo: "**"
excludeAgent: "code-review"
---
```

- `excludeAgent` accepts `"code-review"` or `"cloud-agent"`. Omitting it means the file applies to both.
  (Source: https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions)

VS Code adds optional `name` and `description` frontmatter fields; **no field is required** — omitting `applyTo` makes the file manual-attach only:

```yaml
---
name: 'Display Name'
description: 'Short description'
applyTo: '**/*.ts,**/*.tsx'
---
```

(Source: https://code.visualstudio.com/docs/agent-customization/custom-instructions)

## Glob syntax

- Standard glob notation, relative to workspace/repo root: `**/*.py`, `docs/**/*.md`, `**` (all files).
- VS Code `.claude/rules` files use `paths:` (array) instead of `applyTo:`, default `**`.

## Which surfaces honor path-specific instructions

- GitHub docs: "Path-specific instructions currently work only with **Copilot cloud agent and Copilot code review** on GitHub.com." (Chat on github.com does NOT use them.)
- In IDEs: VS Code Chat, Visual Studio Chat, JetBrains Chat, Xcode Chat, and Copilot CLI all apply path-specific files (per https://docs.github.com/en/copilot/reference/custom-instructions-support).

## Interaction with repo-wide file

- Overlap rule (verbatim): "instructions from both files are used." Path-specific files are ranked above repository-wide in the priority list, but everything relevant is sent together.
  (Source: https://docs.github.com/en/copilot/concepts/prompting/response-customization)

## VS Code settings

- `chat.instructionsFilesLocations` — configure workspace instruction paths
- `chat.includeApplyingInstructions` — enable pattern-based (applyTo) instructions
- `chat.includeReferencedInstructions` — instructions pulled in via Markdown links, e.g. `Apply the [general coding guidelines](./general-coding.instructions.md)`
- `chat.useCustomizationsInParentRepositories` — monorepo parent-repo discovery

## Notes / gotchas for slides

- `excludeAgent` is the new precision knob: e.g. keep style rules out of code review while cloud agent still gets them.
- Docs are silent on a per-file size limit for `.instructions.md` files.
- Comma-separated patterns in ONE quoted string (`"**/*.ts,**/*.tsx"`) is the documented GitHub form — not a YAML list.
