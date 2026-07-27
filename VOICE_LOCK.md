# VOICE_LOCK — Mohamed's Cloned Voice

**Status: APPROVED / LOCKED (2026-07-26).**

## Higgsfield Voice Reference

**Voice name:** `mohamed-voice`
**Voice ID:** `801145c1-885e-433c-a6f4-b272acd10d38`
**Voice type:** `element`
**Source audio:** `voice reference.mp3` (media_id `bcfd1cd7-54af-43c5-a399-44053701f057`)

**Status:** completed, `is_audio_eligible: true`

## Usage rule

Every avatar video generated for this project must use Mohamed's real
cloned voice, never the raw Seedance native voice.

Seedance 2.0's `generate_audio: true` produces its own native TTS voice —
this is NOT Mohamed's voice, and has been confirmed to sound robotic. There
is currently no way to make Seedance generate directly in the cloned voice
at generation time; the correct pipeline is:

1. Generate the video with `generate_audio: true` (native placeholder
   voice, needed so the model has speech timing to lip-sync against).
2. Immediately run `voice_change` on the resulting video with
   `voice_id: 801145c1-885e-433c-a6f4-b272acd10d38`, `voice_type: element`.
   This replaces the native voice with Mohamed's cloned voice while
   preserving lip-sync timing.

This two-step process is already encoded as a required (non-optional) step
in the `avatar-video` skill (`ThefounderStudio/.claude/skills/avatar-video/
SKILL.md`, step 6) — this file exists so the voice lock is also documented
as project knowledge, not just buried inside the skill's pipeline logic.

**Cost note:** `voice_change` does not support the `get_cost` preflight
that `generate_video`/`generate_image` support — its exact cost is only
known after the job runs. Check workspace credit balance before and after
to see the actual charge.

**Known behavior:** `voice_change` jobs commonly sit in `waiting` status
for 10+ minutes before moving to processing. This is normal — don't retry
before ~10 minutes have passed.
