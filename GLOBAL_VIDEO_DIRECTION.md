# GLOBAL VIDEO DIRECTION — AI Scale Engine Welcome Video

**Status: APPROVED — locked as project knowledge (2026-07-27).**

This is the master creative/technical bible for every clip in the AI Scale
Engine Skool welcome video series (and any future avatar video sharing the
same continuity). Every clip generated for this series must comply with
every rule below — the whole point is that separately generated clips feel
like one uninterrupted recording.

---

## CONCEPT

A professional 9:16 vertical founder-style welcome video for the AI Scale
Engine Skool community. The founder is personally welcoming a small group of
early members behind the scenes before the official launch.

**This is NOT a polished corporate advertisement.** It should feel: warm,
personal, energetic, genuine, confident, slightly playful, exclusive,
founder-to-founder, premium but human.

**The viewer should feel:** *"I'm getting early access to something that is
still being built, and my opinion actually matters."*

---

## IDENTITY

Use the locked AI Twin / avatar identity (`mohamed-avatar-2`, Element id
`9cf95684-c068-4807-bfa8-08aaa3add7c5` — see `AVATAR_LOCK.md`) consistently
across every clip. Preserve exactly: facial identity, face proportions,
hairstyle, beard, glasses, skin tone, age, body proportions, wardrobe,
natural facial asymmetries. Do not idealize or beautify the avatar.

---

## STUDIO (locked, must not change between clips)

Professional premium podcast studio — current environment per
`visual-reference.md` / `assets/hero-v4.png`: neon-outline world-map
background, dark metal shelving, dark wood desk, black ceramic mug,
boom-arm podcast microphone, premium black executive chair. Clean, modern,
founder-studio feel. No clutter, no gaming aesthetic.

---

## LIGHTING (locked)

- **Key:** large, soft, diffused, warm-neutral; ~30–45° from camera; soft
  natural facial shadows; realistic warm skin tone. Light must NOT hit the
  face flat/direct-on — angled, off-face soft light (per the approved
  hero-v4 lighting reference).
- **Background:** subtle blue LED accents, stays behind the subject — no
  blue cast on skin.
- **Practical:** warm tungsten-style lamp, ~2700–3200K.
- **Overall contrast:** warm founder / warm skin against cool blue premium
  studio accents.

---

## CAMERA

- 9:16 vertical. Camera directly in front, eye level, subject centered.
- Framing: approximately mid-torso upward, face prominent but not a
  close-up, moderate headroom, hands may naturally enter the lower frame.
- No legs, no under-desk area, no oversized desk foreground.
- Distance: ~90cm–1.2m. Lens: ~50–70mm full-frame equivalent. Natural facial
  proportions — no wide-angle distortion, no fisheye.
- **Camera behavior:** mostly locked. Only extremely subtle natural
  movement allowed — a tiny push-in during emotional lines, subtle
  breathing movement. No obvious zoom, no handheld shake, no dramatic
  camera movement.

---

## PERFORMANCE

Look directly into the lens. Speak as though addressing a small group of
coach friends personally.

**Energy progression across the series:** 1. friendly excitement → 2. clear
explanation → 3. invitation and belonging → 4. playful honesty → 5. genuine
gratitude.

**Voice:** natural, warm, conversational, confident, slightly energetic.
Never robotic, never overly polished, never "sales voice."

**Delivery speed:** ~150–175 words per minute (~2.5–2.9 words/sec) as a
general default. Allow short natural pauses. Do not rush important lines.
(A specific clip may specify an exact words/sec target that overrides this
default — always use the per-clip value when given.)

**Facial performance:** natural smile at opening, genuine excitement on
"AI Scale Engine," slight eyebrow movement on emphasis, friendly eye
contact, subtle smile around playful lines, sincere expression during any
feedback request.

**Gestures:** restrained and natural only. Allowed: small open-hand gesture
when explaining the system, subtle finger/counting gestures for lists,
slight lean forward during important invitation lines, relaxed return to
neutral. Do NOT: wave hands excessively, perform exaggerated influencer
gestures, point aggressively, overact.

---

## CONTINUITY (critical — every clip in the series)

All clips must feel like one uninterrupted recording. Lock across every
clip: avatar, wardrobe, studio, camera position, lens, chair, microphone,
lighting, desk, background, color grade. Do not change the environment
between clips.

---

## AUDIO / SPEECH

Natural voice with realistic breaths and pauses. No background music unless
added later in editing. No text on screen during generation.

