---
url: https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications/, https://genai.owasp.org/download/52117/?tmstv=1765059207, https://genai.owasp.org/2025/12/09/owasp-top-10-for-agentic-applications-the-benchmark-for-agentic-security-in-the-age-of-autonomous-ai/, https://www.finos.org/blog/finos-ai-governance-framework-v2.0-addressing-agentic-ai-risks-in-a-rapidly-evolving-landscape, https://github.com/finos/ai-governance-framework, https://www.endorlabs.com/learn/beyond-mcp-the-new-security-playbook-for-coding-agents, https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/, https://www.pillar.security/blog/the-agent-security-paradox-when-trusted-commands-in-cursor-become-attack-vectors, https://www.straiker.ai/blog/nomshub-cursor-remote-tunneling-sandbox-breakout, https://arxiv.org/abs/2603.02277, https://picrew.github.io/LLM-Harness/main.pdf, https://github.blog/changelog/2026-02-26-enterprise-ai-controls-agent-control-plane-now-generally-available/, https://github.blog/changelog/2026-08-06-mcp-allowlists-in-enterprise-managed-settings/, https://docs.github.com/en/copilot/how-tos/use-copilot-agents/cloud-agent/extend-cloud-agent-with-mcp, https://docs.github.com/en/copilot/how-tos/use-copilot-agents/cloud-agent/customize-the-agent-firewall, https://docs.github.com/en/admin/data-residency/github-copilot-with-data-residency
fetched: 2026-09-30
---

# Agent security and governance for a regulated firm

Round 2 file, new topic (round 1 had no security track). Tags: **[V]** 3-agent
adversarial check passed, **[S]** hand spot-check, **[P]** confirmed against
the primary source on 2026-09-30, **[E]** extracted with quote but not
cross-checked, **[R]** refuted.

**Primary-source pass (2026-09-30):** every claim that was [E] has been
checked against its primary source. Three were wrong and are corrected below:
the OWASP incident mapping (§1), the FINOS risk names (§1) and the
SandboxEscapeBench figures (§3). Still not covered: secrets handling, and the
Claude Agent SDK and Codex CLI permission models.

## 1. Risk catalogues a bank's security team will recognise

### OWASP Top 10 for Agentic Applications 2026 (Dec 9, 2025) [P]

Read in full from the PDF (cover: "Version 2026 / December 2025") and the
launch blog of Dec 9, 2025.

- Separate from the LLM Top 10 but meant to complement it: "The LLM Top 10
  will remain a core, regularly updated resource".
- Contributor counts vary by document: the press release says "over 100
  security researchers, industry practitioners, user organizations and
  leading cybersecurity and Gen AI technology providers"; the launch blog
  says "hundreds of experts". The blog lists review from "national
  cybersecurity agencies, standards bodies, vendors, regulators, enterprises,
  and researchers".
- **For a bank audience:** the public-review list names ABN AMRO and
  JPMorgan; the review board includes NIST and the Alan Turing Institute;
  BBVA is a project supporter. ASI03 and ASI09 use finance scenarios
  (fraudulent payments forwarded between agents, invoice-driven payment
  fraud).

| ID | Risk (PDF wording) | Headline incident in the PDF | Harness part it maps to |
|---|---|---|---|
| ASI01 | Agent Goal Hijack | EchoLeak (crafted email silently triggers Microsoft 365 Copilot) | loop / goal |
| ASI02 | Tool Misuse and Exploitation | Amazon Q DNS secrets leak (reference only) | tools |
| ASI03 | Identity and Privilege Abuse | Generic body examples; Appendix D adds Copilot Studio public-by-default agents, Heroku MCP app hijack | permissions |
| ASI04 | Agentic Supply Chain Vulnerabilities | Amazon Q for VS Code poisoned prompt (v1.84.0); GitHub MCP tool-descriptor poisoning | MCP / plugins |
| ASI05 | Unexpected Code Execution (RCE) | Replit "Vibe Coding" runaway execution; AutoGPT RCE as a reference | sandbox |
| ASI06 | Memory & Context Poisoning | Gemini long-term memory corruption (reference) | memory |
| ASI07 | Insecure Inter-Agent Communication | Generic; Appendix D adds Cursor MCP OAuth exploit, malicious postmark-mcp server | subagents |
| ASI08 | Cascading Failures | Hypothetical (e.g. financial trading cascade) | pipelines |
| ASI09 | Human-Agent Trust Exploitation | Generic (invoice copilot fraud) | approval gates |
| ASI10 | Rogue Agents | Generic, citing two arXiv papers | monitoring |

