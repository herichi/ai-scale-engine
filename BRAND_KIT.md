# AI Scale Engine — Brand Kit

**Status: reference file — attach your brand assets here.**

This is the single place that holds the *visual and legal identity* of the
brand: logo, colors, typography, templates, and policy text. `brand-voice.md`
defines how the brand **talks**; this file defines how the brand **looks**
and what it's **allowed to say/promise**. Every video or carousel generation
that needs brand colors, typography, logo placement, or policy/compliance
language should read this file first.

Read this before: any carousel/static-image generation, any video overlay
or lower-third, any asset that places a logo, watermark, or legal/policy
text on screen.

---

## 1. LOGO

- **Primary logo mark — LOCKED (2026-08-20):**
  `https://d8j0ntlcm91z4.cloudfront.net/user_3BmXuTgLLEXGF8XeA55vjeX2lPV/hf_20260820_214239_2cd4140a-22ee-4f56-8ca2-dddb01d0fa0c.png`
  — hosted URL supplied directly by Mohamed, already public. Use this as
  `profileImage` in every carousel render (`CAROUSEL_LOCK.md` §3) — do not
  omit it and do not attempt a local upload workaround.
- **Logo variants:** *(wordmark, light-background version — attach if a
  need for one comes up; the orange "A" mark on dark/transparent is the
  only variant confirmed so far)*
- **Clear space / minimum size:** *(if defined)*
- **Do NOT:** stretch, recolor outside the locked palette below, place on a
  busy background without sufficient contrast, or crop the mark.

---

## 2. COLOR PALETTE

Locked brand colors (source of truth — also mirrored in the website repo's
`app/src/styles.css` as CSS variables):

- Background: `#0a0a0a` (`--ase-bg`)
- Ink/text: `#f5f1ea` (`--ase-ink`)
- Accent (single locked accent, orange): `#ff7a1a` (`--ase-orange`)
- Line/border: `rgba(245, 241, 234, 0.12)` (`--ase-line`)

Apply these by default to any generated carousel, quiz widget, video
overlay, or mockup for this project — never fall back to generic blue/white
unless explicitly asked. Do not introduce a new accent color without
updating this file first.

---

## 3. TYPOGRAPHY

- **Primary typeface:** *(attach or name it — e.g. font family + weights
  used on the website/carousels)*
- **Heading style:** *(size/weight/case conventions, if defined)*
- **Body style:** *(size/weight conventions, if defined)*
- Source of truth if defined in code: website repo's `app/src/styles.css`.

---

## 4. TEMPLATES

Reusable visual templates for repeatable content formats:

- **Carousel template:** *(attach — slide dimensions, safe zones, where
  the logo/CTA sit)*
- **Video lower-third / caption style template:** *(attach, if defined —
  font used for burned-in captions, position, color)*
- **Thumbnail template:** *(attach, if defined)*
- **Closing outro video (LOCKED, 2026-08-01):**
  [`assets/video/closing-outro-9x16.mp4`](assets/video/closing-outro-9x16.mp4)
  (vertical, 1080x1920) /
  [`assets/video/closing-outro.mp4`](assets/video/closing-outro.mp4)
  (source, 16:9) — "Build the Engine / Join us now! / AI Scale Engine
  Community" on black with an orange flame-burst motion graphic, ~5s.
  Append to the end of every video produced in this project. See
  `CLAUDE.md`'s "Standing rule — Closing outro video" for the usage rule.
- **Full-video motion/sound reference (LOCKED, 2026-08-02):**
  [`assets/video/reference-capcut-edit.mp4`](assets/video/reference-capcut-edit.mp4)
  — Mohamed's CapCut pass over the AI Content Machine video (20.5s, 9:16).
  Analyzed and broken down in `CLAUDE.md`'s "Standing rule — CapCut
  reference edit." Every future text-based video in this project should
  match: (1) the same background-music bed at the same audible loudness
  (not the earlier faded-down 0.32 peak volume — this reference plays it
  louder throughout), (2) an RGB channel-split/glitch effect on the
  punch-word beat, (3) the starfield-particle + subtle cinematic letterbox
  treatment layered onto the closing outro specifically (not the whole
  video — confirmed by frame-by-frame check that the hook/checklist scenes
  are untouched). Same locked outro content ("Build the Engine / Join us
  now! / AI Scale Engine Community"), same logo.

If no templates are attached yet, generated assets default to the locked
colors/typography above with no fixed template — flag this as a gap rather
than inventing a layout.

---

## 5. BRAND DOCUMENTS

Attach any source documents that define the brand's visual or verbal
identity beyond what's already captured in `brand-voice.md`:

- *(e.g. original brand guidelines PDF, style guide, mood board)*

---

## 6. POLICY & LEGAL TEXT

Standing text that must appear correctly, verbatim, wherever required
(disclaimers, compliance language, required legal copy):

- **Disclaimer text:** *(attach/paste exact required wording, if any)*
- **Refund/guarantee policy language:** *(attach/paste, if any — must match
  what's actually offered in `offer.md`, don't let marketing copy imply
  something the policy doesn't cover)*
- **Any platform-required disclosure:** *(e.g. "AI-generated content"
  labeling requirements, if applicable)*

Do not paraphrase policy/legal text when it needs to appear on an asset —
use it verbatim unless the user explicitly approves a shortened version.

---

## 7. OTHER BRAND KIT ASSETS

Anything else that defines the brand and doesn't fit above:

- *(icon set, pattern/texture assets, sound logo, intro/outro stinger,
  etc.)*

---

## How to fill this in

Attach files via the chat and say what each one is (logo, template, policy
doc, etc.) — Claude will save them into
`ai-scale-engine-mo-test-3/assets/brand/` and fill in the matching section
above with the file path and any relevant detail (variant, use case). Paste
policy/legal text directly rather than describing it, so the wording stays
exact.

---

## Why this file exists

Before this file, brand color/typography/policy facts were either missing
or scattered — colors lived only in CLAUDE.md, and there was no home for
logo files, templates, or policy text at all. Any carousel or video
generation needing this information now reads `BRAND_KIT.md` first,
alongside `brand-voice.md` for tone and `visual-reference.md` for the
avatar's visual look. This keeps the same "define once, reuse everywhere"
principle as `AVATAR_LOCK.md` and `VOICE_LOCK.md`.
