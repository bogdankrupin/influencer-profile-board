# Board template — layout, design tokens, interaction

Guidance for rendering the profile board as one clean, self-contained HTML
file. This is opinionated on purpose so output is consistent and looks good;
adapt where a specific board calls for it.

## Output rules
- **Single file.** All CSS and JS inline. No external scripts or stylesheets except a Google Fonts `<link>` (optional). Images embedded as data URIs or omitted.
- **No external calls at runtime.** The board must render fully offline.
- Save to `/mnt/user-data/outputs/` with a descriptive name, e.g. `profile-board-<slug>.html`.

## Design tokens
Use a calm, modern, "card on a soft canvas" aesthetic.

```
--canvas:   #E7EBF1;   /* page background */
--surface:  #FFFFFF;   /* card background */
--ink:      #0F172A;   /* primary text */
--muted:    #5A6B7E;   /* secondary text */
--faint:    #94A3B8;   /* tertiary / labels */
--line:     #E4E9F0;   /* borders, dividers */
--accent:   #2747FF;   /* primary accent */
--accent-soft:#ECEFFF; /* accent wash / chips */
--ok:       #0F8A5F;   /* positive score */
--warn:     #B45309;   /* caution / risk */

Fonts:
--display: 'Space Grotesk', system-ui, sans-serif;  /* headings */
--body:    'Inter', system-ui, sans-serif;          /* body */
--mono:    'IBM Plex Mono', ui-monospace, monospace;/* labels, scores, dates */
```

Rounded corners (~16–18px on the main card), soft shadow
(`0 18px 48px -24px rgba(15,23,42,.28)`), generous padding (28–34px), max width
~880px, centered on the canvas.

## Layout
Top to bottom:

1. **Header** — optional avatar (rounded), name in `--display`, role + one-liner, a small niche chip, location, and an "as of [date]" stamp in `--mono`.
2. **Section nav** — tabs or anchor chips for the sections, so a long board stays scannable.
3. **Contact & channels** — a row of labeled links / buttons; each social as a chip with platform + handle. Add small **copy** buttons where a handle or link is worth copying.
4. **Social presence & audience size** — one row/tile per platform showing the platform name, handle/link, and **follower/subscriber count**, with the count's as-of date. A compact stat-grid (platform label + big number + "~ as of [date]") reads well. Show counts as approximate; omit a platform with no reliable figure. Optional combined-reach line, marked as a sum.
5. **Expertise** — core topics as filterable chips; sub-themes and formats as a short list.
6. **Notable work & links** — a list/grid of cards: title, one-liner, outbound link.
7. **Trajectory** — a short, dated timeline or 2–3 bullets.
8. **Key facts** — a clean list, each item a plain, sourced sentence.
9. **LLM-visibility read** (if included) — five labeled rows, each with a small score pill (use `--ok`/`--accent`/`--warn` by level) and a one-line rationale. A segmented bar per dimension works well.
10. **AI-search visibility** (only if SE Ranking data was pulled) — engine chips for the engines with data; a small per-engine bar for share of mentions with citation/link presence shown separately; a short list of real "what people ask AI" prompts; an optional one-line peer-standing note. Label the block *Source: SE Ranking AI-search, as of [date]* so its provenance is visibly distinct from the web-search content. Omit the block entirely if no data.
11. **Sources** — compact list of outbound links, grouped official vs other.
12. **Footer** — "Built from public information on [date]. Not affiliated with or endorsed by [name]."

## Interaction (keep it lightweight, vanilla JS)
At least one genuinely useful interaction, e.g.:
- **Tabbed / expandable sections** (click a nav chip to jump or toggle).
- **Topic filter chips** that highlight matching expertise/work items.
- **Copy buttons** for handles/links (use the Clipboard API with a tiny "copied" toast).
No frameworks, no build step, no network. Degrade gracefully if JS is off (content still visible).

## Tone & accuracy in the UI
- Keep all copy **analytical and neutral** — factual labels, no praise, hype, or exclamation marks (see the Tone section in SKILL.md).
- Show follower counts as approximate and dated (e.g. "~48K · as of Jun 2026"); never imply a count is exact or live.
- Show the "as of" date prominently — it signals the data is a snapshot.
- Render only fields you actually filled; don't leave empty labeled slots or placeholder dummy text.
- Keep the sources section real and clickable.
