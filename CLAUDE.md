# Lucky Seven website — project notes

Single-file static site (`index.html`) for Lucky Seven, a Tokyo brand & communications
consultancy. Pure HTML/CSS/vanilla JS, no framework, no build step, no database.
`luckyseven-tuner.html` is a personal tinkering copy with live sliders for the particle
motion — NOT part of the live site, don't touch it as part of site work.

Repo: github.com/luckystudiojp/luckyseven_site, branch `main`. Gavin pushes are done via
plain `git` (no `gh` CLI installed). Domain `luckyseven.jp` currently runs the old live
Squarespace site — this repo is the replacement, not yet connected to the domain.

## Locked — do not change without explicit sign-off

The particle field signature: a star/particle canvas that morphs on scroll through
`?` (curiosity) → `◯` maru (brands) → arrow (services) → node-hub (Working with AI) →
`7` (contact). The physics config (in the JS particle-field IIFE) is hand-tuned and
LOCKED:
follow 0.02, scrollSmooth 1, linger 1, chaosSpread 1.9, breakEnd 0.35, formStart 0.8,
stir 0.58, breathe 21, stars 6200 desktop / 2600 mobile, node glyph (not infinity).

## Workflow

For copy/design changes: read the relevant part first, make a surgical edit, let Gavin
preview locally (his browser, not mine — see sandbox note below), and only commit +
push to `main` once he confirms. Don't bundle unrelated changes into one commit unless
told to.

## Sandbox note

If you (the assistant) find your browser/preview tool can't render this folder, you're
in a session rooted in the wrong project — this file being loaded means that's fixed.
If for some reason it's still wrong: this folder has no dev server / build step, so
`file://` opening the raw `index.html` should just work directly in your browser tool.

## Status as of last handoff (2026-07-22)

**Phase 1 — Desktop copy/design: essentially done**, several rounds of copy edits
signed off and pushed. Not "final forever" — Gavin will keep tweaking copy over time.

**Phase 2 — Mobile pass: in progress.** Done and pushed (commit `664b0b8`):
- Hamburger nav (mobile menu overlay, replaces the 4-pill nav that overflowed)
- Hero headline word-wrap fix (letters were individually `inline-block`, causing
  mid-word line breaks on narrow screens — now grouped into `.word` wrapper spans)
- Brands grid: tighter cell padding on mobile to shorten the long scroll
- Footer: stacks vertically on mobile instead of an unbalanced `space-between` row
- Services section: horizontal scroll-jack JS now skipped on mobile (`window.innerWidth
  <= 860` check in `onScroll()`); cards stack vertically with natural height instead of
  the forced min-height + `margin-top:auto` gap between title and copy

**Not yet done / open items** (mirrors the task list from the prior session — recreate
with TaskCreate if useful):
1. Extract the two embedded base64 images (logo ~23KB, about-section photo ~154KB
   decoded) into real external image files. Currently inline data URIs inflate
   `index.html` to ~283KB when the actual code is only ~41KB. Doing this enables
   browser caching/lazy-loading — matters for mobile perf. Not yet started.
2. Verify the mobile fixes above actually work on Gavin's phone (they were pushed but
   not yet confirmed live — no way to test JS execution in the previous session's
   sandbox).
3. Particle field mobile performance — check real frame rate on phone, may need to
   lighten further than the existing 2600-star mobile count. Must preserve the locked
   physics values above.
4. iOS Safari viewport quirks — address bar collapse/expand, safe-area insets.
5. Finger-sized tap targets throughout (~44px).
6. A known, deliberately deferred item: the "maru" circle particle shape overlaps/
   reduces legibility of the Brands grid text on mobile (page is proportionally taller
   on mobile, shifting where scroll-triggered shapes land vs. content). Gavin explicitly
   said to fix everything else first and revisit this later — don't just dive in on it.

**Phase 3 — Deploy prep: not started.** Confirm `index.html` naming (done), add favicon
from the logo, add meta tags (title done, needs description + OG/Twitter card for
LinkedIn link previews), then GitHub Pages + connect `luckyseven.jp` — leave MX/email
DNS records untouched.

## Known gotchas already solved once — don't rediscover these

- **Repo now lives under the `luckystudiojp` GitHub org**, transferred from personal
  account `cranno` on 2026-07-22. GitHub Pages preview is live at
  `luckystudiojp.github.io/luckyseven_site` (carried over automatically through the
  transfer, confirmed working). `cranno` stays reserved for Gavin's personal/non-client
  projects; `luckystudiojp` is the umbrella org for Lucky Seven and other consulting
  client work — solo org, free tier, no billing implications. Local git remote already
  updated to point at the new location.
- **The contact email `hello@luckyseven.jp` bounces** — it's a placeholder that was
  never actually provisioned as a real mailbox. Gavin's current live Squarespace
  contact form actually delivers to his personal iCloud address. He's said he'll create
  the real `hello@` mailbox in Squarespace's email tooling himself, last, before going
  live — don't change the mailto link without him confirming a working address.
- File is large (~285KB) almost entirely because of the two embedded base64 images —
  see open item #1. The actual HTML/CSS/JS is lean (~41KB) and reasonably organized
  (labeled CSS section comments, CSS custom properties, one IIFE for JS) — it is not
  "clunky tacked-on code," Gavin asked about this directly and this was confirmed by
  measuring the file, not by assumption.
