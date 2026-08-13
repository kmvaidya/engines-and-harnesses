---
url: https://www.anthropic.com/engineering/writing-tools-for-agents
fetched: 2026-08-12
---

# Anthropic — "Writing effective tools for agents — with agents" (Sep 11, 2025)

## Core principles
- Tools must be designed for **agent affordances**, not just wrapped API endpoints.
- > "More tools don't always lead to better outcomes." — Anthropic, Writing tools for agents
- **Consolidate**: `schedule_event` instead of `find_availability` + `create_event`; `get_customer_context` that compiles everything at once.
- **Namespacing**: "Namespacing (grouping related tools under common prefixes) can help delineate boundaries between lots of tools." (e.g. `asana_projects_search`, `jira_search`)
- **Return meaningful context**: tools should "return only high signal information back to agents." Prefer semantic fields over technical IDs — `name` over `uuid`, `image_url` over `256px_image_url`.
- **Token efficiency**: pagination, filtering, truncation with sensible defaults; steerable truncation messages that teach the agent to search more efficiently.
- **Descriptions are prompts**: "Even small refinements to tool descriptions can yield dramatic improvements." Make implicit context explicit; unambiguous parameter names.

## The recursive process
Build prototype → run realistic evals → read the agent's reasoning transcripts → **let Claude itself analyze results and refactor the tools** → repeat. (Hence the title: writing tools for agents, *with* agents.)

## Slide relevance
The tool interface is the modern "prompt surface": Anthropic's 2026 doctrine (see new-rules post) moves instruction mass out of the system prompt and into tool definitions — this 2025 post is where that starts.
