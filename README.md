# Handoff: Kristin Leigh Jordan — Personal Site & Resume

## Overview
A single-page personal website Kristin shares with potential employers while looking for a
Programs / Community Director role, plus a two-page print resume in the same visual system.

The site is one scrolling page with a sticky nav: hero → About → What I do → Work →
Films & journalism (with Vimeo embeds) → Writing (Substack) → Contact.

## About the Design Files
The files in this bundle are **design references created in HTML** — prototypes showing the
intended look, copy, and behavior. They are not production code to copy directly.

The task is to **recreate these designs in the target environment** using its established
patterns and libraries. If no environment exists yet, this site is a good fit for a static
generator (Astro, Eleventy, or Next.js static export) plus a real host; there is no backend
requirement beyond a `mailto:` link.

Two of the files are authored in an internal design-component format (`.dc.html`). Read them
as structured HTML: the markup and inline styles inside the `<x-dc>` element are the design.
Ignore the `support.js` runtime, the `<helmet>` wrapper (its contents are a normal `<head>`),
and the `style-hover` attributes (they are hover states — implement as `:hover` CSS).
`kristin-site-reference.html` is a plain-HTML export of the site for easy viewing.

## Fidelity
**High fidelity.** Colors, typography, spacing, and copy are final. Recreate pixel-accurately
using the codebase's existing libraries. All copy in these files is approved and should be used
verbatim — do not rewrite it.

## Design Tokens

### Colors
| Token | Hex | Use |
|---|---|---|
| Paper | `#f9f6f0` | Page background |
| Paper alt | `#efe9df` | Films section background |
| Ink | `#26231f` | Body text, dark section background, hairlines, outline buttons |
| Ink muted | `#4a4540` | Secondary body text, nav links |
| Ink subtle | `#6b655c` | Dates, eyebrow metadata (min contrast-safe grey) |
| Clay | `#a0603f` | Accent: section labels, links, primary button, italic job titles |
| Clay hover | `#8a5136` | Primary button hover |
| Clay light | `#d9a27f` | Section label on dark background |
| Cream text | `#d9d2c6` | Body text on dark background |
| Rule light | `#e4ddd1` | Light hairlines between work entries |
| Rule faint | `#c9bfae` | Text-underline color on the tertiary link |

Contrast note: `#6b655c` was chosen deliberately to clear 4.5:1 on both `#f9f6f0` and
`#efe9df`. Do not lighten it.

### Typography
Google Fonts. Load both families:
```
https://fonts.googleapis.com/css2?family=Newsreader:ital,opsz,wght@0,6..72,400;0,6..72,500;0,6..72,600;1,6..72,400;1,6..72,500&family=Source+Sans+3:wght@400;600&display=swap
```
- **Newsreader** (serif) — display: h1, section h2 in Contact, all h3, pull quotes, About body copy, italic role lines. Weights 400/500/600, italic used.
- **Source Sans 3** (sans) — UI and body: 400/600. Body base 17px / line-height 1.6.

Type scale as authored (all `clamp()` values are literal):
| Element | Value |
|---|---|
| Hero h1 | Newsreader 500, `clamp(40px,6.5vw,76px)`, line-height 1.05, letter-spacing -0.015em, max-width 15ch, `text-wrap:balance` |
| Hero subhead | Newsreader italic 400, `clamp(20px,2.4vw,26px)`, line-height 1.4, max-width 34ch |
| Section eyebrow (h2) | Source Sans 600, 13px, letter-spacing 0.14em, uppercase, clay |
| Section lead paragraph | Newsreader 400, `clamp(20px,2.2vw,24px)`, line-height 1.5 |
| About body | Newsreader 400, `clamp(19px,1.8vw,22px)`, line-height 1.55, max-width 62ch |
| Work entry h3 | Newsreader 500, `clamp(28px,3vw,36px)`, line-height 1.15 |
| Film h3 | Newsreader 500, `clamp(26px,3vw,34px)`, line-height 1.15 |
| "What I do" h3 | Newsreader 500, 26px, line-height 1.2 |
| Role line | Newsreader italic 400, 19px, clay |
| Date / eyebrow meta | Source Sans 400, 14px, `#6b655c` |
| Episode label | Source Sans 600, 13px, letter-spacing 0.08em, uppercase, `#6b655c` |
| Contact headline | Newsreader 500, `clamp(32px,4.5vw,52px)`, line-height 1.1, letter-spacing -0.01em, max-width 20ch, `text-wrap:balance` |
| Nav links | Source Sans 600, 14px, letter-spacing 0.06em, uppercase |
| Buttons / inline links | Source Sans 600, 15px (small links 14px) |

