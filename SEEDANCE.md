# AI Scale Engine — Seedance MCP Prompting Guide

**Status: APPROVED — adapted from the source Seedance Studio Prompting
Guide for this project's actual tool interface (2026-07-29).**

## Where this came from, and what changed

This is the same prompting system as the source guide
(`Seedance_Studio_Prompting_Guide.md`, imported 2026-07-29), rewritten for
the **Higgsfield MCP tool interface** this project actually uses — not the
Higgsfield web UI the source guide assumes.

**The one confirmed, load-bearing difference:** the source guide says to
tag references with `@image_1` / `@audio_1`. That is the **web UI**
convention. This project generates through the `generate_video` /
`generate_image` MCP tools, and their own schema states explicitly:

> "Embed `<<<element_id>>>` inside `params.prompt`... The backend
> auto-injects the image and rewrites it to `@element_name`."

So `<<<element_id>>>` is what gets typed into `params.prompt` here — the
`@name` form is what the backend *rewrites it to internally* after
receiving the call, not something typed directly through this interface.
**Use `<<<element_id>>>` for identity/Element references in this project,
never `@image_1` — the latter has not been confirmed to work through this
MCP and may simply be ignored or misparsed.**

For audio (`@audio_1` in the source guide), this project passes the voice
reference as a `medias[]` entry with `role: "audio"` (see `VOICE_LOCK.md`)
— there is no `@audio_1`-style inline tag confirmed for this MCP either.
Reference the audio by describing what it does ("lip-sync driven by the
provided audio reference"), not by an `@`-tag.

Everything else in the source guide (rules 1, 3–10; pacing math; gesture
bank; template structure; bug fixes) is interface-agnostic and adopted
as-is below.

---

## The 9 rules that stop Seedance from breaking (adapted)

1. **The dialogue is yours — don't rewrite it.** If Mohamed's script says
   something in his own phrasing, that's the line. Wrap it in the prompt
   structure, don't polish it into something he wouldn't actually say.
2. **Trust the reference image.** The locked avatar Element (see
   `AVATAR_LOCK.md`) is embedded via `<<<element_id>>>` — don't
   re-describe the face in the prompt. Over-describing fights the
   reference and is how identity drifts.
3. **Pick one specific choice, never "or."** Decide the studio/wardrobe/
   angle before writing — the model will blend ambiguous alternatives
   into neither.
4. **Single continuous shot = prose, not timestamps.** A talking head is
   ONE take — flowing prose in the action block, with a single time
   range in the header. Internal timestamps (`0:00–0:02 / 0:02–0:05...`)
   tell Seedance to CUT between them, turning "one continuous shot" into
   a choppy multi-cut sequence. Reserve timestamped beats for deliberate
   multi-shot B-roll, never a talking head.
5. **The action header has one job.** State duration and camera
   position/angle once. What happens goes in the prose below, not the
   header.
6. **Style is aesthetic, action is choreography.** Lens, lighting, color
   grade, camera identity → the locked studio/lighting block (from
   `GLOBAL_VIDEO_DIRECTION.md`). What the subject does with hands and
   face → the performance/action prose. Don't mix them.
7. **Lean negative prompts.** Default to a short, targeted negative list
   — not a long stacked list. Stacking negatives can inverse-prime the
   model toward exactly what's being banned. Add one surgical line only
   for a specific recurring bug seen in this project.
8. **Reference the audio, never describe its texture.** State that
   delivery is driven by the provided audio reference; don't add texture
   descriptions ("phone mic," "room bleed") — that recolors clean audio
   toward unwanted artifacts.
9. **The pre-line beat and post-line beat sell the shot.** A breath
   before speaking, a held look after. The silence around the dialogue
   is what makes it feel human, not just the dialogue itself.

(Source guide's Rule 2 on "cinematic" wording folded into the STUDIO
section below — see the "no cinematic" rule already locked in
`GLOBAL_VIDEO_DIRECTION.md`'s camera-behavior section.)

---

## Pacing: pick delivery speed before writing the action prose

| | **Standard (~2.7 words/sec)** | **Dynamic (~4.5 words/sec)** |
|---|---|---|
| Feel | Conversational, punchy but breathable, natural micro-pauses | Ultra-fast hook pace, staccato, zero pauses |
| Best for | Storytelling, teaching a concept, the body of a video | Viral hooks, pattern interrupts, the first 2 seconds |

**Duration comes from the script, not the other way around.** Never
decide "I want a 10-second video" first and pad the script to fit — that
produces rushed or slurred delivery. Write the actual line, count the
words, then:

`duration (seconds) = word count ÷ words-per-second (2.7 or 4.5)`

**Note on this project's prior pacing (2026-07-27/28 sessions):** clips
were generated at 3.0 or 3.7 words/sec — close to but not matching either
of this guide's two validated speeds. Going forward, default to **2.7
(standard)** unless a script specifically needs the faster hook pace,
rather than reusing the ad-hoc 3.0/3.7 figures.

**Duration rounding rule (unchanged from this project's existing
practice):** if word count ÷ pace rounds to just over Seedance's 15-second
hard cap, round the passed duration down to 15 rather than trimming the
script — small pace absorption is preferable to cutting words. If the
overage is more than ~1 second, split into multiple continuity-locked
clips instead (see `GLOBAL_VIDEO_DIRECTION.md` continuity rules).

---

## Hands: the rule that makes or breaks realism

A frozen or looping hand is the fastest way to make a talking head look
fake. Non-negotiable on every generation.

**The rule:** at least one hand stays visible in frame at all times. A
gesture change lands on key words. Every gesture flows into the next — no
frozen holds, no robotic snaps, no looping.

**Gesture bank — map to what the line is actually about:**

| Word / intent | Gesture |
|---|---|
| Now / today | Index taps down once or twice, firm |
| More / increase | Hand rises, fingers open |
| Less / decrease | Hand lowers, palm down |
| No / never | Index makes a small horizontal "no" |
| Yes / exactly | Index points forward, or small nod-gesture |
| Everything / everyone | Arms open, palms up |
| You | Palm or index extended toward the lens |
| Me / I | Thumb or hand touches the sternum |
| Why / think about it | Palms open upward, slight tilt |
| Honestly / really | Flat hand rests briefly on the chest |
| Small / a little | Thumb and index held close together |
| Big / a lot | Arms open wide |
| The past | Hand sweeps back past the shoulder |
| The future | Hand pushes forward |
| Stop / listen | Palm faces forward, open |
| Different | Hand pivots in a half-turn |
| Money / business | Thumb-index rub, or a counting gesture |
| Idea | Index touches the temple briefly |
| First / one | Index raised |
| Key / important | Thumb and index form a small circle |

Write this into the flowing prose, not as timestamp brackets (Rule 4).
Example: *"As he says 'here's the thing nobody tells you,' his hand opens
from a loose fist, palm up, as if handing the idea to the viewer — then
settles as he leans a half-inch closer on 'nobody tells you.'"*

---

## The full template (MCP form)

```
Prompt text passed to generate_video:

<<<AVATAR_ELEMENT_ID>>> [locked studio/lighting/camera block, verbatim
from GLOBAL_VIDEO_DIRECTION.md — same wording every clip in a series].

[One flowing paragraph for ACTION. Open on a breath or a beat already
mid-thought — not a blank stare waiting to start. Weave the dialogue in
with physical beats and hand gestures mapped to key words (gesture bank
above). Close on a held look, a slight settle, eyes staying on the
lens — the post-line beat. No internal timestamps.]

He says, at [2.7 or 4.5] words per second: "[verbatim script]"

Delivery: lip-sync driven by the provided audio reference. [Tone line,
e.g. "confident, warm voice, natural micro-pauses, no hesitation, no
filler."]

Camera: locked tripod throughout, no cuts, no jumps, no zoom. Natural
head movement and hand gestures evolve organically with speech — no
frozen positions, no robotic transitions.

medias: [
  { value: "<hero image job id>", role: "image" },
  { value: "<voice reference media_id>", role: "audio" }
]

Negative prompt (lean, 2-3 items default): No music, no captions, no
frozen or robotic hands.
```

---

## Worked example (standard pace, adapted to this project)

Script: *"I didn't become a coach to edit videos."* (8 words)

At 2.7 words/sec that's ~3s of speech — well under a natural clip length,
which is correct: the pre-line and post-line beats fill the remaining
time. Don't pad the dialogue to hit a duration; pad the silence.

```
<<<9cf95684-c068-4807-bfa8-08aaa3add7c5>>> seated in the locked premium
podcast studio [full locked block from GLOBAL_VIDEO_DIRECTION.md].

Opens already mid-breath, a half-second beat of held eye contact before
speaking — not a cold start. As he says "I didn't become a coach," his
hand rises from resting near his sternum, palm loosely open, "to edit
videos" lands as the hand settles back down, fingers relaxing, a small
self-aware exhale crossing his face on the last word. He holds the look
half a second after the line ends, eyes steady on the lens.

He says, at approximately 2.7 words per second: "I didn't become a coach
to edit videos."

Delivery: lip-sync driven by the provided audio reference. Confident,
warm voice, natural micro-pauses, no hesitation, no filler.

Camera: locked tripod throughout, no cuts, no jumps, no zoom. Natural
head movement and hand gestures evolve organically with speech.

medias: [
  { value: "c2281451-ac7e-4f11-affa-7386146537cc", role: "image" },
  { value: "af1371ee-64cf-4e40-b7d8-13296b214095", role: "audio" }
]

Negative prompt: No music, no captions, no frozen or robotic hands.
```

---

## Bug fixes — likely to apply to this project's talking heads

| Bug | What it looks like | Fix |
|---|---|---|
| **Frozen subject** | "Locked tripod" over-applied to the *subject*, not just camera | State explicitly: "Camera locks. Subject still moves naturally." |
| **Looping gesture** | Same hand motion repeats every ~2s | Map gestures to *specific* words from the actual script (gesture bank above), not a vague "hands move naturally" |
| **Muffled audio / lip-sync drift** | Voice sounds processed, off-time from mouth | Don't describe the audio's texture — "lip-sync driven by the provided audio reference" is the whole line |
| **Plasticky face** | Skin looks smooth/waxy, especially in wide framing | Pull the shot tighter (medium close-up, matches this project's locked 35–42% face-height framing) |
| **Camera won't stay locked** | Subtle dolly/drift creeps in despite "locked tripod" | Remove the word "cinematic" anywhere in the prompt — use "static," "locked," "documentary" instead |
| **Identity drift** | Face looks slightly off from the reference | Don't over-describe the face in the prompt — trust `<<<element_id>>>`, keep the underlying Element's source images clean |

---

## Checklist before generating

- [ ] Script is word-counted; duration calculated FROM the script (word
      count ÷ 2.7 or 4.5), never decided first and padded to fit
- [ ] Pace decided: standard (2.7) or dynamic (4.5) — matches the
      delivery line and negative prompt
- [ ] Locked studio/lighting/camera block copied verbatim from
      `GLOBAL_VIDEO_DIRECTION.md` — no rewording between clips in a
      series
- [ ] No internal timestamps in the action prose — one time range only,
      if stated at all
- [ ] At least 2–3 hand gestures mapped to specific script words, woven
      into the prose
- [ ] Pre-line beat and post-line beat both written in
- [ ] Negative prompt is lean (2–3 items) unless fixing a specific
      recurring bug
- [ ] Identity via `<<<element_id>>>` (never `@image_1` — unconfirmed for
      this MCP), audio via `medias[]` with `role: "audio"` (never
      `@audio_1`)
- [ ] `declined_preset_id` set if a preset-match notice appears on
      preflight and literal generation is wanted (this project's default)
