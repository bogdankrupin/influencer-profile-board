# SE Ranking AI-search enrichment

How to add the **live AI-search visibility** section when the SE Ranking
connector or API is available. This is optional: if SE Ranking is missing or out
of credits, skip everything here and build the board from web search.

> Tool names and parameters can vary by connector version. **Load each tool's
> exact parameters at runtime (tool search) before calling — don't guess.** If
> the `se-ranking-api-docs` skill is available, use it to confirm endpoints.

## When to run
Run only if a capability check finds the SE Ranking AI-search tools. Quick test:
search for a tool like `DATA_getAiSearchOverview`. If it isn't there, the
connector isn't connected → skip to the standard board.

## The data to pull (minimal, credit-aware)
All of these are `DATA_*` research tools — they work on any target and **spend
data-API credits**. Pull only what the section needs; never loop.

1. **Resolve the brand/target** — `DATA_getAiSearchBrand`
   Pass the subject's official domain if they have one, else their public name.
   Confirms the brand name SE Ranking attributes to the target, so the rest of
   the pulls line up with the right entity.

2. **AI-search overview** — `DATA_getAiSearchOverview`
   Visibility metrics for the target across AI engines (e.g. ChatGPT, Google AI
   Overviews / AI Mode): mention share, link/citation presence, counts.

3. **Prompts where the person appears** — `DATA_getAiSearchPromptsByBrand`
   (or `DATA_getAiSearchPromptsByTarget`)
   The actual prompts/questions users ask where the subject is mentioned or
   cited. These become the "what people ask AI about them" examples.

4. **(Optional) Peer comparison** — `DATA_getAiSearchLeaderboard`
   Only if a comparison adds value: how the subject stacks up against a few
   peers/competitors across engines. Skip if it would just spend credits.

## Map results → board section
Build an **AI-search visibility** section with:
- **Engines covered** — chips for the engines that returned data (ChatGPT,
  Google AI Overviews, AI Mode, …). Only show engines that actually have data.
- **Share of mentions** — per engine, a small bar/number for how often the
  subject is mentioned; note link/citation presence separately from mentions.
- **What people ask** — a short list of real example prompts (from step 3) where
  the subject appears; keep it to the most representative handful.
- **(Optional) Standing** — a one-line takeaway from the leaderboard if pulled.
- **Provenance** — label the whole section *Source: SE Ranking AI-search, as of
  [date]*. Separate mentions vs citations explicitly — they are not the same.

## Failure & credit handling (must follow)
Treat the entire section as best-effort:
- **No connector / tool not found** → skip silently, build standard board.
- **Auth / permission error** → skip; optionally note "live AI-search data not
  available".
- **Credits or limits exhausted** (rate-limit / quota / credit errors) → skip
  the section, keep the rest, and build the rest from web search. Do **not**
  retry in a loop.
- **Empty or partial data** → show only the engines/fields that returned data;
  if nothing useful came back, drop the section.
- Never block, delay, or fail the overall board because of an SE Ranking issue.
  The web-search board is always the fallback.

## Honesty rules
- Report mentions and citations as **measured by SE Ranking**, dated — not as
  absolute truth about every AI system.
- Don't merge this measured data with the heuristic LLM-visibility read; keep
  them as separate, clearly-labelled sections.
