# Handoff: Chasing the Sash graphics and production quality

Last updated: 2026-10-11
Owner: Sean. Currency: AUD. Scope: Chasing the Sash (CTS) only.

> Sean normally wants repo docs as schema/plain text (see `HANDOFF.schema`). This file is Markdown because he asked for one for this handover. `HANDOFF.schema` is still the main project log.

## Goal

1. Improve the production quality of CTS videos with templates and better graphics. That covers lower thirds, key-term cards, the logo intro and thumbnails, in 16:9 and 9:16.
2. **Next session (local):** watch four videos on Sean's PC, compare the raw recordings against the polished edit, and come back with recommendations. Then build a prototype template or edit workflow.

## Videos to review (on Sean's PC only, not in the repo or Google Drive)

```
C:\Users\C.Sean Cheng\Downloads\riverside_mediaboard_image_raw-video-cfr_hannah_brooks's stu_0255.mp4
C:\Users\C.Sean Cheng\Downloads\riverside_neil_grigg_raw-video-cfr_hannah_brooks's stu_0254.mp4
C:\Users\C.Sean Cheng\Downloads\riverside_sharon_lenton_raw-video-cfr_hannah_brooks's stu_0253.mp4
C:\Users\C.Sean Cheng\Downloads\Video-72391.mp4
```

- The three `riverside_*` files look like raw Riverside.fm recordings from Hannah Brooks's studio:
  - a media board / image track,
  - Neil Grigg's camera,
  - Sharon Lenton's camera.
- `Video-72391.mp4` is probably the polished edit. **Confirm this with Sean.**
- Neil and Sharon are also listed as tracker users in the CTS tracker README. Hannah is a co-approver of interviewee submissions.

## Current progress

### Graphics Lab (prototype page)

- **File:** `graphics-lab.html` at the repo root.
  - Uses `images/hero.jpg` as sample footage and `images/cts-logo-badge.svg` as the official logo.
- **Live preview:** https://claude.ai/artifact/CQbAba6eUxinovVMseFz65
  - Shared as "anyone with the link".
  - Viewers see republishes immediately.
