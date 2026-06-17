# Board specification

The fields each board section should aim to fill. Treat these as targets, not
mandatory — leave anything you can't source as blank or "not public" rather than
guessing.

## Contents
1. Header (identity)
2. Contact & channels
3. Expertise
4. Notable work & links
5. Trajectory
6. Highlights / interesting facts
7. Sources
8. Optional — LLM-visibility read

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

## 3. Expertise
- **Core topics** — 3–6 areas they're most tightly associated with
- **Sub-themes** — narrower angles within those topics
- **Formats** — how they show up (research, talks, courses, threads, video, OSS…)
- A one-line note on what they're *the* person for, if there's a clear answer

## 4. Notable work & links
For each item: a title, a one-line description, and the URL. Aim for the
strongest 4–8.
- Signature projects / products
- Notable talks, books, podcasts, popular articles
- Awards, recognitions, notable mentions

## 5. Trajectory
- **Recent activity** — what they've shipped/posted lately (with rough dates)
- **Direction** — where their focus seems to be heading
- Keep this short and clearly time-stamped

## 6. Highlights / interesting facts
- 3–6 verifiable, memorable facts (origin story, a record, a famous moment, a
  distinctive POV, a surprising background detail)
- Each should be sourced; nothing private, nothing that reads as a dig

## 7. Sources
- The links the board was built from, grouped loosely (official vs press/third-party)
- This section is required — it makes the board auditable

---

## 8. Optional — LLM-visibility read
Include only if the user wants the "how does an LLM see this person" angle.
Five dimensions, each a short score (e.g. a 0–100 or Low/Med/High) plus a
one-line rationale:

- **Identity (ID)** — is who-they-are-*now* unambiguous and consistent across sources?
- **Topic Association (TA)** — how tightly is the name bound to specific topics vs. a vague generalist footprint?
- **Trust / Corroboration (TR)** — primary-source authority, corroborated across multiple publications/venues?
- **Freshness & Trajectory (FR)** — recent, active, and moving in a clear direction?
- **Risk / Trust boundaries (RX)** — name collisions, sparse sourcing, or anything that muddies the model's picture?

Frame it as legibility to a model, not a judgment of the person.
