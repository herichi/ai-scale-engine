# AI Scale Engine — Seedance MCP Prompting Guide

**Status: APPROVED — updated 2026-07-30, merges Mohamed's revised Seedance
Studio Prompting Guide with GLOBAL_VIDEO_DIRECTION.md and this project's
confirmed MCP-specific fixes.**

## What changed in this update

Mohamed merged the full locked studio/lighting/camera/performance rules
directly into his prompting guide, and updated standard pace from 2.7 to
**3.0 words/sec** to match what's actually been validated in this
project's real generations. Two things needed fixing on import — both
resolved per Mohamed's explicit instruction (2026-07-30):

1. **"Cinematic" contradiction:** the guide's STYLE ANCHOR block described
   the camera as "Cinematic prosumer camera (Sony A7S3-style)," which
   directly contradicts the guide's own Rule 10 ("never use 'cinematic'
   for a locked shot — it pulls the model toward camera drift"). Fixed by
   removing the word "Cinematic" from the Style Anchor wording below,
   keeping "prosumer camera, Sony A7S3-style, locked tripod."
2. **Tag syntax:** the guide says use `@image_1`/`@audio_1`. That remains
   a **web-UI** convention. This project generates through the Higgsfield
   MCP tools, whose own schema states explicitly: "Embed
   `<<<element_id>>>` inside `params.prompt`... the backend auto-injects
   the image and rewrites it to `@element_name`." So `<<<element_id>>>` is
   what gets typed into `params.prompt` here; `@name` is what the backend
   rewrites it to internally, not something typed directly through this
   interface. **This project keeps `<<<element_id>>>` for identity tags —
   confirmed against the live tool schema, not assumed.** Audio has no
   `@audio_1`-style tag confirmed for this MCP either — it's passed as a
   `medias[]` entry with `role: "audio"` (see `VOICE_LOCK.md`), referenced
   in-prompt by function only ("lip-sync driven by the provided audio
   reference").

Everything else below is the guide as written, including the studio/
lighting/camera/performance rules merged in from `GLOBAL_VIDEO_DIRECTION.md`
— they remain the single locked source (this file should not drift from
that one; if either changes, update both together).

---

## What this guide is

The **one** prompting system for Seedance 2.0 via the Higgsfield MCP, for
talking-head videos of the locked AI avatar. This is NOT a polished
corporate advertisement — it should feel warm, personal, energetic,
genuine, confident, slightly playful, exclusive, founder-to-founder,
premium but human.

**The viewer should feel:** "I'm getting early access to something that
is still being built, and my opinion actually matters."

---

## The locked default look (merged from GLOBAL_VIDEO_DIRECTION.md — do not
diverge from this without updating both files)

**IDENTITY:** Locked AI Twin (`mohamed-avatar-2`, Element id
`9cf95684-c068-4807-bfa8-08aaa3add7c5` — see `AVATAR_LOCK.md`), consistent
across every clip. Preserve exactly: facial identity, face proportions,
hairstyle, beard, glasses, skin tone, age, body proportions, wardrobe,
natural facial asymmetries. Do not idealize or beautify.

**LIGHTING (locked):**
- Key: large, soft, diffused, warm-neutral; ~30–45° from camera; soft
  natural facial shadows; realistic warm skin tone. Must NOT hit the face
  flat/direct-on — angled, off-face soft light.
- Background: subtle blue LED accents, stays behind the subject — no blue
  cast on skin.
- Practical: warm tungsten-style lamp, ~2700–3200K.
- Overall contrast: warm founder/warm skin against cool blue premium
  studio accents.

**CAMERA:**
- 9:16 vertical, camera directly in front, eye level, subject centered.
- Framing: mid-torso upward, face prominent but not a close-up, moderate
  headroom, hands may naturally enter the lower frame.
- No legs, no under-desk area, no oversized desk foreground.
- Distance ~90cm–1.2m, lens ~50–70mm full-frame equivalent, natural facial
  proportions — no wide-angle distortion, no fisheye.
- **Camera behavior: mostly locked.** Only extremely subtle natural
  movement allowed — a tiny push-in during emotional lines, subtle
  breathing movement. No obvious zoom, no handheld shake, no dramatic
  camera movement. (A one-off stylistic departure, like a slow-motion
  push or a different set, must be explicitly requested per-clip — it is
  NOT the default and does not change this locked baseline.)

**PERFORMANCE:**
- Look directly into the lens, as if addressing a small group of coach
  friends personally.
- Energy progression across the welcome series: 1. friendly excitement →
  2. clear explanation → 3. invitation and belonging → 4. playful honesty
  → 5. genuine gratitude.
- Voice: natural, warm, conversational, confident, slightly energetic.
  Never robotic, never overly polished, never "sales voice."
