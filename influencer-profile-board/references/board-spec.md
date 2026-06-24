# Board specification

The fields each board section should aim to fill. Treat these as targets, not
mandatory — leave anything you can't source as blank or "not public" rather than
guessing.

## Contents
1. Header (identity)
2. Contact & channels
3. Social presence & audience size
4. Expertise
5. Notable work & links
6. Trajectory
7. Key facts
8. AI-search visibility (optional — only with SE Ranking data)
9. Sources
10. Optional — LLM-visibility read (heuristic)

---

## 1. Header (identity)
- **Full name** (and the name they're publicly known by, if different)
- **Current role(s)** — title + organization; include a founder/independent role if relevant
- **One-liner** — what they do, in a single plain sentence
- **Niche / field** — the domain tag (SEO, fitness, fintech, F1, beauty, …)
- **Location** — only if the person publishes it; city/country level, never an address
- **Photo** — optional; embed as a data URI so the file stays self-contained. Omit if not cleanly available.
- **As-of date** — the date the board was assembled
- **Name note** *(only when needed)* — a short "not to be confused with X" line when a similarly-named person could be conflated, especially in the same field/company
- **Footprint flag** *(only when thin)* — if the public presence is limited, say so plainly (e.g. "a focused / emerging public footprint") rather than padding the board

## 2. Contact & channels
- **Primary site** — personal site or portfolio
- **Active social profiles** — only the ones they actually run; note the platform and handle
- **Newsletter / community** — if any
- **Public business contact** — a "work with me", booking, or press link they publish for that purpose
- (Never a private phone/email/home address — see privacy rules in SKILL.md)

## 3. Social presence & audience size
- **Per platform** — one row per active platform (LinkedIn, X/Twitter, YouTube, Instagram, TikTok, Facebook, Twitch, Substack, etc.)
- For each: **platform · handle/link · follower or subscriber count · as-of date / source**
- Counts are approximate point-in-time figures — label them "~" and dated; don't present a single stale number as exact
- Omit a platform if no reliable count is available rather than guessing
- Optional: a total/combined reach line, clearly marked as a sum of the figures shown

## 4. Expertise
- **Core topics** — 3–6 areas they're most tightly associated with
- **Sub-themes** — narrower angles within those topics
- **Formats** — how they show up (research, talks, courses, threads, video, OSS…)
- A one-line note on what they're most associated with, if there's a clear answer

## 5. Notable work & links
For each item: a title, a one-line description, and the URL. Aim for the
strongest 4–8.
- Signature projects / products
- Notable talks, books, podcasts, popular articles
- Awards, recognitions, notable mentions

## 6. Trajectory
- **Recent activity** — what they've shipped/posted lately (with rough dates)
- **Direction** — where their focus appears to be heading, stated from evidence
- Keep this short and clearly time-stamped

## 7. Key facts
- 3–6 verifiable, material facts (a documented project, a record/first, a stated
  position, a relevant background detail)
- State each plainly and attributively; each should be sourced
- Nothing private, nothing speculative, nothing that reads as praise or a dig

## 8. AI-search visibility *(optional — only when SE Ranking data is available)*
Live data on how the subject shows up when users ask AI about them. Populated
from `references/se-ranking-ai-search.md`; omit the whole section if SE Ranking
isn't available or returned nothing.
- **Engines covered** — chips for engines with data (ChatGPT, Google AI
  Overviews, AI Mode, …)
- **Share of mentions** — per-engine, how often the subject is mentioned
- **Citation / link presence** — shown separately from mentions (not the same thing)
- **What people ask** — a handful of real prompts where the subject appears
- **(Optional) Standing** — one-line leaderboard takeaway vs peers
- **Provenance** — "Source: SE Ranking AI-search, as of [date]"

## 9. Sources
- The links the board was built from, grouped loosely (official vs press/third-party)
- This section is required — it makes the board auditable

---

## 10. Optional — LLM-visibility read (heuristic)
Include only if the user wants the "how does an LLM see this person" angle.
Five dimensions, each a short score (e.g. a 0–100 or Low/Med/High) plus a
one-line rationale:

- **Identity (ID)** — is who-they-are-*now* unambiguous and consistent across sources?
- **Topic Association (TA)** — how tightly is the name bound to specific topics vs. a vague generalist footprint?
- **Trust / Corroboration (TR)** — primary-source authority, corroborated across multiple publications/venues?
- **Freshness & Trajectory (FR)** — recent, active, and moving in a clear direction?
- **Risk / Trust boundaries (RX)** — name collisions, sparse sourcing, or anything that muddies the model's picture?

Frame it as legibility to a model, not a judgment of the person.
