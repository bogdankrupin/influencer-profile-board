---
name: influencer-profile-board
description: >-
  Build a rich, interactive single-file HTML profile board for any public
  figure, creator, or influencer in any niche. Pulls public information via web
  search and structures it into identity & contact, areas of expertise, notable
  work and links, highlights, and an optional LLM-visibility read. Use this
  skill whenever the user wants to profile, research, or "make a card / board /
  dossier" about a creator, influencer, expert, founder, athlete, or public
  personality — phrases like "tell me about [person]", "build a profile of
  [name]", "make an influencer board", or "who is [name] and what are they known
  for". Trigger even when the user doesn't say "board" or "skill", as long as
  they want a structured profile of a named person. When the SE Ranking
  connector or API is available, the board is enriched with live AI-search data
  (how the person shows up in ChatGPT and Google AI Overviews / AI Mode), and it
  falls back to the web-search-only board when SE Ranking is absent or out of
  credits.
compatibility: >-
  Needs the web_search tool to gather public signals, and the ability to write
  an HTML file the user can open (file creation / artifacts). The live AI-search
  layer is optional and needs the SE Ranking MCP connector or API; without it,
  or when its credits are exhausted, the skill builds the board from web search
  alone. Works best when Claude can also read the frontend-design skill for
  styling tokens, but that is not required.
---

# Influencer Profile Board

Turn a person's public footprint into one polished, interactive HTML board: who they are, how to reach them, what they're known for, the links worth keeping, the standout facts, and — optionally — how legible they are to an LLM. The point of this skill is that the research questions, the board structure, and the privacy rules are settled in advance, so every profile comes out complete, accurate, and the same shape.

Everything in a board comes from **public** information and is **sourced**. This is a profile of a public footprint, not a background check.

**Two modes, one output.** The baseline board is built entirely from web search and always works. When the **SE Ranking** connector or API is available, the skill adds a live *AI-search visibility* section — real data on how the person shows up when users ask about them in ChatGPT and Google AI Overviews / AI Mode. If SE Ranking isn't connected, or its credits are used up, the skill silently drops that one section and produces the standard web-search board. SE Ranking is never required for a result.

## Step 1 — Pin down the subject

Before searching, make sure you know *who* you're profiling.

- Get the name and, if useful, the niche or a handle ("the SEO one", "@username", "the F1 driver"). If the name is ambiguous and several notable people share it, either ask which one or proceed with the most likely match **and state that assumption** at the top of the board.
- Confirm scope only if it's unclear: a single board for one person (default).
- This skill profiles **public figures / public-facing professionals** using information they or others have already published. If the subject is a private individual with little public presence, say so and stop — there isn't a public footprint to board, and assembling one isn't appropriate.

## Step 2 — Gather public signals (web search)

Run several **targeted** searches rather than one broad one. Aim to fill every board section. A good sweep covers:

1. **Identity & current role** — full name, current title(s)/company, location if public, one-line "what they do".
2. **Official channels & contact** — personal site, the social profiles they actively run, newsletter, and any *publicly listed* business contact (e.g. a "work with me" / booking page). See privacy rules below.
3. **Areas of expertise** — the topics they're most tightly associated with; what they're cited or invited to speak on.
4. **Notable work & links** — signature projects, talks, books, podcasts, popular pieces, products, awards. Capture the actual URLs.
5. **Trajectory & recent activity** — what they've shipped or posted lately; where their focus is heading.
6. **Interesting / standout facts** — verifiable, noteworthy details that make the profile memorable (a famous project, an origin story, a record, a distinctive POV). Not gossip, not rumor, not anything private.

Sourcing discipline:
- Prefer **primary / official** sources (their own site, verified profiles, first-party bylines) over aggregators.
- For any non-official claim, look for **corroboration across at least two independent sources** before stating it as fact.
- **Date-stamp** time-sensitive facts and record an "as of" date for the whole board — roles and follower counts go stale.
- If a field can't be found, leave it blank or mark "not public". **Never invent** a detail, a link, a number, or a quote to fill a slot.

## Step 3 — (Optional, if available) Live AI-search visibility via SE Ranking

This is the enrichment layer. Do it only when SE Ranking is reachable; otherwise skip straight to Step 4 and build the board the standard way.

**Capability check first.** Look for the SE Ranking AI-search tools (e.g. via tool search). If the connector isn't present, don't attempt anything — go to Step 4. If it is present, pull a small, focused set of AI-search data about the subject. The exact tool sequence, the target to pass, and the field mapping are in `references/se-ranking-ai-search.md` — read it before calling. In short:

