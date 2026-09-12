# Captain Joe's Vegas Weekend

A live itinerary site for a September 18–20, 2026 bachelor weekend in Las Vegas — countdown clock, schedule, crew flight info, and assorted running jokes.

Live at: https://joesbeforehoes.party/

## What's here

| File | What it is |
|---|---|
| `index.html` | The site. Self-contained, no build step. |
| `flyer/index.html` | The print flyer — 8.5 × 11 in, single-sided. Print with background graphics on and no margins, or save as PDF. |
| `flyer/DESIGN.md` | The flyer's design handoff, kept as the reference for both. |
| `tokens.css` | Shared design tokens. Both pages link it. |
| `CNAME` | The custom domain GitHub Pages serves from. Deleting it drops the site back to `nirespire.github.io/joevegas`. |

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
python3 -c "import segno; segno.make('https://joesbeforehoes.party', error='m').save('qr.svg', kind='svg', scale=1, border=0, dark='#0B0509', light=None, xmldecl=False)"
```

then paste the `<path>` into the `<svg class="qr">` in `flyer/index.html` and `index.html`.

## Domain & hosting

The site is served by **GitHub Pages** from the `main` branch at the repository root, on
the custom domain **`joesbeforehoes.party`** (registered at Cloudflare, DNS hosted there).

Two halves have to agree. Only the `CNAME` file lives in this repo; the rest is dashboard
configuration:

**1. GitHub — Settings → Pages**
- Source: deploy from branch `main`, folder `/` (root).
- Custom domain: `joesbeforehoes.party`. The `CNAME` file in this repo sets it; GitHub
  reads it on deploy and fills the field in.
- "Enforce HTTPS": tick it once GitHub reports the certificate as issued (it provisions a
  Let's Encrypt cert automatically, usually within a few minutes of DNS resolving).

**2. Cloudflare — DNS for `joesbeforehoes.party`**

| Type | Name | Content | Proxy |
|---|---|---|---|
| CNAME | `@` | `nirespire.github.io` | DNS only |
| CNAME | `www` | `nirespire.github.io` | DNS only |

Cloudflare flattens the apex `CNAME` automatically, so no A/AAAA records are needed. The
apex-record alternative, if you ever want it, is the four GitHub Pages A records
(`185.199.108.153`, `.109.153`, `.110.153`, `.111.153`) plus the matching AAAA records.

**Keep the proxy off (grey cloud).** With the orange cloud on, GitHub cannot complete the
ACME challenge and certificate issuance fails or silently stalls. If you later want
Cloudflare in front of it, wait until GitHub shows the certificate as issued, then enable
the proxy *and* set SSL/TLS mode to **Full (strict)** — "Flexible" causes a redirect loop
against Pages.

Whichever host name you don't land on redirects to the other automatically: GitHub Pages
issues the apex ↔ `www` redirect itself based on the `CNAME` value.

Changing the domain means changing four things together: `CNAME`, the Cloudflare records,
the QR codes (see Design, above), and the `joesbeforehoes.party` labels in `index.html`,
`flyer/index.html` and `flyer/DESIGN.md`.

## Notes

- All schedule times are pinned to Vegas time (PDT, UTC−7) so the page reads correctly from any device.
- Preview any moment with `?now=2026-09-19T21:15`.
- There are seven secrets on the page. Start by tapping the headline.