- Facial performance: natural smile at opening, genuine excitement on
  "AI Scale Engine," slight eyebrow movement on emphasis, friendly eye
  contact, subtle smile around playful lines, sincere expression during
  any feedback request.
- **Gestures: restrained and natural only.** Allowed: small open-hand
  gesture when explaining the system, subtle finger/counting gestures for
  lists, slight lean forward during important invitation lines, relaxed
  return to neutral. Do NOT: wave hands excessively, perform exaggerated
  influencer gestures, point aggressively, overact. (This is the
  project's own restraint on top of the gesture bank below — map gestures
  to words per the bank, but keep the physical size of each gesture
  small and natural, not big/energetic.)

**CONTINUITY (critical — every clip in a series):** all clips must feel
like one uninterrupted recording. Lock across every clip: avatar,
wardrobe, studio, camera position, lens, chair, microphone, lighting,
desk, background, color grade. Do not change the environment between
clips without an explicit, deliberate one-off request.

**NEGATIVE RULES (apply to every clip, no exceptions):** no robotic lip
movement, no excessive smiling, no corporate presenter energy, no fake
enthusiasm, no exaggerated gestures, no hard selling, no dramatic
cinematic acting, no gaming RGB, no neon wash, no plastic skin, no beauty
filter, no facial identity drift, no wardrobe changes, no studio changes,
no text, no captions, **no teeth showing** (smiles stay closed-mouth/
subtle — flag with Mohamed if a script implies an open, toothy smile).
**No rings or jewelry on the hands, no wedding band** (added 2026-07-30
after a ring hallucinated into a generation with none in the source
prompt or reference).

---

## The 10 rules that stop Seedance from breaking

1. **The dialogue is yours — don't rewrite it.** If the script says
   something in Mohamed's own phrasing, that's the line. Wrap it in the
   prompt structure, don't polish it into something he wouldn't actually
   say.
2. **Trust the reference image.** The locked avatar is clearly defined —
   don't re-describe the face. Over-describing fights the reference and
   is how identity drifts.
3. **Pick one specific choice, never "or."** Decide before writing —
   ambiguous alternatives get blended into neither.
4. **Single continuous shot = prose, not timestamps.** A talking head is
   ONE take — flowing prose in the action block, with a single time range
   in the header. Internal timestamps (`0:00–0:02 / 0:02–0:05...`) tell
   Seedance to CUT between them, turning "one continuous shot" into a
   choppy multi-cut sequence. Reserve timestamped beats for deliberate
   multi-shot B-roll, never a talking head.
5. **The action header has one job.** State duration and camera position/
   angle once. What happens goes in the prose below, not the header.
6. **Style anchor is aesthetic. Action is choreography.** Lens, lighting,
   color grade, camera identity → the locked studio block above. What the
   subject does with hands and face → the action/performance prose. Don't
   mix them.
7. **Lean negative prompts.** Default to a short, targeted list — this
   project's locked negative rules above are already fairly long because
   they're the standing brand rules, not a per-clip stack. Don't add
   *additional* per-clip negatives beyond a bug-specific fix; stacking
   more can inverse-prime the model toward exactly what's being banned.
8. **Reference the audio, never describe its texture.** "Lip-sync driven
   by the provided audio reference" is the whole line — adding texture
   description ("phone mic," "room bleed") recolors clean audio toward
   unwanted artifacts.
9. **The pre-line beat and post-line beat sell the shot.** A breath
   before speaking, a held look after. The silence around the dialogue is
   what makes it feel human, not just the dialogue itself.
10. **"Cinematic" is a loaded word.** It pulls the model toward camera
    drift, dolly, tracking. For this project's locked studio shot, never
    use it — use "static," "locked," "documentary," or "prosumer camera"
    instead. Reserve "cinematic" only for an explicitly requested,
    deliberate departure from the locked look (e.g. a one-off B-roll or
    stylized shot Mohamed asks for by name).

---

## Style anchor block (copy verbatim into every generation — "cinematic"
removed per the fix above)

```
STYLE ANCHOR: Locked studio talking head, podcast / creator aesthetic.
Prosumer camera (Sony A7S3-style) on a locked tripod, no camera movement.
Medium close-up framing — head, shoulders, and upper chest, with clear
room at the bottom of frame for hand gestures to enter and exit
naturally. Shallow depth of field — subject tack-sharp, background
softly blurred (out-of-focus podcast mic stand or bookshelf optional).
Warm key light from camera-front-left, soft fill camera-right, subtle
rim light separating subject from background. Photorealistic — natural
human skin with visible pores, freckles, real eye moisture, subtle
natural micro-movements. 50mm-85mm equivalent lens, eye-level
perspective.
```

