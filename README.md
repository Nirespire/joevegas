# Captain Joe's Vegas Weekend

A live itinerary site for a September 18–20, 2026 bachelor weekend in Las Vegas — countdown clock, schedule, crew flight info, and assorted running jokes.

Live at: https://nirespire.github.io/joevegas/

## What's here

| File | What it is |
|---|---|
| `index.html` | The site. Self-contained, no build step. |
| `flyer/index.html` | The print flyer — 8.5 × 11 in, single-sided. Print with background graphics on and no margins, or save as PDF. |
| `flyer/DESIGN.md` | The flyer's design handoff, kept as the reference for both. |
| `tokens.css` | Shared design tokens. Both pages link it. |

## Design

Both the site and the flyer are direction **1c — "1996 modern show poster"**: flat ink
background (`#0B0509`), Anton condensed headline, a pink (`#FF3D7F`) accent line and date
band, gold (`#FFD166`) hairline section headers, square corners, no glow.

Colours, typefaces and tracking live in `tokens.css` and nowhere else — change a value
there and the site and the flyer move together. Everything else (layout, components) is
inline in each page.

The flyer's QR code is generated locally rather than fetched from a QR service, so a print
run never depends on a third party. To regenerate after a URL change:

```
pip install segno
python3 -c "import segno; segno.make('https://nirespire.github.io/joevegas', error='m').save('qr.svg', kind='svg', scale=1, border=0, dark='#0B0509', light=None, xmldecl=False)"
```

then paste the `<path>` into the `<svg class="qr">` in `flyer/index.html` and `index.html`.

## Notes

- All schedule times are pinned to Vegas time (PDT, UTC−7) so the page reads correctly from any device.
- Preview any moment with `?now=2026-09-19T21:15`.
- There are six secrets on the page. Start by tapping the headline.
