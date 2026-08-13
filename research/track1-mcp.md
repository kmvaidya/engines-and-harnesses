---
url: https://docs.github.com/en/copilot/concepts/context/mcp, https://code.visualstudio.com/docs/agent-customization/mcp-servers, https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/extend-coding-agent-with-mcp
fetched: 2026-08-12
---

# MCP across the Copilot surface

## VS Code (https://code.visualstudio.com/docs/agent-customization/mcp-servers)

- Config files: **workspace `.vscode/mcp.json`** (check into source control); **user `~/.copilot/mcp.json`** or "MCP: Open User Configuration". When **Agent Host** is enabled, VS Code natively reads **`.mcp.json` (workspace)** or **`~/.copilot/mcp-config.json`** instead of the extension-host config.
- Format (verbatim):

```json
{
  "servers": {
    "server-name": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@example/mcp-server"]
    }
  }
}
```

- Transports: `stdio`, `http`, `sse`.
- Install: Extensions view `@mcp` search (MCP Marketplace / "MCP SERVERS - INSTALLED" section), "MCP: Add Server", or CLI:
  `code --add-mcp "{\"name\":\"my-server\",\"command\":\"uvx\",\"args\":[\"mcp-server-fetch\"]}"`
- Autodiscovery of other apps' configs (e.g. Claude Desktop): `chat.mcp.discovery.enabled`.
- Trust: first-start confirmation prompt; "MCP: Reset Trust"; tool invocations may need approval (auto-approved in sandboxed servers).
- **NEW: MCP server sandboxing (macOS/Linux)**:

```json
{
  "servers": { "myServer": { "sandboxEnabled": true } },
  "sandbox": {
    "filesystem": {"allowWrite": ["${workspaceFolder}"]},
    "network": {"allowedDomains": ["api.example.com"]}
  }
}
```

- **NEW 2026:** MCP **Apps** (interactive UI components inline in chat), MCP **resources** (Add Context → MCP Resources), MCP **prompts** (`/<server>.<prompt>`), `chat.mcp.autostart` (experimental), Settings Sync of MCP configs, dev-container `customizations.vscode.mcp` block, enterprise access control via GitHub policies.

## GitHub.com — cloud agent + code review MCP

(Source: https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/extend-coding-agent-with-mcp — titled "Configure MCP servers for your repository")

- Config location: **repo Settings > Copilot > MCP servers** — JSON entered in the UI (NOT a file in the repo).
- **Applies to BOTH cloud agent and code review**; code review usage can be disabled: Settings > Copilot > Code review → toggle "Allow Copilot to use MCP tools when reviewing pull requests".
- **GitHub MCP server and Playwright MCP server are enabled by default and cannot be removed** (customizable).
- Top-level key is `mcpServers` (unlike VS Code's `servers`). Required per server: `type` (`"local"`, `"stdio"`, `"http"`, `"sse"`) and `tools` (array; `["*"]` = all — tools allowlist is REQUIRED here, a difference from VS Code).
- Secrets: must be stored as Agents secrets/variables with the **`COPILOT_MCP_` prefix**; referenced as `$COPILOT_MCP_API_KEY`, `${COPILOT_MCP_API_KEY}`, or `${COPILOT_MCP_API_KEY:-fallback_value}`.
- Constraints (verbatim-ish): "Copilot currently supports only MCP tools, not resources or prompts"; "Remote servers using OAuth authentication are not supported"; "Once configured, Copilot will use MCP tools autonomously without asking for approval first."
- Firewall does NOT apply to MCP servers (see track1-coding-agent.md).

### Verbatim examples (docs)

Sentry (local):

```json
{
  "mcpServers": {
    "sentry": {
      "type": "local",
      "command": "npx",
      "args": ["@sentry/mcp-server@latest", "--host=$SENTRY_HOST"],
      "env": {
        "SENTRY_HOST": "https://contoso.sentry.io",
        "SENTRY_ACCESS_TOKEN": "$COPILOT_MCP_SENTRY_ACCESS_TOKEN"
      }
    }
  }
}
```

Cloudflare (remote SSE):

```json
{
  "mcpServers": {
    "cloudflare": {
      "type": "sse",
      "url": "https://docs.mcp.cloudflare.com/sse",
      "tools": ["*"]
    }
  }
}
```

Azure DevOps (specific tools only):

```json
{
  "mcpServers": {
    "ado": {
      "type": "local",
      "command": "npx",
      "args": ["-y", "@azure-devops/mcp", "<organization>", "-a", "azcli"],
      "tools": ["wit_get_work_item", "wit_get_work_items_batch_by_ids"]
    }
  }
}
```

- Custom agents can embed MCP config: the `mcp-servers` frontmatter property in an agent profile "is a YAML representation of the JSON configuration format" (https://docs.github.com/en/copilot/reference/custom-agents-configuration).

## Surfaces & governance (https://docs.github.com/en/copilot/concepts/context/mcp)

- Local MCP servers: "broad support... in clients such as Visual Studio Code, JetBrains IDEs, Xcode, and others". Remote MCP (OAuth/PAT): VS Code, Visual Studio, JetBrains, Xcode, Eclipse, Cursor, Windsurf.
- **Copilot CLI:** local + remote servers; **GitHub MCP server built in**.
- **Copilot app:** uses repo-level or CLI-level MCP config + app settings.
- **MCP org/enterprise policy:** "Enterprises and organizations can choose to enable or disable use of MCP for members" — the MCP policy is **disabled by default**, and applies ONLY to Business/Enterprise; "Copilot Free, Pro, Pro+, and Max bypass this governance."
- **GitHub MCP Registry**: "a curated list of MCP servers from partners and the community". Enterprises can change/restrict the MCP registry and enforce a **private registry** + **MCP allowlist** (docs nav: "MCP allowlist configuration", "MCP registry configuration", "Restricting MCP registry access", "MCP private registry enforcement" reference).
- **Agent finder** discovers capabilities at runtime "using the Agentic Resource Discovery specification" (new spec name — see track1-other-surfaces.md).

## Contradictions vs 2024-2025

- `.vscode/mcp.json` remains, but Agent Host mode reads `.mcp.json` / `~/.copilot/mcp-config.json` — new dual-config world.
- MCP on github.com config now also drives **code review**, not just the coding agent.
- There is now an enterprise **private MCP registry + allowlist enforcement** story; in 2025 governance was a single on/off policy.
