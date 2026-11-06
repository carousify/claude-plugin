# Designing a brand-new carousel layout

Use this when the user wants something that isn't one of the existing templates ("design a new carousel", "make it
look completely different", "something bold/minimal/editorial").

## Flow
1. `list_accounts` (platform → size) and `list_brand_kits` (palette, fonts, which kit to apply).
2. `get_template_spec` once per conversation. It is the source of truth for the JSON format, element types, the 4
   fixed brand/numbering elements, and the exact lists of shape ids, Lucide icon names and font families. Use names
   exactly as listed: an unknown icon, shape or font is an error, not a fallback.
3. Pick a style from `styles.md` (or the user's own direction) and, for a sense of craft, open one example from
   `examples/` that's closest in spirit. Study its composition — margins, hierarchy, how accents are used — rather
   than copying it. The examples are hand-tuned, published designs (all 56/71; scale positions for 4/5 or 1/1):
   - `daily-posting-lessons.json` — black, huge all-caps white Sora hook, a divider, a small grey setup line and a
     short bold punchline ("It's not."); almost no decoration
   - `fullstack-dev-life.json` — near-black, big Poppins heading with one blue accent phrase, letter-spaced
     "SWIPE →" in the accent color
   - `carousify-founder-story.json` — charcoal, story-led Outfit heading with one terracotta accent word, a quiet grey
     subline, letter-spaced "SWIPE TO READ THE STORY" with a long arrow
4. Write the template and call `create_template` with it (plus `brand_kit_id`, `name`). If it returns errors, fix
   exactly the listed fields and call again; nothing is saved until the whole template is valid.
5. Share the editor link. Text can later be changed with `get_carousel` / `edit_carousel`; a different layout means
   a new `create_template`.

## What makes these designs look professional
- **Hierarchy first.** One dominant element per slide (usually the heading), then the supporting line, then small
  details. Headings 20–60px bold (600–800), subheadings 11–22px semi-bold, body 11–16px regular.
- **Two fonts, three at most.** A display face for headings and a clean sans for body (e.g. Space Grotesk + Inter,
  Playfair Display + Inter, Archivo + Inter). Vary families between designs instead of defaulting to the same pair.
- **One accent color, used with intent.** Highlight one or two words per heading or a single badge; a design where
  everything is accented has no accent.
- **Consistent content slides.** Same positions for the title, body, numbering and icon on every content slide, so
  the set reads as one piece; slide-specific flair goes in decoration, not structure.
- **Breathing room.** Keep text 10–30px from the edges; let decorative shapes bleed off the canvas instead.
- **Depth without clutter.** Big low-opacity watermark numerals, a shape behind a heading, a rotated accent tag,
  thin divider lines — pick two or three motifs and repeat them.
- **Cover and outro as a pair.** The last slide mirrors the cover's identity and puts the brand front and centre.
- **Vertical balance (4/5).** Start the cover's eyebrow around y≈53–60 and let the title flow down, so empty space
  sits below the hero block; keep the outro's last element ending by y≈455. Treat cover/outro blocks as one group
  and move them together. Scale these numbers for other sizes.
- **Text that fits.** Size text boxes to their content (width wide enough for the longest line, height for the line
  count × line-height); single-line titles line-height ~1.1, large multi-line serif titles ~1.15.

## Sizes
- 4/5 (portrait) for LinkedIn and Instagram feeds — the default. 1/1 for square posts. 56/71 for LinkedIn
  document-style carousels. Match what the user is posting to.

## Images
- Leave image `src` empty ("") for a frame the user fills in the editor, or use a public https JPEG/PNG/WebP/GIF/AVIF
  URL (it's copied into the workspace). Prefer designs that don't depend on photos unless the user provides them.