- [R] Round 2 first used the **launch blog's** one-line incident list
  (ASI02 Amazon Q, ASI05 AutoGPT, ASI10 Replit). The full PDF places them
  differently: the Amazon Q supply-chain compromise is ASI04's first example;
  ASI05's headline is Replit; Appendix D maps the Replit meltdown to ASI01,
  ASI09 and ASI10 together. Cite the PDF's placement. The phrase "runtime
  component poisoning" is not in the PDF.
- The mapping column is our reading, not OWASP's.
- OWASP also publishes an "Agentic Threat Modelling Guide", "Securing Agentic
  Applications" guidelines, and **FinBot**
  (genai.owasp.org/resource/finbot-agentic-ai-capture-the-flag-ctf-application/),
  a capture-the-flag exercise built on "a simulated Financial
  Services-focused application". [P]

### FINOS AI Governance Framework v2.0 [P]

FINOS is the Linux Foundation's financial-services open-source body. Checked
against the repo (github.com/finos/ai-governance-framework, tags v1 and v2) and
the FINOS blog (Nov 12, 2025, Colin Eberhardt of Scott Logic).

- Released Oct 20, 2025 (repo tag and website); the blog post came in Nov.
- **46 = 23 risks + 23 mitigations.** The blog says "46 risks and
  mitigations" and "six additional risk / mitigation pairs". [R] The blog's
  "Version 1.0 established ... 30 risks and associated mitigations" does not
  match the v1 tag, which has 17 + 17 = 34. Say "46 (23 risks, 23
  mitigations)" and leave out the v1 count.
- [R] The four names round 2 first listed ("Prompt injection and memory
  poisoning; Persistent agent compromise; Chain-of-thought leakage;
  Supply-chain tampering") are blog bullet points, not framework titles.
  "Chain-of-thought leakage" is not a risk in the framework. The actual
  agentic additions:

  | Risk | Paired mitigation |
  |---|---|
  | AIR-SEC-024 Agent Action Authorization Bypass | MI-18 Agent Authority Least Privilege Framework |
  | AIR-SEC-025 Tool Chain Manipulation and Injection | MI-19 Tool Chain Validation and Sanitization |
  | AIR-SEC-026 MCP Server Supply Chain Compromise | MI-20 MCP Server Security Governance |
  | AIR-SEC-027 Agent State Persistence Poisoning | MI-21 Agent Decision Audit and Explainability |
  | AIR-OP-028 Multi-Agent Trust Boundary Violations | MI-22 Multi-Agent Isolation and Segmentation |
  | AIR-SEC-029 Agent-Mediated Credential Discovery and Harvesting | MI-23 Agentic System Credential Protection Framework |

- At v2.0 it was "cross-referenced to 7 existing frameworks (including OWASP,
  MITRE and EU AI Act)" and "aligned to evolving regulatory guidance across
  the EU AI Act and U.S. prudential standards". The live references page now
  lists about 15, including **SR 11-7**, the **FFIEC IT Handbook**, the IOSCO
  toolkit, NIST SP 800-53r5 and the OWASP Agentic Top 10. Those are the
  references a bank's model-risk team already uses.
- "These mitigations can now be implemented as active runtime defenses,
  bridging the gap between governance and engineering." That means checks
  inside a harness, not only policy documents.

## 2. Threat model: the lethal trifecta [P]

- **Originator:** Simon Willison, "The lethal trifecta for AI agents: private
  data, untrusted content, and external communication" (Jun 16, 2025). His
  three: "Access to your private data", "Exposure to untrusted content",
  "The ability to externally communicate in a way that could be used to
  steal your data". Cite him, not the vendors that repeat it.
