# AVATAR_LOCK — Mohamed's AI Twin Identity

**Status: APPROVED / LOCKED (2026-07-26).**

## Higgsfield Identity Element

**Primary Element:** `mohamed-avatar-2`
**Element ID:** `9cf95684-c068-4807-bfa8-08aaa3add7c5`
**Category:** character

**Identity Source:** Validated Hero Photo + Turnaround Sheet + Close-Up
Sheet, bundled as ONE Higgsfield Element (not three separate elements).

**Status:** APPROVED / LOCKED

**Generation Rule:** Every future avatar image or Seedance video must
reference this Element unless Mohamed explicitly instructs otherwise. Embed
`<<<9cf95684-c068-4807-bfa8-08aaa3add7c5>>>` in the generation prompt; the
Higgsfield backend auto-injects the image and rewrites it to
`@mohamed-avatar-2`.

## Naming note

The intended name was `mohamed-avatar`, but that name (and several variants:
`Mohamed-avatar`, `mohamed-avatar-1`, `Mohamed-avatar-v2`) already existed in
the workspace from prior sessions. Higgsfield auto-suffixed this Element to
`mohamed-avatar-2`. There is no rename action in Higgsfield's Element API
(only `list` / `get` / `create`), so the display name stays as-is — the
Element ID above is the actual reference used in every generation, not the
name. The older elements are superseded and unused; they were left in place
rather than deleted (no destructive action taken without being asked).

## Identity priority (how the 3 bundled images are used together)

- **Hero Photo** → primary facial identity and overall likeness
- **Turnaround Sheet** → profile, side angles, head shape, proportions,
  hairstyle, and consistency across viewpoints
- **Close-Up Sheet** → skin detail, eyes, facial features, beard pattern,
  texture, asymmetry, and realism

Used together as one reference system — no single image should override the
others in a way that damages identity consistency.

## Locked attributes

Do not alter or reinterpret without Mohamed's explicit request:
- face shape
- jawline
- eyes
- nose
- beard structure
- hairstyle
- age
- ethnicity
- skin tone
- defining facial asymmetries
- body proportions
- glasses (when applicable)

## Source assets

- [`assets/hero-v3.png`](assets/hero-v3.png) — Hero Photo (2160×3840, 9:16, 4K)
- Turnaround Sheet — generated at 16:9, 4K (job `4ac6ecbd-de66-43d9-ace1-6756042f48b5`)
- Close-Up Sheet — generated at 3:4, 4K (job `ceddcbf8-93dc-4bd1-bde3-cef98c0f79ed`)

Full generation settings and framing/lighting spec for the Hero Photo are in
[`visual-reference.md`](visual-reference.md).
