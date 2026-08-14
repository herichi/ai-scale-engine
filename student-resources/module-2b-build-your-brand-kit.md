# Build Your Brand Kit

This module gets your visual and legal brand identity — logo, colors,
typography, templates, and policy text — saved into one file,
`BRAND_KIT.md`, so every future carousel or video request automatically
uses your real brand look instead of a generic default.

**Why this matters:** `brand-voice.md` (from the earlier module) tells
Claude how your brand *talks*. It says nothing about how your brand
*looks* or what it's legally allowed to promise. Without a brand kit,
every carousel or overlay Claude generates either guesses at colors/fonts
or asks you to repeat them every single time. Lock it once, and every
future asset request pulls from it automatically.

---

## What you need before you start

Your `brand-voice.md` should already exist (from the earlier module).
This module builds on top of it — do that one first if you haven't.

Have these ready to attach if you have them (not all are required to
start):

- Your logo file(s)
- Your brand color hex codes (or a link/screenshot of your brand
  guidelines if you have one)
- Your font/typeface name(s)
- Any existing templates (carousel layout, video lower-third style,
  thumbnail style)
- Any required policy/legal/disclaimer text (refund policy wording,
  required disclosures, etc.)

If you don't have some of these yet, that's fine — fill in what you have
now and add the rest later. A partially-filled brand kit is still useful;
it just means some sections stay defaults until you attach more.

---

## Step 1 — Attach what you have

Attach your files in chat and say what each one is. Use this prompt:

> Here's my brand kit. [Attach logo, color reference, font info, templates,
> policy text — whatever you have.] Save these into my project and create
> `BRAND_KIT.md` documenting: my logo (and where the file lives), my color
> palette (hex codes), my typography, any templates I gave you, and any
> policy/legal text I gave you. Use my `brand-voice.md` file for tone
> context but don't duplicate it — this file is about the visual/legal
> identity only.

**Prefer a fully guided, step-by-step intake instead?** Use
[`BRAND_KIT-intake-prompt.md`](BRAND_KIT-intake-prompt.md) — a
copy/paste prompt that has Claude walk you through each brand asset
category one at a time (logo, colors, typography, templates, mood board,
policy text, other assets), opening the upload widget for each, rather
than you attaching everything at once.

## Step 2 — Fill in what's missing

If you don't have hex codes handy, ask Claude to help you pick or extract
them:

> I don't have exact hex codes for my brand colors — [describe them, e.g.
> "dark navy background, warm cream text, one orange accent"] or pull them
> from this logo file. Suggest hex codes that match and add them to
> `BRAND_KIT.md`.

## Step 3 — Lock policy/legal text exactly

If you have required disclaimer, refund, or compliance wording, paste it
in verbatim rather than describing it — this text needs to appear exactly
right wherever it's used, not paraphrased:

> Add this exact policy text to the POLICY & LEGAL TEXT section of
> `BRAND_KIT.md`, word for word, not summarized: "[paste your exact
> wording]". Use it verbatim on any asset that needs it — never
> paraphrase it without asking me first.

## Step 4 — Verify it's actually usable going forward

Test that the lock worked by asking for a carousel without specifying
colors:

> "Make me a 5-slide carousel about [some topic]."

Check: did Claude use your locked colors and typography automatically,
without you specifying them? If it defaulted to something generic
instead, your `BRAND_KIT.md` may need more specific detail (exact hex
codes rather than descriptions) — ask Claude to tighten it.

---

## Reference — what `BRAND_KIT.md` contains

```
# [Your Brand] — Brand Kit

## 1. LOGO
[file path(s), variants, clear space rules]

## 2. COLOR PALETTE
[hex codes, what each is used for]

## 3. TYPOGRAPHY
[typeface name(s), heading/body conventions]

## 4. TEMPLATES
[carousel template, lower-third/caption style, thumbnail template]

## 5. BRAND DOCUMENTS
[any source brand guideline docs]

## 6. POLICY & LEGAL TEXT
[exact required wording — disclaimers, refund policy, disclosures]

## 7. OTHER BRAND KIT ASSETS
[anything else — icon set, intro/outro stinger, etc.]
```

---

## Why this matters for every future request

Once this is locked, you never have to re-specify your colors, fonts, or
policy wording again. A future request like *"make me a carousel about
[X]"* or *"add a caption overlay to this video"* will automatically pull
your real brand colors, typography, and any required legal text — you
just supply the topic. Same principle as `AVATAR_LOCK.md` and
`VOICE_LOCK.md`: define it once, correctly, and every future generation
uses it without you repeating yourself.
