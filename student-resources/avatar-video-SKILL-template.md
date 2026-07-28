---
name: avatar-video
description: |
  Generate a Higgsfield/Seedance talking-head video clip of your locked
  AI Twin avatar, fully compliant with your project's GLOBAL VIDEO
  DIRECTION (continuity, lighting, camera, performance, negative rules)
  and speaking in your real voice via a locked voice reference. Use when:
  generating any clip of your avatar speaking a script (welcome videos,
  hooks, funnel/ad scripts, community content, any "make a video of me/my
  avatar saying..." request in this project). Enforces consistent avatar
  identity, studio, lighting, camera, and speech pace across clips so a
  multi-part series reads as one continuous recording, and burns captions
  onto the final assembled output.
  NOT for: generating static hero/reference images (that's a plain
  generate_image call against your visual-reference.md), or video of
  anyone/anything other than your locked avatar.
argument-hint: "[script text] [--duration seconds] [--wps words-per-second]"
allowed-tools: mcp__<HIGGSFIELD_MCP_ID>__generate_video, mcp__<HIGGSFIELD_MCP_ID>__explainer_video, mcp__<HIGGSFIELD_MCP_ID>__job_display, Read, AskUserQuestion
---

# Avatar video generation — AI Scale Engine template

Generates one Seedance clip of YOUR locked avatar, speaking in your real
voice, per your project's locked creative and technical bible, then
produces a captioned final cut.

## Setup — fill these in before first use

Before this skill works for you, do three things:

1. **Replace `<HIGGSFIELD_MCP_ID>`** in the `allowed-tools` line above with
   your own Higgsfield MCP server's connector ID (find it by checking your
   available tools — it looks like `mcp__<long-id>__generate_video`).
2. **Create your own source-of-truth files** inside your project folder
   (copy the structure from this template's sibling
   `GLOBAL_VIDEO_DIRECTION-template.md`, or write your own):
   - `GLOBAL_VIDEO_DIRECTION.md` — your studio, lighting, camera, and
     performance rules (see template).
   - `visual-reference.md` — your locked hero image and its generation
     settings.
   - `AVATAR_LOCK.md` — your Higgsfield Element ID for your avatar
     identity. Fill in `YOUR_AVATAR_ELEMENT_ID` with your own real
     `show_reference_elements` Element id before running this skill.
   - `VOICE_LOCK.md` — your locked voice reference (see Module 3 tutorial).
     Fill in `YOUR_VOICE_MEDIA_ID` with the uploaded audio file's media_id
     — NOT a `create_voice` voice_id, the two are different things and only
     the raw audio file's media_id works as `audio_references`.

Do not run this skill with the placeholder IDs left in place — it will
either error or (worse) silently generate against the wrong identity.

## Inputs needed from the user (ask if not given)

- **Script text** — what the avatar says in this clip.
- **Duration** — if not given, infer from script length at the target
  words/sec (see below), capped at Seedance 2.0's hard 15-second max per
  clip. If the natural duration exceeds 15s, either round the duration down
  to 15 (small pace absorption, preferable to cutting words) or split into
  multiple continuity-locked clips — ask the user which they prefer, never
  silently truncate the script.
- **Words-per-second** — if the user specifies an exact rate, use it
  exactly. Otherwise default to your GLOBAL VIDEO DIRECTION's target words-
  per-minute range (a common starting point is 150–175 wpm, ~2.5–2.9
  words/sec — adjust to your own voice).
- **Performance beat/arc for this specific clip** — if the user gives
  delivery notes (tone per line, pauses, gesture cues), fold them into the
  prompt verbatim rather than genericizing them.

## Steps

1. Read your `GLOBAL_VIDEO_DIRECTION.md`, `visual-reference.md`,
   `AVATAR_LOCK.md`, and `VOICE_LOCK.md` to pull your locked Element ID,
   hero image job id, voice reference media_id, studio/lighting
   description, and all standing rules.
2. Compute target duration from script word count ÷ words-per-second (see
   the duration-handling guidance above). Never silently truncate the
   spoken script to fit.
3. Build the `generate_video` prompt combining:
   - `<<<YOUR_AVATAR_ELEMENT_ID>>>` embed for identity (from your
     AVATAR_LOCK.md)
   - Studio/lighting/camera description (from your
     GLOBAL_VIDEO_DIRECTION.md — keep it IDENTICAL in wording across clips
     in the same series, so the model has the same continuity anchor every
     time)
   - This clip's specific performance arc, script (verbatim, in quotes),
     and delivery notes — mention "speaking in your own natural voice
     matching the provided audio reference" so the model ties delivery to
     the audio input
   - The negative rules from your GLOBAL_VIDEO_DIRECTION.md (no
     captions/text baked into the generation prompt itself — captions
     happen later, at assembly)
4. Call `generate_video` with `model: seedance_2_0`, `aspect_ratio: 9:16`
   (or your preferred output format), the computed `duration`,
   `generate_audio: true`, your locked hero image job id as an `image`
   media role, your locked voice reference media_id (from VOICE_LOCK.md)
   as an `audio` media role, and `declined_preset_id` set if a preset
   match notice appears on a preflight (if you always want literal
   generation, never a stylized preset).
5. Preflight cost with `get_cost: true` first and confirm with the user
   before submitting the real generation — always confirm before every
   paid generation.
6. The generated clip already speaks in your real voice via the
   `audio_references` input — **no separate voice-swap step is needed.**
   Passing a `voice_id` from a voice-cloning feature here does NOT work
   (it errors) — only the raw uploaded audio file's media_id works.
7. **Captions (if your GLOBAL_VIDEO_DIRECTION.md requires them):** once
   the clip is ready — and if this is a multi-clip series, once all clips
   for this piece are ready — run `explainer_video` to assemble/stitch the
   final cut with `subtitles: {font: ...}` set. This transcribes the final
   voiceover via Whisper and burns timed captions onto the output
   automatically. Pick a font matching your brand from the tool's options
   (patrick, caveat, marker, anton).
8. Present the final clip URL to the user for approval. Do not treat a
   generated clip as final/approved without the user explicitly
   confirming it.

## Continuity rule for multi-clip series

When generating Part 2+ of a series, reuse the EXACT same studio/lighting/
camera prompt text used in Part 1 — do not rephrase or "improve" the
wording between clips, since small wording differences can produce visible
drift in the generated environment. Copy the locked block verbatim.
