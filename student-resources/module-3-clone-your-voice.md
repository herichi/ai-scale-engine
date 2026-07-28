# Module 3 — Clone Your Voice & Lock It to Your Avatar Videos

This tutorial walks you through capturing your voice reference, uploading
it to Higgsfield, and locking it as a permanent reference in your project
so every avatar video you generate automatically speaks in your real
voice — no extra step required at generation time.

**Confirmed working (2026-07-27):** Seedance 2.0 accepts your real voice
audio directly as an `audio_references` input during generation. Pass your
uploaded voice-reference media_id alongside your avatar image reference,
and the model generates speech in your actual voice in one pass — you do
not need to run a separate voice-swap step afterward. This is simpler than
earlier guidance suggested; the note below explains what changed.

<details>
<summary>Note: what NOT to pass as audio_references</summary>

The `audio_references` role expects an actual uploaded audio *file*
media_id — not a `voice_id` returned by Higgsfield's separate voice-cloning
feature (`create_voice` / `create_voice_from_confirmed_audio`). Passing a
voice_id there fails with "Audio input not found." Passing your raw
reference audio file's media_id works. In short: skip the voice-cloning
step entirely for this workflow — you only need the uploaded audio file
itself, locked as project knowledge (see below).

</details>

---

## Step 1 — Record or gather your voice reference

You need one clean audio clip of your own voice: 10 seconds to 3 minutes,
clear speech, minimal background noise. A voice memo reading a paragraph
out loud works fine — it doesn't need to be studio quality.

Save it in your project folder, e.g. `assets/voice/voice-reference.mp3`.

## Step 2 — Upload it to Higgsfield

If you're working in a Claude Apps UI-capable client (chat with the
Higgsfield widget available), the easiest path is to ask Claude to open the
media upload widget and select your file there.

If you already have the file sitting on disk and want to skip the widget,
use this prompt:

> "Upload [path to your voice reference file] to Higgsfield as an audio
> file and confirm it. Give me the resulting media_id."

This runs the upload → confirm sequence and returns a `media_id`. Save it —
this is the ID you'll lock as your voice reference.

## Step 3 — Lock it as project knowledge (VOICE_LOCK.md)

Don't leave the media_id floating in a chat message — write it into a
permanent file in your project so every future session, and every video
generation, picks it up automatically without you re-uploading. Use this
prompt:

> "Create a VOICE_LOCK.md file in my project. Document my voice reference:
> source audio at `[path to your file]`, uploaded Higgsfield media_id
> `[the ID from step 2]`, type `audio`. State the usage rule: every avatar
> video generated for this project must pass this media_id as an
> `audio_references` media role directly in the `generate_video` call
> alongside the avatar image reference — Seedance 2.0 generates speech in
> this real voice in a single pass, no separate voice-swap step needed.
> Do not re-upload or ask me for this file again unless I explicitly
> replace the voice reference."

## Step 4 — Wire it into your generation workflow

If you're using an `avatar-video`-style skill (see Module 4 for the full
skill setup), point it at your `VOICE_LOCK.md` file so it reads your
locked media_id automatically instead of you having to paste it into every
prompt. Add this line to your skill's list of source-of-truth files it
reads before generating:

> "Also read `VOICE_LOCK.md` for the locked voice reference media_id, and
> always include it as an `audio_references` media role in every
> `generate_video` call for this project."

If you're generating manually (no skill), just remember: every
`generate_video` call needs two media entries — your avatar image
reference (`role: image`) and your locked voice file (`role: audio`).

## Step 5 — Verify it actually worked

After your first generation, listen to the result. This is not optional —
don't assume it worked just because the job completed without an error. If
it still sounds like a generic AI voice rather than yours, double-check
that you passed the actual audio file's media_id (not a voice_id from a
separate cloning feature — see the note above) and that it's attached with
`role: audio` in the `medias` array.

---

## Quick reference — the locked pipeline

1. Voice reference file uploaded once, locked in `VOICE_LOCK.md`.
2. Every `generate_video` call includes it as `{ value: <media_id>,
   role: "audio" }` alongside your avatar image reference.
3. Result: one generation call, your avatar, your real voice — no second
   step, no waiting on a separate voice-swap job.
