# Blind spots in the brief — and the calls I made

The brief asked me to write down its unknown unknowns, the places its framing breaks,
and what a sharp audience would push back on — then answer those questions myself.
Format: the blind spot, then **My call** (how the deck actually handles it).

---

## 1. The "Anthropic deleted 80% of the system prompt" claim is unsourced

This is the spine's strongest single piece of evidence, and if it isn't publicly
documented, the first sharp question from the audience ("citation?") collapses it on
stage. **My call:** research it first. If it can't be verified, the slide carries
what *is* verifiable — both vendors' migration guides explicitly telling you to
remove forced chain-of-thought and few-shot scaffolding for reasoning models — and
the deletion anecdote is either dropped or framed as reported practice, clearly
flagged. The argument survives without the anecdote; it doesn't survive a bad
citation. (See `research/track2-thin-harness-evidence.md` for the verdict.)

## 2. "Harnesses get thinner" is half-true, and a sharp audience will spot the false half

Harnesses are visibly getting *thicker*: MCP, skills, sub-agents, hooks, and coding
agents didn't exist in 2023. Someone will say "you just showed us ten new harness
features — which is it?" **My call:** split the harness into **compensation**
(prompt scaffolding that papers over model weakness — shrinking) and **capability**
(tools, context plumbing, permissions — growing). The thesis becomes "compensation
shrinks, capability grows," which is stronger and survives scrutiny. Vehicle
version: better engines killed the choke and the hand crank; they didn't kill the
transmission.

## 3. The rental-car jab may insult people who like Copilot's defaults

GitHub tunes those defaults deliberately, for the median user, and some colleagues
may be happy with them. **My call:** keep the analogy, but the insult must land on
"tuned for nobody," never "badly engineered." A rental car is *well*-engineered —
for returnability. Speaker notes carry that nuance so the live delivery doesn't
alienate the room.

## 4. "Attention is n²" invites a FlashAttention rebuttal

Anyone who reads papers will say quadratic attention is mitigated in practice.
**My call:** the slide claims only "attention lets every token look at every other
token — that's its power and its cost." Optimizations acknowledged in one appendix
line. The context-rot argument doesn't depend on exact asymptotics; it depends on
long context degrading retrieval quality, which is empirically documented.

## 5. The strawberry demo can backfire live

Current reasoning models count the r's in "strawberry" correctly. If someone tries
it on their phone mid-talk, the slide looks stale. **My call:** the demo shows the
*tokenization* (in Tiktokenizer), not a model failing. The claim is "here is why
this whole class of failure exists," which stays true even after models patch over
it with reasoning tokens.

## 6. Any frontier FLOPs-per-token number is an estimate

Frontier labs don't publish parameter counts. **My call:** anchor the arithmetic on
an open model with a citable count (Llama-3-class 405B dense → ~8×10¹¹ FLOPs/token
by the 2N rule), cite the estimating methodology (Epoch AI), and label anything
about frontier models as an estimate on the slide itself. Honest numbers that are
slightly smaller land harder than impressive numbers that are challengeable.

## 7. Where do evals, RAG, and fine-tuning sit in the four-part definition?

"AI Engineering = harness + context + memory + prompt engineering" has visible
gaps, and this audience builds software for a living. **My call:** one slide draws
the boundary explicitly: fine-tuning is *engine* work (not our job); RAG is the
retrieval arm of context engineering; evals are the dyno you test the vehicle on —
acknowledged, pointed at, not covered. Naming the boundary defuses the question.

## 8. Copilot specifics rot monthly

Model lists, AGENTS.md precedence, premium-request multipliers — all of it moves.
**My call:** the brief already solved this: `/research/` is the source of truth,
every file carries a fetch date, and the deck says "as of August 2026" where it
states perishable facts.

## 9. Live iframes are a double failure risk

Venue network may block demo domains; WebGL demos may chug on a projector laptop.
**My call:** every embed gets an always-visible "open in new tab ↗" bar; every
demo slide degrades to a readable card with title/description/URL; `?print-pdf`
is the offline floor. No slide's meaning depends on an iframe rendering.

## 10. Papyan's course site is a Google Sites page

Google Sites pages don't embed (X-Frame-Options), can move, and can be slow.
**My call:** treat it as a source and a set of link cards — mine its structure and
demos into the history act — never as a live embed dependency.

## 11. Twelve acts is too many to present, and the brief knows it

The artifact should be complete; the talk is a subset picked live. The failure mode
is a presenter lost in their own deck. **My call:** speaker notes carry "if short
on time, skip to X" at the act boundaries, and the README includes two suggested
paths (a 30-minute cut and a 60-minute cut) so tomorrow-you doesn't improvise the
cut list at 9am.

## 12. Whose name goes on it?

The brief says "my name on it" but never gives the name. **My call:** the git
identity here says "Kay," so the deck footer says Kay, and it's one clearly marked
line in `index.html` to change. Logged in ASSUMPTIONS.

## 13. The end-of-scaling opinion slide has a classic trap

Conflating pre-training scaling, post-training gains, and inference-time (thinking)
scaling is the standard way this argument goes wrong in public. **My call:** the
scaffold slide separates the three axes so the opinion lands on the right one, and
the consensus slide cites who actually claims what.

## 14. Kahoot tone risk

Too cute embarrasses the presenter; too hard humiliates the room. **My call:**
eight questions ramp from gimme to spicy, and every answer is something the deck
actually taught — the quiz doubles as a recap.

## 15. "Memory engineering" is the thinnest leg of the definition

Copilot's memory surface is immature compared to the other three legs, so the deck
risks a section with no substance. **My call:** memory gets covered inside context
engineering (compaction, structured note-taking, instruction files *as* durable
memory) rather than pretending there's a mature product surface to demo.

**Post-research correction:** this blind spot was itself stale — the Track 1 sweep
found **Copilot Memory** is now a real, documented feature (machine-written repo
facts with code citations, validated against the current branch, auto-deleted
after 28 days unused; shared across cloud agent, code review, and CLI), plus
Spaces as curated context bundles. The deck now covers it in the harness map and
the context act; the deep-dive still lives in `research/track1-memory-spaces.md`.
