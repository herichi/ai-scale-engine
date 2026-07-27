# AI Scale Engine — Visual Reference (Avatar / Hero Imagery)

**Status: APPROVED — locked as project knowledge (2026-07-26).**

This is the locked look for any generated image or video depicting Mohamed.
Use it as the starting point for every avatar/hero generation so output stays
visually consistent across content.

---

## LOCKED HERO IMAGE (CURRENT — updated 2026-07-27)

**File:** [`assets/hero-v4.png`](assets/hero-v4.png) — 2160×3840 (9:16), 4K

Approved on 2026-07-27. Mohamed's note: *"perfect lock this one as hero
image."* Generated from the locked `mohamed-avatar-2` identity Element,
combining face/outfit/background from the world-map reference image with
off-face, angled soft lighting from a second reference image (Mohamed
explicitly rejected flat direct-on-face lighting in the first world-map
attempt). Job id `c8aeeb32-aa3e-4c34-a482-37c16edd492e`.

Superseded [`assets/hero-v3.png`](assets/hero-v3.png) (the original
podcast-studio warm/blue hero) — v3 kept on disk for reference, not deleted.

---

## IDENTITY REFERENCE

**Higgsfield media_id:** `71682c17-406a-4c0a-a88b-f2bb36fe5340`
(`reference_Me_.jpg`)

This is the reference photo used to generate the approved hero image. Use it
as the identity/likeness reference for future generations unless Mohamed
supplies a newer one.

Other uploaded references from the same session (available but not used in
the approved render):
- `167278c7-e631-43d3-b90b-381c173cd81b`
- `4d1e3053-4e75-4d9e-970f-1bf9d57c7ae3`
- `bf2dfa16-7e76-40e4-83de-bf28f5cc4d5b` (`Exclusiv Cannes 100.jpg`)

> **Note on Avatar Lock:** `CLAUDE.md` carries a standing Avatar Lock rule
> referencing a locked avatar Element whose ID/location was never confirmed.
> The approved hero image was generated from the reference photo above, NOT
> from a confirmed Avatar Lock Element. If a formal Avatar Lock Element
> exists, reconcile it with this file before the next avatar generation.

---

## GENERATION SETTINGS (what produced the approved image)

- **Model:** `gpt_image_2` — required. Do NOT use `soul_2` or any Higgsfield
  "Soul" model: Soul 2.0 force-rewrites the prompt via `enhance_prompt` with
  no way to disable it, and ignores detailed framing instructions.
- **aspect_ratio:** `9:16` (portrait, TikTok/Instagram/Shorts)
- **resolution:** `4k`
- **quality:** `high`
- **count:** `1`
- **medias:** `[{ value: "71682c17-406a-4c0a-a88b-f2bb36fe5340", role: "image" }]`

Note: the tool takes all of these nested inside a `params` object.

---

## LOCKED FRAMING (v3 — the approved one)

Three framings were tested. v3 is the keeper:

| Version | Camera distance | Subject size | Verdict |
|---|---|---|---|
| v1 | ~2 m back | head 20–25% of frame | too far / too small |
| v2 | 1.3–1.6 m | head 28–35% | closer, still not it |
| **v3** | **90 cm – 1.2 m** | **face 35–42% of frame height** | **APPROVED** |

Framing rules:
- 9:16 vertical, camera eye-level, directly centered, subject centered
- Crop from approximately mid-torso / lower chest upward
- Face prominent but NOT a close-up; shoulders and upper torso fully visible
- Hands may naturally enter the lower frame when gesturing
- Small to moderate headroom — no excessive empty space
- NO legs, NO below-desk space, NO large desk foreground
- Lens feel: 50–70mm full-frame; no wide-angle distortion, no fisheye
- Reads like a high-end podcast host speaking directly to the viewer

---

## LOCKED LIGHTING & ENVIRONMENT (CURRENT — updated 2026-07-26)

Superseded the original podcast-studio warm/blue look below. Mohamed's
note: *"i don't like the lighting in this video, i want to change my
avatar [environment/lighting]"* — he explicitly rejected the old setup and
supplied a new reference image (`my avatar.jpg`, media_id
`b1918e56-d64b-44bf-9434-9d624028636c`), used for environment/lighting/style
only — his locked facial identity (`mohamed-avatar-2`, see AVATAR_LOCK.md)
is unchanged.

