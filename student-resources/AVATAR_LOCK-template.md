# AVATAR_LOCK — TEMPLATE

Copy this into your own project as `AVATAR_LOCK.md` and fill in every
`[bracketed]` value with your own. This is one of the source-of-truth
files the `avatar-video` skill reads before every generation — it tells
the skill which identity Element to use so every generated image/video is
actually you, not a random face.

---

## Higgsfield Identity Element

**Element name:** `[your-name]-avatar` (Higgsfield may auto-suffix this if
the name is already taken in your workspace — e.g. `-2`. If so, the
display name is cosmetic; the Element ID below is what actually matters.)
**Element ID:** `[the Element id returned when you create it]`
**Category:** character

**Identity Source:** `[describe what's bundled into this Element — e.g.
Hero Photo + Turnaround Sheet + Close-Up Sheet, bundled as ONE Element]`

**Generation Rule:** Every avatar image or video generated for your
project must reference this Element. Embed
`<<<[your Element id]>>>` in the generation prompt — the Higgsfield
backend auto-injects the image and rewrites it to `@[your-element-name]`.

## Identity priority (if you bundle multiple reference images into one Element)

- **Hero Photo** → primary facial identity and overall likeness
- **Turnaround Sheet** (if you make one) → profile, side angles, head
  shape, proportions, hairstyle, consistency across viewpoints
- **Close-Up Sheet** (if you make one) → skin detail, eyes, facial
  features, texture, asymmetry, realism

If you bundle more than one image, use them together as one reference
system — no single image should override the others in a way that damages
identity consistency.

## Locked attributes

Do not alter or reinterpret without your explicit request:
- face shape
- jawline
- eyes
- nose
- hairstyle
- age
- ethnicity
- skin tone
- defining facial asymmetries
- body proportions
- glasses (when applicable)
- [add anything else specific to your look — beard, distinguishing marks,
  etc.]

## Source assets

- `[path to your locked hero image, e.g. assets/hero.png]` — [resolution,
  aspect ratio]
- `[any additional reference images, with their job ids if generated via
  Higgsfield]`

Full generation settings and framing/lighting spec for your hero image
should live in your own `visual-reference.md`.
