---
fetched: 2026-11-05
purpose: Round 6. Re-derive each maker's harness philosophy from its own documentation (docs, engineering blog, README), test the State of the Harness deck's v3 wording, and record corrections. Written by three research agents, each quote string-matched on the live page on 2026-11-05.
tags: [P] matched on the live primary page on 2026-11-05; [P*] via summariser or auto-captions; [S] secondary; [R] refuted or corrected; [O] our analysis. "Older than 6 months" = before 2026-05-05.
---

# Round 6: harness philosophies from the makers' own documentation

Why this file exists: Kay flagged the v3 philosophy slides as suspicious (Claude Code's in particular). This round replaced interview soundbites with documented statements. Headline corrections:
- Claude Code: the Ben Mann "20 or 30 percent" quote is about timing a product for the market, not harness design; "thin harness" rests on a May 2025 remark. Anthropic's documented stance is "lean on the model, and keep cutting what it no longer needs", with hard rules enforced by the harness (Part 1 §1).
- Codex: "trained in the harness" is interview-only; the documented stance is co-tuning per model plus an open harness (Part 1 §2).
- Google: the shared harness covers Google's developer tools, not every product (Part 1 §3).
- Cursor: "own the model" was our inference (Part 2 §1). Kiro: the "deterministic code" quote is about its internal self-improvement loop (Part 2 §5).
- Cline: shipped VS Code defaults auto-approve edits since 2026-06-25/26, despite the README (Part 3 §3.6). Zed asks by default and adds an OS sandbox (Part 3 §3.7).



# Part 1. GitHub/Microsoft, Anthropic, OpenAI, Google

## Harness philosophies, in the makers' own words: GitHub/Microsoft, Anthropic, OpenAI, Google

Checked 2026-11-05. Every page tagged [P] below was downloaded today with curl, stripped to text and string-matched, so the words are on the live page. [P, 11/04 pass] means the earlier research verification pass checked it and I did not re-fetch it today. [P\*] means auto-captions or a summariser. [S] means secondary. "Older than 6 months" means published before 2026-05-05.


---

## Summary of verdicts

| Maker | Deck wording now | Verdict | Why, in one line |
|---|---|---|---|
| Anthropic | "Build a little ahead of today's model, and delete what the next one doesn't need" + Ben Mann 20-30% quote + "thin" end of the spectrum | **Reword the aim, replace the quote, move off "thin"** | The Mann quote is about timing a product for the market, not harness design. Anthropic's documented harness rule is "lean on the model, and keep asking what you can stop doing", plus hard rules enforced by the harness. The product is not thin. |
| OpenAI | "Train the model inside its own harness" + Ambrosino "So we do training on the harness now" | **Reword, keep the quote as interview support** | Only interviews and a LinkedIn post say "trained in the harness". OpenAI's own docs and blog say the harness changes results, is tuned per model, and is published as open infrastructure. |
| Google | "One harness, tuned with Gemini, behind every Google product" + Varun Mohan | **Reword ("every Google product" is too broad); swap in the blog quote** | Google's blog says "a single, cohesive developer product offering that leverages a shared agent harness co-optimized with Gemini models". That covers developer tools, not every product. Gemini CLI, Jules and Code Assist sit outside it, and Antigravity now offers Claude models too. |
| GitHub/Microsoft | "Run the harness for you and send each task to a suitable model" + Parikh "Different tasks need different models" | **Keep, with a small reword** | Matches the Oct 28 posts closely. "Microsoft runs the agent loop and sandbox" comes from the Foundry hosting pitch, so for local CLI and VS Code use, "maintain" is more accurate than "run". |

---

## 1. Anthropic (Claude Code)

### 1.1 Stated philosophy, from Anthropic's own docs and blog

**Lean on the model. Every piece of harness is a bet on what the model can't do yet, so re-test it with each model and cut what is no longer needed. Use the harness to enforce only the things that must always (or never) happen: permissions, sandbox, hooks.**

That is a summary of three official sources that agree: the current Claude Code best-practices doc (live today), Lance Martin's "Harnessing Claude's Intelligence" (April 2026), and Thariq Shihipar's tool-design post (April 2026). The containment post (May 2026) adds the safety half: contain at the environment layer first.

### 1.2 Quotes

1. **Current Claude Code docs, best practices** [P], https://code.claude.com/docs/en/best-practices (undated docs page, live 2026-11-05; the old URL anthropic.com/engineering/claude-code-best-practices now redirects here).
   - "Claude Code is built in a way that, in most cases, your first plain prompt in a fresh session already does the right thing, without any setup on your part."
   - "Most of the time, you want Claude to decide. Almost every guideline has exceptions, and current models are good at reading the code in front of them and judging whether a guideline fits the situation."
   - "Deterministic: you configure the instruction, and Claude Code (the harness) *has* to execute this. This can be a hook, a deny rule, or a managed setting."
   - The section "What you can stop doing" opens: "Every one of these was good advice when it was written. Most were workarounds for something the model couldn't reliably do yet, and the models have since caught up."
   - Context: about Claude Code itself. This page is the current replacement for the 2025 essay.

2. **Lance Martin (member of technical staff, Claude Platform team), "Harnessing Claude's Intelligence"**, April 2, 2026, **older than 6 months** [P], https://claude.com/blog/harnessing-claudes-intelligence (redirects to claude.com/resources/articles/harnessing-claudes-intelligence).
   - "agent harnesses encode assumptions about what Claude can't do on its own, but those assumptions grow stale as Claude gets more capable."
   - The three patterns: "use what it already knows, ask what you can stop doing, and carefully set boundaries with the agent harness."
   - Section heading: "1. Lean on the model, not the harness: use what Claude knows". It goes on: "Claude Code is grounded in these same tools" (bash and a text editor).
   - Closing: "Over time, the structure or boundaries in our applications should be pruned based the question: what can I stop doing?" (the "based the" typo is on the page)
   - Context: written for people building on the Claude API, but it names Claude Code as the example and is the clearest statement of Anthropic's harness design view.

3. **Thariq Shihipar (MTS, Claude Code), "Seeing like an agent: how we design tools in Claude Code"**, April 10, 2026, **older than 6 months** [P], https://claude.com/blog/seeing-like-an-agent (now served from claude.dev/blog/seeing-like-an-agent/).
   - "As model capabilities increase, the tools that your models once needed might now be constraining them. It's important to constantly revisit previous assumptions on what tools are needed. This is also why it's useful to stick to a small set of models to support that have a fairly similar capabilities profile."
   - "Claude Code currently has ~20 tools, and our team frequently revisits if we need all of them for Claude to be most effective. The bar to add a new tool is high, because this gives the model one more option to think about."
   - Context: about Claude Code's own harness. The "small set of models" line is the clearest documented contrast with Copilot's multi-model stance.

4. **Containment post** (Max McGuinness, Mikaela Grace, Jiri De Jonghe, Jake Eaton, Abel Ribbink), May 25, 2026, modified Oct 18, 2026 [P], https://www.anthropic.com/engineering/how-we-contain-claude (now redirects to /research/how-we-contain-claude).
   - "Design for containment at the environment layer first, then steer behavior at the model layer."
   - "The deterministic boundary is what gets hit when everything probabilistic misses."
   - Context: covers claude.ai, Claude Code and Cowork. It is about safety design, not the whole harness.

Supporting interview material, not documentation:
- Boris Cherny, YC Root Access transcript, Jul 27, 2026 [P, 11/04 pass; confirmed again today]: "We unship tools all the time. We delete code in the harness all the time. If you look at the code that's in the Claude Code harness today, almost all of it is about safety and permissions and static analysis. There's a bunch of UI code." Context: answering a question about re-testing the system prompt for each new model ("ablation"). The same sentence that the deck uses as evidence for "thin" says what the remaining code is: safety, permissions, static analysis and UI.
- Cherny, Latent Space, May 7, 2025, **older than 6 months** [P, confirmed today]: "this is the thinnest possible wrapper over the model. We literally could not build anything more minimal." This is the source of "thin", and it is 18 months old.

### 1.3 Testing the deck's current wording

**Ben Mann quote: about Claude Code, or product-building in general?** [P, confirmed today on https://www.anthropic.com/features/making-of-claude-code, page undated, interviews "recorded in February–May 2026"; about July 2026 per earlier secondary reports]
- The full sentence starts: "It's not very obvious to people who haven't been working on model productization for a while that you have to build something that works 20 or 30 percent of the time now, so that when the next model comes out, it works 80 percent of the time. And that's enough to get market traction. And then the next model after that is 90-something percent, and then you really make progress. And you have to have high pain tolerance, because you're going to get it wrong over and over."
- It sits in the "Building" section of the Claude Code making-of story, so it is said about Claude Code's history. But the sentence is a general rule of "model productization", and its point is **market timing** ("enough to get market traction"), not how to design a harness. The deck's leading "…" drops the "model productization" framing. Speaker label on the page: "Anthropic co-founder and Labs team lead".
- Verdict: fine as a quote about how Anthropic times product bets, if the lead-in is kept. Not good evidence for a harness philosophy.

**"Thin harness", next to Pi?** Weak. Evidence against, all [P] today:
- 33 hook events in the hooks reference (counted today from https://code.claude.com/docs/en/hooks.md), 46 named tools in the tools reference (https://code.claude.com/docs/en/tools-reference.md; not all loaded at once, since ToolSearch defers some), plus skills, plugins, mods and an auto-mode classifier on by default.
- The best-practices page boasts that defaults do the right thing "without any setup on your part": auto mode, automatic subagents, automatic compaction. That is an opinionated product, the opposite of 2025's "unopinionated".
- Dynamic workflows (Thariq Shihipar and Sid Bidasaria, Jun 2, 2026) [P], https://claude.com/blog/a-harness-for-every-task-dynamic-workflows-in-claude-code: "Claude can now write its own harness on the fly, custom-built for the task at hand." And: "there are certain classes of tasks where we have had to build custom harnesses on top of Claude Code to achieve peak performance". The new direction is the model writing harness code, not a thinner harness.
- Prithvi Rajasekaran (Labs team), "Harness design for long-running apps", Mar 24, 2026, **older than 6 months** [P]: "my conviction is that the space of interesting harness combinations doesn't shrink as models improve. Instead, it moves". Anthropic's own engineering blog rejects "harnesses only shrink".
- Better framing: the **loop and prompts** are kept lean and pruned. The **product** around them is large (safety, extension points, UI). "Prune" describes Anthropic better than "thin".

**"Intentionally low-level and unopinionated" (Apr 18, 2025)**: confirmed on the Wayback snapshot [P]. It is gone from the live page: the old URL redirects to code.claude.com/docs/en/best-practices, which does not contain it. The replacement is the "first plain prompt ... already does the right thing" intro plus the deterministic/non-deterministic split. Do not cite the 2025 line as current.

**"Unix philosophy" in the docs overview**: live [P], https://code.claude.com/docs/en/overview: "Claude Code is composable and follows the Unix philosophy. Pipe logs into it, run it in CI, or chain it with other tools". Context: it sits in the "Pipe, script, and automate with the CLI" accordion, so it is about scripting the CLI, not about how the harness is designed inside.

**Agent SDK post "The key design principle behind Claude Code is that Claude needs the same tools that programmers use every day."** Confirmed [P], Sep 29, 2025, **older than 6 months**; URL now redirects to claude.com/resources/articles/building-agents-with-the-claude-agent-sdk. It is still consistent with the 2026 Lance Martin post ("Claude Code is grounded in these same tools"). It is a good line for the tools part, but it is a year old.

### 1.4 Shipped work that matches, and work that complicates it
Matches [P]: Glob/Grep replaced by embedded tools on native builds (2.1.117, Apr 2026); TodoWrite replaced by Task tools (described in the Apr 10 post); `/doctor prompt-audit` to flag instructions written for older models (2.1.283, Sep 25, 2026, 11/04 pass); a "What you can stop doing" table in the docs; RAG dropped for grep (Apr 10 post).
Complicates: 33 hooks, mods (2.1.287, Oct 1, 2026; "Mods aren't sandboxed."), dynamic workflows (Jun 2026), auto mode on by default (2.1.283/284, Sep 2026), the April 23, 2026 postmortem showing that harness changes alone made users think the model had got worse (**older than 6 months**). The model-only bet sits next to a lot of harness work on safety and UX.

### 1.5 What Anthropic explicitly rejects, in its words [P]
- Per-action approval as the main control: "Theoretically that works, but we've found the approach to be fallible. Our telemetry showed users approved roughly 93% of permission prompts." (containment post, May 25, 2026)
- RAG for code context: "Most importantly, Claude was given this context instead of finding the context itself." (Apr 10, 2026)
- Hand-crafted task prompts: "A common assumption is that system prompts should be hand-crafted with task-specific instructions. The problem is that pre-loading prompts with instructions does not scale across many tasks" (Apr 2, 2026)
- Switching models mid-session: "Don't change models ... Caches are model-specific; switching breaks them." (Apr 2, 2026)
- Custom security components: "Be wary of custom components. Battle-tested hypervisors, syscall filters, and container runtimes have survived more adversarial attention than anything you'll build." (May 25, 2026)

### 1.6 Verdict
**Reword the aim; replace the quote; move Claude Code off the "thin" pole.**
- Suggested aim: **"Lean on the model, and keep cutting what it no longer needs."** (Or, matching the docs: "Let the model decide; make the harness enforce only what must never bend.")
- Suggested lead quote (documented): "agent harnesses encode assumptions about what Claude can't do on its own, but those assumptions grow stale as Claude gets more capable." (Lance Martin, Apr 2, 2026; mark as 7 months old). For a current alternative: "Most of the time, you want Claude to decide." (Claude Code docs, live).
- Keep Mann only with his framing ("model productization", "market traction"), or drop him.
- On the spectrum, put Claude Code at "prunes the loop, thick product shell". Cherny's own "almost all of it is about safety and permissions" line supports that.

---

## 2. OpenAI (Codex)

### 2.1 Stated philosophy, from OpenAI's own docs and blog

**The harness is a big part of the result, so OpenAI builds and tunes it with each model and publishes it as open, reusable infrastructure. As models improve, cut back the scaffolding and instructions you give them.**

There is no single "design principles" page in the Codex docs (searched the 3.4 MB combined manual for "principle", "philosophy", "design goal", "we believe": no hit about the Codex harness). The statements come from the developers.openai.com blog and from shipped configuration.

### 2.2 Quotes

1. **Nicolas Bonamy and Derrick Choi, "Codex as a platform: build on the open agent harness"**, Aug 19, 2026 [P], https://developers.openai.com/blog/codex-as-a-platform
   - "A capable agent is more than a prompt and a model response. ... That surrounding execution system is the harness. Harness design can materially change results: on ARC-AGI-3, retained reasoning and context compaction raised GPT-5.6 Sol's score from 13.3% to 38.3% while reducing output tokens sixfold."
   - "If you are building software that needs an agent, you can start with Codex instead of inventing a new runtime, then decide what the surrounding application should own."
   - "The open-source layer is the harness and integration surface; model access and managed services remain separate."
   - Context: about the Codex harness specifically.

2. **Eric Provencher, "Rethinking skills and prompts for GPT-6 Astra"**, Sep 11, 2026 [P], https://developers.openai.com/blog/rethinking-skills-and-prompts-for-gpt-6-astra
   - "With more capable models, what used to require a lot of handholding and scaffolding no longer does."
   - "Guidance that helps Sol or Luna may overconstrain GPT-6 Astra, so consider which models will use the instructions you leave behind."
   - Context: about user-written skills and AGENTS.md in Codex, not the built-in harness. It is the OpenAI version of Anthropic's "what you can stop doing".

3. **Codex docs, "Working with agents"** [P], https://learn.chatgpt.com/docs/working-with-agents (undated):
   - "Instructions communicate intent; permissions control access."
   - Context check: this page is user guidance on delegating to any OpenAI agent product (ChatGPT Work, dots, Codex Cloud, Agents SDK). It is **not** a statement about how the Codex harness is designed. Use it as "how OpenAI tells users to work", not as the harness philosophy.

4. **Shipped configuration**, `codex-rs/models-manager/models.json`, last commit 2026-10-26 [P]: 12 model entries, all OpenAI. Each one carries its own `model_messages` instructions, `apply_patch_tool_type`, `truncation_policy`, compaction limit and `tool_mode` (`code_mode_only` for every current model except `gpt-5.5`). This is the documented evidence of per-model harness tuning.

Interview support (not docs):
- Andrew Ambrosino ("Design & engineering"), Every, "How Codex Happened", transcript dated Oct 15, 2026 [P on Every's page; Every says "not certified verbatim transcripts"]. Asked by Dan Shipper whether harnesses are "becoming more and more important": "...one of the great successes of Codex as a team was pairing the product team and the research team together very closely, especially when it came to the harness, right? So we do training on the harness now. We use the harness for far more of our products, including upcoming ones." Confirmed today. Context: Codex harness, yes.
- Alexander Embiricos (product), same set [P, same caveat]: "This harness we need to do our best to keep as simple as possible, and then have the right primitives for extensibility, and you let the model orchestrate as much as possible."
- Gabriel Chua (Developer Experience Engineer, OpenAI), LinkedIn post "How I think about Codex", about Feb 2026, **older than 6 months** [S, via Simon Willison's Mar 7, 2026 summary; LinkedIn not fetched]: "Codex models are trained in the presence of the harness. Tool use, execution loops, compaction, and iterative verification aren't bolted on behaviors — they're part of how the model learns to operate."
- Thibault Sottiaux, Pragmatic Engineer, Sep 9, 2026 [P\*, auto-captions, 11/04 pass]: "the harness in a sense is always a little bit ahead of the model" and "the developer message shrinks and then the harness also shrinks".

### 2.3 Shipped work that matches, and work that complicates it
Matches: per-model prompts and tool modes in models.json [P]; code mode forced on for current models [P]; open-source CLI, SDK and app-server [P, learn.chatgpt.com/docs/open-source]; ARC-AGI harness result [P].
Complicates:
- Codex is not locked to OpenAI's own models. The config reference documents `model_providers` with built-in `ollama` and `lmstudio` provider IDs and custom Responses-API providers [P, codex manual]. Sottiaux (interview) asked "why would you couple it to your model?" So "its own harness" means "tuned for", not "only runs".
- Only part of Codex is open: "IDE extension ... Not open source" and "Codex cloud ... Not open source" [P, open-source docs page].
- Open source, but closed to outside code: the repo "doesn't accept external code contributions or pull requests" [P].

### 2.4 What OpenAI explicitly rejects [P]
- Building your own runtime: "start with Codex instead of inventing a new runtime" (Aug 19, 2026).
- Squeezing everything into chat: "The opportunity is not to replace those interfaces with a universal chat box" (Aug 19, 2026; quoted in round 5, phrase confirmed on the page today).
- Over-prescriptive guidance for new models: "overly specific guidance can now hinder results where it previously helped" (Sep 11, 2026).
- Outside code PRs (open-source page and contributing.md).

### 2.5 Verdict
**Reword. Keep Ambrosino as interview support, labelled.**
- "Train the model inside its own harness" is said only in interviews (Ambrosino, Glaese) and a staff LinkedIn post. The documented, checkable version is **co-tuning plus an open harness**.
- Suggested aim: **"Tune each model and the harness together, and publish the harness."**
- Suggested lead quote (documented): "Harness design can materially change results" with the ARC-AGI-3 13.3% to 38.3% figure (Bonamy and Choi, Aug 19, 2026). Then Ambrosino as "said in interview, Every transcript, not certified verbatim".
- Do not use "Instructions communicate intent; permissions control access" as Codex's harness philosophy. It is advice to users about agents in general.

---

## 3. Google (Antigravity, Gemini CLI)

### 3.1 Stated philosophy, from Google's own blog

**One agent harness, built together with the Gemini models and the Gemini training stack, shared across Google's developer tools, so that improving it once improves every surface.**

### 3.2 Quotes

1. **"Google Antigravity CLI", The Antigravity Team, May 19, 2026** [P], https://antigravity.google/blog/introducing-google-antigravity-cli
   - "At Google, we drive the most long-term value to our users by having a single, cohesive developer product offering that leverages a shared agent harness co-optimized with Gemini models."
   - "A primary goal for the Antigravity CLI was the consolidation of a single agent harness across Google-built developer surfaces for more rapid future improvements."
   - Context: about the Antigravity harness. This is the strongest documented Google statement. Note the scope words: "developer product offering" and "developer surfaces".

2. **"Introducing Google Antigravity 2.0", The Antigravity Team, May 19, 2026** [P], https://antigravity.google/blog/introducing-google-antigravity-2
   - "The product, agent harness, and model layers all had to be co-optimized and co-developed, and while agentic coding is a necessary step towards general model intelligence, it is not sufficient."
   - Goal listed: "Integrate the Antigravity product agent harness with the Gemini training and evaluation stacks".
   - "And we have the momentum of the model and agent harness being co-optimized."

3. **Gemini CLI README** (live, google-gemini/gemini-cli `main`) [P]: "Don't use Gemini CLI to benchmark Gemini models—its harness isn't tuned for Gemini 4+ and produces unrepresentative scores." Context: Google says in its own repo that a harness has to be tuned per model generation, and that its older open-source harness is not.

4. **"Gemini 3.5 Flash in Google Antigravity", May 19, 2026** [P]: "The Antigravity agent harness and Gemini 3.5 Flash have been co-optimized, making Google Antigravity one of the most powerful ways to leverage Gemini 3.5 Flash."

Spoken support: Varun Mohan, Google I/O '26 keynote, May 19, 2026 [P, manual captions, 11/04 pass; not re-pulled today]: "...with Gemini 3.5 Flash having been optimized with the Antigravity harness." Same claim as quote 4, on stage.

### 3.3 Testing "behind every Google product"
- Documented reach of the shared harness [P]: Antigravity 2.0 App and Antigravity CLI ("use the same Antigravity agent harness"), the Antigravity SDK ("the same harness used for Google's internal research"), AI Studio Build ("AI Studio Build now also uses the Antigravity agent harness", I/O post), and enterprise ("Same agent harness, same core product surfaces", enterprise post, May 19). The I/O developer keynote adds Gemini Spark and Gemini API managed agents [P, 11/04 pass].
- Outside it: **Gemini CLI** stays a separate open-source harness for enterprise and paid-API users; **Jules** runs until Dec 31, 2026; **Gemini Code Assist** agent mode is still sold to existing customers. "Every Google product" is too broad. "Google's developer tools" is what the blog says.
- **"Tuned with Gemini" is now complicated.** Since Oct 15, 2026 the Antigravity picker "also offers Claude Opus 5.5 and Claude Sonnet 5.5 when your project has access to them" (App v2.24.0 / CLI v1.3.6; [P, 11/04 pass]; the changelog renders in JavaScript and could not be re-read today).
- The co-optimisation claim is made for 3.5 Flash only. The later model posts for 3.6 Flash (Jul 21), 3.7 Flash (Aug 13), 3.8 Flash (Sep 1) and Gemini 4 Argon (Oct 13) do not mention the harness at all [P by absence, all five fetched today].

### 3.4 Shipped work that matches, and work that complicates it
Matches [P]: one harness across App and CLI; SDK (Apache 2.0) "extend the same harness"; Gemini CLI consumer access moved to Antigravity on June 18, 2026; Jules wound down "to unify our agentic coding efforts" (11/04 pass).
Complicates: Claude models in the picker (Oct 2026); the closed Antigravity CLI replacing an open-source Gemini CLI, with no reason given (transition post does not mention open source, 11/04 pass); `/browser` is a manual switch because "agents were still not capable enough to determine exactly when to be using the browser" (Antigravity 2.0 post, [P]). That last one is a harness rule added because the model fell short, which is honest but runs against "the model will handle it".

### 3.5 What Google explicitly rejects [P]
- Both visibility extremes: "either they show the user every single action and tool call the agent has made or they only show the final code change ... Neither engenders user trust" (launch post, Nov 18, 2025, **older than 6 months**).
- Remote-only agents without feedback: "A core failing of a remote-only form factor is the inability to iterate easily with the agent." (same post)
- Agent tied to a repository: "We've also removed the tight coupling between agent and repository." (Antigravity 2.0, May 19, 2026)
- Several separate products: "pouring our energy into a single product built for today's multi-agent reality" (Gemini CLI transition post, May 19, 2026; 11/04 pass).

### 3.6 Verdict
**Reword. Swap the spoken quote for the blog line.**
- Suggested aim: **"One harness, co-developed with Gemini, shared across Google's developer tools."**
- Suggested lead quote (documented): "a single, cohesive developer product offering that leverages a shared agent harness co-optimized with Gemini models" (Antigravity Team, May 19, 2026). Varun Mohan can stay as the spoken version.
- Add the honest footnote: since October, Antigravity also offers Claude models, and Google's posts on later Gemini models do not repeat the co-optimisation claim.

---

## 4. GitHub and Microsoft (Copilot)

### 4.1 Stated philosophy, from GitHub and Microsoft's own blogs and docs

**One harness, maintained by GitHub and Microsoft and shared by every Copilot surface, that works across many model families and picks or combines models per task. The goals they name are speed, token efficiency, predictability and built-in governance. Developers stay accountable for what ships.**

### 4.2 Quotes

1. **Tina Schuchman (CVP, Foundry) and Vladimir Fedorov (CTO, GitHub), "Introducing the Microsoft Copilot harness: Unlocking the potential of truly multi-model agentic work"**, Oct 28, 2026 [P], https://blogs.microsoft.com/blog/2026/10/28/introducing-the-microsoft-copilot-harness-unlocking-the-potential-of-truly-multi-model-agentic-work/
   - Opening line: "If you want to compete, you need to be multi-model. And if you want to take advantage of everything that different AI models have to offer, you need a great harness."
   - "Instead of doing the work to keep up with and eval new models, lean on us to intelligently route work to the right model or models based on the task."
   - "A unified harness lets us ship faster, learn faster, and improve Copilot over time."
   - "With the Copilot harness, Microsoft runs the agent loop and sandbox, with governance and optimization built in from day one. You bring the instructions, skills, tools, and model choice."
   - Context: the post launches the harness as a managed Foundry service for people building agents. It says the harness "powers Copilot Code, Copilot Studio, the GitHub Copilot app, the CLI, VS Code, and more". The "runs the agent loop and sandbox" line is about the hosted Foundry offering. For a developer at the bank, the CLI and VS Code run the harness locally.

2. **Shibani Basava and Carlos Castro, "Evaluating performance and efficiency of the GitHub Copilot agentic harness across models and tasks"**, GitHub Blog, June 25, 2026 [P], https://github.blog/ai-and-ml/github-copilot/evaluating-performance-and-efficiency-of-the-github-copilot-agentic-harness-across-models-and-tasks/
   - "A harness should be fast, token-efficient, and predictable for developers. That's what we designed GitHub Copilot's agentic harness to do."
   - "While the model provides the raw intelligence, the harness shapes how effectively that intelligence is applied."
   - "Improve the harness, and every surface benefits."
   - Context: the Copilot harness specifically. This is GitHub's clearest design-goal statement.

3. **Jay Parikh, "GitHub Universe 2026: Evolving every layer of the stack"**, GitHub Blog, Oct 28, 2026 [P], https://github.blog/news-insights/company-news/github-universe-2026-evolving-every-layer-of-the-stack/
   - "Different tasks need different models. Developers shouldn't have to manage every model choice to get the right result at the right price." (Context: the Copilot Fusion section, i.e. the model router.)
   - "Developers set the direction, make decisions, and stay accountable for what ships. Agents implement and verify changes."
   - Byline shows "Jay Parikh @jayparikh". His title (EVP, Microsoft CoreAI) comes from the 11/04 pass, not from this page.

4. **Stephen Toub, "Migrating the GitHub Copilot runtime to Rust, using Copilot"**, Sep 16, 2026 (updated Sep 23) [P], https://github.blog/ai-and-ml/generative-ai/migrating-the-github-copilot-runtime-to-rust-using-copilot/
   - "These are very different products, and none of them wants to or should need to implement everything that goes into a production agent harness. They want all of the intelligence, security, reliability, and performance, and they want it shared so that a fix in one place fixes it in all of them."
   - Design requirements listed: a runtime "that does not include the TUI", "minimal dependencies and minimal overhead", "cleanly embedded in-process", usable by "all six Copilot SDK language versions". Rust was chosen for "embedding through a C ABI, low startup and steady-state overhead, and predictable resource use."

Also confirmed today [P]: VS Code Wrapped (Oct 28, 2026), "Access to multiple models remains one of Copilot's pillars"; rubber-duck post (McKenna and Perz, Apr 6, 2026, **older than 6 months**), "a model reviewing its own work is still bounded by its own training biases: the same training data and techniques, the same blind spots"; VS Code docs "Understand agent harnesses" (undated), "VS Code supports multiple agent harnesses, including Copilot, Anthropic Claude, and OpenAI Codex. The Copilot harness uses a shared runtime for core capabilities and more consistent behavior across VS Code, GitHub Copilot CLI, and the GitHub Copilot app." The GitHub Docs page "About GitHub Copilot CLI" states no design principles (no hit for "harness", "principle" or "philosophy").

### 4.3 Shipped work that matches, and work that complicates it
Matches: Fusion router GA (Oct 28, 2026; 11/04 pass); rubber duck cross-family reviewer (Apr 2026) [P]; one runtime behind CLI, app, VS Code, Visual Studio, cloud agent and code review (Rust post) [P]; Copilot harness made the VS Code default in 1.143 (11/04 pass); harness study claiming "effective parity" with vendor harnesses at lower token use [P].
Complicates:
- **Open in 2025, closed in 2026.** In 2025 VS Code said it open-sourced its AI code because "Large language models have significantly improved, mitigating the need for "secret sauce" prompting strategies" and pledged "open, collaborative, and community-driven" [P, May 19, 2025, **older than 6 months**]. The 2026 shared runtime is closed (CLI licence allows redistribution only "in unmodified form"; 11/04 pass). Neither the Rust post nor the Oct 28 Microsoft post mentions licensing [P by absence, 11/04 pass]. Openness now rests on protocols and the MIT SDK clients.
- **Choice vs routing.** "Access to multiple models remains one of Copilot's pillars" sits next to "Developers shouldn't have to manage every model choice". Both hold, since the picker remains, but the direction is towards GitHub choosing.
- **Multi-harness vs one harness.** The VS Code docs support Claude and Codex harnesses, but enterprise policy `temporaryAllowLocalHarness: false` "prohibits Local, Claude, and Codex harnesses" (1.143; 11/04 pass). For a bank, the one-harness reading is the one that applies.
- **"Runs it for you".** True for the cloud agent and Foundry. For the CLI and VS Code the harness runs on the developer's machine. GitHub maintains it, but does not host it.

### 4.4 What they explicitly reject [P]
- Maintaining your own harness or router: "building your own harness or model router to keep up can be painful and slow" (Microsoft, Oct 28, 2026).
- One model checking its own work: "the same blind spots" (rubber duck, Apr 2026).
- Each product writing its own agent loop: "none of them wants to or should need to implement everything that goes into a production agent harness" (Toub, Sep 2026).
- Secret-sauce prompting as a moat (2025, **older than 6 months**). Their own 2026 closed runtime is in tension with this.

### 4.5 Verdict
**Keep, with a small reword.**
- Suggested aim: **"Maintain one harness for every Copilot surface, and send each task to a suitable model."** ("Maintain" in place of "run", because the CLI and VS Code run it locally.)
- Quote: Parikh "Different tasks need different models." is verified and in context. Stronger openers: "If you want to compete, you need to be multi-model." (Schuchman and Fedorov), or the design goals "A harness should be fast, token-efficient, and predictable for developers." (Basava and Castro).
- Keep the open-vs-closed tension on the slide or in the notes. It is the one honest caveat a bank audience will care about.

---

## 5. Strongest single documented statement per maker

| Maker | Statement | Source | Tag |
|---|---|---|---|
| Anthropic | "agent harnesses encode assumptions about what Claude can't do on its own, but those assumptions grow stale as Claude gets more capable." | Lance Martin, claude.com, Apr 2, 2026 (older than 6 months). Current alternative: "Most of the time, you want Claude to decide." (Claude Code best-practices doc, live) | [P] |
| OpenAI | "Harness design can materially change results: on ARC-AGI-3, retained reasoning and context compaction raised GPT-5.6 Sol's score from 13.3% to 38.3% while reducing output tokens sixfold." | Bonamy and Choi, developers.openai.com, Aug 19, 2026 | [P] |
| Google | "At Google, we drive the most long-term value to our users by having a single, cohesive developer product offering that leverages a shared agent harness co-optimized with Gemini models." | Antigravity Team, antigravity.google, May 19, 2026 | [P] |
| GitHub/Microsoft | "If you want to compete, you need to be multi-model. And if you want to take advantage of everything that different AI models have to offer, you need a great harness." Paired with "A harness should be fast, token-efficient, and predictable for developers." | Schuchman and Fedorov, Oct 28, 2026; Basava and Castro, Jun 25, 2026 | [P] |

A contrast worth showing: Anthropic's own Claude Code tool-design post says "it's useful to stick to a small set of models to support that have a fairly similar capabilities profile" (Apr 10, 2026), and Lance Martin's post says "Don't change models" within a session. Copilot is built on the opposite bet: many model families, routed per task. Both are documented, and that difference is a real one to put in front of the room.

## 6. Could not verify today
- Antigravity changelog (renders in JavaScript): the Claude Opus/Sonnet 5.5 line relies on the 11/04 pass.
- openai.com posts ("Harness engineering", "Unrolling the Codex agent loop"): HTTP 403 again.
- Gabriel Chua's LinkedIn original: not fetched; quote is via Willison [S].
- YouTube caption quotes (Mohan, Sottiaux, Cherny YC video): not re-pulled; tags from the 11/04 pass stand.
- Exact publication day of the making-of page: still only secondary (about Jul 7, 2026).


# Part 2. Cursor, Cognition, Amp, Factory, AWS Kiro, JetBrains


## What six harness makers say their philosophy is (checked 2026-11-05)

## Summary table

| Maker | What the deck says now | Verdict | Strongest own-words statement |
|---|---|---|---|
| Cursor | "Own the model as well as the harness" + "…we're training a significantly larger model from scratch…" | **Reword.** The quote is a one-line announcement in a model release post. It shows what Cursor is doing, not what it believes. Cursor never uses the words "own the model". It does name the model as one of three layers it now has in place. | "With Cursor 3, we have the foundational pieces in place—model, product, and runtime—to build more autonomous agents and better collaboration across teams." (Truell and Asif, Apr 2, 2026, older than 6 months) |
| Cognition | "Combine models for each task, its own included" + Series E quote | **Keep.** It is a fair summary, repeated in four Cognition posts. A product post gives a better quote than a funding post. | "From the beginning, Devin has been built to use the best model for each task instead of being tied to a single model." (Wu and Wang, Jun 2, 2026) |
| Amp | "Build for this year's best models, and drop what older ones needed" + Neo quote | **Keep, with a light tweak.** Amp itself labels the quote "A core principle behind the rebuild". The ellipsis cuts "and what they will be able to do in the future", so "this year's" undersells it. | "build for what the frontier models can do now, in 2026, and what they will be able to do in the future. Do not build for what once was." (Amp, May 6, 2026) |
| Factory | "We believe the best agent harness is one built for every model" (speaker notes only) | **Keep.** Verbatim, and it is the post's stated thesis. Caveat: "built for every model" means *tuned separately for each* model. | "Factory is model-independent by design. We believe the best agent harness is one built for every model…" (Factory Research, Oct 29, 2026) |
| AWS Kiro | "Let models suggest changes, and let fixed rules decide" + kiro-trace quote | **Reword.** The quote is verbatim but describes only kiro-trace, Kiro's in-house loop for improving its *own* harness. It is not about how Kiro treats a model's output in your session. Kiro's headline philosophy is spec-driven development. The "fixed rules decide" idea does appear widely across Kiro's 2026 posts (Cedar, kernel sandbox, Lean, CI gates), so the aim can stay close to the current wording if the label changes. | "developers deserve better than vibe coding. They deserve tools that help them think clearly, build confidently, and ship production-ready software without trading speed for quality." (Deepak Singh, Jul 14, 2026) |
| JetBrains | "Run whichever vendor's agent you choose, and keep a person accountable" + 3:00 am quote | **Keep.** Both halves are stated principles in the CEO's post. Optionally swap in the sentence just before the 3:00 am line, which states the principle directly. | "Multi-vendor support is a foundational design principle of JetBrains Air" and "while the work can be delegated, accountability cannot." (Skrygan, Sep 22, 2026) |

---

## 1. Cursor (Anysphere, a SpaceX subsidiary since Aug 14, 2026)

### 1.1 Stated philosophy (own writing only)

Cursor says software is moving into a "third era" where fleets of agents work on their own. Cursor's job is to help developers "build the factory that creates their software", and the human role becomes defining the problem and setting review criteria. To get there it builds every layer itself (its words: "model, product, and runtime"). It tunes the harness on live traffic, and it feeds what the harness learns back into training its next models.

### 1.2 Quotes (all [P], matched on the live page 2026-11-05)

1. **"As a result, Cursor is no longer primarily about writing code. It is about helping developers build the factory that creates their software."** Michael Truell (CEO), "The third era of AI software development", Feb 26, 2026 (older than 6 months). https://cursor.com/blog/third-era. Context: company direction. Same post: **"The human role shifts from guiding each line of code to defining the problem and setting review criteria."** That sentence comes from the cloud-agents section, about why artifacts (logs, video, previews) make it practical to run agents in parallel.
2. **"With Cursor 3, we have the foundational pieces in place—model, product, and runtime—to build more autonomous agents and better collaboration across teams. We will also continue to invest in the IDE until codebases are self-driving."** Michael Truell and Sualeh Asif (co-founders), "Meet the new Cursor", Apr 2, 2026 (older than 6 months, by about a month). https://cursor.com/blog/cursor-3. Context: the closing section, "The best way to code with AI". This is the nearest Cursor comes, in its own words, to "own the model as well as the harness". The same post says: "we forked VS Code instead of building an extension so we could shape our own surface."
3. **"The harness gives us direct control over how each request is assembled, how context is reused, and when work is divided across agents."** and **"Over time, we continue to add and remove instructions as new models require new guidance, which then flows into the training of future models. Leveraging A/B tests on a large user base is crucial to effectively optimizing the harness for real traffic."** Jediah Katz, Connor O'Keefe and Calvin Yee, "Improved token efficiency for longer agent runs", Sep 23, 2026. https://cursor.com/blog/improved-token-efficiency. Context: harness design. This is the most recent primary statement that Cursor treats harness and model as one loop.
4. **"We will have access to the largest fleet of GPUs in the world, giving us the compute to build stronger models that are also more economical to run. This means we can provide customers with more capable models at lower cost."** Cursor Team, "Cursor is now a part of SpaceX", Aug 14, 2026. https://cursor.com/blog/joining-spacex. Context: the acquisition. It is about models and cost, not harness design.

The deck's current quote, re-checked: **"Together with SpaceXAI, we're training a significantly larger model from scratch, using 10x more total compute."** Cursor Team, "Introducing Composer 2.5", May 18, 2026, https://cursor.com/blog/composer-2-5 [P]. Context: a single paragraph in a model-release post, placed right after "Composer 2.5 is built on the same open-source checkpoint as Composer 2, Moonshot's Kimi K2.5." It announces a training run and gives no reason for it. It is not stated as a principle.

Also confirmed today [P]: "Constraints are more effective than instructions." (Wilson Lin, "Towards self-driving codebases", Feb 5, 2026, older than 6 months, https://cursor.com/blog/self-driving-codebases). The full line continues: "'No TODOs, no partial implementations' works better than 'remember to finish implementations.' Models generally do good things by default. Constraints are defining their boundaries." Context: principles for Cursor's multi-agent research system, not the shipping product.

Anysphere's own site, today: "Cursor is an applied research lab working on the future of programming." (https://anysphere.inc) [P].

[R] The blog index shows a pull quote, "We're building toward a future of self-driving codebases, where agents merge PRs, manage rollouts, and monitor production." credited to "Towards self-driving codebases". That sentence is not in the post text we fetched. Treat it as blog-index copy, not as a quote from Lin's post.

### 1.3 Shipped: matches and complications

- Matches the "own every layer" reading: Tab, Composer 1/2/2.5 trained inside the Cursor harness. Cursor calls Grok 4.7 "our most capable model for long-running coding and knowledge work" (https://cursor.com/blog/grok-4-7, Sep 21, 2026) [P]. Origin code hosting (Aug 17), Agent SDK GA (Oct 20), Self-Hosted Machines (Sep 2). Embeddings index dropped for a grep index (Jul 2026).
- Matches "factory / human sets the criteria": Projects (Sep 10, 2026), whose coordinator "doesn't write code itself but directs other agents that do" [P]. The same post: "Early on, you review each PR closely. As the fixes hold up, you review less" [P].
- **Complications:**
  - Composer 2 and 2.5 are built on Moonshot's open-weight Kimi K2.5, so "own model" so far means post-training someone else's base.
  - Cursor still sells Anthropic, OpenAI and Google models at Premium tier and above. "Own the model" does not mean "only our model".
  - The from-scratch model has not been announced as shipped under any name (round 5 file A7).
  - Factory's Oct 29 post says "Cursor isn't shown: it has no access to OpenAI models" in its GPT-6.1 Sol chart [P on factory.com]. That is a competitor's claim and contradicts Cursor's own models list (round 5 A7). Don't use it without checking.

### 1.4 What Cursor rejects, in its words

- Prohibition-heavy prompts: "Instead of long lists of 'DO NOT do this,' 'You must,' or 'Important' instructions, we could simply define how a tool behaves and models would generally comply." (Sep 23, 2026) [P].
- Judging only on hard evals: evals "often represent 'hard' problems and don't properly reflect the true distribution of user requests" (Sep 23, 2026) [P].
- Earlier rejections, all older than 6 months (round 5 A8): shared-file locking for agent swarms, prompt-based compaction, embeddings for search.

### 1.5 Verdict: reword

"Own the model as well as the harness" is **our inference**. It is supported by what Cursor does and by one Cursor sentence listing "model, product, and runtime" as its foundations. Cursor's stated aim is the "factory" and "self-driving codebases", with owning the stack as the means. The current quote is a training announcement, so it doesn't show a philosophy.

Suggested replacement:
- **Aim:** "Build every layer itself, from model to cloud runtime, so agents can work on their own."
- **Quote (preferred):** "…we have the foundational pieces in place—model, product, and runtime—to build more autonomous agents…" Truell and Asif, Cursor 3, Apr 2026 (flag: about seven months old).
- **Quote (newer alternative):** "…new models require new guidance, which then flows into the training of future models." Cursor, Sep 2026.
- Fix in the speaker notes: the body says "a much larger one"; the page says "significantly larger".

---

## 2. Cognition (Devin, Devin Desktop, Devin CLI)

### 2.1 Stated philosophy

Cognition calls itself "an independent agent lab". It uses whichever models suit each task, including its own SWE models, and it now pairs a frontier "lead" model with a cheaper "sidekick" in one harness so that "frontier intelligence is always in charge". It judges cost per task, not per token. On multi-agent systems it allows helper agents but "writes stay single-threaded". It runs agents in full VMs, not containers. The engineer's job shifts to "agent management".

### 2.2 Quotes (all [P] today)

1. **"It is also why we are building Cognition as an independent agent lab. We can choose and combine the models best suited to the work, including our own, rather than tie customers to one provider."** The Cognition Team, "Do it all with Devin: Announcing our Series E", 2026-09-08. https://cognition.com/blog/series-e. Context: a funding announcement. The first sentence ties the model claim to independence as a business strategy. It isn't presented as a harness design note, but it is consistent with product posts.
2. **"From the beginning, Devin has been built to use the best model for each task instead of being tied to a single model."** Scott Wu (CEO) and Jeff Wang, "Introducing Devin Desktop", 2026-06-02. https://cognition.com/blog/introducing-devin-desktop. Context: product design; the post goes on to extend the same idea to running any ACP agent inside Devin Desktop. Same post: **"the work of software engineers is shifting towards agent management."**
3. **"At Cognition, we specialize in routing across frontier models without sacrificing intelligence."** and **"The age of using one model for all of your work is coming to an end."** The Cognition Team, "Devin Fusion", 2026-06-29. https://cognition.com/blog/devin-fusion. Context: harness design (the "multi-model harness").
4. **"The Fusion architecture ensures that frontier intelligence is always in charge. We don't assign tasks to a cheaper model hoping that the routing decision was correct. The lead always reviews the work, identifies problems, and can take control back when the sidekick is out of its depth."** No named author, "Introducing Fusion in Devin Desktop & CLI", 2026-09-11. https://cognition.com/blog/local-fusion. Context: harness design.

Supporting lines [P]:
- "Devin is model-independent — we use the right model for each task, helping customers optimize price performance." (Scott Wu, AI Productivity Guarantee, 2026-06-04)
- "multi-agent systems work best today when writes stay single-threaded and the additional agents contribute intelligence rather than actions." (Walden Yan, 2026-04-22, older than 6 months, https://cognition.com/blog/multi-agents-working)
- "Containerized agents can't complete real engineering work" (a section heading, The Cognition Team, 2026-04-23, older than 6 months, https://cognition.com/blog/what-we-learned-building-cloud-agents)
- "One of our key findings is that using more expensive models can make the entire system cheaper." (local-fusion, 2026-09-11)

[R] Correction to round 5: "When the judgment is the deliverable, delegating it backfires." was struck as "not on the page" for Joon Hee Lee's Jul 13 post. It **is** on the Devin Fusion post (2026-06-29), as the caption to a worked example where Fusion's score fell from 54 to 27. It is usable, attributed to that post.

### 2.3 Shipped: matches and complications

- Matches: Devin Fusion (Jun 29; local Sep 11) pairs a frontier lead with a sidekick that can be Cognition's own SWE-2 (e.g. "Fable 5.1 + SWE-2", "Astra + SWE-2" in the Sep 11 tables). SWE-1.7 (Jul 8), SWE-2 (Sep 10) and SWE-2 Flash (Nov 4) are trained by Cognition on open-weight bases. Devin Desktop runs any ACP agent. Managed Devins use a coordinator with child VMs.
- **Complications:**
  - The Series E post says "We believed engineers should operate more like architects and delegate execution to swarms of agents." Walden Yan, Apr 2026: "the unstructured-swarm approach … is mostly a distraction." Probably loose marketing wording, but it is a tension in Cognition's own pages.
  - Model independence has a price: the Fusion post says Fable 5 tuning was incomplete "since access was cut off before we could apply them" [P].
  - All cost and score numbers are vendor-run (FrontierCode is Cognition's benchmark). The Sep 11 chart itself shows Claude Code with Sonnet 5.5 (68.4) scoring above Fusion (68.1).

### 2.4 What Cognition rejects, in its words

- Basic per-prompt model routing: "existing tools for mixing models suck. They look nice on most benchmarks but fail to write code you'd actually merge." and "Model routers often route to a single model for the entire task." (Fusion, Jun 29) [P]. "Model routing is not enough" (section heading, Sep 11) [P].
- Unstructured swarms (Yan, Apr 22, older than 6 months) [P].
- Containers as the isolation boundary (Apr 23, older than 6 months) [P].
- Forcing delegation: "A model coerced into delegating doesn't gain that judgment; it just delegates the wrong things." (Joon Hee Lee, Jul 13) [P].
- Usage metrics: "The industry needs to move from maximizing usage metrics to maximizing outcomes" (Wu, Jun 4) [P].

### 2.5 Verdict: keep

The aim "Combine models for each task, its own included" is accurate and repeated across four Cognition posts. Optional improvements:
- Swap the quote for the Devin Desktop line (a product post, not a funding post), or add Fusion's "frontier intelligence is always in charge" to show the design idea: a strong model stays in charge, and cheap models do the legwork.
- If you keep the Series E quote, the full sentence starts "We can choose…"; the ellipsis at the end drops "rather than tie customers to one provider", which is the point of the sentence. Consider including it.

---

## 3. Amp (Amp Frontier Corporation)

### 3.1 Stated philosophy

Amp builds for what the newest models can do and deletes features that only older models needed. Its 2026 view is that the harness is no longer the bottleneck. What limits results is the task, the context you give, how you review, and how your organisation and codebase are set up. So it pushes for longer leashes, remote isolated machines, and proof of work instead of step-by-step approval.

### 3.2 Quotes (all [P] today; Amp news posts carry author "Amp" in page metadata, Notes carry a named author)

1. **"A core principle behind the rebuild: build for what the frontier models can do now, in 2026, and what they will be able to do in the future. Do not build for what once was."** Amp, "Amp, Rebuilt" (Neo), May 6, 2026. https://ampcode.com/news/neo. Context: harness design. It introduces the switch to automatic compaction, and the same post removes permission prompts. Same post: **"Some features made sense when models needed more babysitting, more manual context management, more careful steering. They don't anymore. When a feature starts tying you to the old way to use agents, it goes."**
2. **"With the newest models, the agent — the prompts and tools you wrap around a model — is no longer the limiting factor."** and **"How you organize your codebase for agents, how your organization uses them — those are now the bottlenecks."** Amp, "The Coding Agent Is Dead", Feb 19, 2026 (older than 6 months). https://ampcode.com/news/the-coding-agent-is-dead. Same post: **"Our only promise was that when the frontier moved, we would move too."**
3. **"What does change your output are three things, none of which is a model: how hard the task is, what context you put in, and how closely you review what comes out."** Amp, "Who Cares About the Model?", Jul 29, 2026. https://ampcode.com/news/who-cares-about-the-model. Context: after switching the default from Claude Opus 4.8 to GPT-5.6 Sol. Same post: "The default is good because someone is paid to care about it, and it doesn't have to be you."
4. **"The cost of producing code has collapsed, which means the response to the risk of shipping bad code should change too, from a system based around mistake prevention to one based around the idea that mistakes are cheap: isolation over permission, quick reversibility rather than careful review, and parallelism instead of queues."** Alex Kemper, "Pave the Road" (Amp Notes), Aug 10, 2026. https://ampcode.com/notes/pave-the-road. Context: an essay by an Amp staff member about engineering process, not the harness itself. It is the clearest statement of Amp's safety stance. The same essay says "as long as you're bouncing down those dirt roads, the next model doesn't matter." **This runs directly against a bank's controls. Present it as Amp's view, not as advice.**

Supporting [P]:
- "If you have the patience to watch your agents work, you're giving them too short a leash." (Less Noise, Sep 25, 2026)
- "Remember last year, when other agents asked you to approve the agent's work step-by-step, edit-by-edit? Amp users realized before anyone else that was dumb and slow, and Amp never did that." (Subscriptions, Jul 18, 2026)
- "It's near-impossible to determine statically whether a tool invocation will be destructive or not." (Neo)

### 3.3 Shipped: matches and complications

- Matches: Neo (May 6) removed handoff, file rollback, user-invoked skills, custom themes, `$` bash and default permission prompts. Editor extensions were killed (Feb 19, dead Mar 5). The Dial (Jul 9) replaced named modes ("The old modes were models in disguise"). Orbs (remote isolated machines) arrived in Jul, and self-hosted orbs on Oct 22. The TUI sidebar was removed (Aug 27).
- **Complications:**
  1. "Build for the frontier" produces reversals, not one-way deletion. Compaction was removed in Oct 2025 ("Handoff") and restored in May 2026. Queue-by-default came in May and was replaced by steer-by-default on Sep 8 ("Steer, Don't Queue"). BYOK was removed in May 2025 and restored free on Sep 13, 2026.
  2. "Who cares about the model" sits beside constant model swaps: the medium default went from Claude to GPT on Jul 9 and back to Claude (Opus 5.5) on Sep 28. Amp's reason is that "small differences compound" across all threads.
  3. Removing approvals did not remove control. Permissions moved into a plugin and a decision-model API, and Enterprise has MCP and model allowlists (round 5 §3.5).

### 3.4 What Amp rejects, in its words

- Step-by-step approval ("dumb and slow").
- Static command checks ("a false sense of security").
- Editor sidebars ("By keeping these new models in an editor sidebar, we restrict them.").
- Manual context management ("No More Manual Context Management", Neo).
- Mistake-prevention processes ("isolation over permission", Kemper).
- Making users pick models ("models in disguise").

### 3.5 Verdict: keep, with a tweak

The quote is labelled by Amp itself as "A core principle behind the rebuild". That makes it the best-documented philosophy line of the six. Suggested tweaks:
- Aim: "Build for what the newest models can do, and delete what older ones needed". This drops "this year's", which the full quote doesn't limit to.
- Consider adding, in the notes, the Jul 29 "three things, none of which is a model" line or Kemper's "isolation over permission". Both are more useful to a bank audience than the deletion list. Kemper's is a staff essay; label it that way.

---

## 4. Factory (Droid)

### 4.1 Stated philosophy

Factory says its harness is model-independent by design. A harness tuned against many models generalises better than one tuned to a single model's quirks. In practice it tunes prompts, tool descriptions and tool-calling mode per model, using an agent-run improvement loop that engineers sign off on. Its company mission is "autonomy" and "self-improving software factories" that enterprises "can control, trust, and measure".

### 4.2 Quotes (all [P] today)

1. **"Factory is model-independent by design. We believe the best agent harness is one built for every model, so our users can choose the best model on the market or let Droid choose the most efficient mix using our auto model router, Factory Router."** Factory Research, "Droid 1.0: Building a Frontier Harness", October 29, 2026. https://factory.com/news/frontier-harness. Context: the post's stated thesis about harness design.
2. **"Building a harness optimized for many models makes the harness better. When you tune against a single model, it's hard to separate real progress from adaptations to that model's quirks."** Same post.
3. The principles every harness change is held to: **"Budget every token, and keep large tool results in files. / Grow the request by always maintaining the prompt cache. / Profile the hot path to inference, and cache anything you can. / Track background work, such as long commands and subagents, and wake the model when it finishes. / When the agent gets stuck, always have a next step ready: nudge, retry, summarize, or stop."** Same post. Also: "Engineers sit at the end of the loop. They read each proposal with its evidence, check it against these principles, and decide what ships."
4. **"We founded Factory in 2023 with the mission to bring autonomy to software engineering and create a world where software builds and improves itself."** Matan Grinberg and Eno Reyes (bylines), "Factory raises $200M at $5B valuation", September 15, 2026. https://factory.com/news/5-billion-valuation. Context: the company mission, from a funding post.

Also [P]: "The rules live in the loop rather than the model, so they hold for every provider Droid supports, and a new model gets them on day 0." (Droid 1.0, on stuck-loop detection).

### 4.3 Shipped: matches and complications

- Matches: per-model tuning ("Droid tunes its prompts, tool descriptions, and tool-calling mode for each model it supports"). Factory Router (June). Droid Core open-weight pool. Script tool (programmatic tool calling) as the default across ten listed models (Oct 29). Factory Private / air-gapped deployment (Sep 18).
- **Complications:**
  - "Built for every model" is not one harness used the same way everywhere. Script mode is on for some models and not others, and line numbering shipped as an opt-in because it raised cost by 32% on Kimi.
  - The head-to-head benchmark is run by Factory itself, with adjustments it describes in the methodology section (round 5 §4.8).

### 4.4 What Factory rejects, in its words

- Tuning to one model ("adaptations to that model's quirks").
- Hand-tuning: "No team can keep up by tuning a harness for each one by hand." [P].
- Standalone tools: "Rather than stitching together fragmented tools and standalone agents, teams using Factory govern a single, trusted system across the entire software development lifecycle." (Sep 15) [P].

### 4.5 Verdict: keep

The quote is verbatim and is the post's central claim. If it moves from the notes onto a slide, add "model-independent by design". When explaining it, say that Factory means tuned for each model, not one setting for all.

---

## 5. AWS Kiro

### 5.1 Stated philosophy

Kiro's public philosophy is spec-driven development. Write down requirements, design and tasks before the agent codes, so intent is explicit, versioned and checkable: "developers deserve better than vibe coding". In 2026 a second theme runs through its engineering posts. Put the decisions in layers the team controls and can check (the spec, a formally verified permission policy, a kernel-enforced sandbox, code-based gates, proofs) rather than relying on the model's judgment.

### 5.2 Quotes (all [P] today)

1. **"A year ago today, we introduced Kiro to the world with a simple belief: developers deserve better than vibe coding. They deserve tools that help them think clearly, build confidently, and ship production-ready software without trading speed for quality."** Deepak Singh (VP DevEx & Agents), "One year of Kiro", July 14, 2026. https://kiro.dev/blog/one-year/. Context: product philosophy.
2. **"A specification is a kind of (version controlled, human-readable) super prompt."** Marc Brooker (VP / Distinguished Engineer), July 15, 2025 (**older than 6 months**). https://kiro.dev/blog/kiro-and-the-future-of-software-development/. The preceding sentence: "the specification tames the chaos of prompt-driven vibe coding on large code bases, moving away from an ad-hoc exercise in prompt engineering, to way for programmers to crisply express their intent to agents." (sic: "to way").
3. **"Models can propose changes, but we use deterministic code to accept or reject them."** Myeongsoo Kim and eight co-authors (Applied Science / Engineering), "How Kiro fixes itself, and how we keep the fixes honest", October 20, 2026. https://kiro.dev/blog/how-kiro-fixes-itself/. **Context: this is about kiro-trace, an internal system that reads Kiro's own runs, proposes changes to Kiro's prompts and tools, and keeps them only if a code-based gate passes them, followed by human code review.** It is a statement about how the Kiro team improves its harness. It is **not** about how the Kiro product handles model output in a user's session. Same post: "Separate the proposer from the judge. Put accept and reject in code the model cannot reach." and "Try removing before adding. The safest wins are often removals, especially as models get better." and "We judge an agent experiment first by what it rejects."
4. **"Closing that gap isn't about adding a better model or tacking on a security review at the end. It's about moving the work earlier, to a layer you fully control: the specification."** Rajdeep Mukherjee (Applied Science) and Debashis Das (Information Security), "Spec it safe", October 30, 2026. https://kiro.dev/blog/spec-it-safe/. Context: adding security requirements to specs. It is the clearest recent link between the spec philosophy and "control lives outside the model". The same post limits its own claim: "It does not verify the generated code, prove the absence of vulnerabilities, or replace SAST, DAST, dependency scanning, or human review."

Supporting [P]:
- "Reads of popular credential paths are denied in the kernel, so an agent that asks for ~/.ssh/id_rsa is simply refused, no judgment call required" and "The tool-call check is necessary but not sufficient on its own" (Mike Landi and Doug Clauson, Local sandboxing, Oct 14, 2026).
- "a single capability-based permission model backed by Cedar, a formally verified policy language" (One agent, Aug 3, 2026).
- "Ordinary non-exhaustive test suites sample behavior; a proof establishes a universal result for the formal model." (Lean post, Nov 2, 2026).
- "How do we build automatic tests and checks strong enough that we trust them more than our own reading? A human cannot read every change, but a pipeline can test all of them, every time, the same way." (Kiro Crew team, "Keeping a software factory stable at 1,000 PRs a week", Oct 26, 2026). This one is a team running Kiro Crew, not a product principle.

### 5.3 Shipped: matches and complications

- Matches: spec workflow (requirements, design and tasks files; EARS acceptance criteria; property-based testing). Cedar permissions (Aug 3). Kernel sandbox on macOS, Linux and Windows (Oct 14). Lean proofs of harness properties: 70 of 96 proved, 18 falsified and reproduced (Nov 2). Spec hardening power (Oct 30).
- **Complications:**
  - "Sandboxing is off by default today." (Oct 14) [P]. Memory is also "off by default for this launch" (round 5). The deterministic controls exist, but users must turn them on.
  - The Kiro Crew team auto-merges "Simple tier PRs" and gave up line-by-line human review (Oct 26) [P]. Fixed rules decide, but in that team's setup a person does not see every change.
  - Kiro is model-agnostic with an Auto router and adds models from Anthropic, OpenAI and open-weight providers ("so you can choose the right model for the job", Jul 14) [P]. Model choice is not part of its stated philosophy.

### 5.4 What Kiro rejects, in its words

- Vibe coding as the end state ("developers deserve better than vibe coding").
- Ad-hoc prompt engineering on large codebases (Brooker, older than 6 months).
- Self-graded improvement loops ("A loop that grades its own fixes would have shipped it.").
- Library-shaped harnesses ("Then you're back to diverging implementations.", Aug 3).
- Relying on a better model or late review for security ("isn't about adding a better model or tacking on a security review at the end").

### 5.5 Verdict: reword

The current aim and quote take a sentence about Kiro's internal harness-improvement loop and present it as Kiro's general philosophy. The idea is not wrong: Cedar, the kernel sandbox, Lean proofs, CI gates and spec hardening all put decisions in checkable code. But the deck should not imply that this one sentence describes Kiro the product. Two options:

- **Option A (closer to Kiro's headline):** Aim "Write down what you want first, then let checks you control decide what passes". Quote: "…moving the work earlier, to a layer you fully control: the specification." Mukherjee and Das, Kiro, Oct 2026. Or the Singh line "developers deserve better than vibe coding" (Jul 2026).
- **Option B (minimal change):** Keep the aim and the kiro-trace quote, but re-attribute it: "Kiro team, on how it improves its own harness, Oct 2026". Add a line in the notes that Kiro's headline idea is spec-driven development.

Speaker-note check: "confirm 70 rules about its own code" is accurate only if framed as 70 of 96 candidate properties proved across 26 functions in three codebases (agent server, Kiro CLI, Kiro Crew).

---

## 6. JetBrains (Junie, Air)

### 6.1 Stated philosophy

JetBrains says agentic development will be multi-vendor, so Air is built to run, see, govern and account for any vendor's agents and models, including but not requiring its own Junie. As code gets cheaper to write, the bottleneck becomes understanding and verifying it. Accountability stays with people and organisations. JetBrains' contribution is "deterministic code intelligence" from the IDE (index, debugger, build, tests), which it says makes any agent cheaper and more accurate.

### 6.2 Quotes (all [P] today; post date 2026-09-22 from the page's datetime attribute)

1. **"Multi-vendor support is a foundational design principle of JetBrains Air, shaping how the system is being built from the outset."** Kirill Skrygan (CEO), "JetBrains Air: Building a System of Products for Agentic Software Development", 2026-09-22. https://blog.jetbrains.com/blog/2026/09/22/introducing-jetbrains-air/. Context: product design. Same post: "That system is based on a core belief that the future of agentic development will be multi-vendor. No single model, agent, or service will be right for every developer, team, or task."
2. **"And while the work can be delegated, accountability cannot. An agent will not get the call at 3:00 am when something breaks. The responsibility for what ships still belongs to the people and organizations that ship it."** Same post, section "The bottleneck is shifting with the work". Context: the 3:00 am line illustrates the principle in the sentence before it. The next sentence: "This is why control becomes harder, not easier, as AI improves."
3. **"As agents take on more of the execution, the bottleneck shifts from producing change to understanding, verifying, and owning it. Code becomes cheaper to generate but more expensive to verify."** Same post.
4. **"We believe that delegating work to an agent should be something you can afford to do often, not just for heroic one-offs. Thus Junie supports any model, without lock-in – and that's how you control cost."** Dmitry Savelev, "Junie: The JetBrains AI Coding Agent Leaves Beta", 2026-06-17. https://blog.jetbrains.com/junie/2026/06/junie-coding-agent-out-of-beta/. Context: Junie's model policy.

Supporting [P]:
- "We build our own agent, and we intend to make it excellent. But JetBrains Air does not require customers to use ours" (Skrygan).
- "That deterministic code intelligence provides a foundation for making agentic work more reliable, efficient, and understandable across different models and agents." (Skrygan).
- "The goal is not more code. It is software that developers, teams, and organizations can understand, verify, and stand behind." (Skrygan, closing line).
- "When something goes wrong, most coding agents add log statements. Junie opens the debugger." and "Junie uses your IDE's semantic index, build configurations, test runners, and debugger, not its own approximation of them." (Junie GA).
- "The Air plugin for JetBrains IDEs is a conduit for agents and subscriptions you already use. It is not an AI provider, and it ships with no agents installed." (Rolink and Shiryaev, Air in IDEs EAP, early Oct 2026, https://blog.jetbrains.com/ai/2026/10/air-in-ides-eap/).

### 6.3 Shipped: matches and complications

- Matches: Air ships with no agents installed and supports "Codex, Gemini, GitHub Copilot, Claude Agent, and Junie out of the box" (Air in IDEs EAP, early Oct) [P]. Air Governance covers policy, cost and audit. Junie can use your Copilot subscription (docs, Oct 30). Junie's plan document is "a first-class artifact" the user approves (GA) [P].
- **Complications:**
  - JetBrains also builds its own stack: Junie, Mellum models, and Junie Local with a model JetBrains "chose and tuned" (round 5 §3.1). Multi-vendor does not mean JetBrains stays out of models.
  - "Keep a person accountable" is organisational accountability, not step-by-step approval. Junie has a "brave mode" that skips approvals, and headless runs "are trusted by design" and load project config without asking (round 5 §3.2).
  - Deck speaker note says "Since November 3 that includes Copilot". The early-October Air in IDEs post already lists GitHub Copilot as supported out of the box. Check what the Nov 3 GitHub changelog item actually adds before keeping that date.

### 6.4 What JetBrains rejects, in its words

- Single-vendor commitment: "Standardizing on one AI vendor today means making a multi-year commitment in a market that won't look the same next quarter." [P].
- Agents bolted into chat: "Orchestrating several tasks concurrently is fundamentally different from having a conversation with AI." [P].
- Println debugging by agents [P].
- "Better prompting" as a substitute for a reviewed plan: "This approach is superior to 'better prompting'" [P].
- The idea that better models remove the need for control: "A more capable model may produce better output. It does not establish organizational policy, preserve provenance, provide cost visibility, or decide who accepts responsibility for the resulting change." [P].

### 6.5 Verdict: keep

Both halves of the aim are stated principles. Optional improvement: use the full two-sentence quote ("…while the work can be delegated, accountability cannot. An agent will not get the call at 3:00 am when something breaks."). The first sentence is the principle and the 3:00 am line is the colour. Or put "Multi-vendor support is a foundational design principle" on the slide and keep the 3:00 am line in the notes.

---

## 7. Corrections to earlier files found in this pass

- [R] round5-cursor-cognition.md B8 strikes "When the judgment is the deliverable, delegating it backfires." It **is** verbatim on https://cognition.com/blog/devin-fusion (2026-06-29), as an example caption. It was only misattributed to the Lee post.
- [R] The Cursor blog index pull quote "We're building toward a future of self-driving codebases, where agents merge PRs, manage rollouts, and monitor production." is not in the text of the post it credits (fetched today).
- Deck speaker notes, Cursor: "a much larger one" should be "a significantly larger one" (the "If asked" section already has it right).
- Deck speaker notes, JetBrains: check "Since November 3 that includes Copilot" against the early-October Air post, which already lists Copilot.
- The Amp quote's ellipsis drops "and what they will be able to do in the future". Fine to cut, but then the aim shouldn't say "this year's".

## 8. Could not verify / not attempted

- The Cursor models page and pricing (Grok-only Plus tier) were not re-fetched today; that rests on the round 5 [P] tag.
- Amp's OpenAI customer story still gives 403 (round 5).
- Factory's HumanLayer post (Nov 4) was not re-fetched.
- No podcasts or interviews were used. Every quote above is from the maker's own blog, docs or notes pages.


# Part 3. Open source (Pi, mini-swe-agent, OpenCode, Goose, OpenHands, Cline, Zed) and enterprise-first vendors


## Harness philosophies, open source and enterprise-first: what the makers actually say (2026-11-05)

**Tags.** [P] read on the live primary page or raw repo file today (2026-11-05) and matched word for word. [P-prior] confirmed [P] in an earlier round5 file on 2026-11-04 and not re-fetched today. [S] secondary. [O] my analysis. "Older than 6 months" = dated before 2026-05-05. Quotes are not spliced: where text is left out I write "(...)". Curly quotes on pages are shown as straight quotes.

---

## 1. Short version

1. **The "person in charge" camp is wrong for Cline and only half right for Zed.**
   - **Cline no longer approves each change by default.** Since 2026-06-25/26 the VS Code extension's default settings for new users auto-approve file reads, file edits, web fetch and MCP. Only commands still ask. Sources: the code, PRs #11840 and #11865 by founder Saoud Rizwan, and an end-to-end test named "File Edit Auto-Approval". The CLI's `--auto-approve` flag defaults to `true` for all tools, except in ACP mode, where it defaults to `false`. Cline's README and docs overview still say every action needs your approval [P]. Cline's own homepage now presents it as "The open agent. One open source agent runtime." [P]
   - **Zed does ask by default.** Its default setting is `"confirm" - Always prompt (default)` for edits, terminal and other gated tools. On top of that, an OS sandbox has been on by default for the agent's terminal since release 1.14 (Aug 5, 2026). So the sandbox is a second layer, not a replacement for approval. The Maki quote is real, but it is one engineer's personal workflow advice from Jan 2026 (older than 6 months), not a product spec [P].
2. **"Build only what you need" is Zechner's personal Nov 2025 line, not Pi's current official wording.** pi.dev and the README now say "minimal, extensible agent harness that you can make your own" and "Primitives, not features". The MCP reversal post (Earendil, Sep 29, 2026) says "the world is not static" [P]. The minimal core survived: four default tools, no sub-agents, no plan mode, no permission system. "No MCP" did not survive.
3. **"Platforms: open base anyone can inspect and extend" fits OpenCode, Goose and OpenHands, but it does not tell them apart.** Pi says "make it your own" and mini-swe-agent says "a hackable tool, not a black box", so the slogan fits every open-source project here. What actually sets the platform group apart, in their own words:
   - **OpenCode:** let models write code and orchestrate, and build every feature as a plugin.
   - **Goose:** "the most hackable agent", vendor-neutral and general-purpose.
   - **OpenHands:** a self-hosted control center that also runs other people's agents.

   Cline now pitches itself the same way ("One open source agent runtime (...) embed it in your own products"), so it belongs in this group.
4. **The OpenHands quote is trimmed and re-capitalised.** The page says "(...) because agent infrastructure should not be a black box." (mid-sentence, lower-case "agent") [P].
5. **Enterprise-first vendors state a deployment-and-accountability philosophy, not a harness-design one.**
   - **Tabnine:** "run entirely within your environment". Its CLI agent is now a Tabnine-branded build of OpenCode, and tabnine.com redirects to Tricentis.
   - **GitLab:** agents run as CI/CD jobs on your runners, inside Anthropic's sandbox runtime, under a "composite identity" that cannot exceed the triggering user's access.
   - **IBM:** guardrails plus human-in-the-loop checkpoints.
   - **Mistral:** sovereignty, "Intelligence you own, not rent."

   For a Copilot-only bank, recommend one comparison slide, not a fourth camp (see §5).
6. **Defaults rarely match the slogans.** This may be the most useful honest point for a bank audience:
   - Mini-swe-agent (the "minimalist") asks before every action by default.
   - Cline (the "person in charge") auto-approves edits.
   - Goose runs "Completely Autonomous" by default, and OpenCode's base policy is allow-all.
   - Pi has no permission system at all and says so plainly.

---

## 2. Verdict table

| Project | Deck camp today | Their own stated philosophy (one line) | Shipped default for approvals / isolation | Verdict |
|---|---|---|---|---|
| Pi | Minimalist | Minimal core you extend yourself: "Primitives, not features" | No permission system; runs as the user; container/VM patterns documented | **Reword** slogan and quote |
| mini-swe-agent | Minimalist | 100x simpler, bash only, the model does the work | CLI asks before each action (confirm mode) by default | **Keep camp**, reword slogan |
| OpenCode | Platform | Any model, privacy, one local service, everything a plugin, let models orchestrate | Base policy allow-all (asks for `.env`); shell has host user's authority | **Keep**, reword |
| Goose | Platform | "Most hackable agent", not bound to any model/protocol/stack, general-purpose | "Autonomous Mode is applied by default"; no OS sandbox documented | **Keep**, reword |
| OpenHands | Platform | Self-hosted control center for any agent; open so you can inspect, modify, decide where it runs | Local by default, no sandbox unless you choose Docker; LLM risk check, confirm on high risk | **Keep**, fix quote |
| Cline | Person in charge | "The open agent": one open-source runtime, every model, no lock-in | VS Code: edits auto-approved, commands ask (since Jun 26, 2026); CLI: auto-approve all by default | **Move** to platforms |
| Zed | Person in charge | Human judgement; agents can't be trusted to judge intent, so ask and enforce limits at the OS | Confirm by default + OS sandbox for terminal on by default + diff review | **Keep, reword** ("ask, then enforce") |
| Tabnine | (absent) | Private, runs entirely in your environment; governance on top of someone else's harness | Admin "tool governance" can prompt or block; harness is OpenCode | Enterprise slide |
| GitLab Duo Agent Platform | (absent) | Agents embedded across the lifecycle; run as CI/CD jobs; agent identity bounded by the user | Remote flows use Anthropic SRT; fail open with warning unless admin requires sandbox (19.6+) | Enterprise slide |
| IBM Bob | (absent) | Guardrails and humans in the loop before speed | Configurable checkpoints "from manual approvals to auto-approve by task type" | Enterprise slide |
| Mistral Vibe | (absent) | Sovereignty: "Intelligence you own, not rent." | CLI default agent `accept-edits` auto-approves edits only | Enterprise slide |

---

## 3. Open-source projects

### 3.1 Pi (Mario Zechner; owned by Earendil Inc. since Apr 2026)

**1. Stated philosophy.** Pi is a deliberately small agent harness. You make it your own by adding extensions or packages, or by asking Pi to build features itself, instead of getting them built in. Safety comes from where you run it (container, VM), not from prompts or approvals.

**2. Quotes**
- "Pi is a minimal, extensible agent harness that you can make your own." README (root and `packages/coding-agent`), https://github.com/earendil-works/pi (raw README last changed 2026-11-02). No author; project voice. [P]
- "Pi ships with powerful defaults but skips features like sub-agents and plan mode. Ask Pi to build what you want, or install a package that does it your way." Same README. [P]
- "Pi is aggressively extensible so it doesn't have to dictate your workflow. Features that other tools bake in can be built with extensions, skills, or installed from third-party Pi packages. This keeps the core minimal while letting you shape Pi to fit how you work." https://pi.dev/ , section "What we didn't build". Undated homepage, live today. Another section on the same page is headed "Primitives, not features". [P]
- "The first thing to remember is that the world is not static." and "We believe the best way to positively influence something is to embrace it." From "You Said No MCP!", https://earendil.com/posts/you-said-no-mcp/ , dated Tue, 29 Sep 2026, signed "Earendil Engineering". Context: explaining why MCP moved into Pi's core. [P]
- "My philosophy in all of this was: if I don't need it, it won't be built. And I don't need a lot of things." Mario Zechner (Pi's creator), https://mariozechner.at/posts/2025-11-30-pi-coding-agent/ , 2025-11-30. **Older than 6 months.** pi.dev still links to this post ("Read the blog post"). [P]
- "Safety comes from limiting the files, credentials, processes, and network services Pi can access and affect if a generated action is wrong or hostile. Watching the transcript, using project trust, and reviewing changes do not create a security boundary." From https://github.com/earendil-works/pi/blob/main/packages/coding-agent/docs/security.md (undated docs, live today). [P]

**3. Shipped behaviour**
- **Matches:**
  - Default tools are `read`, `bash`, `edit`, `write` [P-prior].
  - No built-in sub-agents or plan mode [P].
  - "Pi does not include a built-in permission system for restricting filesystem, process, network, or credential access. By default, it runs with the permissions of the user and process that launched it." (README) [P]
  - Three isolation patterns are documented: Gondolin micro-VM, Docker, OpenShell [P].
  - MCP tools are hidden from the model's context by default ("codemode" exposure) [P-prior]. That is consistent with the 2025 aim of controlling the context.
- **Contradicts:** "pi does not and will not support MCP" (Zechner, 2025-11-30) [P]. The 0.99.0 changelog (2026-09-29) reads "Added codemode, tool search, and MCP support as built-in extensions" [P]. pi.dev now shows the old "No MCP" entry next to "Now with MCP+Codemode (...) Why we changed our minds" [P].
- **Growth beyond "only what I need":**
  - Pi 1.0 shipped with "Pi Durable" (homepage banner: "We've shipped Pi 1.0 with Pi Durable.") [P].
  - The monorepo now also contains `chord`, `pi-telemetry` and `pi-durable` [P].
  - The core stays small, but the product around it is growing.

**4. What it rejects (pi.dev "What we didn't build", live today) [P]**
- "No sub-agents: Spawn Pi instances via tmux, or build your own with extensions, or install a package that does it your way."
- "No permission popups: Run in a container, or build your own confirmation flow with extensions inline with your environment and security requirements."
- "No plan mode."
- "No built-in to-dos."
- "No background bash: Use tmux. Full observability, direct interaction."

(On the page each item is a heading followed by a sentence; the colon is mine.) From the 2025 essay, older than 6 months: "If you look at the security measures in other coding agents, they're mostly security theater." [P]

**5. Verdict: reword.**
- The camp is right; the slogan is dated. "Build only what you need" describes Zechner's 2025 attitude.
- Pi's 2026 official framing is "small core, you shape the rest", and the team openly changed its mind on MCP.
- Suggested line: "Small core, you build the rest."
- Quote options: the README sentence "Pi ships with powerful defaults but skips features like sub-agents and plan mode. Ask Pi to build what you want, or install a package that does it your way." (Nov 2026). Or keep the Zechner quote, labelled "(Nov 2025)" and paired with "the world is not static" (Earendil, Sep 2026).

### 3.2 mini-swe-agent (Princeton and Stanford SWE-bench / SWE-agent team)

**1. Stated philosophy.** Find out how far a radically simple agent gets: bash as the only tool and a linear message history, with the model doing the work rather than the scaffolding. It is meant as a research baseline that is also a usable, hackable command-line tool.

**2. Quotes** (README, https://github.com/SWE-agent/mini-swe-agent , raw README last changed 2026-06-13; no individual author; the team describes itself as "the Princeton & Stanford team behind SWE-bench, SWE-agent, and more") [P]
- "We now ask: **What if our agent was 100x simpler, and still worked nearly as well?**" (bold in the original)
- "Does not have any tools other than bash — it doesn't even need to use the tool-calling interface of the LMs."
- "Back then, we placed a lot of emphasis on tools and special interfaces for the agent. However, one year later, as LMs have become more capable, a lot of this is not needed at all to build a useful agent!"
- "This makes it perfect as a baseline system and for a system that puts the language model (rather than the agent scaffold) in the middle of our attention."
- "Unlike other agents (including our own swe-agent), it is radically simpler, because it:" (followed by the bash-only, `subprocess.run` and linear-history bullets)

**3. Shipped behaviour**
- **Matches:**
  - "Just some 100 lines of python for the agent class".
  - Each action runs independently via `subprocess.run`.
  - Supports Docker/Podman, Apptainer, bubblewrap and others [P].
- **Notable default:** https://mini-swe-agent.com/latest/usage/mini/ : "mini starts in confirm mode by default. To start in yolo mode, you can add -y/--yolo to the command line." In confirm mode, "The LM proposes an action and the user is prompted to confirm (press Enter) or reject" [P]. So the "minimalist" asks before every action by default. That is the behaviour the deck credits to Cline.
- **No contradictions found.** Last release was v2.4.6 (Jul 23, 2026) [P-prior].

**4. What it rejects** [P, README]
- "Some agents are overfitted research artifacts. Others are UI-heavy frontend monsters."
- "The `mini` agent wants to be a hackable tool, not a black box."
- It also rejects custom tools for each job ("Instead of implementing custom tools for every specific thing the agent might want to do, the focus is fully on the LM utilizing the shell to its full potential.") and stateful shell sessions.

**5. Verdict: keep in the minimal camp, reword the slogan.**
- Its own word is "radically simpler", and its point is that the model, not the scaffold, does the work.
- Suggested line for the pair: "Small core; the model does the work." Pi adds "and you extend it".
- Note for the room: mini-swe-agent is mostly a research and benchmark baseline, not a daily IDE tool.

### 3.3 OpenCode (Anomaly, formerly SST)

**1. Stated philosophy.** An open-source coding agent that works with any model and stores none of your code. OpenCode 2.0 adds three things:
- One background service that every client attaches to.
- Nearly every feature built as a plugin.
- A harness that gets out of the way so models can write code and orchestrate subagents themselves.

**2. Quotes**
- "Free models included or connect any model from any provider, including Claude, GPT, Gemini and more." https://opencode.ai/ (undated, live today). [P]
- "OpenCode does not store any of your code or context data, so that it can operate in privacy sensitive environments." Same page. [P]
- "The latest batch of models are incredibly good at orchestration and it is important for harnesses to let them express the full extent of that capability." From "OpenCode 2.0", https://anoma.ly/notes/opencode-2-0/ , published 2026-10-12, no personal byline (credited to "Anomaly"). Context: introducing background subagents and background shell commands. [P]
- "we forced ourselves to implement nearly every OpenCode 2.0 feature as an internal plugin and there are now 80+ of them. This guarantees that the Plugin API stays well maintained." Same note. [P]
- "The models love to write code and OpenCode 2.0 takes advantage of that more than any other coding agent." Same note, on Code Mode. [P]
- Older and now gone from the README: "As models evolve the gaps between them will close and pricing will drop so being provider-agnostic is important." README FAQ, commit 8063e645, 2025-11-20. **Older than 6 months.** The current README (last changed 2026-10-26) has no philosophy or FAQ section, only install, agents and docs links [P today]. [P-prior]

**3. Shipped behaviour**
- **Matches:**
  - Logins for GitHub Copilot and ChatGPT accounts, and "75+ LLM providers through Models.dev, including local models" [P].
  - "All MCP servers in 2.0 are opted into codemode by default." [P]
  - Background subagents and shells [P].
  - A single local service: "When you open up a TUI, the web interface or the desktop app they're all talking to the same central process." [P]
- **Permissive by default (they do not claim otherwise):**
  - Every agent "starts with this ordered base policy": `{ "action": "*", "resource": "*", "effect": "allow" }`, then `ask` for `*.env` and `*.env.*` files [P].
  - "shell runs with the host user's filesystem, process, and network authority." [P]
  - "default policy allows external_directory, so external paths are not prompted unless you add a rule." [P]
- **Nuance on privacy:** the homepage FAQ adds "Your data and information is only stored when you use our free models." [P]

**4. What it rejects**
- Its own old design: "The old API grew haphazardly as we and the world collectively learned what agents are and should be. It was bad." [P]
- Heavy sandboxes for Code Mode: "It can run these scripts natively without the complexity of Node.js VMs or embedding complicated solutions like QuickJS." [P] [O] QuickJS is what Pi uses.
- Provider coupling, in the older README text quoted above.

**5. Verdict: keep in the platform group, reword.**
- OpenCode does not talk about "inspect" at all. Its stated values are any model, privacy, one service, plugins, and letting the model orchestrate.
- Suggested description: "Open runtime, any model, the model orchestrates." Best quote: the "express the full extent of that capability" line (Oct 2026).

### 3.4 Goose (Agentic AI Foundation, Linux Foundation; originally Block)

**1. Stated philosophy.** The most hackable, vendor-neutral agent, governed in the open. It is a general-purpose agent ("not just for code") that adapts to any model, protocol or stack.

**2. Quotes**
- "Our goal is to make goose the most hackable agent available." GOVERNANCE.md, "Core Values", https://github.com/aaif-goose/goose/blob/main/GOVERNANCE.md (file last changed 2026-04-07, **older than 6 months**). [P]
- "Choice: We're not bound to any one model, protocol, or stack. goose is built for choice and open standards, adapting to your tools, workflow, and identity as a creator." Same file. In the original, "Choice" is bold, followed by a colon. [P]
- "Flexible: we prefer open models – but we don't restrict ourselves." Same file. [P]
- "goose is a general-purpose AI agent that runs on your machine. Not just for code — use it for research, writing, automation, data analysis, or anything you need to get done." README (last changed 2026-07-31). [P]
- "Now we can change how an agent behaves without adding another branch to it." Douwe Osinga, https://goose-docs.ai/blog/2026/09/16/agentic-state-machines , Sep 16, 2026. Context: replacing "the classic agent loop with a re-entrant state machine". [P]

**3. Shipped behaviour**
- **Matches:**
  - Part of AAIF at the Linux Foundation [P].
  - 15+ providers, plus Claude, ChatGPT and Gemini subscriptions via ACP [P].
  - "goose Development Kit (GDK)" for building your own agents (docs home) [P].
  - Custom distributions [P].
- **Safety default:** "Autonomous Mode is applied by default." It is shown as a warning on https://goose-docs.ai/docs/guides/managing-tools/goose-permissions [P]. In autonomous mode "goose can modify files, use extensions, and delete files without requiring approval" [P]. Smart approval's read/write classification is "interpreted by your LLM provider" and is a "best effort attempt" [P].
- **Sandbox:** the permissions page no longer mentions any sandbox. Searching the repo for "seatbelt" finds only the 2026-02-23 v1.25.0 release blog. The removal notice recorded on 2026-11-04 is no longer on the page. [P] No OS sandbox is documented today.

**4. What it rejects**
- Being "bound to any one model, protocol, or stack" [P].
- The "classic agent loop" [P].
- The PR as the main way to contribute: "we have to let go of the PR as the main contribution mechanism" (Osinga, 2026-07-30) [P-prior].

**5. Verdict: keep in the platform group.**
- Their key word is "hackable" plus "choice", which is close to the deck's "open base anyone can inspect and extend".
- Note for a bank: it runs autonomously by default, and it is a general-purpose agent rather than a coding-only harness.

### 3.5 OpenHands (All Hands AI)

**1. Stated philosophy.**
- Open, self-hostable infrastructure for running coding agents: OpenHands' own agent or anyone else's.
- You should be able to inspect it, change it, and choose where it runs.
- The engine is an event-sourced SDK with optional isolation.

**2. Quotes**
- "The self-hosted developer control center for coding agents and automations." and "Run OpenHands, Claude Code, Codex, Gemini, Pi, OpenCode, or any ACP-compatible agent across local, remote, and cloud backends." README, https://github.com/OpenHands/OpenHands (last changed 2026-11-03). [P]
- "Agent Canvas is part of the open-source OpenHands platform because agent infrastructure should not be a black box." Olivia Greene, "Introducing Agent Canvas", https://openhands.dev/blog/introducing-agent-canvas , June 16, 2026. The post does not state her role. Context: section headed "Open Source is the point". [P]
- "If agents are going to run real engineering work, developers should be able to inspect how they operate, modify how they behave, and decide where they run." Same post, the next sentence. [P]
- "It gives developers one place to run, inspect, automate, and scale agents without being locked into one backend, one model, or one agent harness." Same post. [P]
- "Optional isolation. The agent runs locally by default but can switch to a sandboxed environment when additional safety or resource control is required." SDK paper, arXiv 2511.03690 v2 (Apr 22, 2026, **older than 6 months**). [P-prior]

**3. Shipped behaviour**
- **Matches:**
  - Agent Canvas runs third-party agents over ACP [P].
  - The SDK is "the engine behind the OpenHands CLI and OpenHands Cloud" [P].
  - Automations triggered by Slack, GitHub, Linear and others [P].
- **Safety default:**
  - Quickstart "Option 1: Without a Sandbox" warns: "the agent will have full access to your filesystem!" [P]
  - Docker, and one Docker container per conversation, are options 2 and 3 [P].
  - The SDK default is an LLM-based risk analyser that asks for confirmation only above "high" risk [P-prior].

**4. What it rejects**
- "Agent Canvas is not a closed coding assistant." [P]
- Lock-in to "one backend, one model, or one agent harness" [P].
- From the paper: mandatory containerisation, and a database-backed state model that "would couple the SDK to a specific storage backend" [P-prior].

**5. Verdict: keep in the platform group, fix the quote.**
- The deck's "Agent infrastructure should not be a black box." changes the case and drops "because". Quote the full sentence, or use the "inspect how they operate, modify how they behave, and decide where they run" sentence, which says the philosophy more completely.
- OpenHands' distinctive move is hosting other agents, which the deck can say in one clause.

### 3.6 Cline (Cline Bot Inc.)

**1. Stated philosophy, now.**
- **Today's pitch:** one open-source agent runtime with every model and no vendor lock-in, used in the editor, the terminal, a desktop app, or embedded in your own product.
- **Human approval:** the README and docs still describe this as the norm. The shipped defaults no longer match (see 3).

**2. Quotes**
- "The open agent" / "One open source agent runtime." / "Use it in your editor, your terminal, or embed it in your own products." / "Open source. Plan-and-Act. Every model. No vendor lock-in." https://cline.bot/ (undated, live today). [P]
- "We've built it around open-source software, open models, and giving developers control over how they work with agents." Etisha Garg, "Cline Desktop", https://cline.bot/blog/cline-desktop-an-open-source-app-for-open-weight-models , 2026-09-14. [P]
- "Choosing a model is only part of getting an agent to work well: the harness determines how it uses tools, manages context, and recovers from errors." Same post. [P]
- "Every file edit and terminal command requires your approval, so you stay in control of what actually changes. Or toggle auto-approve and let Cline run autonomously." README, https://github.com/cline/cline (last changed 2026-10-21). [P]
- "Every action requires your explicit approval. You're always in control." Docs overview, https://docs.cline.bot/cline-overview.md (live today). [P]
- "The legacy harness isn't bad code. It's a period piece." Saoud Rizwan (founder), https://cline.bot/blog/how-we-migrated-11-million-users-to-clines-biggest-harness-upgrade , 2026-09-02. [P]

**3. Shipped behaviour: contradicts the approval claim**
- **What the code defaults to:**
  - `DEFAULT_AUTO_APPROVAL_SETTINGS` in https://github.com/cline/cline/blob/main/apps/vscode/src/shared/AutoApprovalSettings.ts (main, today): `readFiles: true`, `editFiles: true`, `useBrowser: true`, `useMcp: true`, `executeSafeCommands: false` [P].
  - In PR #11840 "fix(vscode): enable auto-approval defaults", merged 2026-06-25 by saoudrizwan, the description says "This PR updates the VS Code app's fresh/default auto-approval settings so every auto-approve action starts enabled by default." It adds "Existing user settings are not migrated or overwritten by this PR; it affects fresh/default state." [P]
  - PR #11865 "fix(vscode): disable command auto-approval by default", merged 2026-06-26, then turned commands back to "ask". It added a test, "does not auto-approve command tools by default". [P]
  - The end-to-end test on main is titled "File Edit Auto-Approval". Its comment says it "asserts the default auto-approval flow: ask row appears without manual approval buttons, the file is modified on disk". [P]
- **CLI:** "`--auto-approve <boolean>` | Set tool auto-approval for all tools (default: `true`; in ACP mode the default is `false`)", https://docs.cline.bot/cli/cli-reference.md [P]. Also: "prompt (...) Default to start in act mode with auto-approve enabled." [P]
- **The docs contradict each other.** The Auto Approve page still recommends "Leave edits, commands, browser, and MCP off until you have a specific reason", https://docs.cline.bot/features/auto-approve.md [P]. Command risk is judged by the model: "Cline does not use a fixed allowlist. The model marks each command with a `requires_approval` flag" [P].
- **Matches the new pitch:** the same `@cline/sdk` runtime runs in VS Code, JetBrains, CLI, Desktop and Kanban, with plugins and hooks [P-prior]. Any provider, BYO key or weights [P].

**4. What it rejects**
- Its own 2024 harness, built to compensate for weaker models ("The harness guarded, compensated, and spelled everything out.") [P].
- Vendor lock-in ("No vendor lock-in") [P].
- Codebase indexing: "We don't index your codebase, and this choice isn't an oversight." (Nick Baumann, 2025-05-27, **older than 6 months**) [P-prior].

**5. Verdict: replace (move Cline).**
- Cline does not belong in a "person approves each change" camp:
  - Its homepage now leads with "open agent runtime".
  - New VS Code installs have auto-approved edits since late June 2026.
  - The CLI auto-approves everything by default.
- Move it to the open-runtime / platform group.
- For a bank, this makes a good honesty example: the README promises approval for every edit, but the shipped default does not. Check settings rather than trusting the README.

### 3.7 Zed agent (Zed Industries)

**1. Stated philosophy.**
- **Human judgement stays central:** "LLMs automate typing, not thinking"; a human in the driver's seat.
- **The harness does not trust the agent to judge what you want.** So by default it asks before acting, and the OS enforces hard limits on the agent's terminal.
- **Direction:** collaboration and review. Zed wants threads to replace pull requests (Delta).

**2. Quotes**
- "In short, LLMs automate typing, not thinking." and "Every line of agent-generated code needs your sign-off before it ships. Treat the code it writes like a PR from an external contributor: it doesn't know your engineering practices, values, or standards, so its code must be placed under stricter scrutiny than you would a colleague's." Mikayla Maki, "On Programming with Agents", https://zed.dev/blog/on-programming-with-agents , January 23rd, 2026. **Older than 6 months.** Her role is not stated on the post. Context: "my framework for thinking about agentic development"; three personal rules for developers, not a product design document. [P]
- "The tension comes from the fact that agents cannot be trusted to determine whether an action is something the user would want." and "Until we do, sandboxing is the best way to constrain an agent's behavior." Cameron Mcloughlin, "Sandboxing", https://zed.dev/blog/sandboxing , August 5th, 2026. [P]
- "These restrictions are enforced by the operating system and do not rely on an agent following instructions." and "Sandboxing is enabled by default for all users, starting on the 1.14 release." Same post. [P]
- "On the flip side, I know that well-designed systems still require a human in the driver's seat." and "Agents can write the code, but deciding what to build, and how to build it still takes human craft and expertise." Conrad Irwin, https://zed.dev/blog/not-building-ai-for-the-money , May 5th, 2026 (right at the 6-month line). [P]
- "We believe that threads will be the new fundamental unit of software development, and the best way to model their state is with deltas." and "Pull requests are the first part of the GitHub workflow we're leaving behind." Nathan Sobo, https://zed.dev/blog/delta-public-beta , September 16th, 2026. [P]

**3. Shipped behaviour**
- **Asks by default (matches the deck):**
  - Zed's default settings file (`assets/settings/default.json`, main) has `"tool_permissions": { (...) // "confirm" - Always prompt (default) "default": "confirm"` [P].
  - The docs say "default — Fallback when no patterns match: "confirm" (default), "allow", or "deny"". Gated tools include `terminal`, `edit_file`, `write_file`, `delete_path`, `move_path`, `fetch`, MCP tools and others. https://zed.dev/docs/ai/tool-permissions [P]
- **Enforced limits on top:**
  - The terminal tool is sandboxed by default (Seatbelt on macOS, Bubblewrap on Linux, WSL on Windows). There are no writes outside project directories, no writes to `.git`, and no network unless you approve [P].
  - The sandbox doc says: "Tool permissions restrict the agent's ability to run certain tool actions in the first place / Once a tool action is actually running, sandboxing restricts what it can do", https://zed.dev/docs/ai/sandboxing [P].
- **Review:** "Review the agent's work in an editable unified diff. Accept or reject all changes before committing them." https://zed.dev/agentic [P]
- **Limits of the sandbox:** "Sandboxing applies only to Zed Agent. It does not sandbox Zed itself, language servers, extensions, tasks, your normal terminal tabs, External Agents, or Terminal Threads." [P] Windows sandboxes "may not prevent all escape attempts" [P].
- **Fetch conflict from round 5 resolved:** `fetch` is "not run inside the terminal OS sandbox" (tools doc) but is limited to approved hosts ("fetch — Hosts which can be accessed", sandbox doc) [P].
- **Tension with Maki's "PR" framing:** Zed's direction is to drop pull requests. Irwin: "Discretized commits, pull requests, and snapshot-based reviews served us well, but they're overhead in a world where agents can produce working code faster than we can review it." [P] Delta keeps human review ("a dedicated review subthread") but not the PR as the mechanism [P].

**4. What it rejects**
- Command rules as a security control: "Fine-grained rules work well as a guideline when dealing with a well-aligned agent. They fall over instantly in the presence of an even vaguely sophisticated attacker." [P]
- Relying on instructions: "Instructions also do very little to protect against prompt injection attacks." [P]
- Using an LLM in place of understanding: "Please don't use an LLM to avoid having to understand the problem you're solving, or how to solve it" (Irwin; the sentence continues after a semicolon) [P].

**5. Verdict: keep Zed in a human-control camp, but reword.**
- The suspicion is half right. The OS sandbox is Zed's distinctive harness move, but it sits on top of ask-by-default, not instead of it.
- Suggested line: "Ask first, then let the OS enforce limits."
- **Quote options:**
  - Best fit for a harness talk: Mcloughlin's "agents cannot be trusted to determine whether an action is something the user would want" (Aug 2026).
  - If you keep Maki, label it "Jan 2026, workflow advice" and keep the colon-trimmed form: "Treat the code it writes like a PR from an external contributor (...)".
- **Copilot anchor:** carried from round5-enterprise-harnesses.md [P-prior]. Copilot's local sandbox is "turned off by default" after its Oct 7, 2026 GA, while Zed's is on by default for its agent terminal.

---

## 4. Suggested regrouping of the open-source camps

The current split mixes two ideas: how big the harness is, and who approves actions. The approval idea does not hold up against shipped defaults. Two options follow.

**Option A (recommended): group by what each project says it is for.**

| Camp | Members | One line (plain English) | Best current quote |
|---|---|---|---|
| Small core | Pi, mini-swe-agent | Keep the harness tiny; the model does the work and you extend the rest | Pi README: "Pi ships with powerful defaults but skips features like sub-agents and plan mode. Ask Pi to build what you want, or install a package that does it your way." (Earendil, README, Nov 2026) or mini: "What if our agent was 100x simpler, and still worked nearly as well?" |
| Open runtime you build on | OpenCode, Goose, OpenHands, Cline | One open runtime, any model, many front ends; build on it or host other agents | OpenHands: "If agents are going to run real engineering work, developers should be able to inspect how they operate, modify how they behave, and decide where they run." (Olivia Greene, Jun 2026) |
| Ask first, enforce limits | Zed | The agent can't judge what you want, so it asks, and the OS fences its terminal | "The tension comes from the fact that agents cannot be trusted to determine whether an action is something the user would want." (Cameron Mcloughlin, Zed, Aug 2026) |

One member in a camp is fine here, because Zed is the only open-source editor agent left standing alongside Cline (Roo shut down, Continue was acquired; see round5-oss-ide-extensions.md).

**Option B (bank lens, as a companion table): group by what happens on a fresh install.**

| Fresh-install default | Who | Evidence (all [P] today) |
|---|---|---|
| Asks before each action | Zed (edits, terminal, fetch), mini-swe-agent CLI | Zed `"default": "confirm"`; mini "starts in confirm mode by default" |
| Auto-approves edits, asks for commands | Cline VS Code (since Jun 26, 2026), Mistral Vibe CLI | Cline `editFiles: true`, `executeSafeCommands: false`; Vibe "`accept-edits`: The default agent. Auto-approves file edits only" |
| Runs everything without asking | Pi, Goose, OpenCode, Cline CLI | Pi: no permission system; Goose: "Autonomous Mode is applied by default"; OpenCode base policy allow-all; Cline CLI `--auto-approve` default `true` |
| OS sandbox on by default | Zed only (agent terminal) | "Sandboxing is enabled by default for all users, starting on the 1.14 release." |

[O] Option B is the more useful slide for bank developers, because it shows that slogans and defaults differ. It also needs no philosophy quotes.

---

## 5. Enterprise-first vendors

Common thread [O]: these vendors sell where the agent runs, who is accountable, and governance. Two of them borrow the harness itself: Tabnine ships OpenCode, and GitLab wraps flows in Anthropic's sandbox runtime.

### 5.1 Tabnine (now owned by Tricentis)

**1. Stated philosophy.** A private agent that runs entirely inside the customer's environment, with organisation-level governance layered on top.

**2. Quotes**
- "Tabnine is a fully private, organization-aware AI coding agent designed to run entirely within your environment." Docs overview, https://docs.tabnine.com/main (page shows "Last updated 4 months ago", so about July 2026). [P]
- "The Tabnine solution can also be deployed in a completely air-gapped environment." https://docs.tabnine.com/main/welcome/readme/architecture/deployment-options ("Last updated 7 months ago", so about April 2026, **older than 6 months**). [P]
- "The Tabnine plugin for OpenCode is Tabnine's distribution of the OpenCode CLI coding agent." and "You use OpenCode's features with Tabnine sign-in, Tabnine-served models, built-in Tabnine MCP servers, and your organization's Tabnine governance applied on top." https://docs.tabnine.com/main/getting-started/tabnine-plugin-for-opencode ("Last updated 1 month ago"). [P]
- "The provider is locked to tabnine, so no other providers appear." Same page. [P]

**3. Shipped behaviour**
- **Matches:** SaaS, VPC, on-prem and air-gapped options [P]. "Tool governance, which can prompt you before the agent edits files or runs commands, or block a tool entirely." [P]
- **Tension with "run entirely within your environment":** the agent harness is now OpenCode (MIT, made by Anomaly).
- **Ownership:** www.tabnine.com returns HTTP 301 to tricentis.com/products (checked today) [P].

**4. What it rejects:** model choice outside Tabnine's list (the provider is locked) [P]. No explicit "we reject X" statement found.

**5. Bank relevance:** high for "air-gap is possible". Low for harness philosophy, since Tabnine's harness is OpenCode.

### 5.2 GitLab Duo Agent Platform

**1. Stated philosophy.**
- Agents are embedded across the software lifecycle.
- Remote agents run as CI/CD jobs on your runners.
- An agent never gets more access than the person who triggered it, and every agent action is attributable.

**2. Quotes**
- "The GitLab Duo Agent Platform is an AI-native solution that embeds multiple intelligent assistants ("agents") throughout the software development lifecycle." and "Instead of following a linear workflow, collaborate asynchronously with AI agents." https://docs.gitlab.com/user/duo_agent_platform/ (live today). [P]
- "Flows executed from the GitLab UI use CI/CD." and "Flows executed in an IDE run locally." https://docs.gitlab.com/user/duo_agent_platform/flows/execution/ [P]
- "agents need to act with access that does not exceed the access of the user who triggered them, or the access that the service account was granted, while maintaining a distinct identity that clearly shows the action was performed by an agent, not directly by the human user." https://docs.gitlab.com/user/duo_agent_platform/composite_identity/ [P]
- "Accountability: The human user's identity is embedded in the token, creating an audit trail that links agent actions back to the person who initiated them." Same page. [P]

**3. Shipped behaviour**
- **Sandbox:** remote flows use "Anthropic Sandbox Runtime (SRT)". If SRT is unavailable, "the flow runs directly with a warning message, unless the sandbox is required." From GitLab 19.6 an admin can require it, and then "the CI/CD job fails instead of running the flow without the sandbox". "Projects cannot turn off the requirement in the agent-config.yml file." https://docs.gitlab.com/user/duo_agent_platform/environment_sandbox/ [P]
- **Composite identity:** generally available in 18.8. It is always on from 18.9 (the off switch was removed) [P].
- **Default model:** the overview page lists "Anthropic Claude Sonnet 4" [P].

**4. What it rejects:** "a linear workflow" [P]. Implicitly, it also rejects agents acting with their own unbounded identity ("This intersectional access prevents privilege escalation.") [P].

**5. Bank relevance:** high. Composite identity, CI-runner execution and "require the sandbox" are the governance ideas a bank will recognise. Compare with Copilot's cloud agent where possible (not researched here).

### 5.3 IBM Bob

**1. Stated philosophy.** Speed without guardrails is risk. How you deploy the model, structure context and keep humans in the loop matters more than raw model capability.

**2. Quotes** (IBM press release, https://newsroom.ibm.com/2026-04-28-introducing-ibm-bob-ai-development-partner-that-takes-enterprises-from-ai-assisted-coding-to-production-ready-software , April 28, 2026, **older than 6 months, by one week**)
- "Fast AI without the right guardrails is not progress. It is just faster risk." Unsigned body text of the release (not a named person). [P]
- "We built Bob around a simple belief: model capability alone isn't enough. How you deploy it, how you structure context, and how you keep humans in the loop is what determines whether AI actually delivers." Neel Sundaresan, General Manager, Automation & AI, IBM Software. [P]
- "Bob's approval model lets developers configure checkpoints that match their workflow, from manual approvals to auto-approve by task type, keeping humans in the loop." Same release. [P]

**3. Shipped behaviour.**
- Product page: "Deploy in customer-controlled environments, including air-gapped environments" and "Engineered trust through automated, auditable guardrails embedded at authoring time", https://www.ibm.com/us-en/products/ai-coding-agent [P].
- At GA, Bob was "generally available as a SaaS offering" [P-prior]. The self-hosted GA date (Sep 24, 2026) is [S].

**4. What it rejects:** "speed without control and transparency is a liability" (Dinesh Nirmal, SVP IBM Software, same release) [P].

**5. Bank relevance:** medium. The message is close to a bank's own risk language. Little about harness mechanics is published.

### 5.4 Mistral Vibe

**1. Stated philosophy.** Sovereignty: you own the models, data and deployment (on-prem, private cloud, or Mistral Cloud with data residency). The CLI is open source.

**2. Quotes**
- "Intelligence you own, not rent." followed by "Customize every layer: models fine-tuned on your data, agents that sharpen with use, and full data residency in any cloud or datacenter. Your intelligence stays yours." https://mistral.ai/products/vibe (live today; the page now covers Vibe for work, formerly Le Chat, and Vibe for code). [P]
- "Enterprise customers can deploy Vibe on-premises, in a private cloud, or on Mistral Cloud with full data residency." Same page, FAQ. [P]
- "Mistral's open-source CLI coding assistant." README, https://github.com/mistralai/mistral-vibe (last changed 2026-11-04). [P]

**3. Shipped behaviour.**
- README: "`accept-edits`: The default agent. Auto-approves file edits only (`write_file`, `edit`)." and "`ask`: Requires approval for tool executions." [P]
- **Correction to round 5:** "Vibe asks before it acts." (Vibe 2.0 post, Jan 27, 2026, "By Mistral", **older than 6 months**) is about clarifying questions, not permissions. The full line is "Multi-choice clarifications: Vibe asks before it acts. When intent is ambiguous, it prompts with options instead of guessing." [P] Do not use it as a safety claim.

**4. What it rejects:** renting intelligence (the tagline). Nothing harness-specific found.

**5. Bank relevance:** medium. "Own, not rent" is a company-wide sovereignty slogan, not a harness philosophy.

### 5.5 Does the bank audience need them?

[O] Yes, but as one slide, not a fourth philosophy camp. Suggested title: "Enterprise vendors sell where it runs and who answers for it". Three columns:
- **Where it runs:** Tabnine air-gapped, IBM air-gapped, Mistral on-prem, GitLab on your runners.
- **Who is accountable:** GitLab composite identity, IBM checkpoints.
- **Whose harness:** Tabnine ships OpenCode; GitLab uses Anthropic SRT.

Anchor on Copilot as the first row, using already-verified round5 facts: managed harness ("Microsoft runs the agent loop and sandbox"); local sandbox off by default. This keeps the deck Copilot-centred. It also answers the question a bank developer will ask: "could we run something like this ourselves, and what would we give up?"

---

## 6. Corrections to earlier round5 files

1. **round5-oss-ide-extensions.md §1.5** "Default: ask" and **round5-synthesis.md / short version** "Cline: approve every edit and command by default [P]" are **refuted** for shipped behaviour.
   - The README sentence is real, but the VS Code default has auto-approved edits since 2026-06-25/26 (PRs #11840, #11865).
   - The CLI `--auto-approve` defaults to `true`, except in ACP mode.
2. **OpenHands quote:** the source sentence is "Agent Canvas is part of the open-source OpenHands platform because agent infrastructure should not be a black box." The deck's capitalised standalone version is a trim. Use the full sentence or mark the cut.
3. **Zed `fetch` conflict resolved:** fetch is not OS-sandboxed, but its hosts are restricted (sandbox doc table).
4. **Goose seatbelt:** the removal sentence quoted on 2026-11-04 is no longer on the permissions page. The page now says nothing about sandboxing. Only the Feb 23, 2026 release blog mentions seatbelt.
5. **Mistral "Vibe asks before it acts"** refers to clarifying questions, not tool approval.
6. **Cline migration post:** on the page, "The legacy harness isn't bad code. It's a period piece." comes before "Cline's original harness was designed in mid-2024 around Claude 3.5 Sonnet" (same paragraph). Fine to quote either alone.
7. **New primary sources not in round 5:**
   - Earendil's "You Said No MCP!" (Sep 29, 2026).
   - pi.dev "What we didn't build" / "Primitives, not features".
   - Pi `security.md`.
   - mini-swe-agent confirm-mode default.
   - Zed default settings `"confirm"` and the sandbox doc.
   - GitLab composite identity.
   - Cline CLI auto-approve default.

## 7. Could not verify / not checked

- Roles of Mikayla Maki and Olivia Greene: not stated on their posts; not looked up elsewhere.
- Whether Cline's new defaults reached existing users: the PR says existing settings are "not migrated or overwritten", so long-time users may still see their old, stricter settings.
- Cline JetBrains and Desktop defaults: not checked; only VS Code (code) and CLI (docs) were checked.
- Zed's `"confirm"` default for external ACP agents: the settings comment says Zed's deny/confirm "still take precedence"; not tested.
- IBM Bob's default approval mode (manual vs auto) in the shipped IDE: not found in the pages read.
- Copilot's own default approval behaviour and any Copilot equivalent of GitLab's composite identity: out of scope here; the Copilot anchor facts are carried from round5-enterprise-harnesses.md.
- Earendil "Values"/"Purpose" pages: not read.