- Endor Labs, "Beyond MCP: the new security playbook for coding agents" (Jul
  21, 2026; George Apostolopoulos, Dimitris Nikolaidis), applies it to coding
  agents. Endor sells hook integrations for coding agents, so it has a
  commercial interest in the hook argument. Quotes confirmed verbatim:
  - "Despite their tremendous progress, LLMs can still not reliably
    distinguish between data and instructions."
  - Skills "can contain anything, including, of course, prompt injection
    attempts."
- An egress allowlist breaks the third leg. Checking each tool's safety on
  its own misses risk because the danger is in the combination; the MCP
  team's tool-annotations post makes the same point
  (`round2-harness-reference-designs.md` §9).
- Pre-tool hooks (MCP, shell, file access) can block risky actions under
  policy control. MCP servers running in the agent's environment behave like
  a malicious dependency.

## 3. Sandboxes are necessary but not sufficient [P]

- **Cursor escapes, with primary disclosures:**
  - Pillar Security "trusted commands" attack (Jan 14, 2026): **CVE-2026-22708
    / GHSA-82wg-qcm4-fp2w**, "Terminal Tool Allowlist Bypass via Environment
    Variables", High, Cursor ≤2.2, fixed in 2.3. Abuses shell built-ins
    (`export`, `typeset`, `declare`) to turn approved commands into code
    execution. Strictly an allowlist bypass in the non-default Auto-Run +
    Allowlist mode, not a sandbox escape.
  - "cursor-tunnel" is **NomShub** (Straiker STAR Labs, Apr 3, 2026): prompt
    injection plus a shell-builtin parser bypass plus Cursor's remote tunnel
    gives a persistent shell. macOS, Cursor before 3.0, patched Apr 2, 2026.
    No CVE or GHSA found.
  - Cursor's advisory list has about seven separately numbered "sandbox
    escape" CVEs from Feb to Jul 2026 (e.g. CVE-2026-26268 via Git hooks;
    CVE-2026-50548/50549, critical).
- **SandboxEscapeBench** [P, corrected]. "Quantifying Frontier LLM
  Capabilities for Container Sandbox Escape" (Marchand et al., UK AI Security
  Institute and Oxford; arXiv 2603.02277, ICML 2026; v3 Aug 1, 2026). Nested
  capture-the-flag tasks on Docker and Kubernetes. Overall success: GPT-5
  0.50, Opus 0.49, GPT-5.2 0.27, Haiku 0.18, GPT-OSS-120B 0.16. Difficulty-3
  tasks 0.40; levels 4-5 zero. The v3 update: "Claude Mythos Preview ...
  saturates this public benchmark". [R] The "15% to 35%" range round 2 first
  used comes from the harness survey, not the paper; it understates the top
  models.
- The paper quotes UK NCSC guidance that container separation alone is
  "generally insufficient" and that hypervisor isolation should be the "bare
  minimum". Managed sandboxes are moving from shared-kernel containers to
  dedicated-kernel microVMs.
