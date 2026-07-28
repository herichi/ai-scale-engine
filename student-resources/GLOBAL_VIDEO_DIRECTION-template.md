# GLOBAL VIDEO DIRECTION — TEMPLATE

Copy this into your own project as `GLOBAL_VIDEO_DIRECTION.md` and fill in
every `[bracketed]` section with your own choices. This is the master
creative/technical bible the `avatar-video` skill reads before every
generation — the whole point is that separately generated clips feel like
one uninterrupted recording, so be as specific as you can.

---

## CONCEPT

[Describe the video series in one paragraph: who's the founder, what's the
context (welcome video? ad? course intro?), who's the audience, what should
the viewer feel by the end.]

**The viewer should feel:** *"[one sentence — the specific emotional
takeaway you want]"*

---

## IDENTITY

Use your locked AI Twin / avatar identity consistently across every clip:
`[YOUR_AVATAR_ELEMENT_NAME]`, Element id `[YOUR_AVATAR_ELEMENT_ID]` — see
your `AVATAR_LOCK.md`.

Preserve exactly: facial identity, face proportions, hairstyle, beard/
makeup, glasses (if any), skin tone, age, body proportions, natural facial
asymmetries. Do not idealize or beautify the avatar.

---

## STUDIO (locked, must not change between clips)

[Describe your environment in detail: wall/background style, furniture,
props, desk, chair, any signage/branding visible. Be specific — vague
descriptions produce inconsistent backgrounds across clips.]

---

## LIGHTING (locked)

- **Key light:** [soft/hard, warm/cool, angle from camera]
- **Background accents:** [any colored light, LED strips, neon, etc. —
  specify it must stay OFF the face if you don't want tinted skin]
- **Practical lights:** [any visible lamps and their color temperature]
- **Overall look:** [describe the contrast/mood in one sentence]

---

## CAMERA

- Aspect ratio: [9:16 / 16:9 / etc.]
- Framing: [where the crop starts/ends — e.g. mid-torso up, headroom
  amount, whether legs/desk are visible]
- Distance: [approximate camera distance]
- Lens feel: [approximate focal length equivalent]
- **Camera behavior:** [locked? subtle push-ins allowed? handheld feel?]

---

## PERFORMANCE

**Energy progression across the series:** [list the emotional beats, in
order, e.g. friendly → explanatory → invitation → gratitude]

**Voice:** [describe the target vocal quality — natural/warm/energetic/
authoritative/etc., and what to avoid, e.g. "never robotic," "never sales
voice"]

**Delivery speed:** [target words per minute or words per second — this
feeds directly into duration calculations, so be precise]

**Facial performance:** [smile style, eyebrow movement, eye contact notes]

**Gestures:** [what's allowed vs. not — be specific, e.g. "small open-hand
gestures when listing items" vs. "no exaggerated pointing"]

---

## CONTINUITY (critical — every clip in the series)

All clips must feel like one uninterrupted recording. Lock across every
clip: avatar, wardrobe, studio, camera position, lens, chair, microphone,
lighting, desk, background, color grade. Do not change the environment
between clips.

---

## AUDIO / SPEECH

Natural voice with realistic breaths and pauses. [Background music: added
later in editing, or not at all?] [Captions: burned in at generation, or
added later at assembly via explainer_video? State your choice clearly —
this determines which pipeline step handles it.]

---

## NEGATIVE RULES (apply to every clip, no exceptions)

[List everything you explicitly do NOT want — e.g. no robotic lip
movement, no over-smiling, no corporate energy, no beauty filter, no
identity drift, no wardrobe/studio changes between clips, no on-screen
text if captions are handled separately, etc.]

---

## Pipeline notes (technical — for the avatar-video skill)

- Model: `seedance_2_0`. Max clip duration is 15 seconds (hard limit) — a
  script must fit its target words/sec × duration, or split into multiple
  continuity-locked clips.
- Pass your voice reference file's media_id (from `VOICE_LOCK.md`) as an
  `audio_references` media role directly in the same `generate_video` call
  — Seedance 2.0 generates speech in your real voice in one pass, no
  separate voice-swap step needed.
- Always pass your locked hero image job id as the `image` media reference
  AND embed `<<<YOUR_AVATAR_ELEMENT_ID>>>` in the prompt text for the
  identity Element.