- **Background:** illuminated neon-outline world map on the wall behind the
  subject, white/cool-white line art on a muted purple/lavender-washed wall.
- **Ambient color:** overall cool purple/lavender wash across the scene —
  replaces the old warm-vs-blue contrast with a single cool tonal wash.
- **Studio furniture:** dark metal shelving/rack visible to one side, dark
  wood desk, black ceramic mug, boom-arm podcast microphone positioned to
  one side (not blocking the face), laptop visible at the desk edge.
- **Wardrobe (this look):** beige/tan blazer over a black crew-neck top —
  distinct from the white/cream top in the original hero reference; use
  this wardrobe only when generating in this new environment.
- **Framing:** stays consistent with the locked framing rules below (medium
  shot, hands visible, no legs) — only the lighting/background/wardrobe
  changed, not the camera distance/crop logic.

**Reference images:**
- `0c606b9b-8398-4c08-8f0c-6d19e7c27cc9` — face/outfit/background reference
  (world-map, beige blazer, black top, dark shelving, desk/mic/mug)
- `401402ba-d2eb-4905-9d26-a5c45221b0b2` — lighting/camera-angle reference
  ONLY: soft off-face key light (light does NOT hit the face directly/flat),
  natural shadow falloff, subtle cool blue accent, natural eye-level medium
  shot rather than a flat dead-center mugshot angle

Use both alongside the `mohamed-avatar-2` identity Element, NOT as
replacement identity references — face always comes from the locked
Element.

<details>
<summary>Superseded — original podcast-studio warm/blue look (kept for reference, not currently in use)</summary>

- **Key light:** large, soft, diffused; slightly above eye level; ~30–45°
  from camera; warm-neutral on skin; soft facial shadows, flattering but
  realistic.
- **Fill:** very subtle, opposite side — keeps facial dimension, doesn't
  flatten.
- **Background accent:** blue LED behind the subject, visible cool blue glow
  on acoustic panels/wall. Subtle and controlled — must NOT light the face
  blue.
- **Practical:** warm tungsten-style lamp in background, ~2700–3200K,
  creating warm contrast against the blue.
- **Net result:** refined warm/orange subject against cool blue background
  accents. Skin stays natural and warm.
- **Environment:** premium, professional podcast studio: dark wood or dark
  acoustic wall panels, modern and minimal, warm practical lamp, subtle blue
  LED behind subject, shelves/monitor/acoustic panels softly visible in
  background. Podcast mic on a boom arm — to one side, never blocking the
  face, never oversized. Must NOT read as: gaming room, neon streamer setup,
  cluttered office, cheap webcam setup.

</details>

Depth: shallow but realistic — subject very sharp, background softly
blurred, no extreme bokeh (unchanged in the new look).

---

## REALISM RULES (non-negotiable)

Preserve exact facial identity from the reference photo: age, ethnicity,
face shape, jawline, beard pattern, hairstyle, glasses, skin tone, natural
asymmetry, real facial proportions.

Skin must show visible pores, natural texture, slight imperfections,
realistic eye moisture, natural beard and lip texture, real under-eye
detail.

Never: beauty filter, skin smoothing, plastic skin, artificial symmetry,
CGI/3D-render look, idealization.

**Wardrobe:** match the reference photo (white/cream top) unless a specific
look is requested.

**Expression:** calm confidence — engaged, present, authoritative but
approachable, like explaining something valuable mid-interview.

---

## STANDING NEGATIVE PROMPT

No full-body shot. No legs. No under-desk space. No extreme zoom-out. No
excessive empty space or headroom. No tight facial close-up. No selfie or
phone-camera distortion. No fisheye or wide-angle. No oversized mic or mic
blocking the face. No huge desk foreground. No gaming setup. No RGB rainbow
lighting. No strong blue light on skin. No harsh shadows. No flat office
lighting. No plastic skin. No beauty filter. No CGI face. No unrealistic
eyes. No exaggerated gestures. No cropped head. No awkward hands. No
captions, text, logos, or social-media UI.
