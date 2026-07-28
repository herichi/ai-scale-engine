# Module 3 — Clone Your Voice & Lock Your AI Twin

This is a complete, standalone setup module. By the end of it, your avatar
identity AND your voice are both locked into your project, and you have a
working `avatar-video` skill that generates videos of you, speaking in
your real voice, automatically — every time, no re-setup.

You do not need anything from an earlier module to complete this one.
Everything you need is below.

---

## What actually gets attached, and when — read this first

- **The 5 documents below** (this module's text, plus 4 template files) are
  things you **copy once**, not attach to a chat message. You paste each
  one into your own project as a real file, fill in your own details, and
  move on. You never re-paste or re-attach them again after setup.
- **The ONE thing you actually attach in chat** is your voice recording —
  one audio file, one time, during Step 2 below.
- **The main action of this module is: one setup prompt + your voice
  recording attached.** That single message creates all 5 documents for
  you, correctly filled in, and locks everything.

---

## What you need before you start

1. **Three avatar reference images** (not just one — this matters for
   identity quality):
   - **Hero Photo** — your primary facial identity and overall likeness. A
     clear, forward-facing photo or a generated portrait.
   - **Turnaround Sheet** — profile/side angles, head shape, proportions,
     hairstyle, consistent across viewpoints. Can be generated from your
     Hero Photo (front/left/right/back views on one sheet).
   - **Close-Up Sheet** — skin detail, eyes, facial features, beard
     pattern (if applicable), texture, asymmetry, realism. Also can be
     generated from your Hero Photo.
   If you only have one photo right now, that's fine to start — see the
   note in Step 2 about generating the other two from it.
2. **One voice recording** — 10 seconds to 3 minutes of clear speech,
   minimal background noise. A voice memo reading a paragraph out loud is
   enough.
3. **A project folder** where Claude can create and read files for you
   (any folder on your computer that you point Claude at).

---

## Step 1 — The 5 documents (what they are, before you create them)

These are the files the `avatar-video` skill reads automatically before
every single video generation. You're about to create real versions of
all 5, filled in with your own information, in one setup pass.

1. **`AVATAR_LOCK.md`** — your locked face/identity reference (a
   Higgsfield "Element" built from your photo).
2. **`VOICE_LOCK.md`** — your locked voice reference (your uploaded audio
   file's ID).
3. **`GLOBAL_VIDEO_DIRECTION.md`** — your studio, lighting, camera, and
   performance rules, so every video you generate looks and feels
   consistent.
4. **`visual-reference.md`** — your locked hero image and the exact
   settings used to generate it.
5. **The `avatar-video` skill itself** — the tool that reads all four
   files above and actually generates your videos.

The full text of each template is included at the bottom of this module,
so you can see exactly what gets created. You don't need to copy them
manually — the setup prompt in Step 2 creates all of them for you.

## Step 2 — Attach your photo and voice recording, then send this one prompt

Attach **both** your face photo and your voice recording to the same chat
message (drag them in, or use your client's attach button), then send this
prompt in the same message:

> I'm attaching a photo of my face and a recording of my voice. Set up my
> complete AI Twin system, in order:
>
> **Avatar identity — bundle 3 reference images as ONE Element:**
> 1. Using my attached photo as the Hero Photo, generate two more reference
>    assets from it: a Turnaround Sheet (front/left/right/back views on one
>    sheet) and a Close-Up Sheet (eyes, skin texture, facial features in
>    detail). Show me both for approval before continuing — do not proceed
>    to step 2 until I approve them.
> 2. Once approved, bundle all THREE images (Hero Photo + Turnaround Sheet
>    + Close-Up Sheet) together into ONE reusable Higgsfield Element —
>    do NOT save them as 3 separate Elements, this must be one identity
>    bundle. Name it `[YOUR-NAME]-avatar`. If that exact name is taken,
>    use whatever name Higgsfield assigns and tell me the actual name and
>    ID — don't just assume the requested name was used.
> 3. Create `AVATAR_LOCK.md` in my project at `[YOUR-PROJECT-FOLDER]/`
>    documenting: the Element name, the Element ID, that it contains all 3
>    bundled images, the identity priority (Hero Photo = primary likeness,
>    Turnaround = angles/proportions/hairstyle, Close-Up = skin/eyes/
>    texture/asymmetry — used together, no single image should override
>    the others), the locked attributes (face shape, jawline, eyes, nose,
>    hairstyle, age, ethnicity, skin tone, defining asymmetries — not to be
>    altered without my explicit request), and the generation rule: every
>    future avatar image or video must embed `<<<the Element ID>>>` in the
>    generation prompt. Do not ask me to re-upload the Hero Photo,
>    Turnaround Sheet, or Close-Up Sheet again unless I explicitly replace
>    the avatar reference set, the Element becomes unavailable, or I
>    intentionally create a new avatar version.
>
> If Higgsfield does not allow creating or saving the Element directly from
> this environment, do not pretend it was created — tell me the exact
> manual action I need to take instead, in the minimum number of steps.
>
> **Voice reference:**
> 3. Upload my attached voice recording to Higgsfield as an audio file and
>    confirm it. Give me the resulting media_id.
> 4. Save the recording itself into my project at
>    `[YOUR-PROJECT-FOLDER]/assets/voice/voice-reference.mp3` (or the
>    matching extension for my file type).
> 5. Create `VOICE_LOCK.md` in `[YOUR-PROJECT-FOLDER]/` documenting the
>    source audio path, the uploaded media_id, and the usage rule: every
>    avatar video generated for this project must pass this media_id as an
>    `audio_references` media role directly in the `generate_video` call,
>    alongside the avatar image reference — one generation call, no
>    separate voice-swap step needed. Note explicitly that a
>    `create_voice`-style `voice_id` must NOT be used here — only the raw
>    uploaded audio file's media_id works as `audio_references`.
>
> **Video direction and hero image:**
> 6. Ask me a few quick questions to fill in `GLOBAL_VIDEO_DIRECTION.md`
>    for my project: what's the video series for, what studio/background
>    style do I want, what lighting mood, what camera framing, what
>    performance energy, and my target speaking pace. Save my answers into
>    `GLOBAL_VIDEO_DIRECTION.md` in `[YOUR-PROJECT-FOLDER]/`.
> 7. Generate one hero image of me using the locked avatar Element and the
>    studio/lighting I described, show it to me for approval before saving
>    it anywhere.
> 8. Once I approve it, save it into my project and create
>    `visual-reference.md` documenting the image file path, the generation
>    settings used (model, aspect ratio, resolution), and the locked
>    framing/lighting spec from my answers in step 6.
>
> **The skill:**
> 9. Create an `avatar-video` skill for my project that reads all 4 files
>    above (`AVATAR_LOCK.md`, `VOICE_LOCK.md`, `GLOBAL_VIDEO_DIRECTION.md`,
>    `visual-reference.md`) before every generation, and builds
>    `generate_video` calls that include my locked avatar image as the
>    `image` media role and my locked voice media_id as the `audio` media
>    role — so every future video request from me uses both automatically.
>
> Confirm back to me when all 5 are created and working, and don't ask me
> to re-attach my photo, my voice recording, or re-paste any of these
> documents again after this setup — treat everything as locked unless I
> explicitly say I'm replacing something.

## Step 3 — Verify it actually worked

Ask for a short test:

> "Generate a 5-second test video of my avatar saying 'Hey, this is a
> quick test' using the avatar-video skill."

Watch and listen to the result. This step is not optional — don't assume
setup worked just because nothing errored. Check: does the face look like
you? Does the voice sound like you? If either is off, tell Claude which
part is wrong (the specific file — `AVATAR_LOCK.md` or `VOICE_LOCK.md` —
holds the piece that needs fixing) rather than starting over from scratch.

---

## Reference — the 5 template documents in full

These are exactly what gets created for you in Step 2. Included here so
you know what to expect, and so you can hand-edit any of them later if you
want to change something (a different studio look, a new voice recording,
etc.) without re-running the whole setup prompt.

### 1. `AVATAR_LOCK.md`

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
in the generation prompt — this auto-injects the bundled images and
rewrites the reference to @[your-name]-avatar.

## Identity priority (how the 3 bundled images are used together)

- **Hero Photo** → primary facial identity and overall likeness
- **Turnaround Sheet** → profile, side angles, head shape, proportions,
  hairstyle, consistency across viewpoints
- **Close-Up Sheet** → skin detail, eyes, facial features, beard pattern,
  texture, asymmetry, realism

Used together as one reference system — no single image should override
the others in a way that damages identity consistency.

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

### 2. `VOICE_LOCK.md`

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

### 3. `GLOBAL_VIDEO_DIRECTION.md`

```
# GLOBAL VIDEO DIRECTION

## CONCEPT
[What's the video series for, who's the audience, what should the
viewer feel by the end.]

## IDENTITY
Use the locked avatar identity ([YOUR_AVATAR_ELEMENT_NAME], Element id
[YOUR_AVATAR_ELEMENT_ID] — see AVATAR_LOCK.md) consistently across every
clip. Preserve facial identity, proportions, hairstyle, skin tone, age,
body proportions exactly. Do not idealize or beautify.

## STUDIO (locked, must not change between clips)
[Background, furniture, props, desk, chair — be specific.]

## LIGHTING (locked)
[Key light angle/quality, background accents, practical lights, overall
mood.]

## CAMERA
[Aspect ratio, framing, distance, lens feel, camera behavior.]

## PERFORMANCE
[Energy progression across the series, voice quality target, delivery
speed in words/sec, facial performance notes, allowed gestures.]

## CONTINUITY
All clips must feel like one uninterrupted recording. Lock avatar,
wardrobe, studio, camera position, lighting, background across every clip.

## AUDIO / SPEECH
Natural voice with realistic breaths and pauses. [Captions: burned in
at generation, or added later at assembly?]

## NEGATIVE RULES
[Everything explicitly not wanted — e.g. no robotic lip movement, no
beauty filter, no identity drift, no wardrobe/studio changes between
clips.]

## Pipeline notes
- Model: seedance_2_0. Max clip duration 15 seconds (hard limit).
- Pass the voice reference media_id (from VOICE_LOCK.md) as
  audio_references alongside the image reference — one generation call,
  real voice, no voice-swap step needed.
- Always embed <<<YOUR_AVATAR_ELEMENT_ID>>> in the prompt text.
```

### 4. `visual-reference.md`

```
# Visual Reference — Hero Image

## LOCKED HERO IMAGE
**File:** [path to your approved hero image]
Approved on [date]. Generated from the locked avatar Element.

## GENERATION SETTINGS
- Model: gpt_image_2 (do not use Soul models — they force-rewrite
  prompts and ignore framing instructions)
- Aspect ratio: [9:16 / etc.]
- Resolution: 4k
- medias: [{ value: "[your Element id or reference photo id]", role: "image" }]

## LOCKED FRAMING
[Camera distance, face-to-frame ratio, crop points — matching
GLOBAL_VIDEO_DIRECTION.md's camera section.]

## LOCKED LIGHTING & ENVIRONMENT
[Matching GLOBAL_VIDEO_DIRECTION.md's studio/lighting section.]

## REALISM RULES
Preserve exact facial identity. Visible pores, natural skin texture,
no beauty filter, no smoothing, no CGI look.
```

### 5. The `avatar-video` skill

```
---
name: avatar-video
description: Generate a talking-head video clip of your locked AI Twin
  avatar, using your locked voice reference, per your GLOBAL_VIDEO_DIRECTION.
allowed-tools: mcp__<HIGGSFIELD_MCP_ID>__generate_video, mcp__<HIGGSFIELD_MCP_ID>__explainer_video, mcp__<HIGGSFIELD_MCP_ID>__job_display, Read, AskUserQuestion
---

# Avatar video generation

Before every generation, read: GLOBAL_VIDEO_DIRECTION.md,
visual-reference.md, AVATAR_LOCK.md, VOICE_LOCK.md.

1. Compute duration from script word count ÷ target words/sec (max 15s
   per clip — split longer scripts into continuity-locked clips).
2. Build the generate_video prompt: <<<ELEMENT_ID>>> embed, the locked
   studio/lighting/camera block (verbatim, unchanged across clips in a
   series), this clip's script and performance notes.
3. Call generate_video with model seedance_2_0, the hero image as the
   image media role, the voice reference media_id as the audio media
   role, generate_audio: true.
4. Preflight cost with get_cost: true, confirm with the user before the
   real generation.
5. No voice-swap step needed — audio_references produces the real voice
   directly.
6. If captions are required, run explainer_video with subtitles set
   once the clip(s) are ready.
7. Show the result to the user for approval.
```

---

Once all 5 are in place, every future request like *"make a video of me
saying [X]"* just works — no re-setup, no re-attaching anything.
