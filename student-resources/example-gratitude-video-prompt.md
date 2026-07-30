# Example — "Thank You" Video Prompt (SEEDANCE.md template applied)

This is a worked example of applying `SEEDANCE.md`'s prompting rules to a
real script: a gratitude/reflective message to your community. Use it as a
reference for how to fill in your own `generate_video` call once your
`AVATAR_LOCK.md` and `VOICE_LOCK.md` are set up (see Module 3).

**Script (yours to adapt):**
> "I want to thank the [your community name] community, helping me scale
> my business and save me valuable time — time I now spend making impact
> with my clients."

28 words. At standard pace (2.7 words/sec) that's ~10.4 seconds — a clean
fit for a 10-second clip, no trimming or splitting needed. This is a
gratitude/reflective message, so standard pace is the right tonal choice
(save dynamic/4.5 wps for fast hooks, not reflective content).

---

## The prompt template (fill in your own placeholders)

> `<<<YOUR_AVATAR_ELEMENT_ID>>>` seated in [your locked studio description
> from your own `GLOBAL_VIDEO_DIRECTION.md` — background, furniture,
> lighting, camera framing, copied verbatim so every clip in your series
> stays visually consistent].
>
> Opens already mid-breath, a half-second beat of held eye contact before
> speaking — not a cold start. As you say "I want to thank the [community
> name] community," your hand rises from resting near your sternum, palm
> open, honest and warm — "helping me scale my business" lands as the
> hand settles, fingers relaxing. On "and save me valuable time," your
> other hand opens slightly, palm up, as if weighing something light. You
> lean a half-inch closer on "time I now spend making impact with my
> clients," genuine warmth crossing your face. You hold the look half a
> second after the line ends, eyes steady on the lens, a small sincere
> exhale.
>
> You say, at approximately 2.7 words per second: *"I want to thank the
> [your community name] community, helping me scale my business and save
> me valuable time — time I now spend making impact with my clients."*
>
> Delivery: lip-sync driven by the provided audio reference. Warm,
> sincere, grateful voice, natural micro-pauses, no hesitation, no
> filler.
>
> Camera locks. Subject still moves naturally — natural head movement and
> hand gestures evolve organically with the speech, at least one hand
> visible in frame at all times, no frozen positions, no robotic
> transitions.
>
> Negative prompt: no music, no captions, no frozen or robotic hands.

---

## What to fill in

- **`<<<YOUR_AVATAR_ELEMENT_ID>>>`** — your locked avatar Element ID, from
  your own `AVATAR_LOCK.md` (see Module 3, Step A).
- **Studio description** — your own locked studio/lighting/camera block,
  from your own `GLOBAL_VIDEO_DIRECTION.md`. Copy it verbatim — don't
  reword it between clips, or your videos will look visually inconsistent.
- **`medias[]`** in the actual `generate_video` call:
  ```
  medias: [
    { value: "<your hero image job id>", role: "image" },
    { value: "<your voice reference media_id, from VOICE_LOCK.md>", role: "audio" }
  ]
  ```
- **Script** — swap "[your community name]" for your actual community/
  offer name, and adjust the rest to sound like something you'd actually
  say (see `SEEDANCE.md` Rule 1 — don't over-polish your own phrasing away).

---

## Why this example is worth studying

- **Gesture mapping**: two distinct hand gestures, each tied to a specific
  phrase in the script (open palm on "thank," weighing gesture on "save
  time") — not a generic "hands move naturally" instruction.
- **Pre-line and post-line beats**: the video doesn't start cold on the
  first word, and doesn't cut the moment the last word ends — there's a
  breath before and a held look after. This is what makes it read as
  human rather than a teleprompter reading.
- **Lean negative prompt**: three items, not a long stacked list.
- **No "cinematic" anywhere**: the studio look stays locked and static
  on purpose — see `SEEDANCE.md`'s bug-fix table for why that word causes
  camera drift.