**Captions (updated 2026-07-27 — reverses the original "no captions"
rule):** every finished video in this series gets burned-in captions.
Seedance 2.0 has no captioning capability at generation time, so captions
are added as a separate assembly step: once the clip(s) are generated (see
Voice below — no voice_change needed first), run them through
`explainer_video` with `subtitles: {font: ...}` — it transcribes the final
voiceover (Whisper) and burns timed captions automatically. Raw generated
clips (pre-assembly) stay caption-free; the assembled/stitched final output
is the one with captions.

**Known gap (2026-07-28):** `explainer_video` requires at least 2 distinct
clips per call — it's a stitching tool with captions as a side effect, not
a standalone single-clip captioner. There is currently no tool available
to burn captions onto one standalone clip that isn't being combined with
another. **For a single, independent clip (not part of a multi-part
series meant to be stitched together), skip Higgsfield captioning
entirely and rely on the destination platform's own native auto-caption
feature after upload** (TikTok/Instagram both offer this). Do not pair an
unrelated clip with the standalone one just to satisfy the 2-item minimum
— that produces a merged video the user didn't ask for, which is worse
than no captions.

**Known gap #2 (2026-07-28) — TikTok's native auto-caption fails on
Seedance audio:** confirmed on 2 separately published clips
(`audio_references`-driven Seedance 2.0 generations) — TikTok's caption
toggle greys out with "Voix non reconnue" / "Voice not recognized," so
native auto-captioning does not work as a fallback for these clips despite
the plan above. Root cause not confirmed (likely an audio encoding/format
mismatch between Seedance's output track and TikTok's speech recognizer —
not a content or language issue). **Workarounds, in order of effort:**
1. Type captions in manually via TikTok's manual caption/text editor
   (guaranteed to work, slower).
2. Try Higgsfield's `explainer_video` (Whisper-based transcription) —
   different engine than TikTok's, may succeed where TikTok's recognizer
   fails, but requires pairing with a second clip (see gap #1 above).
3. Instagram's native auto-caption has not yet been confirmed to have the
   same issue — test there before assuming it also fails.

---

## NEGATIVE RULES (apply to every clip, no exceptions)

No robotic lip movement. No excessive smiling. No corporate presenter
energy. No fake enthusiasm. No exaggerated gestures. No hard selling. No
dramatic cinematic acting. No gaming RGB. No neon wash. No plastic skin. No
beauty filter. No facial identity drift. No wardrobe changes. No studio
changes. No text. No captions. **No teeth showing** (smiles stay closed-
mouth/subtle per this rule — flagged as worth double-checking with Mohamed
if a specific script implies an open, toothy smile).

---

## Pipeline notes (technical, not creative — see `SEEDANCE.md` and the
`avatar-video` skill)

**Full prompting system (imported 2026-07-29):** [`SEEDANCE.md`](SEEDANCE.md)
is the master technical prompting guide for Seedance generations in this
project — adapted from an external Seedance Studio Prompting Guide for this
project's actual MCP tool interface. Read it before building any
`generate_video` prompt: it covers pacing math (2.7/4.5 words per sec),
the hand-gesture bank, lean negative prompts, the "no cinematic" rule, and
bug fixes for frozen hands/looping gestures/plasticky faces/identity drift.

Quick summary (see `SEEDANCE.md` for full detail):
- Model: `seedance_2_0`. Max clip duration is 15 seconds (hard limit) — a
  script must fit its target words/sec × duration, or it needs to be split
  into multiple continuity-locked clips.
- **Voice (CONFIRMED WORKING, 2026-07-27):** pass Mohamed's locked voice
  reference file directly as `audio_references` alongside the image
  reference — see `VOICE_LOCK.md` for the media_id. Seedance 2.0 generates
  the avatar speaking in his real voice in one pass. No `voice_change` step
  is needed; that earlier two-step approach is superseded. Reference the
  audio by function only ("lip-sync driven by the provided audio
  reference") — never describe its texture in the prompt.
- Always pass the locked hero image job id as the `image` media reference
  AND embed `<<<9cf95684-c068-4807-bfa8-08aaa3add7c5>>>` in the prompt text
  for the identity Element. **Never use `@image_1`/`@audio_1`-style tags —
  those are a Higgsfield web-UI convention, unconfirmed for this MCP
  interface.**
- Default pacing going forward: **2.7 words/sec (standard)** unless a hook
  specifically needs the faster 4.5 words/sec dynamic pace. (Prior clips in
  this project used ad-hoc 3.0/3.7 figures — those worked but weren't
  validated against a reference; new clips should use the SEEDANCE.md
  table.)