### Spacing & layout
- Content container: `max-width:1080px; margin:0 auto; padding:0 28px`
- Section vertical padding: `80px` top and bottom. Hero: `112px` top, `96px` bottom. Contact: `96px` top, `80px` bottom.
- Section internal column gap: `48px`
- Two-column section pattern: `grid-template-columns:repeat(auto-fit,minmax(260px,1fr))` with the content block spanning 2 tracks (eyebrow label in the first track, content in the rest). Films and Writing use `minmax(280px,1fr)`.
- Work entries: stacked, `gap:56px`, each with `padding-bottom:56px; border-bottom:1px solid #e4ddd1` (last entry has no border).
- Film entries: `padding-top:24px; border-top:1px solid #26231f` each.
- Body text measure: `max-width:62ch` (Writing: 56ch).
- `text-wrap:pretty` on body paragraphs; `text-wrap:balance` on the two big headlines.

### Radius, borders, shadows
- Border radius: `3px` on buttons only. No other rounding, **no shadows anywhere.**
- Hairlines: `1px solid #26231f` for major section divisions; `1px solid #e4ddd1` for minor.

## Screens / Views

### Site — one scrolling page (`Kristin Jordan Site.dc.html`)

**Nav (sticky)**
Position sticky, top 0, z-index 5. Background `rgba(249,246,240,0.92)` with
`backdrop-filter:blur(8px)`, bottom border `1px solid #e4ddd1`. Inner row: `padding:16px 28px`,
space-between, `gap:24px`, wraps. Left: "Kristin Leigh Jordan" in Newsreader 500 20px ink,
links to `#top`. Right: ABOUT / WORK / FILMS / WRITING / CONTACT, `gap:24px`, all
`#4a4540` except CONTACT which is clay. `html{scroll-behavior:smooth}`.

**Hero (`#top`)** — h1, italic subhead, then a button row (`gap:14px`, wraps, `margin-top:8px`):
1. Primary: "Email me" → `mailto:mountainyogabozeman@gmail.com`. Clay background, `#f9f6f0` text, `padding:14px 24px`, radius 3px. Hover: background `#8a5136`.
2. Secondary: "Read my resume" → the resume. `1px solid #26231f`, ink text, `padding:13px 24px`. Hover: ink background, paper text.
3. Tertiary: "Get in touch" → `#contact`. Ink text, underline, `text-underline-offset:4px`, `text-decoration-color:#c9bfae`.

**About (`#about`)** — top border `1px solid #26231f`. Eyebrow "ABOUT" + three Newsreader paragraphs.

**What I do** — full-bleed dark band: background `#26231f`, text `#f9f6f0`. Eyebrow in `#d9a27f`.
Three columns (`repeat(auto-fit,minmax(220px,1fr))`, `gap:40px`), each a Newsreader 26px heading
plus a 16px `#d9d2c6` paragraph.

**Work (`#work`)** — four entries, newest first: Mountain Collective Bozeman (2021–Present,
Founder & Program Director), Bozeman Health Cancer Center (2022–2026, Patient Care Technician),
Mountain Yoga Studio (2014–2021, Owner & Teacher), Lululemon & Yoga Soup (2005–2012, Regional
Marketing Director · Marketing Manager). Each: left column has date / company h3 / italic clay
role line; right column (spans 2) has 2 paragraphs, and for Mountain Collective an inline link
to mountaincollectivebozeman.com.

**Films & journalism (`#films`)** — background `#efe9df`. Section lead, then three film entries.
Left column: date+place, title, description, links. Right column (spans 2): the players.

Vimeo embeds. Wrapper: `position:relative; width:100%; padding-top:56.25%; background:#26231f`;
iframe absolutely positioned to fill, `border:0`, `loading="lazy"`,
`allow="fullscreen; picture-in-picture"`, src `https://player.vimeo.com/video/<ID>?title=0&byline=0&portrait=0`.

- **The Ride Home** (2012–2013 · Montana) — five episodes in a grid, `repeat(auto-fit,minmax(300px,1fr))`, `gap:20px`, each labeled EPISODE 1–5 beneath. IDs in order: `44007671`, `44478035`, `45218637`, `46257874`, `64830728`. Links: "Full series on Vimeo" → https://vimeo.com/channels/348513 ; "IMDb" → https://www.imdb.com/title/tt1564569/
- **Maasai at the Crossroads** (2008–2010 · Kenya) — single trailer, ID `14944432`, labeled TRAILER. Link: "Watch on Vimeo" → https://vimeo.com/14944432
- **Hlabisa: An Unbroken Spirit** (2004–2005 · South Africa) — text only, two paragraphs, no player.

