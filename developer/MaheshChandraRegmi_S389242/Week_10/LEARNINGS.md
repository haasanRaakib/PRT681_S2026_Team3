# Week 10 — Prompting techniques + vibe coding

Half this term went faster because I was pairing with AI tools (Weeks 1 and 3 especially — Gemini picked the project ideas). This week I stepped back and studied the technique instead of just using it.

## Prompting techniques

- zero-shot vs few-shot — one worked example of the output I want beats a paragraph describing it
- role prompting — "you are a code reviewer" changes what comes back
- chain of thought — ask for the reasoning step by step before the answer
- specifying output format up front (JSON schema, table, diff) instead of re-formatting afterwards
- pasting the real context — the actual EF model, the actual stack trace — instead of describing it from memory
- iterating: treat the first answer as a draft, critique it, refine the prompt

## Vibe coding

- the loop: describe → generate → run it → read the errors → refine the prompt
- keeping a human in the loop — review every diff, tests are the safety net
- where it shines: boilerplate, CRUD endpoints, config files, first drafts
- where it bites: hallucinated package APIs, plausible-looking security mistakes, code I can't explain in a demo
- what I actually used it for this term: the Week 7 CORS + Vite proxy config, EF mapping gotchas, and test ideas

## Things I sat with

**Context beats clever wording.** The prompts that produced usable code weren't the fancy ones — they were the ones where I pasted the real schema and the real error.

**Tests are what make vibe coding safe.** I only trusted generated code once it passed tests I understood. If I can't write the test, I don't understand the feature well enough to accept the code.
