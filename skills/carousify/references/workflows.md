# Workflows: posting, scheduling, approvals, files, analytics

## Accounts and time
- `list_accounts` returns each account as `{id, type, platform}`: LinkedIn personal profile (`profile`, `linkedin`),
  LinkedIn company page (`pages`, `linkedin`), Instagram (`profile`, `instagram`). Pass these exactly.
- It also returns the workspace timezone. Convert the user's times into ISO 8601 with that offset (e.g. 10:00 in
  Asia/Kolkata on 2026-11-02 → `2026-11-02T10:00:00+05:30`). Scheduled times must be at least 5 minutes ahead.
- If the timezone is "not set", ask which timezone the user means before scheduling.

## Posts
- **Create**: `create_draft` (nothing goes out). Include `selectedAccounts` if you know where it's going.
- **Change**: `edit_post` (text, media, document title, follow-up comments). Comments not passed are kept.
- **Schedule**: `schedule_post` with the post id and time. **Publish now**: `publish_post`. Both need a clear yes.
- **Delete**: `delete_post` moves it to the trash; a published post stays live on the network.
- `create_post` / `update_post` do all of the above in one tool; prefer the single-action tools so the user's
  approval settings apply per action.
- Limits: LinkedIn 3000 characters, Instagram 2200. LinkedIn: up to 20 images, or one video, or one document (PDF,
  needs a title). Instagram: up to 10 images/videos, no documents.
- **Follow-up comments** (e.g. the link in the first comment) go in `comments` with a delay; good for keeping links
  out of the main post.

## Approvals and permissions
- Some members' posts need approval: scheduling then returns "submitted for approval" — tell the user an approver
  must approve it. Approvers use `get_posts` (status `pending-approval`) and `review_post`.
- "Your role doesn't allow…" errors are real permission limits; say so and suggest asking a workspace admin.

## Carousels
- **From a template**: `list_templates` (sources: `carousify` library, `workspace`, `saved`, `community`; filter by
  `size`: 4/5 or 1/1 for feeds, 56/71 for LinkedIn documents) → `get_template` → plan slides → `create_carousel`
  with an ordered `slides` list: the cover once, the repeatable slide once per point, the last slide once.
- **Brand-new design**: see `template-design.md`.
- **Refine**: `get_carousel` shows slots, current text and the brand; `edit_carousel` rewrites, reorders,
  duplicates (repeat a slide_id), removes (leave it out), renames or switches brand kit.
- **Delete**: `delete_carousel` (to the trash, restorable in the app).
- **Turn into a post**: if a `create_carousel_post` tool is available, use it (LinkedIn gets a PDF document,
  Instagram gets images), then `schedule_post` / `publish_post`. If it isn't available, tell the user to open the
  editor link and use Publish/Schedule there.
- A new draft shows "Preview appears after you open and save it" in the Drafts list until it has thumbnails; that's
  expected.

## Files from the user
- You have the file's bytes (≤ 3.5 MB)? `upload_media` with base64.
- Otherwise `create_upload_link`, give the user the link (30 minutes, up to 10 files, they must be logged in), then
  `get_uploaded_files` with the `upload_id` once they say they're done. Pass the returned URLs as `media`.
- Public URLs also work directly as `media`; private/internal addresses are refused.

## Analytics
- `get_posts` status `posted` for recent posts; `get_analytics` with a post `id` or an account
  (`accountId`, `accountType`, `accountPlatform`) and a `startDate`/`endDate` (only the latest 200 snapshots come
  back without a range).
- Report insight, not tables: what topics, formats and hooks did best, and one or two concrete next steps.
