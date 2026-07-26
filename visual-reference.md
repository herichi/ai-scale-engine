# AI Scale Engine — Visual Reference (Avatar / Hero Imagery)

**Status: APPROVED — locked as project knowledge (2026-07-26).**

This is the locked look for any generated image or video depicting Mohamed.
Use it as the starting point for every avatar/hero generation so output stays
visually consistent across content.

---

## LOCKED HERO IMAGE

**File:** [`assets/hero-v3.png`](assets/hero-v3.png) — 2160×3840 (9:16), 4K

Approved on 2026-07-26 after three iterations. Mohamed's note: *"will keep
the last one as reference — the lighting is good."* The lighting setup in
this image is the reference standard, not just the framing.

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

## LOCKED LIGHTING (the part Mohamed specifically approved)

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

---

## ENVIRONMENT

Premium, professional podcast studio: dark wood or dark acoustic wall
panels, modern and minimal, warm practical lamp, subtle blue LED behind
subject, shelves/monitor/acoustic panels softly visible in background.
Optional podcast mic on a boom arm — to one side, never blocking the face,
never oversized.

Must NOT read as: gaming room, neon streamer setup, cluttered office, cheap
webcam setup.

Depth: shallow but realistic — subject very sharp, background softly
blurred, no extreme bokeh.

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
