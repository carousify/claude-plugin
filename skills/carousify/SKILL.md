---
name: carousify
description: How to use the Carousify connector well to plan, write, design, brand, schedule and analyze LinkedIn and Instagram carousels and posts. Use this skill whenever the Carousify tools are available or the user mentions Carousify, carousels, LinkedIn or Instagram posts, slides, hooks, templates, brand kits, scheduling or post analytics — including requests like "turn this article into a carousel", "design a new carousel layout", "post this to my company page tomorrow", "make it on brand" or "how did my last posts do", even if they don't name Carousify.
---

# Carousify

Carousify is a carousel maker and scheduler for LinkedIn and Instagram. Through its connector you can read the user's
connected accounts, write and schedule posts, build carousels from templates or design brand-new ones, apply brand
kits, upload the user's own files, and read analytics — all inside one Carousify workspace (the one the user picked
when connecting).

The tools are the hands; this skill is the craft. Read the reference file that matches the task before you act:

| Task | Read |
|---|---|
| Posting, scheduling, approvals, uploads, analytics, timezones | `references/workflows.md` |
| Writing any carousel or post (hooks, slide flow, length, CTA) | `references/carousel-writing.md` |
| Making a carousel from an existing template | `references/carousel-writing.md`, then the "From a template" part of `references/workflows.md` |
| Designing a completely new layout (create_template) | `references/template-design.md` and `references/styles.md` (and one example from `examples/`) |
| Anything involving brand kits, logos, names, handles | `references/brand-kits.md` |

## Golden rules (why they matter)

1. **Start with context, not content.** Call `list_accounts` first: it gives the exact account ids you need and the
   workspace timezone. Guessing ids fails, and "tomorrow 9am" means the user's timezone, not UTC.
2. **Draft first; anything public needs a yes.** Saving a draft is safe and reversible. Publishing, scheduling and
   deleting reach real audiences or remove work, so show the user the final text, media, accounts and time, and wait
   for an explicit go-ahead. Tool permissions in the client may also ask the user to approve these calls.
3. **Write for the slot, not the page.** Template text slots come with a sample and a character count. Text that is
   much longer than the sample overflows the design; keep close to it.
4. **One idea per slide, one promise per carousel.** The cover makes a promise, each slide pays a piece of it off,
   the last slide tells the reader what to do next.
5. **Use the user's brand.** Pick the brand kit they name (or the workspace default) so the name, handle and logo on
   every slide are theirs. If a logo looks wrong, `edit_carousel` with `brand_kit_id` refreshes it.
6. **Errors are instructions.** When a Carousify tool returns an error it says exactly what to fix (a slot name, a
   field, an id, a limit). Fix that and call again rather than starting over or guessing a different approach.
7. **Hand back a link.** Carousels are drafts the user reviews in the Carousify editor; always give the editor link
   and say what's left for them (review, then post or schedule).

## Typical flows

- **"Make a carousel about X"** → `list_accounts` → choose a template (`list_templates`, `get_template`) or design one
  (`get_template_spec`, `create_template`) → write slides → `create_carousel` → share the editor link → if asked,
  turn it into a post (see workflows).
- **"Post this tomorrow at 10"** → `list_accounts` → `create_draft` → show the final post → after a yes,
  `schedule_post` in the workspace timezone.
- **"Use my photo / PDF"** → `upload_media` if you have the file's bytes, otherwise `create_upload_link` and
  `get_uploaded_files` after the user uploads.
- **"How are my posts doing?"** → `get_posts` with status `posted`, then `get_analytics` per post or account with a
  date range; summarize what worked, don't dump numbers.