- **Branch:** `claude/jolly-cori-wsd1p0`.
- **Draft PR:** [cseancheng2018-hub/CTS_WEBSITE#2](https://github.com/cseancheng2018-hub/CTS_WEBSITE/pull/2).
  - No CI on the repo.
  - No review comments yet.
  - **Do not merge until Sean picks designs.** Merging publishes the page at chasingthesash.com/graphics-lab.html.

The page has four graphic types. Every one has a 16:9 / 9:16 toggle, a "Compare all 12" grid and safe-zone overlays.

| Graphic type | Options | Notes |
|---|---|---|
| Person lower third | 12 styles: A Editorial, B The Sash, C Entrant Card, D Race Book, E Photo Finish, F Hatbox, G Frosted, H Night Meet, I Swing Tag, J Monogram, K Catwalk, L Trophy Plaque | Position presets: bottom-left, bottom-centre, bottom-right, top-left, top-right. Size slider 50–160%. Offset sliders in video pixels. |
| Key-term lower third | Same 12 styles | Four term presets: Millinery, Fascinator, Fashions on the Field, The Sash. Pronunciation and word type show in styles C and I only. |
| Logo intro | 12 animations of the badge only: Soft Focus, Ring Draw, Ink Outline, Letter Drop, Stamp, Coin Flip, Iris, Diagonal Wipe, Pop, Light Sweep, Pull Back, Split Slide | Sean asked for the logo alone, animated differently, with nothing around it. The badge SVG is inlined in `<template id="logoTpl">` and split into 14 letter paths: row 1 is CHASING, row 2 is THE SASH, in absolute coordinates on an 1880×1880 canvas. |
| Thumbnail | 12 designs: Big Type, Sash Band, Cover Story, Blush Circle, Spotlight, Race Book, Night Meet, Polaroid, Big Number, Duotone, Quote, Sticker | Sizes: 1280×720 for YouTube and 1080×1920 vertical. Headline is editable, and `*stars*` turn words pink. Name, episode, photo upload and a photo-focus slider are also editable. |

**Brand:**
- Website colours: black `#090907`, cream `#F4EDE0`, pink `#FF1F6E`, gold `#C6993A`.
- Badge colours: blush `#F2D9D9`, ink `#2A2420`.
- Fonts: Cormorant Garamond for headings, Montserrat for body text.
- Tagline: "Stories behind the Sash".

**Placeholder text (not verified):**
- Brooke Strahan's title, "Season 1" and entrant number 07.
- The headline "One sash changes everything", adapted from the website logline.

### Waiting on Sean

- Pick favourites: 2–3 lower-third styles, 1–2 logo animations and 2–3 thumbnails.
- Real names, titles and episode stills.

## What worked

- **One HTML page with a scaled stage.** It renders at true video resolution (1920×1080, 1080×1920, 1280×720) and is scaled with CSS, so the offsets and sizes are real pixel values for the edit.
- **CSS keyframe animations**, triggered by toggling `.play` and `.out` classes on `.frame`. The `.static` class freezes the animation while the user is typing.
- **Per-letter logo animation**, done by splitting the badge's single `<path>` on `M` commands. Each subpath is one letter, and counters such as the hole in the A stay inside it as relative `m`. `pathLength="1"` allows stroke-draw effects.
- **Playwright screenshots** for a visual check: Chromium is at `/opt/pw-browsers/chromium`, run with `NODE_PATH=$(npm root -g)`.

## What didn't work

- **Lowercase format classes `.frame.h` and `.frame.v`.** When the file is opened without a doctype, browsers ignore case in class names, so `.H` (style H) clashed with `.h` (16:9 format). They were renamed to `.fh` / `.fv`. Keep class names distinct regardless of case.
- **The cloud session couldn't reach the videos.** They are local Windows paths, and they aren't in Google Drive. That's why the review moves to a local session.
- **The artifact viewer blocks downloads**, so the page can't export PNGs or video. Render final assets locally instead, for example with Playwright screenshots, or rebuild them in Premiere or After Effects.
- **Logo intros with frames around the badge** (bands, rosettes, plaques, tags). Sean rejected these and wants animation variations of the logo alone.
- **Dead code:** per-style logo CSS (`.A-wm`, `.B-band`, `.C-ros` and similar) is still in the file but no longer used. It's safe to delete during cleanup.

## Next steps (local session)

1. Ask Sean which video is the polished one, and confirm it's `Video-72391.mp4`.
2. Watch all four files. Locally, use `ffprobe` for specs and `ffmpeg` to pull frames every 5–10 seconds, and transcribe with Whisper if needed. Note:
   - **Tech:** resolution, frame rate, audio levels and sync across the Riverside tracks, framing, lighting.
   - **Edit:** pacing, cuts between speakers, use of the media-board track, b-roll.
   - **Graphics in the polished cut today:** lower thirds, titles, logo, captions, end card.
   - **Gaps against the Graphics Lab options.**
3. Report back in plain English, short and in AUD where cost comes up:
   - what's working,
   - the top 5 quality improvements,
   - which templates to build first.
4. Agree a prototype with Sean. Likely options:
   - a Premiere Pro template project (.prproj) with a multicam setup for the Riverside tracks,
   - .mogrt lower thirds and logo intro using the chosen Graphics Lab styles,
   - an export preset for YouTube 16:9 and 9:16 Reels,
   - a caption style.
5. Keep `HANDOFF.schema` updated (append-only, plain text) and refresh this file.
6. Once a style is chosen, offer to write a CTS graphics skill file so the rules stay consistent.

## Pending housekeeping

- A safety-net check-in on PR #2 was scheduled from the cloud session (trigger `trig_01F5aa8V8uJAohYdH1JczLGJ`, about 12:03 UTC, 2026-10-11).
- Don't push to `main`. Work on `claude/jolly-cori-wsd1p0` or a new branch.
