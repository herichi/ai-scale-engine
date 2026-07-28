# VOICE_LOCK — Mohamed's Voice Reference

**Status: APPROVED / LOCKED (2026-07-27).**

## Higgsfield Voice Reference (CURRENT — updated 2026-07-27)

**Source audio:** [`assets/voice/voice-reference.mp3`](assets/voice/voice-reference.mp3)
**Uploaded media_id:** `af1371ee-64cf-4e40-b7d8-13296b214095`
**Media type:** `audio`

## Usage rule (CONFIRMED WORKING, 2026-07-27)

Every avatar video generated for this project must include this media_id
as an `audio_references` media role directly in the `generate_video` call,
alongside the avatar image reference:

```
medias: [
  { value: "<hero image job id>", role: "image" },
  { value: "af1371ee-64cf-4e40-b7d8-13296b214095", role: "audio" }
]
```

Seedance 2.0 generates the avatar speaking in this real voice in a single
pass. **No separate `voice_change` step is needed.** This was verified with
a real test generation on 2026-07-27 (job `3fe128ed-ea95-44ca-b975-39af965d2bdc`)
and confirmed by Mohamed: *"this is my voice."*

**Important — do not confuse this with Higgsfield's separate voice-cloning
feature** (`create_voice` / `create_voice_from_confirmed_audio`, which
returns a `voice_id`). Passing a `voice_id` as `audio_references` fails
with "Audio input not found" — that role expects the raw uploaded audio
*file's* media_id, not a cloned-voice identity. This project does not need
the voice-cloning feature at all for this pipeline.

<details>
<summary>Superseded — earlier (incorrect) two-step voice_change approach, kept for history only</summary>

An earlier attempt used Higgsfield's voice-cloning feature
(`mohamed-voice-v2`, voice_id `865307a6-0146-4d08-a51e-17fe0d912da5`,
cloned from this same source audio) combined with a required post-
generation `voice_change` step, on the assumption that Seedance could not
accept real voice audio directly. That assumption was wrong — testing
confirmed `audio_references` works directly with the raw uploaded file.
The voice_change step is no longer part of this project's pipeline. The
clone (`mohamed-voice-v2`) still exists in the Higgsfield workspace but is
unused.

</details>

**Do not re-upload or ask Mohamed for this file again** unless he
explicitly replaces the voice reference.
