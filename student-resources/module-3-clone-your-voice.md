# Module 3 — Lock Your AI Twin (Avatar) & Clone Your Voice

This module has **two separate steps, run one after the other**:

- **Step A — Lock the Avatar** (B5): bundle your 3 reference images into
  one Higgsfield Element. This finishes and stops on its own — you get a
  clear completion message before moving on.
- **Step B — Lock the Voice** (B6): a completely separate prompt, run
  after Step A is done. It does NOT recreate the avatar — it references
  the Element Step A already locked.

Do not run these as one combined prompt. Run B5, wait for its completion
response, confirm it's correct, then run B6.

---

## What actually gets attached, and when

- **The document templates** (this module's text, plus the reference files
  shown at the bottom) are things you copy once — not attach to a chat
  message. You paste each into your project, fill in your own details, and
  move on.
- **What you actually attach in chat:** your 3 avatar reference images (or
  the 1 source photo you generate them from) in Step A, and your voice
  recording in Step B. Two separate attach moments, matching the two
  separate steps.

---

## STEP A — Lock the Avatar (B5)

### What you need

**Three avatar reference images** — or one source photo you'll generate
the other two from:
- **Hero Photo** — your primary facial identity and overall likeness.
- **Turnaround Sheet** — profile/side angles, head shape, proportions,
  hairstyle, consistent across viewpoints.
- **Close-Up Sheet** — skin detail, eyes, facial features, beard pattern
  (if applicable), texture, asymmetry, realism.

If you only have one photo, generate the other two from it first (ask
Claude to create a Turnaround Sheet and Close-Up Sheet from your Hero
Photo, and approve both before continuing) — then run the prompt below
once all 3 are approved.

### The B5 prompt

Attach your 3 approved reference images (or your 1 source photo, if you
want Claude to generate the other two as part of this same request), then
send:

> **OBJECTIVE**
>
> Now that the 3 avatar reference assets are ready — Hero Photo, Turnaround
> Sheet, Close-Up Sheet — bundle them together into ONE reusable Higgsfield
> Element. This becomes the permanent identity reference for all future AI
> Twin image and Seedance video generation in this project.
>
> **TASK**
>
> Create one Higgsfield Element containing all 3 images. Save it under the
> naming convention `[YOUR-NAME]-avatar`.
>
> **IMPORTANT RULE**
>
> These 3 images must be treated as ONE identity bundle. Do NOT save them
> as 3 separate reusable Elements. The Element must represent one locked
> avatar identity. Once created, use this single Element as the reference
> source for all future avatar-related generation.
>
> **REFERENCE SYNTAX**
>
> After the Element is created, reference it in future prompts using
> `@[YOUR-NAME]-avatar`.
>
> **FUTURE IMAGE GENERATION RULE**
>
> For every future Higgsfield image generation involving my AI Twin, use
> `@[YOUR-NAME]-avatar` as the primary identity reference. Do not ask me to
> re-upload the Hero Photo, Turnaround Sheet, or Close-Up Sheet again
> unless I explicitly replace the avatar reference set, the Element becomes
> unavailable, or I intentionally create a new avatar version.
>
> **FUTURE SEEDANCE VIDEO RULE**
>
> For every future Seedance / talking-head / B-roll video involving my AI
> Twin, use `@[YOUR-NAME]-avatar` as the identity reference. The avatar
> identity should remain locked across: face, facial proportions,
> hairstyle, beard pattern, skin tone, glasses (when applicable), age, body
> proportions, overall likeness.
>
> **IDENTITY PRIORITY**
>
> The 3 bundled images serve different purposes: Hero Photo → primary
> facial identity and overall likeness. Turnaround Sheet → profile, side
> angles, head shape, proportions, hairstyle, consistency across
> viewpoints. Close-Up Sheet → skin detail, eyes, facial features, beard
> pattern, texture, asymmetry, realism. Use all 3 together as one reference
> system — do not allow one image to override the others in a way that
> damages identity consistency.
>
> **AVATAR LOCK RULE**
>
> Once `@[YOUR-NAME]-avatar` is created and validated, treat it as LOCKED.
> Do not alter or reinterpret face shape, jawline, eyes, nose, beard
> structure, hairstyle, age, ethnicity, skin tone, or defining facial
> asymmetries unless I explicitly request a change.
>
> **PROJECT MEMORY UPDATE**
>
> After successful creation, update my project memory. Add to `CLAUDE.md`:
>
> ```
> ## AI Twin — Higgsfield Element
> Element name: @[YOUR-NAME]-avatar
> Status: LOCKED / APPROVED
> Contains: Hero Photo, Turnaround Sheet, Close-Up Sheet
> Usage rule: Use this Element as the default identity reference for
> every future Higgsfield image and Seedance video involving the AI Twin.
> Do not request re-upload of the source images unless the Element is
> replaced or unavailable.
> ```
>
> **AVATAR LOCK DOCUMENT UPDATE**
>
> Also create/update `AVATAR_LOCK.md` in `[YOUR-PROJECT-FOLDER]/` with:
>
> ```
> ## Higgsfield Identity Element
> Primary Element: @[YOUR-NAME]-avatar
> Identity Source: Validated Hero Photo + Turnaround Sheet + Close-Up Sheet
> Status: APPROVED / LOCKED
> Generation Rule: Every future avatar image or Seedance video must
> reference @[YOUR-NAME]-avatar unless explicitly instructed otherwise.
> ```
>
> **COMPLETION RESPONSE**
>
> Once the Element has been successfully created and stored, respond only
> with: "Avatar bundle locked. @[YOUR-NAME]-avatar is now the permanent
> Higgsfield identity reference for this project."
>
> If Higgsfield does not allow you to directly create or save the Element
> from this environment, do not pretend it was created. Instead, give me
> the exact final action I need to take, in the minimum number of steps.

