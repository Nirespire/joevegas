# Flyer — design spec

The flyer lives at [`flyer/index.html`](index.html): a fixed 816 × 1056 px (8.5 × 11 in
at 96 dpi) print artifact. It shares [`../tokens.css`](../tokens.css) with the site, so
the two are edited together — change a colour or a typeface once and both move.

Direction **1c — "1996 modern show poster"** is the approved one, and it is the direction
the site at [`../index.html`](../index.html) is built to match. What follows is the
original design handoff, kept verbatim as the reference for the flyer's intent.

---

# Handoff: Captain Joe's Vegas Weekend — Event Flyer

## Overview
A single-sided 8.5 x 11 in print flyer announcing a Las Vegas bachelor weekend
("Captain Joe's Vegas Weekend", Sept 18-20 2026). It is a gag reveal handed to the
groom and the four other attendees: headline, dates, the five-man company with roles,
five house rules, and a QR code to the live companion site
(https://nirespire.github.io/joevegas).

Three era-themed variations were explored. **1c (1996 modern show poster) is the
approved direction.** 1a and 1b are retained in the same file as historical context —
implement 1c unless told otherwise.

## About the Design Files
The files in this bundle are **design references created in HTML** — prototypes that
show the intended look and content, not production code to paste in. The task is to
**recreate the design in the target codebase's own environment** (React, Vue, a static
site generator, an InDesign/print pipeline, whatever exists) using its established
patterns. If there is no existing environment, pick the most appropriate one for a
print-destined single-page artifact and implement it there.

Note on the prototype format: the HTML uses a lightweight in-house component runtime
(`support.js`, the `<x-dc>` wrapper). Neither the runtime nor the wrapper is part of the
design — ignore both. All design intent lives in the inline styles on the markup inside
`<x-dc>`. `support.js` is included only so the file opens and renders in a browser.

## Fidelity
**High-fidelity.** Exact colors, typefaces, sizes, letter-spacing, and copy are final and
are all listed below. Recreate pixel-for-pixel at 816 x 1056 px (= 8.5 x 11 in at 96 dpi).
Print output should be 8.5 x 11 in with full-bleed dark background; no crop marks were
designed in — add 0.125 in bleed if the print shop requires it.

## Screens / Views

### 1c — Vegas Weekend Flyer (the approved design)
- **Name:** Flyer, front (single-sided)
- **Purpose:** Physical handout / PDF. Reader learns what the weekend is, when it is,
  who is on it, the rules, and how to reach the live schedule.
- **Page:** `816px x 1056px`, background `#0B0509`, text `#F4E9D8`, `overflow:hidden`,
  vertical flex column. Horizontal gutters are `46px` on every band.
  (In the prototype the page also carries `box-shadow: 0 40px 90px -30px #000` — that is
  screen-presentation only, drop it in print.)

Bands, top to bottom:

**1. Eyebrow rule**
- Container: `padding: 40px 46px 0`, flex row, `justify-content: space-between`,
  `align-items: baseline`
- Left text: "Las Vegas · 2 nights only" — Anton, 14px, uppercase, letter-spacing `.24em`,
  `#FFD166`
- Right text: "No. 001" — same type, color `rgba(244,233,216,.45)`

**2. Hero**
- Container: `padding: 30px 46px 0`
- Script kicker: "two nights only" — Great Vibes, 36px, `#FFD166`, `line-height:1`,
  `margin-bottom:6px` (rendered lowercase as authored)
- Headline line 1: "Captain Joe's" — Anton, 104px, uppercase, `line-height:.86`,
  `letter-spacing:-.02em`, `#F4E9D8`
- Headline line 2: "Vegas Weekend" — identical type, `#FF3D7F`
- Intro paragraph: `margin-top:16px`, `max-width:640px`, Space Grotesk 17px,
  `line-height:1.45`, `rgba(244,233,216,.78)`, `text-wrap:pretty`. Copy:
  "Five men, one weekend, and the last unsupervised hours before the wedding. Two nights
  in Las Vegas — shows, cards, questionable decisions, and a running order nobody intends
  to follow."
  (This copy is deliberately about the weekend, not about the groom personally.)