> **Open item for the developer:** confirm with Kristin that the IMDb title ID `tt1564569`
> belongs to The Ride Home before shipping. It was supplied alongside the Ride Home links but
> was never verified.

**Writing (`#writing`)** — top border ink. Eyebrow "WRITING", lead "Essays on nature, practice,
and paying attention.", body "New pieces arrive on Substack.", and an outline button
"Read on Substack" → https://substack.com/@kristinjordan (`align-self:flex-start`).

**Contact (`#contact`)** — top border ink. Big Newsreader headline, then the Email me /
Read my resume button pair, then a metadata row (`gap:8px 28px`, wraps, 15px `#4a4540`,
`padding-top:24px; border-top:1px solid #e4ddd1`): Bozeman, Montana · mountainyogabozeman@gmail.com ·
310.428.0434 · mountaincollectivebozeman.com · Substack.

### Resume — two pages (`Kristin Jordan Resume.dc.html`)
US Letter, 8.5in × 11in, cream `#f9f6f0`, `padding:48px 64px 44px`. Base 13px / 1.45.
Two-column grid per block: `132px` label column + content, `gap:28px`. Section labels are the
same clay 11px uppercase 0.14em eyebrow.

Page 1: header (name Newsreader 500 44px; clay italic 19px tagline
"Community Builder · Program Designer · Storyteller"; right-aligned contact block;
`border-bottom:1px solid #26231f`), Profile, Strengths (3 columns of bulleted lists with
4×4px clay square markers, `list-style:none`), Experience (Mountain Collective, Bozeman Health,
Mountain Yoga). Page 2: Experience continued (Yoga Soup, Lululemon), Film & Journalism (one
paragraph), Education, Certifications & interests. Both pages carry an uppercase footer with her
name and page number above a `1px solid #d9d2c6` rule.

`Kristin Jordan Resume -print-.html` is the print/PDF version: `@page{size:letter;margin:0}`,
fixed 8.5in × 11in pages with `break-after:page`, `print-color-adjust:exact` so the cream
background prints. Print with margins set to None and background graphics enabled.

## Interactions & Behavior
- Smooth scroll on in-page anchor links (`html{scroll-behavior:smooth}`).
- Nav is sticky and translucent with a blur; no scroll-spy / active-state highlighting in the design.
- Button hovers as specified above. Text links: clay, underline on hover.
- No animations, transitions, carousels, modals, or scroll-triggered reveals. Keep it still.
- Vimeo players are lazy-loaded; no custom player controls or autoplay.
- No forms, no JS state, no data fetching. The only actions are `mailto:` and external links.

## Responsive behavior
Fully fluid — every layout uses `repeat(auto-fit,minmax(...,1fr))` and wrapping flex rows, so
columns collapse naturally as the viewport narrows. `clamp()` handles type scaling. No media
queries are required. Verified at 924px with no horizontal overflow. Test the nav row wrap and
the 5-up episode grid at ~375px.

## State Management
None. This is a static content site.

## Assets
- No images, icons, or illustrations. The design is entirely type, color, and rules — this is intentional; do not add stock photography.
- Fonts: Newsreader and Source Sans 3 from Google Fonts (link above).
- Video: hosted on Vimeo, embedded by ID. Nothing to self-host.
- **Missing asset:** no photography of Kristin, the retreat, or the studio was ever supplied. If she provides photos later, natural insertion points are the hero (right column), each Work entry, and the Films section.

## Files in this bundle
| File | What it is |
|---|---|
| `kristin-site-reference.html` | Plain-HTML export of the site — open this first |
| `Kristin Jordan Site.dc.html` | Site source, design-component format |
| `Kristin Jordan Resume.dc.html` | Resume source, design-component format |
| `Kristin Jordan Resume -print-.html` | Print/PDF resume, plain HTML, US Letter |
| `support.js` | Runtime for the `.dc.html` files. Not part of the design — ignore when porting |
| `doc-page.js` | Paged-document helper used by the resume. Not part of the design — ignore when porting |

## Screenshots
`screenshots/01-site.png` … `10-site.png` — the site top to bottom (Vimeo iframes appear as
dark boxes; the capture tool cannot render third-party iframe content).
`screenshots/01-resume.png`, `02-resume.png` — resume pages 1 and 2.

## Content note
All copy was written and revised with Kristin and is approved. Use it verbatim. The voice is
deliberately plain and warm, first person, no marketing language — if you need to add or cut
copy, ask rather than rewriting.
