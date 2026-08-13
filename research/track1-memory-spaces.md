---
url: https://docs.github.com/en/copilot/concepts/agents/copilot-memory, https://docs.github.com/en/copilot/concepts/context/spaces
fetched: 2026-08-12
---

# Copilot Memory + Copilot Spaces

## Copilot Memory — NEW first-class feature (did not exist in 2024-2025 docs)

Source: https://docs.github.com/en/copilot/concepts/agents/copilot-memory (concept: "About GitHub Copilot Memory"); how-to: https://docs.github.com/en/copilot/how-tos/use-copilot-agents/copilot-memory

### What it stores — two scopes

- **Repository-level facts:** "coding conventions, architectural decisions, build commands, and project-specific rules" — shared with all users who have Copilot Memory access to that repo.
- **User-level preferences:** "implied or stated personal preferences about how a user wants to interact with Copilot" — private to the individual, cross-repository.

### Who reads/writes it

Used by **Copilot cloud agent, Copilot code review, and Copilot CLI**. Cross-feature: "Facts and preferences captured by one Copilot feature can be used by another" — e.g. cloud agent learns how the repo handles DB connections, code review later flags inconsistent patterns. Scope differences: CLI uses repo facts + the initiating user's preferences; **code review uses repository facts exclusively**.

### Trust & hygiene mechanics (presentation-worthy)

- Memories carry **citations**: repo facts include "citations pointing to the code that supports them"; Copilot **validates them against the current branch before use**. User preferences may cite direct user quotes.
- **Auto-expiry: unused memories are "automatically deleted after 28 days"**; the timer resets each time a memory is validated and used.

### Controls

- Users view/delete their own preferences; repo owners review/delete repo facts.
- Business/Enterprise: admins can export or bulk-delete user preferences; feature requires admin enablement before users can opt in/out. Individual plans: on by default per user.
- Docs nav also lists "Copilot Memory management (personal)" and "(admin)" how-tos.

## Copilot Spaces

Source: https://docs.github.com/en/copilot/concepts/context/spaces (concept: "About GitHub Copilot Spaces")

- Verbatim: "Copilot Spaces let you organize the context that Copilot uses to answer your questions."
- Can contain: "repositories, code, pull requests, issues, free-text content like transcripts or notes, images, and file uploads."
- Where used: **Copilot Chat on github.com**, AND **"in your IDE, using the GitHub MCP server"** to pull space context into the editor (this MCP bridge is new vs 2025).
- Sharing: org spaces with admin/editor/viewer roles; personal spaces private, shared with specific users, or public view-only.
- Plans: "Anyone with a Copilot license, including Copilot Free, can create and use Spaces."
- Billing: questions in spaces "count as Copilot Chat requests and consume AI credits based on the model used and the number of tokens processed."
- Docs say spaces "stay in sync as your project evolves" (live sources, not snapshots).
- Docs are silent (on this concept page) about: a per-space source-count limit, and the space "instructions" field details.
- Related tutorial: "Speeding up development work with Copilot Spaces" (docs nav).

## Memory vs Spaces vs instructions — positioning for slides

- Instructions = authored, versioned in git. Spaces = curated context bundles, shared via UI. Memory = machine-written, self-maintaining knowledge with citations + 28-day GC. Three different context channels, all additive.