**3. Date band**
- `margin: 30px 46px 0`, background `#FF3D7F`, text `#fff`, `padding: 16px 22px`,
  flex row `space-between`, `align-items:center`, no border radius
- Left: "Sept 18 – 20 · 2026" (en dash) — Anton 20px, uppercase, letter-spacing `.2em`
- Right: "Final weekend before the final 2" — same type

**4. Two-column body**
- `display:grid; grid-template-columns: 1.05fr 1fr; gap:34px; padding: 34px 46px 0`
- Both column headers: Anton 14px, uppercase, letter-spacing `.26em`, `#FFD166`,
  `padding-bottom:10px`, `border-bottom: 1px solid rgba(244,233,216,.2)`
- **Left column — "The company":** `display:grid; gap:11px; margin-top:14px`. Each row is a
  flex row, `gap:12px`, `align-items:baseline`; name = Anton 22px uppercase with
  `min-width:96px`; role = Space Grotesk 15px `rgba(244,233,216,.7)`.
  - Joe — "The groom. Won the casserole."
  - Sanjay — "Logistics. Every table is under his name."
  - Derrick — "Three coworkers, one recommendation."
  - Jake — "Out at 6 AM. His choice."
  - Bryen — "Holds the tickets. Details classified."
- **Right column — "House rules":** `display:grid; gap:10px; margin-top:14px`,
  Space Grotesk 15px, `line-height:1.35`, `rgba(244,233,216,.82)`. Each rule is prefixed by
  a two-digit numeral in Anton `#FF3D7F`, followed by a non-breaking-space gap
  (`&nbsp;` in the prototype ≈ 6px):
  - 01 The groom does not open his wallet. Not even for water.
  - 02 Nobody says "one more hand" after 2 AM. Say it, buy the round.
  - 03 Saturday is an all-Caesars day. Do not wander.
  - 04 Alternate every cocktail with water.
  - 05 Mention the wedding budget, take the 7:30 AM flight.

**5. Footer** (pinned to the bottom via `margin-top:auto`)
- `border-top: 1px solid rgba(244,233,216,.2)`, `padding: 26px 46px 34px`, flex row,
  `align-items:center`, `gap:20px`
- QR code: 92 x 92 px, `background:#F4E9D8`, `padding:5px`, no radius. Encodes
  `https://nirespire.github.io/joevegas`. Alt text: "QR code to the live itinerary".
- Label: "Scan for the plizan" — Anton 18px, uppercase, letter-spacing `.16em`, `#F4E9D8`
- Sub-label: "nirespire.github.io/joevegas · live countdown & running order" —
  Space Grotesk 15px, `rgba(244,233,216,.6)`
- Right, `margin-left:auto`, right-aligned, 14px, `rgba(244,233,216,.4)`, `line-height:1.4`:
  "Built by the groomsmen." / "Debugged by nobody." (two lines)

### 1a — 1957 letterpress showbill (not selected)
Cream `#F4E9D8` page, oxblood `#5A1024` double rule frame (2px outer + 1px inner, 28px page
padding, 6px between rules), centred composition, Great Vibes + Anton headline stack at
46px / 70px, reversed oxblood date block, two-column cast grid and Roman-numeral house
rules. Full source in the bundled HTML.

### 1b — 1978 neon marquee (not selected)
Near-black `#120A16` page with pink/green radial glows, gold hairline frame with a
chasing-bulb dot pattern on all four edges, Monoton headline at 66px with a four-layer
pink neon `text-shadow`, scanline-striped date block, dark rounded house-rules card.
Full source in the bundled HTML.

## Interactions & Behavior
None — this is a static print artifact. No hover, focus, or animation states are designed.
Requirements that do matter:
- The page must be exactly 816 x 1056 px (8.5 x 11 in) with content fully contained; no
  scroll, no clipping. Everything uses `box-sizing: border-box`.
- The footer must stay pinned to the bottom edge (flex `margin-top:auto`), with the body
  bands flowing from the top — do not vertically centre.