- **Two kinds of isolation** (harness survey, quote confirmed): "an
  infrastructure sandbox constrains the blast radius of an action once it is
  executed, while semantic isolation constrains which actions are permitted
  in the first place. A complete agent harness requires both." Examples:
  CaMeL (arXiv 2503.18813, "Defeating Prompt Injections by Design", Google,
  Google DeepMind and ETH Zurich; 77% of AgentDojo tasks solved "with
  provable security") and Progent (arXiv 2504.11703, "Progent: Securing AI
  Agents with Privilege Control"; OWASP cites it under ASI02).
- OpenDev's five-layer safety stack is one worked example of combining both
  (`round2-harness-reference-designs.md` §4).

## 4. Copilot Enterprise controls

### Enterprise AI Controls and agent control plane (GA Feb 26, 2026) [V]

- A dedicated AI administrator role; all AI policies in one AI Controls tab.
- Enterprise-wide custom-agent standards with version control; a one-click
  push rule protects `.github/agents/*.md`; an API for custom-agent
  definitions.
- Audit logs mark agent actions with `actor_is_agent` and record `user` and
  `user_id` to show on whose behalf the agent acted. Current docs add
  `agent_session_id`. A separate 180-day view filters by `actor:Copilot`.
- Admins can see all cloud agent sessions from the last 24 hours.

### MCP allowlists [P]

- At the Feb 26 GA: "Managing enterprise-wide MCP allowlists will remain in
  preview at this time." The registry-based policy ("Registry only" / "Allow
  all") is **still public preview** and, per the docs, "not the recommended
  method for restricting access to MCP servers."
- **GA on Aug 6, 2026:** MCP allowlists in enterprise managed settings
  (`allowedMcpServers` / `deniedMcpServers` in `managed-settings.json`,
  matching on server URL, command or name). The docs call it "the more
  secure, generally available method". Enforced in the **Copilot app,
  Copilot CLI and VS Code only. The cloud agent is not listed.**

### MCP on the cloud agent: what controls exist [P]

No enterprise or org MCP allowlist applies to the cloud agent, and the
firewall does not cover MCP server processes. What does exist:

1. Repo admins configure MCP servers in repository settings. The `tools`
   field is required (allowlist specific tools or `*`). Only secrets and
   variables prefixed `COPILOT_MCP_` reach MCP configs. Remote MCP servers
   using OAuth are not supported. GitHub and Playwright MCP servers are on by
   default; GitHub's is read-only. Warning from the docs: Copilot "will not
   ask for your approval before using them."
2. The on/off policy "MCP servers in Copilot" does apply to the cloud agent;
   "Restrict MCP access to registry servers" does not.
3. GitHub Well-Architected names **rulesets** protecting
   `.github/copilot/mcp.json` and `.mcp.json` as "the primary technical
   control against unauthorized MCP endpoints across all surfaces except for
   cloud agent", and says registry enforcement on the cloud agent is "a
   governance signal ... not a hard security boundary." It also recommends
   human review of MCP config changes, CODEOWNERS, and watching `copilot.mcp_*`
   audit events.
4. **Gap:** no primary GitHub source describes network egress control for MCP
   server processes on the cloud agent.

### Well-Architected baseline [P]

wellarchitected.github.com now redirects to learn.github.com/well-architected/.
"Set enterprise-level controls for security and compliance baselines, then let
teams tailor custom instructions and MCP access at the repository level for
maximum effectiveness." Its first principle is "Minimize enterprise-level
baseline", with "audit log streaming and model restrictions" as the
non-negotiables.

### Other Copilot controls (detail in `round2-copilot-changes.md`)

- Cloud agent firewall: does **not** cover MCP server processes or setup-step
  processes (§3 there). [V]
- Content exclusions now cover the Copilot app and CLI; VS Code Edit and
  Agent modes still do not honour them (§1 there). [V]
- Local sandboxing in the Copilot app, off by default, fails closed (§2
  there). [V]
- Data residency: US and EU only, off by default, 10% credit surcharge,
  covers the cloud agent and CLI, and the newest Claude models are not on the
  compliant lists (§6 there). Retirements on Oct 2 and Oct 19 remove six
  EU-compliant models (§4 there). [S], [P]
- **Enterprise-managed permissions (GA Sep 9, 2026)** [P]: deny/ask/allow
  rules for shell, file and domain access that users, auto-approval, saved
  approvals and bypass mode cannot weaken. App, CLI and VS Code Agent Host
  only; not the cloud agent or JetBrains (§10.1 there).
- Copilot policy hooks **fail open on timeout**, including admin-deployed
  ones (§10.3 there). [P]
- Code review reads review instructions from the PR's head branch, so a PR
  author can change them (§9.3 there). [P]

## 5. Open questions for the bank context

- How do teams control egress from MCP servers on the cloud agent, given
  that neither the firewall nor the MCP allowlist nor managed permissions
  cover them? (Possibly only by not attaching untrusted servers.)
- Permission models and secrets handling for the Claude Agent SDK, Codex CLI,
  OpenAI Agents SDK and Copilot are now in `round2-agent-permission-models.md`;
  its §6 lists what is still open.
