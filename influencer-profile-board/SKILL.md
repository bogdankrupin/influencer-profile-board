---
name: influencer-profile-board
description: >-
  Build a rich, interactive single-file HTML profile board for any public
  figure, creator, or influencer in any niche. Pulls public information via web
  search and structures it into identity & contact, areas of expertise, notable
  work and links, highlights & interesting facts, and an optional LLM-visibility
  read. Use this skill whenever the user wants to profile, research, or "make a
  card / board / dossier" about a creator, influencer, expert, founder, athlete,
  or public personality — phrases like "tell me about [person]", "build a
  profile of [name]", "make an influencer board", "research this creator", or
  "who is [name] and what are they known for". Trigger even when the user does
  not say "board" or "skill" explicitly, as long as they want a structured,
  shareable profile of a named person built from public sources.
compatibility: >-
  Needs the web_search tool to gather public signals, and the ability to write
  an HTML file the user can open (file creation / artifacts). Works best when
  Claude can also read the frontend-design skill for styling tokens, but it is
  not required.
---

# Influencer Profile Board

Turn a person's public footprint into one polished, interactive HTML board: who they are, how to reach them, what they're known for, the links worth keeping, the standout facts, and — optionally — how legible they are to an LLM. The point of this skill is that the research questions, the board structure, and the privacy rules are settled in advance, so every profile comes out complete, accurate, and the same shape.

Everything in a board comes from **public** information and is **sourced**. This is a profile of a public footprint, not a background check.

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

## Step 3 — Structure the data

Organize what you found into the board schema before rendering. The full section-by-section field list is in `references/board-spec.md` — read it so the board is complete and consistently shaped. At a glance the sections are: Header (identity), Contact & channels, Expertise, Notable work & links, Trajectory, Highlights / fun facts, Sources.

Two things to calibrate here:
- **Match the footprint.** A well-documented public figure earns a rich board; someone with a thinner or emerging presence gets a compact one. Don't pad a sparse profile with filler or speculation — a short, honest board that notes "a focused / emerging public footprint" is the right output.
- **Disambiguate when names collide.** If a similarly-named person could be confused with the subject — especially someone in the same field or company — add a short name-note near the header (e.g. "not to be confused with X") and reflect it in the Risk dimension if you include the LLM-visibility read.

## Step 4 — (Optional) LLM-visibility read

If the user wants the "how does an LLM see this person" angle — or it's clearly useful — add a compact scored read using five dimensions: **Identity** (is who-they-are-now unambiguous), **Topic Association** (how tightly bound to specific topics), **Trust / Corroboration** (primary-source, multi-publication), **Freshness & Trajectory** (recent, active), and **Risk / Trust boundaries** (anything that muddies the model's picture). Each dimension gets a short score plus a one-line rationale. Keep it honest — it describes legibility to a model, not the person's worth. Omit this section entirely if it isn't wanted.

## Step 5 — Render the interactive board

Produce a **single self-contained HTML file** (all CSS/JS inline, images as data URIs or omitted) and save it to `/mnt/user-data/outputs/`. It should:

- Open with a clean header: name, role, one-liner, location, and an "as of" date.
- Lay out the sections as scannable cards or tabs; make expertise and links easy to skim.
- Be interactive in at least one useful way — e.g. tabbed/expandable sections, copy-link buttons, or filter chips for topics. Keep it lightweight; no external calls.
- End with a **Sources** section listing the links the board was built from.
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
