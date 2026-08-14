---
name: avatar-video
description: |
  Generate a Higgsfield/Seedance talking-head video clip of Mohamed's locked
  AI Twin avatar (mohamed-avatar-2) for the AI Scale Engine project, fully
  compliant with SEEDANCE.md (concept, identity, continuity, lighting,
  camera, performance, negative rules) and speaking in his real voice via a
  locked voice reference. Use when: generating any clip of Mohamed's avatar
  speaking a script (welcome videos, hooks, funnel/ad scripts, Skool
  content, any "make a video of me/my avatar saying..." request in this
  project). Enforces consistent avatar identity, studio, lighting, camera,
  and speech pace across clips so a multi-part series reads as one
  continuous recording, and burns captions onto the final assembled output.
  NOT for: generating static hero/reference images (that's a plain
  generate_image call against visual-reference.md), or video of anyone/
  anything other than Mohamed's locked avatar.
argument-hint: "[script text] [--duration seconds] [--wps words-per-second]"
allowed-tools: mcp__fbc7be1f-a61a-40a8-b9df-6066b4219553__generate_video, mcp__fbc7be1f-a61a-40a8-b9df-6066b4219553__explainer_video, mcp__fbc7be1f-a61a-40a8-b9df-6066b4219553__job_display, Read, AskUserQuestion
---

# Avatar video generation (AI Scale Engine)

Generates one Seedance clip of Mohamed's locked avatar, speaking in his
real voice, per the project's locked creative and technical bible, then
produces a captioned final cut.

**Note on location:** this skill file lives at the `ThefounderStudio` repo
root (not inside `ai-scale-engine-mo-test-3/`) so it's reliably discovered
regardless of which subfolder the session is working from. This is a
deliberate exception to the project's "everything lives inside
ai-scale-engine-mo-test-3" storage rule — see `CLAUDE.md` in that project
folder for the note explaining why. All actual creative/generation content
still lives inside `ai-scale-engine-mo-test-3/` — this file only orchestrates
it and must be re-read from there every run.

Read the source-of-truth files before every invocation — do not hardcode
their content here, since they may be updated independently of this skill:

1. `ai-scale-engine-mo-test-3/SEEDANCE.md` — the **one and only** creative
   and technical bible for this project (concept, identity, studio,
   lighting, camera, performance, continuity, negative rules, captions
   policy, pacing math, hand-gesture bank, lean negative prompts, prompt
   template, bug fixes). Read this before building any prompt — it's the
   primary reference for both WHAT to include and HOW to write the
   generate_video call. `GLOBAL_VIDEO_DIRECTION.md` was merged into this
   file and deleted (2026-07-30) — do not reference or recreate it.
2. `ai-scale-engine-mo-test-3/visual-reference.md` — current locked hero
   image / generation settings.
3. `ai-scale-engine-mo-test-3/AVATAR_LOCK.md` — Element ID and usage rule.
4. `ai-scale-engine-mo-test-3/VOICE_LOCK.md` — locked voice reference
   media_id, passed directly as `audio_references`.

## Inputs needed from the user (ask if not given)

- **Script text** — what the avatar says in this clip.
- **Duration** — if not given, infer from script length at the target
  words/sec (see below), capped at Seedance 2.0's hard 15-second max per
  clip. If the natural duration exceeds 15s, tell the user the script needs
  to be split into multiple continuity-locked clips (same studio/lighting/
  camera) rather than silently truncating it.
- **Words-per-second** — if the user specifies an exact rate, use it
  exactly. Otherwise default to SEEDANCE.md's standard pace, **3.0
  words/sec** (updated 2026-07-30), unless the script is a fast hook that
  calls for the dynamic 4.5 words/sec pace (see SEEDANCE.md's pacing table
  for when to use which).
- **Performance beat/arc for this specific clip** — if the user gives
  delivery notes (tone per line, pauses, gesture cues), fold them into the
  prompt verbatim rather than genericizing them.

## Steps

1. Read `SEEDANCE.md`, `visual-reference.md`, `AVATAR_LOCK.md`, and
   `VOICE_LOCK.md` to pull the current locked Element ID, hero image job
   id, voice reference media_id, studio/lighting description, and all
   standing rules.
