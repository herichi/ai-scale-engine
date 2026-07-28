# Module 3 — Clone Your Voice & Lock It to Your Avatar Videos

This tutorial gets your real voice locked into your project as a
permanent reference, so every avatar video you generate afterward
automatically speaks in your real voice — no extra step, no re-uploading,
no separate voice-swap.

**Confirmed working (2026-07-27):** Seedance 2.0 accepts your real voice
audio directly as an `audio_references` input during generation. Attach
your voice file once, lock it in your project, and every future video
generation call picks it up automatically.

<details>
<summary>Note: what NOT to attach</summary>

`audio_references` expects an actual uploaded audio *file* — not a
`voice_id` from Higgsfield's separate voice-cloning feature (`create_voice`
/ `create_voice_from_confirmed_audio`). Passing a voice_id there fails with
"Audio input not found." You do not need the voice-cloning feature at all
for this workflow — just your raw reference audio file, attached and
locked.

</details>

---

## What you need before you start

**One file:** a clean audio clip of your own voice — 10 seconds to 3
minutes, clear speech, minimal background noise. A voice memo reading a
paragraph out loud is enough, it doesn't need to be studio quality.

**Which skill this feeds:** the `avatar-video` skill. That skill reads
four project files before every generation — `GLOBAL_VIDEO_DIRECTION.md`,
`visual-reference.md`, `AVATAR_LOCK.md`, and `VOICE_LOCK.md`. This module
sets up the last one. If you haven't done Module 2 (lock your avatar
image/Element) yet, do that first — `VOICE_LOCK.md` on its own is useless
without `AVATAR_LOCK.md` already in place, since a video needs both an
image reference and an audio reference.

---

## Step 1 — Attach your voice file directly in chat

Unlike a typed prompt, an audio file has to actually be attached to your
message — Claude can't read a file path you just type out. Attach your
voice memo/recording to your chat message (drag it in, or use your
client's attach/upload button), then send the full setup prompt below in
the same message.

## Step 2 — The complete setup prompt (copy, fill in the blanks, send with your file attached)

This one prompt does everything: uploads your attached voice file to
Higgsfield, creates `VOICE_LOCK.md` documenting it, and wires it into your
`avatar-video` skill so it's used automatically from now on.

> I'm attaching my voice reference recording. Do the following, in order:
>
> 1. Upload this attached audio file to Higgsfield and confirm it. Give me
>    the resulting media_id.
> 2. Save the file itself into my project at
>    `[YOUR-PROJECT-FOLDER]/assets/voice/voice-reference.mp3` (or `.m4a`/
>    `.wav`, matching my actual file type).
> 3. Create (or update) `VOICE_LOCK.md` in `[YOUR-PROJECT-FOLDER]/`
>    documenting: the source audio file path, the uploaded Higgsfield
>    media_id from step 1, and media type `audio`. State the usage rule:
>    every avatar video generated for this project must pass this media_id
>    as an `audio_references` media role directly in the `generate_video`
>    call, alongside the avatar image reference from `AVATAR_LOCK.md` — one
>    generation call, no separate voice-swap step needed. Note explicitly
>    that a `create_voice`-style `voice_id` must NOT be passed here — only
>    the raw uploaded audio file's media_id works.
> 4. Update my `avatar-video` skill (or confirm it already does this) so
>    that its list of source-of-truth files it reads before every
>    generation includes `VOICE_LOCK.md`, and that every `generate_video`
>    call it builds includes the locked voice media_id as an `audio` media
>    role alongside the `image` media role from `AVATAR_LOCK.md`.
> 5. Confirm back to me: the media_id, the file path it's saved to, and
>    that the skill now references it.
>
> Do not ask me to re-attach or re-upload this file again after this setup
> — treat it as locked unless I explicitly say I'm replacing it.

**What "attach the file" looks like in practice:** you're not typing a
file path into the prompt — you're literally dragging your audio file (or
using your chat client's attachment button) into the same message as this
text. If your client shows a media/upload widget after you send this,
that's the actual upload step happening — follow it if prompted, it's part
of the same flow, not a separate thing you need to redo.

## Step 3 — Verify it actually worked

Ask for a short test generation once setup is done:

> "Generate a 5-second test video of my avatar saying 'Hey, this is a
> quick voice test' using the avatar-video skill."

Listen to the result. This step is not optional — don't assume it worked
just because the job completed without an error. If it still sounds like a
generic AI voice rather than yours, the wrong ID may have been attached
(a `voice_id` instead of the audio file's `media_id` — see the note
above), or `VOICE_LOCK.md` didn't get wired into the skill correctly. Ask
Claude to check `VOICE_LOCK.md` and the skill's media roles if this
happens.

---

## Quick reference — what's locked after this module

| File | What it holds |
|---|---|
| `assets/voice/voice-reference.mp3` (or your format) | Your actual voice recording, saved in the project |
| `VOICE_LOCK.md` | The uploaded media_id + the usage rule |
| `avatar-video` skill | Reads `VOICE_LOCK.md` automatically, attaches your voice to every generation |

From here on: every time you ask for an avatar video, it speaks in your
real voice automatically. No re-uploading, no re-attaching, no separate
voice-swap step.
