---
url: https://www.anthropic.com/engineering/code-execution-with-mcp
fetched: 2026-08-12
---

# Anthropic — "Code execution with MCP: Building more efficient agents" (Nov 4, 2025)

## The problem: tool definitions eat the context window
> "Tool descriptions occupy more context window space, increasing response time and costs. In cases where agents are connected to thousands of tools, they'll need to process hundreds of thousands of tokens before reading a request."
> — Anthropic, Code execution with MCP

Second problem: intermediate results flow through the model repeatedly (e.g., a 2-hour meeting transcript passing through context twice → 50,000+ extra tokens).

## The solution
Present MCP servers as **code APIs on a filesystem** instead of direct tool-call definitions; the agent writes code, filters/processes data in the execution environment, and returns only what matters.

## The headline number (quotable)
Presenting tools as code reduced one workflow "from 150,000 tokens to 2,000 tokens — a time and cost saving of 98.7%."

## Progressive disclosure (quotable)
> "Models are great at navigating filesystems. Presenting tools as code on a filesystem allows models to read tool definitions on-demand, rather than reading them all up-front."

## Other benefits
- **Privacy**: sensitive intermediate data can flow through a workflow "without ever entering the model's context."
- **State/skills**: agents persist progress to files; resumable work, accumulating skills.

## Slide relevance
This is Anthropic's clearest concrete demonstration of the context-engineering thesis: don't stuff context — give the model an environment and let it fetch what it needs. Direct precursor to the "upfront context → progressive disclosure" shift in the July 2026 new-rules post.