2. Compute target duration from script word count ÷ words-per-second. If
   duration would round up over 15s, either round the passed `duration`
   down to 15 (small pace absorption is preferable to cutting script text)
   or split into multiple continuity-locked clips — ask the user which
   they prefer when the overage is more than trivial. Never silently
   truncate the spoken script.
3. Build the `generate_video` prompt following SEEDANCE.md's template and
   rules:
   - `<<<ELEMENT_ID>>>` embed for identity (from AVATAR_LOCK.md) — never
     `@image_1`/`@audio_1`-style tags, those are a web-UI convention
     unconfirmed for this MCP interface
   - Studio/lighting/camera description (from SEEDANCE.md — keep it
     IDENTICAL in wording across clips in the same series, so the model
     has the same continuity anchor every time)
   - One flowing paragraph for the performance/action — a pre-line beat,
     the script woven with 2-3 hand gestures mapped to specific words
     (SEEDANCE.md's gesture bank), a post-line beat. No internal
     timestamps — single continuous shot, not a multi-cut sequence.
   - **Gestures stay small and restrained**, per SEEDANCE.md's PERFORMANCE
     rule — map to words per the gesture bank, but this is a
     founder talking to friends, not an energetic hype reel. A request for
     "more dynamic/energetic" gestures or camera movement is a deliberate
     per-clip departure the user must explicitly ask for — never apply it
     by default (confirmed 2026-07-30: a test departure produced a
     noticeably worse result than the locked restrained-gesture baseline).
   - Reference the audio by function only: "lip-sync driven by the
     provided audio reference" — never describe its texture (no "phone
     mic," no "room bleed"), that recolors clean audio toward unwanted
     artifacts.
   - Avoid the word "cinematic" anywhere in the prompt for this locked
     studio look — use "static," "locked," "documentary," or "prosumer
     camera" instead.
   - Negative prompt: use SEEDANCE.md's full locked NEGATIVE RULES list
     (not a shortened ad-hoc 2-3 item list) — those are standing
     brand rules, not a per-clip stack. Always include "no rings or jewelry
     on the hands, no wedding band" (added 2026-07-30 after a hallucinated
     ring appeared with nothing in the prompt or reference suggesting it).
     Add one additional surgical line only for a new specific recurring
     bug, don't otherwise stack beyond the locked list.
4. Call `generate_video` with `model: seedance_2_0`, `aspect_ratio: 9:16`,
   the computed `duration`, `generate_audio: true`, the locked hero image
   job id as an `image` media role, the locked voice reference media_id
   (from VOICE_LOCK.md) as an `audio` media role, and `declined_preset_id`
   set if a preset match notice appears on a preflight (this project always
   wants literal generation, never a stylized preset).
5. Preflight cost with `get_cost: true` first and confirm with the user
   before submitting the real generation — this project's standing rule is
   explicit confirmation before every paid generation, every time.
6. The generated clip already speaks in Mohamed's real voice — **no
   separate voice-swap step is needed.** (An earlier version of this
   pipeline used a two-step generate-then-`voice_change` approach; that was
   superseded once direct `audio_references` generation was confirmed
   working. Do not reintroduce it.)
7. **Captions (required, per SEEDANCE.md):** once the clip is
   ready — and if this is a multi-clip series, once all clips for this
   piece are ready — run `explainer_video` to assemble/stitch the final cut
   with `subtitles: {font: ...}` set. This transcribes the final voiceover
   via Whisper and burns timed captions onto the output automatically. A
   single-clip piece still goes through this step (list it as the only
   `items` entry) so captions get applied consistently. Pick a font
   matching the brand: default to `anton` (bold condensed impact) for
   hook-heavy short-form unless the user specifies a different one from the
   tool's options (patrick, caveat, marker, anton).
8. Present the final captioned clip URL to the user for approval. Do not
   treat a generated clip as final/approved without the user explicitly
   confirming it.

## Continuity rule for multi-clip series

When generating Part 2+ of a series, reuse the EXACT same studio/lighting/
camera prompt text used in Part 1 — do not rephrase or "improve" the
wording between clips, since small wording differences can produce visible
drift in the generated environment. Copy the locked block verbatim.
