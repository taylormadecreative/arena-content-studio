# Arena Group Network — Content Studio

Client content-review dashboard for **Arena Hudson (AGN)**, built on the reusable
Taylormade Creative studio pattern (clone of the Panty Cakes studio, AGN-branded).

**Live:** https://taylormadecreative.github.io/arena-content-studio/

Arena can: review every post, **approve** or **request changes**, leave **notes**,
and **upload brand assets** — all of it saves on her device and is emailed straight
to Nelson (with a durable retry queue so nothing is ever lost).

## Updating content
Everything lives in the `POSTS` array near the top of the `<script>` in `index.html`.
Each post: `id, type, platform[], title, tag, goLive, time, deliveredAt, slides[], caption, status`.
Slides are webp files under `_assets/carousels/<post>/`. Commit + push `main` to update the live site.

### Drop in a finished Reel
A Reel shows "In production" until it has media. To make it live:
1. Export the video to `_assets/reels/<file>.mp4` (+ optional `<file>.webp` poster).
2. On that post, set `video:"_assets/reels/<file>.mp4"` (and `poster:` if you have one) and remove `video:null`.
3. Commit + push. The slot swaps from "In production" to a real player automatically.

**Pending reels to add:** the two rendered June reels (`new-construction`, `moving-to-dfw`)
live only in `~/Documents/.../review-dashboard/_assets/reels/` — copy them in when convenient.

## Edits → Nelson
- Approvals, change requests, and notes save to `localStorage` (namespaced `agn_*`) **and**
  email Nelson via FormSubmit (alias → taylormademd@gmail.com), with an SMS/mailto escape hatch.
- Unsent items queue in `agn_outbox` and auto-retry on next load.

## Optional: 1-tap desktop upload
Set `DROPBOX_REQUEST` (top of the script) to an AGN Dropbox File Request URL to add a
direct desktop upload button. Without it, phone uploads use the native share sheet and
desktop uploads open an email to Nelson.

## Deploy
Static site on GitHub Pages from `main` (root). `.nojekyll` is required so the `_assets`
folder is served. To update: edit, commit, push `main`.
