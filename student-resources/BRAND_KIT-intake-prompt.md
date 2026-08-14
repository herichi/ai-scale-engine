# Brand Kit Intake Prompt — copy/paste tool

This is a ready-to-use prompt for students building their brand kit **from
scratch**. Paste the block below into a Claude Code session inside your own
project folder. It turns Claude into a guided intake assistant that asks
for your brand assets **one category at a time**, opens an upload
widget for each, and — once you've gone through every category — builds
your `BRAND_KIT.md` and updates your `CLAUDE.md` automatically.

This is the tool itself. If you want the explanation of *why* each part
matters, see [`module-2b-build-your-brand-kit.md`](module-2b-build-your-brand-kit.md).

---

## How to use this

1. Open Claude Code in your own project folder (the same one your
   `brand-voice.md` lives in, if you've already done that module).
2. Copy everything inside the fenced block below.
3. Paste it as your message and send it.
4. Answer each question as it comes — attach files when asked, or say
   "skip" / "don't have this yet" to move on. Nothing is required to
   start; a partially-filled brand kit is still useful.
5. At the end, Claude will show you the finished `BRAND_KIT.md` and ask
   you to confirm before saving it.

---

## The prompt

```
I want to build my Brand Kit from scratch — a single reference file that
holds my brand's visual and legal identity, so every future carousel,
video, or design request you generate for me automatically uses my real
brand instead of a generic default.

Act as a guided intake assistant. Walk me through this ONE CATEGORY AT A
TIME, in this exact order. For each category: ask me for it, wait for my
answer, then move to the next. Don't ask about the next category until
I've responded to the current one. If a category needs a file (image,
PDF, etc.), use the media/file upload widget so I can attach it directly
rather than asking me to describe it in text. If I say "skip" or "don't
have it," note the category as empty and move on — don't block on it.

Go through these categories in order:

1. LOGO — my primary logo file, plus any variants I have (wordmark,
   icon-only, light-background version, dark-background version).
2. COLOR PALETTE — my brand's exact colors. If I don't have hex codes,
   help me extract them from my logo or other attached files, or suggest
   codes based on my description.
3. TYPOGRAPHY — my brand's typeface(s), and any heading/body size or
   weight conventions I already use.
4. TEMPLATES — any existing reusable layouts I have: carousel template,
   video lower-third/caption style, thumbnail template. Ask what each one
   is for as I attach it.
5. BRAND DOCUMENTS / MOOD BOARD — any brand guideline PDF, style guide,
   or mood board images that capture my brand's overall visual direction,
   beyond what's captured in the categories above.
6. POLICY & LEGAL TEXT — any required disclaimer wording, refund/
   guarantee policy language, or platform-required disclosures (e.g.
   "AI-generated content" labeling) that must appear verbatim wherever
   it's used. Tell me to paste this text directly rather than describing
   it, so the wording stays exact — don't let this get paraphrased.
7. OTHER BRAND ASSETS — anything else that defines my brand visually:
   icon sets, pattern/texture assets, a sound logo, an intro/outro
   stinger video, etc.

After going through all 7 categories:

- Show me a summary of everything collected (and what's still empty) and
  ask me to confirm before saving anything.
- Once I confirm, create/update `BRAND_KIT.md` in my project with
  everything I gave you, organized under these same 7 sections. Save any
  uploaded files into an `assets/brand/` folder in my project and
  reference them by path in the file.
- Update my `CLAUDE.md` (or create it if it doesn't exist) with a short
  standing rule: "Read `BRAND_KIT.md` before any carousel, video, or
  design generation that needs brand colors, typography, logo placement,
  or policy/compliance text — same as `AVATAR_LOCK.md` and
  `VOICE_LOCK.md` lock identity and voice."
- Don't invent or assume any brand fact I didn't give you — leave a
  category as an explicit placeholder (not a guess) if I skipped it.
```

---

## What happens after

Once `BRAND_KIT.md` exists, test that it actually gets used:

> "Make me a 5-slide carousel about [some topic]."

If Claude pulls your real colors, fonts, and logo automatically without
you re-specifying them, the lock worked. If it defaults to something
generic, go back and add more specific detail (exact hex codes over vague
descriptions) — ask Claude to tighten the relevant section in
`BRAND_KIT.md`.

You can re-run the prompt above any time your brand changes — say
"update my brand kit" and attach the new asset, rather than starting the
whole intake over.