**Stop here and confirm the completion response before moving to Step B.**

---

## STEP B — Lock the Voice (B6)

Only run this once Step A is done and confirmed. This step does NOT touch
the avatar Element — it only sets up your voice reference and connects it
to what Step A already locked.

### What you need

**One voice recording** — 10 seconds to 3 minutes of clear speech, minimal
background noise. A voice memo reading a paragraph out loud is enough.

### The B6 prompt

Attach your voice recording, then send:

> **OBJECTIVE**
>
> My avatar identity is already locked (see `AVATAR_LOCK.md`,
> `@[YOUR-NAME]-avatar`). Now lock my voice reference so every future
> avatar video speaks in my real voice automatically.
>
> **TASK**
>
> 1. Upload my attached voice recording to Higgsfield as an audio file and
>    confirm it. Give me the resulting media_id.
> 2. Save the recording itself into my project at
>    `[YOUR-PROJECT-FOLDER]/assets/voice/voice-reference.mp3` (or the
>    matching extension for my file type).
> 3. Create `VOICE_LOCK.md` in `[YOUR-PROJECT-FOLDER]/` documenting the
>    source audio path, the uploaded media_id, and this usage rule: every
>    avatar video generated for this project must pass this media_id as an
>    `audio_references` media role directly in the `generate_video` call,
>    alongside the avatar image reference from `AVATAR_LOCK.md` — one
>    generation call, no separate voice-swap step needed.
>
> **IMPORTANT RULE**
>
> Do not confuse this with Higgsfield's separate voice-cloning feature
> (`create_voice` / `create_voice_from_confirmed_audio`, which returns a
> `voice_id`). Passing a `voice_id` as `audio_references` fails with
> "Audio input not found." Only the raw uploaded audio file's media_id
> works here — I do not need the voice-cloning feature for this.
>
> **FUTURE VIDEO RULE**
>
> Do not ask me to re-upload or re-attach this voice recording again
> unless I explicitly replace the voice reference with a new recording.
>
> **COMPLETION RESPONSE**
>
> Once `VOICE_LOCK.md` is created and the media_id is confirmed, respond
> only with: "Voice locked. Every future avatar video for this project will
> use this voice reference automatically."

---

## After both steps: the skill that uses them

Steps A and B lock your identity and voice. To actually generate videos
using them consistently, you also need `GLOBAL_VIDEO_DIRECTION.md` (your
studio/lighting/camera/performance rules) and an `avatar-video` skill that
reads all of `AVATAR_LOCK.md`, `VOICE_LOCK.md`, `GLOBAL_VIDEO_DIRECTION.md`,
and `visual-reference.md` before every generation. That setup is covered
separately — see the `avatar-video-SKILL-template.md` and
`GLOBAL_VIDEO_DIRECTION-template.md` files alongside this module.

## Verify it actually worked

Once everything is set up, ask for a short test:

> "Generate a 5-second test video of my avatar saying 'Hey, this is a
> quick test' using the avatar-video skill."

Watch and listen. Don't assume it worked just because nothing errored —
check that the face is actually yours and the voice is actually yours. If
either is wrong, the fix lives in the relevant file: `AVATAR_LOCK.md` for
identity issues, `VOICE_LOCK.md` for voice issues.

---

## Reference — `AVATAR_LOCK.md` and `VOICE_LOCK.md` in full

### `AVATAR_LOCK.md` (created by Step A)

```
# AVATAR_LOCK

## Higgsfield Identity Element

**Element name:** [your-name]-avatar
**Element ID:** [the Element id returned when created]
**Category:** character
**Status:** APPROVED / LOCKED

**Identity Source:** Validated Hero Photo + Turnaround Sheet + Close-Up
Sheet, bundled together as ONE Higgsfield Element (not 3 separate ones).

**Generation Rule:** Every avatar image or video generated for this
project must reference this Element. Embed `<<<[your Element id]>>>`
in the generation prompt.

## Identity priority

- **Hero Photo** → primary facial identity and overall likeness
- **Turnaround Sheet** → profile, side angles, head shape, proportions,
  hairstyle, consistency across viewpoints
- **Close-Up Sheet** → skin detail, eyes, facial features, beard pattern,
  texture, asymmetry, realism

## Locked attributes

Do not alter or reinterpret without explicit request:
- face shape, jawline, eyes, nose, beard structure, hairstyle, age,
  ethnicity, skin tone, defining facial asymmetries, body proportions,
  glasses (if applicable)

## Source assets

- [path to your Hero Photo] — [resolution, aspect ratio]
- [Turnaround Sheet — job id if generated via Higgsfield]
- [Close-Up Sheet — job id if generated via Higgsfield]
```

### `VOICE_LOCK.md` (created by Step B)

```
# VOICE_LOCK

## Voice Reference (CURRENT)

**Source audio:** [path to your voice file, e.g. assets/voice/voice-reference.mp3]
**Uploaded media_id:** [the media_id returned after upload]
**Media type:** audio

## Usage rule

Every avatar video generated for this project must include this media_id
as an `audio_references` media role directly in the `generate_video` call,
alongside the avatar image reference:

medias: [
  { value: "<hero image job id, from AVATAR_LOCK.md>", role: "image" },
  { value: "[your voice file's media_id]", role: "audio" }
]

Seedance 2.0 generates the avatar speaking in this real voice in a single
pass. No separate voice-swap step is needed.

Do not confuse this with a voice-cloning feature's `voice_id` — that
fails here. Only the raw uploaded audio file's media_id works.
```
