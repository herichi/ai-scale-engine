# VOICE_LOCK — TEMPLATE

Copy this into your own project as `VOICE_LOCK.md` and fill in every
`[bracketed]` value with your own. This is one of the source-of-truth files
the `avatar-video` skill reads before every generation — it tells the
skill which voice reference to attach so your avatar speaks in your real
voice.

---

## Voice Reference (CURRENT)

**Source audio:** `[path to your voice file in your project, e.g.
assets/voice/voice-reference.mp3]`
**Uploaded media_id:** `[the media_id returned after uploading your file to
Higgsfield]`
**Media type:** `audio`

## Usage rule

Every avatar video generated for this project must include this media_id
as an `audio_references` media role directly in the `generate_video` call,
alongside the avatar image reference:

```
medias: [
  { value: "<hero image job id, from your AVATAR_LOCK.md>", role: "image" },
  { value: "[your voice file's media_id]", role: "audio" }
]
```

Seedance 2.0 generates the avatar speaking in this real voice in a single
pass. **No separate voice-swap step is needed.**

**Important — do not confuse this with Higgsfield's separate voice-cloning
feature** (`create_voice` / `create_voice_from_confirmed_audio`, which
returns a `voice_id`). Passing a `voice_id` as `audio_references` fails
with "Audio input not found" — that role expects the raw uploaded audio
*file's* media_id, not a cloned-voice identity. You do not need the
voice-cloning feature for this pipeline — just your uploaded audio file.

**Do not re-upload or ask for this file again** once it's locked here,
unless you're explicitly replacing the voice reference with a new
recording.
