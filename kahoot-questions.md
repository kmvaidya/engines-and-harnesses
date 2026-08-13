# Kahoot — 24 questions, in act order (the quiz doubles as a recap)

Every answer was on a slide. Difficulty is deliberately medium: distractors are
plausible, and a few questions are traps where the obvious answer is wrong
(marked 🪤). Kahoot limits: question ≤ 120 chars, answers ≤ 75 chars — all fit.
Correct answer marked ✔. Suggested timer: 20s default, 30s where marked.

---

## Act 1 — the engine

**1. In "405B parameters," what exactly are the parameters?** *(warm-up)*
- Tokens the model can recognize
- ✔ Learned weights — the knobs training turns
- The GPUs used during training
- Stored training examples

**2. Why can one trained network complete code it has never seen?**
- It searches the training set at runtime
- It memorized GitHub verbatim
- ✔ Training compressed the patterns into its weights
- The harness looks the answer up for it

**3. Turning temperature UP does what to the token odds?**
- ✔ Flattens them — long shots get a real chance
- Sharpens them — the favorite always wins
- Makes the model think longer
- Expands the vocabulary it can pick from

## Act 2 — tokens

**4. Modern reasoning models CAN count the r's in "strawberry." What changed?** *(🪤)*
- A new tokenizer that finally sees letters
- ✔ Nothing — they think in steps now; the eyesight never changed
- Much bigger context windows
- They call a letter-counting tool

**5. The model receives "1234567890" as chunks like 123·456·7890. Split by what?**
- Place value, in groups of three
- Where commas would go
- The number of digits a register holds
- ✔ How often each chunk appeared in training text

**6. Why must a position stamp be mixed into every token's vector?**
- ✔ Attention reads everything at once — order is otherwise invisible
- So the model knows when to stop generating
- To mark sentence boundaries for grammar
- To keep embeddings from overlapping in memory

## Act 3 — scale

**7. 810 billion operations per token for Llama 405B — where does that number come from?** *(30s)*
- Measured on an H100 with a profiler
- Vocabulary size × number of layers
- ✔ Two per parameter: every weight works on every token
- Meta's marketing material

**8. A ~500-token chat answer equals how many years of a human doing one multiply per second?** *(30s)*
- 13 thousand
- ✔ 13 million
- 26 hundred
- 13 billion

**9. DeepSeek-V3 has MORE total parameters than Llama 405B, yet is ~11× cheaper per token. How?**
- Better GPUs
- It skips the attention step
- Lower-precision arithmetic
- ✔ Mixture-of-experts: only ~37B parameters wake up per token

## Act 4 — thinking tokens

**10. Your reasoning model goes down a dead end and backtracks. Those wasted tokens are…**
- ✔ Billed like everything else — wrong turns cost the same
- Refunded once the final answer lands
- Free — you only pay for answer tokens
- Discarded before they reach the meter

## Act 5 — where this is heading

**11. METR's "time horizon" — the one exponential still visibly running — measures what?**
- Benchmark score growth per dollar
- Tokens per second at inference
- Context window growth per year
- ✔ Length of task an agent finishes at 50% success

## The Turn

**12. Per the deck, what's identical for you, your competitor, and a teenager in a dorm?**
- The harness
- The context budget
- ✔ The engine — the model's frozen weights
- The benchmark scores

**13. In the vehicle taxonomy, the "truck" is…** *(30s)*
- Bare chat plus one sharp tool
- Your configured IDE assistant
- A team workspace with shared MCP racks
- ✔ An autonomous agent in CI — issue in, PR out, nobody in the cab

## Act 6 — harness engineering

**14. Which harness piece stays OUT of context until its description matches the task?**
- Prompt files
- ✔ Skills
- Custom agents
- Repo instructions

**15. The Planner custom agent cannot edit code. What actually stops it?** *(🪤)*
- The "do NOT edit code" line in its prompt
- A hook that reverts its edits
- ✔ It was never given an edit tool — safety by construction
- Cloud-side content filters

**16. What can a hook do that no instructions file can?**
- ✔ Deterministically block a tool call before it runs
- Explain the repo's conventions
- Suggest a better prompt
- Pick a cheaper model

**17. Why write AGENTS.md instead of putting everything in copilot-instructions.md?**
- It loads faster
- It supports longer files
- ✔ Copilot, Claude Code, Codex, Cursor and Gemini all read it
- GitHub deprecated the Copilot file

**18. Why does the deck warn against hitching MCP servers "just in case"?**
- Each server slows every request
- They can edit files unsupervised
- Licensing costs per server
- ✔ Every tool description spends context tokens, used or not

## Act 7 — context engineering

**19. A model ships with a 10× bigger context window. What did you actually get?** *(🪤)*
- ✔ A bigger fuel tank — storage, not comprehension
- 10× better recall of what's inside
- Cheaper attention per token
- Nothing — window sizes are marketing

**20. Anthropic deleted 80% of Claude Code's system prompt. Result on their coding evals?**
- A small, acceptable quality drop
- ✔ No measurable loss
- A big cost win, small quality loss
- It only worked after adding few-shot examples

**21. Why do Anthropic's OLDER models still get the fat system prompt?** *(spicy, 30s)*
- ✔ They lack the judgment for lean prompts — harness matched to engine
- Backwards compatibility with old APIs
- Nobody has updated it yet
- Longer prompts run cheaper on old models

**22. Per OpenAI, contradictory instructions hurt GPT-5 MORE than older models. Why?**
- It refuses and returns an error
- ✔ It burns billed reasoning tokens trying to reconcile them
- It always follows the first rule it read
- Its context window is smaller

## Act 8 — picking an engine

**23. Swapping ONLY the scaffold — no retraining — moved DeepSeek R1's SWE-bench score by about…** *(30s)*
- 3 points
- 8 points
- ✔ 25 points
- 40 points

## The thesis

**24. As engines get better, the harness should…** *(the closer)*
- Get thicker — more rules, more examples
- Stay frozen — it already works
- Disappear — the model does everything
- ✔ Shed compensation, grow capability

---

Setup: kahoot.com → Create → at 24 questions, Kahoot's spreadsheet import is
now worth it (Add question → Import spreadsheet, fill their .xlsx template from
this file) — or enter by hand in one sitting. Correct answers are spread evenly
across the four slots. Grab the join QR from the lobby screen and drop it into
the placeholder box on the Kahoot slide.