- Resolve the subject as a target/brand (their official domain if they have one, otherwise their public name), confirming how SE Ranking attributes the brand.
- Pull the **AI-search overview** (visibility across engines) and the **prompts where the person appears** — the real questions users ask about them in ChatGPT and Google AI Overviews / AI Mode — and, if useful, a small **leaderboard** comparison.
- Turn that into the board's *AI-search visibility* section: which engines mention them, share of mentions, whether they're cited/linked, and a few example prompts.

**Credit & failure discipline (important):**
- These are `DATA_*` research calls that **cost SE Ranking data-API credits** — pull only the few calls this section needs; don't loop or over-fetch.
- If **any** call fails — no connector, auth error, **credits/limits exhausted**, empty result — **abandon this section gracefully**, keep everything else, and build the rest of the board from web search. Never let an SE Ranking problem block or break the board.
- Mark this section's data as sourced from **SE Ranking AI-search, as of [date]**, so its provenance is distinct from the web-search content. If the section is skipped, the board simply doesn't include it (optionally note "live AI-search data not available").

## Step 4 — Structure the data

Organize what you found into the board schema before rendering. The full section-by-section field list is in `references/board-spec.md` — read it so the board is complete and consistently shaped. At a glance the sections are: Header (identity), Contact & channels, Expertise, Notable work & links, Trajectory, Highlights / fun facts, **AI-search visibility** (only if Step 3 produced data), and Sources.

Two things to calibrate here:
- **Match the footprint.** A well-documented public figure earns a rich board; someone with a thinner or emerging presence gets a compact one. Don't pad a sparse profile with filler or speculation — a short, honest board that notes "a focused / emerging public footprint" is the right output.
- **Disambiguate when names collide.** If a similarly-named person could be confused with the subject — especially someone in the same field or company — add a short name-note near the header (e.g. "not to be confused with X") and reflect it in the Risk dimension if you include the LLM-visibility read.

## Step 5 — (Optional) LLM-visibility read (heuristic)

If the user wants the "how does an LLM see this person" angle — or it's clearly useful — add a compact scored read using five dimensions: **Identity** (is who-they-are-now unambiguous), **Topic Association** (how tightly bound to specific topics), **Trust / Corroboration** (primary-source, multi-publication), **Freshness & Trajectory** (recent, active), and **Risk / Trust boundaries** (anything that muddies the model's picture). Each dimension gets a short score plus a one-line rationale. Keep it honest — it describes legibility to a model, not the person's worth. Omit this section entirely if it isn't wanted.

Note this is a **heuristic** read — your qualitative judgment from the web evidence. It's different from the Step 3 *AI-search visibility* section, which is **measured** data from SE Ranking. If you have both, keep them as separate sections (measured data first); if you only have the heuristic, this section stands on its own.

## Step 6 — Render the interactive board

Produce a **single self-contained HTML file** (all CSS/JS inline, images as data URIs or omitted) and save it to `/mnt/user-data/outputs/`. It should:

- Open with a clean header: name, role, one-liner, location, and an "as of" date.
- Lay out the sections as scannable cards or tabs; make expertise and links easy to skim.
- Be interactive in at least one useful way — e.g. tabbed/expandable sections, copy-link buttons, or filter chips for topics. Keep it lightweight; no external calls.
- End with a **Sources** section listing the links the board was built from.
- If Step 3 produced data, include the **AI-search visibility** section (engines, share of mentions, citation/link status, example prompts) and clearly label it *Source: SE Ranking AI-search, as of [date]* so its provenance is distinct from the web-search content.
- Be responsive and look good when shared or screenshotted.

Read `references/board-template.md` for the layout, the design tokens (fonts, colors, spacing), and the interaction patterns to use. If the `frontend-design` skill is available, consult it too for styling — but the template here is enough to produce a strong result on its own.

After saving, present the file to the user.

## Privacy & accuracy (read every time)

These keep the board appropriate and trustworthy:

- **Public information only.** Use what the subject or reputable sources have already published. Do **not** include a home address, personal phone number, private email, exact location, family details, or anything else not clearly meant to be public — even if you can find it. Business/booking contacts that the person publishes for that purpose are fine.
- **No sensitive inferences.** Don't assert or guess health, religion, sexual orientation, political affiliation, or similar, unless the person has clearly made it part of their public identity and it's relevant.
- **Verifiable, not gossip.** "Interesting facts" must be sourced and noteworthy, not rumor or anything that reads as snark about a real person.
- **Mark uncertainty and date it.** Flag anything unconfirmed; stamp the board with the date so stale numbers are obvious.
- **Sources, always.** Every board ends with the sources it was built from, so it's auditable.

## Language

Match the language of the request. If the board is for a specific audience and the language isn't obvious, ask which language it should be in.
