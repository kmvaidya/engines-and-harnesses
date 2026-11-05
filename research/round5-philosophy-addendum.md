---
url: https://www.youtube.com/watch?v=PQU9o_5rHC4, https://rosetta.to/u/ycombinator/inside-claude-code-with-its-creator-boris-cherny, https://every.to/p/how-codex-happened/companion/transcripts.md?edition=gift, https://every.to/p/how-codex-happened/interviews/andrew/?edition=gift#final-20261015-0004, https://every.to/p/how-codex-happened/interviews/alex/?edition=gift#final-20261015-0185, https://every.to/p/how-codex-happened/interviews/mia/?edition=gift#final-20261015-0077, https://every.to/p/how-codex-happened/interviews/greg/?edition=gift#final-20261015-0010, https://www.youtube.com/watch?v=Fls_onRviPM, https://simonwillison.net/2026/Sep/29/openai-devday-2026-live-blog/, https://openai.com/index/devday-2026-recap/, https://www.youtube.com/watch?v=sLSTM9znQNs, https://www.youtube.com/watch?v=9WiBJRO84yY, https://antigravity.google/blog/introducing-google-antigravity-2, https://antigravity.google/blog/google-io-2026, https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/, https://www.youtube.com/watch?v=wYSncx9zLIU, https://www.youtube.com/watch?v=aqmpZocmR8o, https://github.blog/ai-and-ml/generative-ai/migrating-the-github-copilot-runtime-to-rust-using-copilot/, https://blogs.microsoft.com/blog/2026/10/28/introducing-the-microsoft-copilot-harness-unlocking-the-potential-of-truly-multi-model-agentic-work/, https://github.com/github/copilot-sdk, https://github.com/github/copilot-cli/blob/main/LICENSE.md, https://github.com/github/copilot-cli/issues/83, https://github.com/github/copilot-cli/issues/3241, https://code.visualstudio.com/blogs/2025/05/19/openSourceAIEditor, https://anoma.ly/notes/opencode-2-0/, https://opencode.ai/changelog, https://thenewstack.io/opencode-2-shared-service/, https://cognition.com/blog/swe-2, https://cognition.com/blog/swe-grep, https://cognition.com/blog/introducing-devin-desktop, https://www.warp.dev/blog/the-factory-stack, https://blog.kilo.ai/p/thank-you-roo, https://blog.kilo.ai/p/new-kilo-for-vs-code-is-live, https://www.youtube.com/watch?v=96jN2OCOfLs, https://www.youtube.com/watch?v=kwSVtQ7dziU, https://mitchellh.com/writing/my-ai-adoption-journey, https://arxiv.org/pdf/2609.00006
fetched: 2026-11-04
fills: gaps flagged by the critic in round5-philosophy-direction.md and round5-synthesis.md §4.2, §5
---

# Round 5 addendum: sourced harness philosophy, by family