- No responsive behavior. Fixed-size canvas only.
- Export target: PDF at 8.5 x 11 in, or PNG at 2x (1632 x 2112) for digital sharing.

## State Management
None. No state, no data fetching. All content is static copy, hard-coded above.

## Design Tokens

Colors
| Token | Value | Use |
|---|---|---|
| ink | `#0B0509` | 1c page background |
| cream | `#F4E9D8` | primary text, QR plate; 1a page background |
| pink | `#FF3D7F` | accent headline line, date band, rule numerals |
| gold | `#FFD166` | eyebrow, section headers, script kicker |
| oxblood | `#5A1024` | 1a frame + reversed block |
| dark plum | `#120A16` | 1b page background |
| deep maroon | `#2A0E18` | 1a headline ink |
| muted maroon | `#7A3345` | 1a secondary text |
| white | `#FFFFFF` | text on the pink date band |
| text 78% | `rgba(244,233,216,.78)` | intro paragraph |
| text 70% | `rgba(244,233,216,.7)` | role descriptions |
| text 82% | `rgba(244,233,216,.82)` | house rules |
| text 60% | `rgba(244,233,216,.6)` | footer sub-label |
| text 45% | `rgba(244,233,216,.45)` | "No. 001" |
| text 40% | `rgba(244,233,216,.4)` | footer credit |
| hairline | `rgba(244,233,216,.2)` | section + footer rules |

Spacing scale (px): 5, 6, 10, 11, 12, 14, 16, 20, 22, 26, 30, 34, 40, 46
- page gutter 46 · band separation 30-34 · list row gap 10-11 · footer bottom pad 34

Typography
| Role | Family | Size | Tracking | Case |
|---|---|---|---|---|
| Headline | Anton 400 | 104px / `line-height:.86` | `-.02em` | uppercase |
| Script kicker | Great Vibes 400 | 36px / 1 | normal | as authored |
| Date band | Anton 400 | 20px | `.2em` | uppercase |
| Name (company list) | Anton 400 | 22px | normal | uppercase |
| Section header | Anton 400 | 14px | `.26em` | uppercase |
| Eyebrow | Anton 400 | 14px | `.24em` | uppercase |
| Footer label | Anton 400 | 18px | `.16em` | uppercase |
| Intro paragraph | Space Grotesk 400 | 17px / 1.45 | normal | sentence |
| Body / roles / rules | Space Grotesk 400 | 15px / 1.3-1.35 | normal | sentence |
| Footer credit | Space Grotesk 400 | 14px / 1.4 | normal | sentence |

Border radius: `0` throughout 1c (1b uses 6-12px on its cards only).
Shadows: none in print. The prototype's `0 40px 90px -30px #000` page shadow is
presentation chrome for the on-screen canvas only.

## Assets
- **Fonts** — Google Fonts: Anton, Great Vibes, Space Grotesk (400/500/700), Monoton
  (1b only), DM Serif Display (loaded but unused). Self-host or substitute with the
  codebase's licensed equivalents; if substituting, match the condensed-grotesque weight
  of Anton for the headline — it carries the whole design.
- **QR code** — generated at request time from
  `https://api.qrserver.com/v1/create-qr-code/?size=180x180&margin=0&color=0B0509&bgcolor=F4E9D8&data=<url>`.
  For production, generate the QR locally (any QR library) as an SVG at
  foreground `#0B0509` / background `#F4E9D8`, error correction M, and embed it — do not
  depend on the third-party endpoint for a print run.
- **No images or icons.** No photography was used; if imagery is added later it is a new
  design decision, not part of this handoff.

## Files
- `Vegas Flyer.dc.html` — all three variations (1a, 1b, 1c). 1c starts at the
  `<!-- 1c — 1996 modern show poster -->` comment; its page root is the element with
  `data-screen-label="1c"`.
- `support.js` — prototype runtime only, not design. Required for the HTML to render.
- Companion (not in this bundle): `Vegas Weekend Site.dc.html` — the live schedule site at
  https://nirespire.github.io/joevegas that the flyer's QR code points to. Separate
  deliverable; ask if you need it documented too.