**Why these specific choices:**
- **Medium close-up, not wide** — wide shots spread Seedance's detail
  budget thin and faces go plasticky. Pull in close, the realism budget
  concentrates on the face.
- **Room at the bottom of frame** — hands need somewhere to move into.
  Crop them out and the model either freezes them or invents awkward
  motion to compensate.
- **Warm key + soft fill + rim, not flat light** — the actual three-point
  setup from the avatar build, kept consistent with static images.
- **No "cinematic," no dolly** — this look is locked on purpose. A coach
  mid-explanation who is also drifting through a dolly move reads as
  distracting, not premium.

---

## Pacing: pick delivery speed before writing the action prose

| | **Standard (~3.0 words/sec)** | **Dynamic (~4.5 words/sec)** |
|---|---|---|
| Feel | Conversational, punchy but breathable, natural micro-pauses | Ultra-fast hook pace, staccato, zero pauses |
| Best for | Storytelling, teaching a concept, the body of a video | Viral hooks, pattern interrupts, the first 2 seconds |
| DELIVERY line | "Confident voice, slightly elevated tempo (~3.0 words per second), natural micro-pauses allowed, no hesitation, no filler." | "Ultra-fast hook pace, ~4–5 words per second, staccato delivery, high-energy hook velocity, words flowing in tight rapid-fire succession." |