**Tags.** [P] confirmed on the primary page or official recording (raw page text or the uploader's own caption track read by us). [P\*] primary source, but the wording passed through a summariser or through YouTube auto-generated captions (machine transcription, not listened to; cue timestamps are exact, words may be misheard). [S] secondary only. [E] extracted, not cross-checked. [R] refuted or misquoted wording, recorded so nobody reuses it. [O] our analysis. Vendor numbers are marked "vendor claim". Anything before about 2026-05-04 is marked "(older than 6 months)".

**How the transcripts were read.** YouTube caption tracks were pulled with `youtube-transcript-api` and grepped. Where the track is auto-generated (Cherny, Sottiaux, Kundel, Karpathy), quotes are [P\*]. Where the uploader supplied manual captions (OpenAI DevDay keynote, Google I/O keynotes), quotes are [P] unless the captions are visibly garbled. The every.to Codex transcripts were downloaded in full from Every's own markdown export; Every labels them "not certified verbatim transcripts".

## Short version

1. **Cherny's "never bet against the model" is now sourced to the official YC video with timestamps** [P\*]. It is at 00:38:37 of "Inside Claude Code With Its Creator Boris Cherny" (Y Combinator, uploaded 2026-02-17). The "10 20%" figure appears twice (00:08:22 and 00:39:00). The words "wiped out" appear only in the first passage (00:08:26), not next to "never bet against the model". Quote them as two separate passages.
2. **"So we do training on the harness now" is Andrew Ambrosino (Codex design and engineering)**, at 0:58 of his every.to interview transcript, dated Oct 15, 2026 [P on Every's page, with Every's "not certified verbatim" caveat]. This upgrades round5-openai-codex.md's [S].
3. **OpenAI has a clear 2026 harness philosophy in its own voice.** Thibault Sottiaux (Sep 9, 2026): "the harness in a sense is always a little bit ahead of the model" and "over time what we see is like ... the developer message shrinks and then the harness also shrinks" [P\*]. Embiricos: keep the harness "as simple as possible" and "let the model orchestrate as much as possible" [P, Every]. Dominik Kundel (Oct 2026): do not replace the system prompt because the team works "to make sure that the actual prompt is in distribution" [P\*]. DevDay 2026 had no dedicated harness talk that we could find; the keynote mentions the open-source Codex harness in passing (Sam Altman, per Willison's live blog [S]). Kundel's advice is "start with developer instructions", not a ban on custom prompts (see §2.2).
4. **Google's philosophy is co-optimisation of harness and model, said on stage at I/O by Varun Mohan** (May 19, 2026): "Gemini 3.5 Flash having been optimized with the Antigravity harness" [P, manual captions]. No named Google engineer has published a design-philosophy essay on the Antigravity or Gemini CLI harness in 2026 that we found.
5. **GitHub and Microsoft have not explained why the Copilot runtime is closed while the SDK is MIT.** Toub's Rust-port post and the Oct 28 Microsoft harness post say nothing about licensing [P by absence]. The "Open Source?" issue on github/copilot-cli has been open since Sep 27, 2025 with no staff answer [P]. Microsoft's stated pitch is managed service: "Microsoft runs the agent loop and sandbox" [P] (upgraded from [P\*] in the verification pass; raw page read).
6. **OpenCode 2.0's launch note is dated Oct 12, 2026, not Sep 11** (npm 2.0.0 was published Sep 11). It is unsigned ("Anomaly") and says "it is important for harnesses to let them express the full extent of that capability" [P]. No primary 2026 Dax Raad statement was reachable.
7. **Cognition's harness rationale is in its model posts**: retrieval is a subagent with "carefully restricted tool set" co-designed with the model (SWE-grep, Oct 2025, older than 6 months) [P]; SWE-2 (Sep 10, 2026) evaluates each model "using the harness for which it was primarily developed" [P], but only where no public score exists (see §6 correction). Cognition has published no edit-format rationale.
8. **Karpathy in 2026 talks about "agentic engineering" and calls Claude Code and Codex "agent harnesses"** (No Priors, Mar 20; Sequoia, Apr 29) [P\*]. He has not proposed a harness design philosophy. **"Harness engineering" origin stands**: Mitchell Hashimoto, Feb 5, 2026, re-read today [P].

---

## 1. Anthropic (Claude Code)

### 1.1 "Never bet against the model" and the 10-20% scaffolding claim

Source: "Inside Claude Code With Its Creator Boris Cherny", Y Combinator YouTube channel (The Light Cone), uploaded 2026-02-17T07:00:42-08:00 (older than 6 months), https://www.youtube.com/watch?v=PQU9o_5rHC4. YouTube's oEmbed confirms title and channel. The only English caption track is auto-generated, so all wording below is [P\*]. The third-party transcript at rosetta.to (round5-philosophy-direction.md's [E] source) matches the caption track word for word, including its errors.

**Passage A, 00:08:10 to 00:08:48** (Cherny, answering on early use cases; preceded by his "biggest principle in product is latent demand"):

> "There's this other general principle that I think is maybe interesting where you can build for the model and then you can build scaffolding around the model in order to improve performance a little bit and depending on the domain you can improve performance maybe 10 20% something like that and then essentially the gain is wiped out with the next model. So either you can build build the scaffolding and then you know get some performance gain and then rebuild it again or you just wait for the next model and then you kind of get it for free." [P\*]

He continues: "really I think that's why we stayed in the CLI is because we felt there is no UI we could build that would still be relevant in 6 months because the model was improving so quickly" (00:08:39 to 00:08:48) [P\*].

**Passage B, 00:37:43 to 00:39:15** (host at 00:37:36: "Boris, you had other advice for for builders"):

> "don't build for the model of today, build for the model of 6 months from now." (00:37:49 to 00:37:54) [P\*]

> "we have a framed copy of the bitter lesson on the wall. ... what it boils down to is never bet against the model." (00:38:20 to 00:38:39) [P\*]

> "We could make it better as a product and we call this scaffolding. That's all this code that's not the model itself. But we could also just wait like a couple months and the model can probably just do the thing instead. ... engineering work now and you can kind of extend the capability a little bit, maybe 10 20% or whatever in whatever domain ... or you can just wait and the next model will do it." (00:38:45 to 00:39:09) [P\*]

Asked if scaffolding was deleted (00:39:23): "Oh so much. ... We unhip [unship] tools every couple weeks. We add new tools every couple weeks. There's no part of quad code [Claude Code] that was around six months ago." (00:39:26 to 00:39:40) [P\*]

Notes:
- [R] The caption track renders the bitter-lesson summary as "the more general model will always be the more specific model" (00:38:28 to 00:38:33). This is a transcription error for "beat". Quote only from "never bet against the model".
- [R] "Scaffolding gains of 10-20% get wiped out" as a single quote attached to "never bet against the model" is a splice. "Wiped out" is at 00:08:26; "never bet against the model" is at 00:38:37, thirty minutes later, where he says "maybe 10 20% or whatever" without "wiped out". Cite both timestamps or quote Passage A alone.
- [O] Cherny's own framing is a trade-off, not a ban: "always always think in terms of this trade-off where where do you actually want to invest" (00:39:09).
- Upgrade: round5-philosophy-direction.md §1.1 and round5-synthesis.md §4.2 can move this from [E] to [P\*] with the YouTube URL and timestamps.

---

## 2. OpenAI (Codex)

### 2.1 "So we do training on the harness now"

Source: Dan Shipper, "How Codex Happened", every.to, six interview transcripts, all marked "Final interview transcript supplied October 15, 2026". Every's header: "These captures are not certified verbatim transcripts; preserve their provenance and transcription notes." Read in full from https://every.to/p/how-codex-happened/companion/transcripts.md?edition=gift. Tag [P] for "this is what Every published", with the not-verbatim caveat.

**Speaker: Andrew Ambrosino, "Design & engineering"**, passage final-20261015-0004, timestamp 0:58, https://every.to/p/how-codex-happened/interviews/andrew/?edition=gift#final-20261015-0004. Prompt from Shipper (0:28): "harnesses seem to be becoming more and more important."

> "Yes. Many such cases. I see this feedback all the time. And I think one of the great successes of Codex as a team was pairing the product team and the research team together very closely, especially when it came to the harness, right? So we do training on the harness now. We use the harness for far more of our products, including upcoming ones. The Workspace Agents products that we have out uses this." [P]

Same answer, on what moved quality most: "the big jumps that I've seen have been when it's easier to get more context to the model, especially automatically, which is app, it's connectors, it's computer use." and "When the model can verify more of what it has built ... that to me has been, depending on the task, bigger, equal or larger of a jump than model jumps." [P]

Other harness statements in the same set [P, Every]:
- Alexander Embiricos (product), 42:00, #final-20261015-0185: "So broadly, the way we think about the agent is you have to have very clear layers. So okay, model coming through the Responses API, open source harness. This harness we need to do our best to keep as simple as possible, and then have the right primitives for extensibility, and you let the model orchestrate as much as possible." He adds that computer use and browser use are "built as a plugin".
- Mia Glaese, 15:44, #final-20261015-0077: "we can build the model for that and we can build the product and the harness and everything that we need for that together. Because we are thinking about this as a joint thing that we build together."
- Greg Brockman, 6:21, #final-20261015-0010: "having a single agentic implementation, the harness, the connectors, all of those things, each of those are pretty general purpose regardless of what your use case is. So you really want to build them once in a unified way."

### 2.2 2026 OpenAI talks on harness design

**DevDay, Sep 29, 2026.** The official recap at openai.com returned 403 to every fetcher. The keynote video is on OpenAI's channel: "OpenAI DevDay 2026 Keynote (FULL)", uploaded 2026-09-29, https://www.youtube.com/watch?v=Fls_onRviPM. The English track is manual, but garbled at the relevant point. At 00:27:38 to 00:28:00 the captions read: "We want you to have access to the same foundations we have at open AI this. Starts with a codeck harness. It powers codex work and dots. We have put a lot of work into makeing this efficient and it's open scattered showers so you can look under the hood". [P\*] for the passage; the speaker is not named in the captions. Simon Willison's live blog renders the line as "This starts with the open source Codex harness." [S] https://simonwillison.net/2026/Sep/29/openai-devday-2026-live-blog/. [R] "speaker not identified" is superseded: Willison's entry at 10:29 reads "Sam is back. Now talking about "supporting developers" - giving developers access to the same foundations they have at OpenAI. This starts with the open source Codex harness." So the speaker is Sam Altman per Willison [S]; the captions still do not name him. At 00:29:12 the keynote says the new API "includes great components like the harness, multi-agent controls and much more." [P] for those words. [R] The name "Agents API" is not in the captions (they read "a new AP I canner"); the name comes from Willison's "Agents API, now with Computer Use" [S].
- Willison also logs "Our models helped optimize the harness we use for Computer Use" (10:26) and, from the closing session, "Thibault talks about how dots came out of the Codex harness getting more reliable" (16:20) and "Thibault likes using Pi!" (16:25) [S, paraphrase in a live blog]. We found no recording of the closing session.
- [O] We found no DevDay 2026 session dedicated to Codex harness design. The harness appears as infrastructure for Dots, Codex Cloud and the Agents API.

**Thibault Sottiaux on The Pragmatic Engineer**, "Building Codex with Tibo Sottiaux", uploaded 2026-09-09, https://www.youtube.com/watch?v=sLSTM9znQNs. Auto-generated captions, so [P\*].
- 00:37:30 (verification pass: the cue at 00:37:26.96 is the host's question tail and "yeah this is a good question so the uh"; the quoted words start at 00:37:30.72): "the harness in a sense is always a little bit ahead of the model ... you have the model, it's capable of certain things, but then you set it up with like a couple of crutches so that it can actually do the thing um to a level of reliability".
- 00:38:00: "that's the role of the harness, right? is like you know provide guard rails like safety, make it more efficient, make it more like steerable, controllable".
- 00:38:29 to 00:38:59: "maybe you're like oh it doesn't run tests. So you know you have to remind it to run tests and then you know we train a battle [better] model ... and then you know you don't actually have to tell it anymore. So over time what we see is like the system uh the the developer message shrinks and then the harness also shrinks".
- 00:40:07 to 00:40:32: "we always like look at it it's like okay this should this be like a harness change or should this be a model change and if it's a model change like how soon can we have it ... Then we might decide to not even do something in the harness at all and not and just wait for for for the model to to solve it."
- 01:01:50 to 01:02:16: "the harness is a crutch, right? ... slash goal was like necessary to allow like no to keep the the model like on track ... But with the new generation of models like what we're seeing is like you know you don't need SL goal anymore. You don't need a harness around it."
- On open source (00:21:46 to 00:22:20): "fundamentally what you're building is you're building a coding agent. And so we were sort of like thinking about well if you have that you know you're obviously going to point it at itself". On other providers (00:26:18): "building an excellent coding harness is like why would you couple it to your model? That that that felt like sort of like quite disappointing to make that decision."
- [O] This is the closest OpenAI statement to Cherny's: harness code is a temporary crutch that research absorbs into the model. Sottiaux adds a planning step Cherny does not describe: each gap is triaged as "harness change" or "model change" with a timeline.

**Dominik Kundel, "Building on the Codex Harness"**, AI Engineer channel, uploaded 2026-10-09, https://www.youtube.com/watch?v=9WiBJRO84yY (event not named in the metadata; he refers to "the keynote yesterday" and says "otherwise you probably didn't listen to Roman", most likely Romain Huet [O]). Auto-generated captions, [P\*]. The YouTube title confirms the speaker: "Building on the Codex Harness - Dominik Kundel, OpenAI"; the description calls him part of "OpenAI's Codex developer experience team".
- 00:01:13: "the app server is actually the protocol that wraps the Codex harness."
- 00:16:07 and 00:16:35: "ship your own version of the harness."
- 00:17:07 to 00:17:30: "It might feel like you want to immediately rush to I'm going to write my own system prompt, but there is a lot of different things that we constantly have to think about when we're building a harness to make sure that the actual prompt is in distribution and make sure that the agent performs well. And you're losing out on all of that if you're actually jumping in and like writing your own system prompt."
- Context check (verification pass): the advice is softer than "never write your own system prompt". Just before the quote (00:17:06 to 00:17:14) he says "if you are changing the instructions, try to start with ... adding developer instructions rather than changing the base instructions", and he closes with "So be careful there". The words "in distribution" sit at 00:17:24 to 00:17:26. Paraphrase as "start with developer instructions; replacing the base prompt costs you OpenAI's tuning", not as a ban.
- [O] "In distribution" is the co-training argument from the user's side: the prompt matches what the model was trained against, so replacing it costs quality.

---

## 3. Google (Antigravity, Gemini CLI)

- **Varun Mohan, Google I/O '26 Keynote**, Google channel, uploaded 2026-05-19, https://www.youtube.com/watch?v=wYSncx9zLIU. Manual captions with a speaker label ("VARUN MOHAN:" at 00:25:26). [P]
  > "The Antigravity agent harness, the invisible framework for Gemini to perform real world tasks has become much more powerful, with new core primitives such as subagents, hooks, and asynchronous task management. And underpinning all of this are the Gemini models, with Gemini 3.5 Flash having been optimized with the Antigravity harness." (00:27:24 to 00:27:44)
  Earlier in the same segment: "I said, unabashedly agent first." (00:27:14)
- **Developer Keynote (Google I/O '26)**, Google for Developers, uploaded 2026-05-19, https://www.youtube.com/watch?v=aqmpZocmR8o. Manual captions; the speaker is introduced as "Logan" at 00:37:49. [R] "surname not in captions" is wrong: the manual captions label him ">> LOGAN KILPATRICK:" at 00:37:58. [P]
  - Logan Kilpatrick: "Inside Google, we're using the Antigravity Harness to empower our agents to intelligently tackle the most complex tasks. It's the same technology behind Gemini Spark and our coding agent and Google AI Studio. And today, we're making that same Antigravity harness available to you, with managed agents in the Gemini API." (00:38:41 to 00:39:03)
  - Antigravity SDK: "It gives developers and researchers the exact same agent harness optimized for Gemini" (00:49:13). Antigravity CLI: "It gives you the exact same harness, and the same models" (00:55:22).
  - [R] Speaker correction (verification pass): these two lines are not Logan Kilpatrick's. His segment ends by 00:43:19 (">> PAIGE BAILEY: Awesome! Thank you, Logan!"). The SDK line falls in Paige Bailey's segment (the last caption speaker label before 00:49:13 is PAIGE BAILEY at 00:44:58; Anshul is introduced at 00:50:22). The CLI line at 00:55:22 is in the Anshul Ramachandran and Kevin Hou demo (">> ANSHUL RAMACHANDRAN:" at 00:55:00). Attribute as "Google I/O '26 Developer Keynote", not to Logan.
- **Antigravity 2.0 post**, "The Antigravity Team", May 19, 2026, https://antigravity.google/blog/introducing-google-antigravity-2. Main quotes already [P] in round5-google-amazon-jetbrains.md §1.4. One more line: "And we have the momentum of the model and agent harness being co-optimized." Upgraded [P\*] to [P] in the verification pass (raw page text read). The same page also says: "The product, agent harness, and model layers all had to be co-optimized and co-developed" [P].
- **I/O blog post**, "The Antigravity Team", May 19, 2026, https://antigravity.google/blog/google-io-2026: the SDK lets developers "build custom agents using the Antigravity agent harness that has been co-optimized with Gemini" [P] (upgraded from [P\*]; raw page read).
- **Gemini CLI transition post**, Dmitry Lyalin (Group Product Manager) and Taylor Mullen (Principal Engineer), May 19, 2026, https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/ [P; upgraded from P\* in the verification pass, all three quotes found in raw page text, and the words "open source" do not appear on the page]:
  - "we can serve you best by pouring our energy into a single product built for today's multi-agent reality."
  - Antigravity CLI "shares the same agent harness as Antigravity 2.0", "ensuring that all future improvements to core agents are automatically applied wherever you use them."
  - The post does not mention open source or explain why the successor is closed.
- Not found: a 2026 post by the Gemini CLI team on harness design principles (tools, edit format, prompt). [O] Google's stated philosophy is one co-optimised harness behind every surface, and the stated reasons are product consolidation and model fit. Nothing published argues for specific harness mechanics.

---

## 4. GitHub and Microsoft (Copilot)

**Question: why is the Copilot runtime closed while the SDK is MIT?** Answer from primary sources: nobody at GitHub or Microsoft has said.

- Stephen Toub, "Migrating the GitHub Copilot runtime to Rust, using Copilot", GitHub Blog, Sep 16, 2026 (updated Sep 23), https://github.blog/ai-and-ml/generative-ai/migrating-the-github-copilot-runtime-to-rust-using-copilot/. Raw page text searched for "licens", "proprietary", "closed", "open source": no hit in the article body (only site navigation) [P by absence]. What it does say: the runtime is "an agentic harness that can be embedded into applications and services", and products "initially implemented their own agent loop, but have since replaced it with the GitHub Copilot SDK, which is the entry point to the Copilot agent runtime. Doing so enables them to focus on their core business value and leave the details to the runtime." [P]
- Tina Schuchman and Vladimir Fedorov, "Introducing the Microsoft Copilot harness", Microsoft blog, Oct 28, 2026 (blogs.microsoft.com blocked curl; read through a summariser). The post contains no mention of open source, licence, MIT, closed or proprietary [P\* by absence]. Its pitch is a managed service [P\*]. Verification pass: curl returned the page (HTTP 200) on 2026-11-04; all four quotes below match the raw text, the byline reads "Tina Schuchman CVP, Foundry and Vladimir Fedorov, CTO, GitHub", `article:published_time` is 2026-10-28, and the only "licens" hit is the site footer link "Licensing". Upgraded to [P] and [P by absence].
  - "And building your own harness or model router to keep up can be painful and slow."
  - "Now, you can build on the same harness Microsoft and GitHub ship in our own products, and you don't have to maintain it."
  - "With the Copilot harness, Microsoft runs the agent loop and sandbox, with governance and optimization built in from day one."
  - "Instead of doing the work to keep up with and eval new models, lean on us to intelligently route work to the right model or models based on the task."
- Licences [P]: github/copilot-sdk is MIT (GitHub API). github/copilot-cli reports `NOASSERTION`; its LICENSE.md is the "GitHub Copilot CLI License", which permits redistribution only "in unmodified form" and "solely as part of an application or service that provides material functionality beyond the Software itself". The SDK README: "The GitHub Copilot SDK exposes the same engine behind Copilot CLI" and "All SDKs communicate with the Copilot CLI server via JSON-RPC".
- Community requests [P]: issue #83 "Open Source?" (opened Sep 27, 2025) is still open, four comments, none from staff. Issue #3241 "Open sourcing the copilot cli" (May 11, 2026) was closed on Oct 26, 2026 by a collaborator as a duplicate of #83, with no reasoning given. https://github.com/github/copilot-cli/issues/83. Verification pass (GitHub API): all four #83 comments have author_association NONE; #3241 was closed 2026-10-26T20:16Z, state_reason "duplicate", by account patniko (COLLABORATOR), whose comment points to #83 and is footnoted "Triaged as part of a Copilot SDK backlog review, with help from GitHub Copilot." So the only reason given is "duplicate"; nothing is said about open-sourcing.
- The 2025 counter-statement [P], VS Code team, "Why open source now?" (May 19, 2025, older than 6 months), https://code.visualstudio.com/blogs/2025/05/19/openSourceAIEditor: "Large language models have significantly improved, mitigating the need for "secret sauce" prompting strategies."
- [O] The inference available from shipped facts: the closed runtime is sold as a managed, governed service (Foundry, Copilot plans), the openness is in the protocols and client libraries, and the redistribution licence protects the runtime as a product. Do not present this as GitHub's stated reason.

---

## 5. OpenCode (Anomaly)

- **Launch note**: "OpenCode 2.0", anoma.ly/notes, `article:published_time` 2026-10-12, no personal byline (site credit "Anomaly"), https://anoma.ly/notes/opencode-2-0/. Read from the raw HTML [P]. Soft hyphens in the page were removed when quoting.
  - "OpenCode 2.0 is a major overhaul. It draws on millions of daily users' experience to deliver a system that can flex to everything an agent needs to be."
  - "The old API grew haphazardly as we and the world collectively learned what agents are and should be. It was bad. We started from scratch".
  - "The models love to write code and OpenCode 2.0 takes advantage of that more than any other coding agent." (Code Mode; "All MCP servers in 2.0 are opted into code mode by default.")
  - "The latest batch of models are incredibly good at orchestration and it is important for harnesses to let them express the full extent of that capability." (background subagents and shell commands)
  - "we forced ourselves to implement nearly every OpenCode 2.0 feature as an internal plugin and there are now 80+ of them."
  - "From the beginning OpenCode adopted a client/server model. ... In 2.0 this server now automatically runs as a single background process on your machine."
- **Date conflict** [P/O]: npm `@opencode/cli` 2.0.0 was published 2026-09-11 (round5-oss-terminal.md). The launch note is dated 2026-10-12, and secondary coverage (The New Stack, AlternativeTo) dates the official launch to Oct 11 or 12. [O] Say "2.0 shipped on npm Sep 11 and was announced Oct 12, 2026".
- **Dax Raad, 2026**: the "0.x prototype, 1.x validation, 2.0 ground-up rebuild" line is only in secondary coverage (KuCoin, Huxiu) [S]. No primary 2026 post or transcript from Raad was reachable (X not readable; the Pragmatic Engineer and Syntax episodes were not transcribed here). OpenCode's GitHub releases page carries no 2.0.0 release note.
- [O] Stated philosophy in one line: let the model write code and orchestrate, and keep the core extensible by making every feature a plugin.

---

## 6. Cognition (Devin, SWE-2, SWE-grep)

- **SWE-grep**, Ben Pan, Carlo Baronio, Albert Tam, Pietro Marsella, Mokshit Jain, Daniel Chiu, Swyx, Silas Alberti, Oct 16, 2025 (older than 6 months), https://cognition.com/blog/swe-grep [P, raw page]:
  - On embeddings: "The embeddings can even be counterproductive, as the agent can give too much weight to irrelevant information."
  - On agentic search: "Both Claude Code and Cline have noted that this works well for them, and up until today, we agreed."
  - Why a subagent: "By having the main agent delegate retrieval to a subagent, we save on (valuable) agent tokens and avoid polluting the agent's context with irrelevant information."
  - Why not summaries: "Often sub-agents are implemented such that they summarize their findings for the main agent. ... A fast model summary can draw wrong conclusion and mislead the smart model." The subagent returns "a list of files with line ranges" so the reward is deterministic.
  - Tools: "we found that we can get strong results with only 4 serial turns – by leveraging highly parallel tool calls" and "We optimized how these tool calls run (e.g. indexing, multi-threading, carefully restricted tool set) and co-designed the SWE-grep models with this custom set of tool calls."
- **SWE-2**, "The Cognition Team", Sep 10, 2026, https://cognition.com/blog/swe-2 [P, raw page]:
  - Behaviour, not harness: "the largest efficiency gains from SWE-2 come from focused exploration"; first real edit "after a median of 18 steps, compared with 48 for SWE-1.7" (vendor claim).
  - Harness as evaluation variable: "we evaluate the model on our internal evaluation framework using the harness for which it was primarily developed: Claude Code for Anthropic models, Codex for OpenAI models, Grok Build for xAI models, and Devin CLI for open-weight models."
  - [R] Scope correction (verification pass): this applies only where no public number exists. The sentence before it reads "For each model–benchmark pair, we report the publicly available result where one exists. Otherwise, we evaluate the model ...". So "each model is evaluated in the harness for which it was primarily developed" overstates it; say "where no public score exists, Cognition runs each model in its home harness". The "18 vs 48 steps" figure is for "SWE-2 medium" on "FrontierCode 1.1 Main" (vendor claim).
  - The post groups steps by tool category ("Explore (read / grep / ls)", "Plan / todo", "Write / edit code", "Build", "Run tests", "git add / commit") but does not describe the edit tool's format.
- **Devin Desktop**, Scott Wu and Jeff Wang, Jun 2, 2026, https://cognition.com/blog/introducing-devin-desktop [P]: "the work of software engineers is shifting towards agent management." "From the beginning, Devin has been built to use the best model for each task instead of being tied to a single model." "At the same time, we believe the IDE still matters to serious developers. ... Some work needs you to jump in, inspect the code, and make the last-mile edit yourself."
- Not found: any Cognition statement on edit format. Carry forward CU's "do not put one on a slide".

---

## 7. Warp, Kilo Code, Devin Desktop

- **Warp, Zach Lloyd, "The Factory Stack", Sep 5, 2026**, https://www.warp.dev/blog/the-factory-stack [P, raw page; author and date in the page header]:
  - "Software factories should be built on an infrastructure stack that is open, composable and defined in code."
  - "The Inference Layer should support running any model and any agent so that you can evolve and test your factory configuration to optimize quality, cost and speed. It also prevents lock-in and any single model provider having pricing power over your org over time".
  - "you should have at least one harness that supports open-weight models like Warp Agent or OpenCode, plus the ability to run the main model harnesses from the model labs directly, like Claude Code and Codex."
  - "No external provider should get to train on this data. ZDR is a must." [O] Directly relevant to a bank.
  - Open-source rationale (Apr 28, 2026, older than 6 months) is [P] in round5-platforms-research.md §6: "we think we can ship a better Warp, more quickly, if we open source".
- **Kilo Code** [P, raw pages]:
  - Job Rietbergen, Apr 2, 2026 (older than 6 months), https://blog.kilo.ai/p/new-kilo-for-vs-code-is-live: "every Kilo surface — CLI, JetBrains, and Cloud Agents — was still running VS Code internals, whether it needed them or not. That created a ceiling on what we could build." "Instead of patching around VS Code dependencies, we built a portable core that runs natively on every surface."
  - Brian Turcotte, Apr 21, 2026 (older than 6 months), https://blog.kilo.ai/p/thank-you-roo: "The IDE is not over. Far from it, actually." Credits Roo with "the whole “let the agent actually do things” philosophy that’s now table stakes." The extension was rebuilt "on the OpenCode server, a portable open-source core".
  - No post-Anaconda (after ~Jul 17, 2026) philosophy statement found.
- **Devin Desktop**: see §6.

---

## 8. Karpathy in 2026, and the origin of "harness engineering"

**Karpathy** (both auto-generated captions, [P\*]):
- No Priors, "Skill Issue: Andrej Karpathy on Code Agents, AutoResearch, and the Loopy Era of AI", uploaded 2026-03-20 (older than 6 months), https://www.youtube.com/watch?v=kwSVtQ7dziU:
  - 00:01:41 to 00:01:58: "in December is when it really just something flipped where I kind of went from 80/20 of like, you know, uh to like 20/80 of writing code by myself versus just delegating to agents. ... I don't think I've typed like a line of code probably since December basically."
  - 00:02:28 to 00:02:35: "How is it how can I have not just a single session of, you know, um Claude code or Codex or some of these agent harnesses? How can I have more of them?"
- Sequoia Capital, "Andrej Karpathy: From Vibe Coding to Agentic Engineering w/ Stephanie Zhan", uploaded 2026-04-29 (older than 6 months), https://www.youtube.com/watch?v=96jN2OCOfLs:
  - 00:15:58 to 00:16:24: "vibe coding is about raising the floor for everyone in terms of what they can do in software. ... But then I would say agentic engineering is about preserving the quality bar of what existed before in professional software. So, you're not allowed to introduce uh vulnerabilities due to vibe coding. ... you're still responsible for your software just as before, but can you go faster?"
  - 00:16:29 to 00:16:39: "You have these agents which are these like spiky entities, they're a bit fallible, a little bit stochastic, but they are extremely powerful. And it's how do you how do you coordinate them to go faster without sacrificing your quality bar?"
  - On skill (00:17:54): "investing into your own kind of setup".
- This upgrades round5-philosophy-direction.md's [S] "agentic engineering at Sequoia AI Ascent" to [P\*] (video uploaded Apr 29). The original X post coining "agentic engineering" is still unread.
- [O] Karpathy uses "harness" as the common noun for Claude Code and Codex. He does not argue for thin or thick harnesses. His slide-worthy line for a bank is the "preserving the quality bar" definition.

**"Harness engineering" origin** (checks round5-philosophy-direction.md §1.7):
- [P] Re-read today: Mitchell Hashimoto, "My AI Adoption Journey", dated February 5, 2026 on the page: "I don't know if there is a broad industry-accepted term for this yet, but I've grown to calling this "harness engineering." It is the idea that anytime you find an agent makes a mistake, you take the time to engineer a solution such that the agent never makes that mistake again. I don't need to invent any new terms here; if another one exists, I'll jump on the bandwagon." https://mitchellh.com/writing/my-ai-adoption-journey
- [S] A source-code study (arXiv 2609.00006) also dates the term's entry into circulation to February 2026 with Hashimoto; a search for 2025 uses of the phrase found none.
  - Verification pass correction: the paper is "Harness Engineering: Anatomy, Architecture, and Evolution of Coding Agents -- A Source-Code Study of Eleven Systems", citation_date 2026-07-15. Its wording: the term "entered circulation in February 2026: first used in passing by Mitchell Hashimoto, then defined and elaborated by Trivedy in the context of LangChain's Deep Agents work", with a footnote that "the term was named and defined from within LangChain". Its introduction separately says the phrase was "coined in a vendor blog post", which conflicts with the Hashimoto line; it does not mention OpenAI's Feb 11 post. [R] "a search for 2025 uses found none" is not a claim the paper makes; it is the research agent's own search [O]. A quick web search in this pass surfaced secondary pages asserting earlier origins ("May 2024", "late 2025") without sources; not verified, not followed further. Hashimoto as earliest named user stays the best-supported reading, not a proven first use.
- The PD file's sequence (Anthropic and OpenAI using "harness" as a noun in Nov 2025 and Jan 2026; Hashimoto names the practice Feb 5; OpenAI's titled post Feb 11; Böckeler Feb 17 and Apr 2; LangChain Mar 10) is consistent with what we found. The [R] on "OpenAI coined harness engineering" stands.

---

## 9. Summary table

| Family | Stated philosophy, one line | Best quote | Source | Tag |
|---|---|---|---|---|
| Anthropic (Claude Code) | Build for the model six months out; harness code is temporary | "never bet against the model" (00:38:37); "maybe 10 20% ... and then essentially the gain is wiped out with the next model" (00:08:22-00:08:26) | Boris Cherny, YC Light Cone, Feb 17, 2026, youtube.com/watch?v=PQU9o_5rHC4 | [P\*] |
| OpenAI (Codex) | Harness and model co-designed; harness is a crutch the model absorbs | "the developer message shrinks and then the harness also shrinks" | Thibault Sottiaux, Pragmatic Engineer, Sep 9, 2026, youtube.com/watch?v=sLSTM9znQNs (00:38:57) | [P\*] |
| OpenAI (Codex) | Train against the shipped harness | "So we do training on the harness now." | Andrew Ambrosino, every.to, Oct 15, 2026 (0:58) | [P], not certified verbatim |
| OpenAI (Codex) | Simple harness, model orchestrates, features as plugins | "This harness we need to do our best to keep as simple as possible ... you let the model orchestrate as much as possible." | Alexander Embiricos, every.to, Oct 15, 2026 (42:00) | [P], not certified verbatim |
| Google (Antigravity, Gemini CLI) | One harness co-optimised with Gemini, behind every surface | "Gemini 3.5 Flash having been optimized with the Antigravity harness." | Varun Mohan, Google I/O '26 Keynote, May 19, 2026, youtube.com/watch?v=wYSncx9zLIU (00:27:41) | [P] |
| GitHub / Microsoft (Copilot) | Managed multi-model harness; open protocols and SDK, closed runtime (reason not stated) | "With the Copilot harness, Microsoft runs the agent loop and sandbox, with governance and optimization built in from day one." | Schuchman and Fedorov, Microsoft blog, Oct 28, 2026 | [P] (was [P\*]) |
| OpenCode (Anomaly) | Let models write code and orchestrate; everything is a plugin | "it is important for harnesses to let them express the full extent of that capability." | Anomaly, "OpenCode 2.0", Oct 12, 2026, anoma.ly/notes/opencode-2-0/ | [P] |
| Cognition (Devin) | Specialised fast subagents with restricted tools, co-trained with the model; best model per task | "co-designed the SWE-grep models with this custom set of tool calls." | Pan et al., Oct 16, 2025, cognition.com/blog/swe-grep (older than 6 months) | [P] |
| Devin Desktop | Engineers manage agents; the IDE stays for the last mile | "the work of software engineers is shifting towards agent management." | Scott Wu and Jeff Wang, Jun 2, 2026 | [P] |
| Warp | Open, composable, code-defined factory; any model, any harness | "The Inference Layer should support running any model and any agent" | Zach Lloyd, Sep 5, 2026, warp.dev/blog/the-factory-stack | [P] |
| Kilo Code | One portable open core under every surface; the IDE still matters | "The IDE is not over. Far from it, actually." | Brian Turcotte, Apr 21, 2026, blog.kilo.ai/p/thank-you-roo (older than 6 months) | [P] |
| Karpathy (commentator) | Agentic engineering keeps the professional quality bar | "agentic engineering is about preserving the quality bar of what existed before in professional software." | Sequoia, Apr 29, 2026, youtube.com/watch?v=96jN2OCOfLs (00:16:06) | [P\*] |
| Term origin | Fix each agent mistake permanently in the environment | "I've grown to calling this "harness engineering."" | Mitchell Hashimoto, Feb 5, 2026 | [P] |

---

## 10. Could not verify

- openai.com DevDay 2026 recap (403). No recording of the DevDay closing session with Sottiaux; its content is known only from Willison's live-blog paraphrase [S]. The keynote speaker who mentions the Codex harness is not named in the captions (Willison names him as Sam Altman [S]; not confirmed from the video).
- Kundel's talk: the event name and talk date are not in the YouTube metadata (uploaded Oct 9, 2026).
- Any GitHub or Microsoft statement of why the Copilot runtime is closed. None exists in Toub's post, the Oct 28 post, the SDK README, or the copilot-cli issue tracker.
- A primary 2026 statement by Dax Raad; the "prototype, validation, rebuild" framing is secondary only.
- A 2026 Gemini CLI team essay on harness design; none found.
- Cognition's edit format; not published.
- Karpathy's original "agentic engineering" X post (X not readable).
- All YouTube quotes from auto-generated captions (Cherny, Sottiaux, Kundel, Karpathy) should be checked by listening before they go on a slide verbatim; timestamps are exact to the caption cue.

---

## Verification pass (2026-11-04)

Adversarial re-check. Method: caption tracks for all eight YouTube videos re-pulled independently with `youtube-transcript-api` and grepped; upload dates and titles from the watch-page JSON and oEmbed; web sources fetched raw with curl and stripped to text; GitHub facts from the GitHub API; npm facts from registry.npmjs.org; arXiv paper read from the PDF. Auto-captions were still not listened to, so [P\*] tags on Cherny, Sottiaux, Kundel and Karpathy stand.

**Checked and confirmed (wording, speaker, timestamp, date as stated):**
1. Cherny, YC video PQU9o_5rHC4, uploaded 2026-02-17T07:00:42-08:00, auto-captions only. "10 20%" at 00:08:22 and 00:39:00; "wiped out" at 00:08:26; "never bet against" at 00:38:37; "build for the model of 6 months from now" at 00:37:49 to 00:37:54; "more general model will always be the more specific model" caption error at 00:38:31 to 00:38:33; "unhip tools" at 00:39:31. The splice [R] is correct.
2. Ambrosino "So we do training on the harness now", passage final-20261015-0004 at 0:58, role "Design & engineering"; Every page `published_time` 2026-10-15; "not certified verbatim" header present.
3. Embiricos (Product) at 42:00 #0185, Glaese (Model research) at 15:44 #0077, Brockman (Company direction) at 6:21 #0010: all quotes match Every's markdown export.
4. Sottiaux, Pragmatic Engineer sLSTM9znQNs, uploaded 2026-09-09: "shrinks" at 00:38:54 to 00:38:59, "harness change or ... model change" at 00:40:11 to 00:40:15, "the harness is a crutch" at 01:01:50, "why would you couple it to your model" at 00:26:28 to 00:26:30, open-source passage at 00:21:46 onward.
5. Kundel, AI Engineer 9WiBJRO84yY, uploaded 2026-10-09; title names "Dominik Kundel, OpenAI"; "wraps the Codex harness" at 00:01:13 to 00:01:15; "ship your own version of the harness" at 00:16:07 and 00:16:35; "in distribution" at 00:17:24.
6. Varun Mohan, I/O '26 keynote wYSncx9zLIU, uploaded 2026-05-19, manual captions with "VARUN MOHAN:" label at 00:25:26; quote at 00:27:24 to 00:27:44 verbatim.
7. DevDay keynote Fls_onRviPM, uploaded 2026-09-29, manual English track: garbled harness passage at 00:27:38 to 00:28:00 matches the quoted text exactly.
8. OpenCode 2.0 note: `article:published_time` 2026-10-12, no personal byline; all six quotes found (soft hyphens removed). npm `@opencode/cli` 2.0.0 published 2026-09-11T23:44:52Z; package created 2026-09-02; repository anomalyco/opencode; sole maintainer thdxr.
9. SWE-grep (2025-10-16, eight named authors) quotes all match; SWE-2 `datePublished` 2026-09-10 and its quotes match; Devin Desktop 2026-06-02, Scott Wu and Jeff Wang, quotes match.
10. Warp "The Factory Stack", Zach Lloyd, September 5, 2026: all four quotes match. Kilo: Turcotte 2026-04-21 and Rietbergen 2026-04-02 quotes match.
11. Copilot: copilot-sdk licence MIT, copilot-cli NOASSERTION; LICENSE.md contains "distributed only in unmodified form" and "material functionality beyond the Software itself"; issue #83 opened 2025-09-27, open, 4 non-staff comments; Toub post published 2026-09-16 PT (2026-09-17 UTC), modified 2026-09-23, no licensing language in the body; VS Code 2025 "secret sauce" quote matches.
12. Karpathy: No Priors kwSVtQ7dziU (2026-03-20) "agent harnesses" at 00:02:33 to 00:02:35 and "80/20 ... 20/80" at 00:01:46 to 00:01:49; Sequoia 96jN2OCOfLs (2026-04-29) "preserving the quality bar" at 00:16:06 to 00:16:11.
13. Hashimoto, "My AI Adoption Journey", February 5, 2026: full quoted paragraph matches.
14. Willison live blog lines at 10:26, 16:20, 16:25 exist as quoted.

**Corrected:**
- Google Developer Keynote: the captions do give the surname ("LOGAN KILPATRICK:" at 00:37:58). The SDK line (00:49:13) and CLI line (00:55:22) are not his; they fall in the Paige Bailey and Anshul Ramachandran/Kevin Hou segments. Fixed in §3.
- DevDay keynote: Willison identifies the speaker of the Codex-harness line as Sam ("Sam is back", 10:29) [S]. The name "Agents API" is from Willison, not the captions. Fixed in §2.2, §10 and the short version.
- SWE-2: the home-harness methodology applies only where no public score exists. The digest's "each model is evaluated in..." overstated it. Fixed in §6 and the short version.
- Kundel: his advice is to start with developer instructions and "be careful" replacing the base prompt, not an outright "do not". Context added in §2.2.
- Sottiaux "ahead of the model" timestamp: 00:37:30, not 00:37:28.
- arXiv 2609.00006: the paper credits Hashimoto with first passing use but LangChain (Trivedy) with naming and defining the term, and elsewhere says "coined in a vendor blog post". "A search for 2025 uses found none" is the agent's search, not the paper's. Fixed in §8.
- Issue #3241: closing reason is "duplicate", via a triage comment noting it was done "with help from GitHub Copilot". Added.

**Upgraded:** Microsoft Copilot harness post quotes [P\*] to [P] (raw page now fetchable); Antigravity 2.0 "co-optimized" line, Antigravity I/O blog line and Gemini CLI transition post quotes [P\*] to [P].

**Still unverifiable:**
- openai.com DevDay recap (not retried) and any recording of the DevDay closing session.
- The New Stack's launch date for OpenCode 2.0 (page body not returned to the fetcher). The Oct 12 note date and Sep 11 npm date are confirmed.
- Kundel's event name (not in title, description or captions).
- Any primary 2026 Dax Raad statement; Karpathy's original "agentic engineering" X post.
- Secondary claims of a pre-2026 origin for "harness engineering" (seen in search snippets, unsourced).
- Exact wording of all auto-captioned quotes until someone listens to the audio.