**This is the current default (2026-07-30): 3.0 words/sec standard.**
(Supersedes the earlier 2.7 figure from the first SEEDANCE.md import — 3.0
matches this project's actual validated generations.)

**Duration comes from the script, not the other way around.** Never
decide "I want a 10-second video" first and pad the script to fit — that
produces rushed or slurred delivery. Write the actual line, count the
words, then:

`duration (seconds) = word count ÷ words-per-second (3.0 or 4.5)`

**If a recorded audio file already exists:** its actual length IS the
duration. If the audio is shorter than the target video length, write a
closing visual beat for the leftover seconds — a held look, a slight nod,
eyes staying on the lens. Never leave dead air with nothing scripted.

**Duration rounding rule (unchanged from this project's existing
practice):** if word count ÷ pace rounds to just over Seedance's 15-second
hard cap, round the passed duration down to 15 rather than trimming the
script — small pace absorption is preferable to cutting words. If the
overage is more than ~1 second, split into multiple continuity-locked
clips instead.

---

## Hands: the rule that makes or breaks realism

A frozen or looping hand is the fastest way to make a talking head look
fake. Non-negotiable on every generation. **Combined with this project's
own restraint rule above: gestures map to words, but stay small/natural,
not big/energetic — this is a founder talking to friends, not a hype
reel.**

**The rule:** at least one hand stays visible in frame at all times. A
gesture change lands on every key word (standard pace) or the punchy word
of every beat (dynamic pace). Every gesture flows into the next — no
frozen holds, no robotic snaps, no looping.

**Gesture bank — map to what the line is actually about, don't force all
of them into one script:**

| Word / intent | Gesture |
|---|---|
| Now / today | Index taps down once or twice, firm |
| More / increase | Hand rises, fingers open |
| Less / decrease | Hand lowers, palm down |
| No / never | Index makes a small horizontal "no" |
| Yes / exactly | Index points forward, or small nod-gesture |
| Everything / everyone | Arms open, palms up (keep small/restrained per this project's gesture rule) |
| You | Palm or index extended toward the lens |
| Me / I | Thumb or hand touches the sternum |
| Why / think about it | Palms open upward, slight tilt |
| Honestly / really | Flat hand rests briefly on the chest |
| Small / a little | Thumb and index held close together |
| Big / a lot | Arms open wide (use sparingly — keep restrained) |
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

## The full template (MCP form — `<<<element_id>>>`, not `@image_1`)

```
Prompt text passed to generate_video:

<<<AVATAR_ELEMENT_ID>>> [STYLE ANCHOR block above, verbatim, no
"cinematic"].

[One flowing paragraph for ACTION. Open on a breath or a beat already
mid-thought — not a blank stare waiting to start. Weave the dialogue in
with physical beats and hand gestures mapped to key words (gesture bank
above, kept small/restrained per this project's rule). Close on a held
look, a slight settle, eyes staying on the lens — the post-line beat. No
internal timestamps.]

He says, at approximately 3.0 words per second (or 4.5 for a fast hook):
"[verbatim script]"

Delivery: lip-sync driven by the provided audio reference. [Tone line —
confident, warm voice, natural micro-pauses, no hesitation, no filler.]

Camera locks. Subject still moves naturally — natural head movement and
hand gestures evolve organically with the speech, at least one hand
visible in frame at all times, no frozen positions, no robotic
transitions.

medias: [
  { value: "<hero image job id>", role: "image" },
  { value: "<voice reference media_id>", role: "audio" }
]

Negative prompt (this project's locked negative rules — see above; do
not stack additional items beyond a specific recurring-bug fix).
```

---

## Worked example (standard pace, matches this project's locked style)

Script: *"I didn't become a coach to edit videos."* (8 words)

At 3.0 words/sec that's ~2.7s of speech — well under a natural clip
length, which is correct: the pre-line and post-line beats fill the
remaining time. Don't pad the dialogue to hit a duration; pad the
silence.

```
<<<9cf95684-c068-4807-bfa8-08aaa3add7c5>>> seated in the locked premium
podcast studio: neon-outline world-map background, dark metal shelving,
dark wood desk, black ceramic mug, boom-arm podcast microphone, premium
black executive chair. STYLE ANCHOR: Locked studio talking head, podcast
/ creator aesthetic. Prosumer camera (Sony A7S3-style) on a locked
tripod, no camera movement. Medium close-up framing, clear room at the
bottom of frame for hand gestures. Shallow depth of field. Warm key
light camera-front-left, soft fill camera-right, subtle rim light.
Photorealistic, visible pores, real eye moisture. 50-85mm equivalent
lens, eye-level.

Opens already mid-breath, a half-second beat of held eye contact before
speaking — not a cold start. As he says "I didn't become a coach," his
hand rises from resting near his sternum, palm loosely open, "to edit
videos" lands as the hand settles back down, fingers relaxing, a small
self-aware exhale crossing his face on the last word. He holds the look
half a second after the line ends, eyes steady on the lens.

He says, at approximately 3.0 words per second: "I didn't become a coach
to edit videos."

Delivery: lip-sync driven by the provided audio reference. Confident,
warm voice, natural micro-pauses, no hesitation, no filler.

Camera locks. Subject still moves naturally — natural head movement and
hand gestures evolve organically with the speech.

medias: [
  { value: "c2281451-ac7e-4f11-affa-7386146537cc", role: "image" },
  { value: "af1371ee-64cf-4e40-b7d8-13296b214095", role: "audio" }
]

Negative prompt: no robotic lip movement, no excessive smiling, no
exaggerated gestures, no dramatic cinematic acting, no plastic skin, no
beauty filter, no facial identity drift, no teeth showing, no frozen or
robotic hands, no rings or jewelry.
```

---

## Bug fixes — likely to apply to this project's talking heads

| Bug | What it looks like | Fix |
|---|---|---|
| **Frozen subject** | "Locked tripod" over-applied to the *subject*, not just camera | State explicitly: "Camera locks. Subject still moves naturally." |
| **Looping gesture** | Same hand motion repeats every ~2s | Map gestures to *specific* words from the actual script, not a vague "hands move naturally" |
| **Muffled audio / lip-sync drift** | Voice sounds processed, off-time from mouth | Don't describe the audio's texture — "lip-sync driven by the provided audio reference" is the whole line |
| **Plasticky face** | Skin looks smooth/waxy, especially in wide framing | Pull the shot tighter (medium close-up, matches locked 35–42% face-height framing) |
| **Camera won't stay locked** | Subtle dolly/drift creeps in despite "locked tripod" | Remove the word "cinematic" anywhere in the prompt |
| **Identity drift** | Face looks slightly off from the reference | Don't over-describe the face — trust `<<<element_id>>>` |
| **Hallucinated jewelry/accessories** | Ring, watch, or other item appears with no source | Add explicit negative ("no rings or jewelry on the hands") even when nothing in the prompt or reference suggests it — a confirmed occurrence in this project (2026-07-30) with no identified root cause in the prompt text |

---

## Checklist before generating

- [ ] Script is word-counted; duration calculated FROM the script (word
      count ÷ 3.0 or 4.5), never decided first and padded to fit
- [ ] Pace decided: standard (3.0) or dynamic (4.5) — matches the
      delivery line
- [ ] STYLE ANCHOR is the locked block above, verbatim, no "cinematic"
      unless this is an explicitly requested one-off departure
- [ ] Action prose has no internal timestamps — one time range only, if
      stated at all
- [ ] 2–3 hand gestures mapped to specific script words, kept small/
      restrained per this project's gesture rule
- [ ] Pre-line beat and post-line beat both written in
- [ ] Negative prompt includes this project's locked negative rules (not
      a shortened ad-hoc list) plus any bug-specific addition
- [ ] Identity via `<<<element_id>>>` (never `@image_1`), audio via
      `medias[]` with `role: "audio"` (never `@audio_1`)
- [ ] `declined_preset_id` set if a preset-match notice appears on
      preflight and literal generation is wanted (this project's default)
- [ ] Any deliberate departure from the locked studio/camera/gesture
      rules (different set, dynamic camera movement, energetic gestures)
      is explicitly confirmed with Mohamed per-clip, not treated as a new
      default
