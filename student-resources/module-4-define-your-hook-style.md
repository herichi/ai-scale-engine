# Define Your Hook Style & Lock It to Your Brand Voice

This module gets your personal hook style written down and locked into
your `brand-voice.md` — so when you ask for a video later, Claude already
knows exactly which hook pattern is yours, instead of guessing or
defaulting to something generic.

**Why this matters:** a hook is the first 2-3 seconds of a short-form
video — it decides whether someone keeps watching or scrolls past. If your
hook style isn't written down anywhere, every script request starts from
zero. Once it's locked, every future "make me a video" request
automatically pulls from your real, tested hook style.

---

## What you need before you start

Your `brand-voice.md` should already exist (from an earlier module) with
your audience, offer, and tone defined. If it doesn't exist yet, do that
module first — hook style builds on top of your existing voice, it doesn't
replace it.

---

## Step 1 — Write 3 real hook scripts

Pick ONE hook pattern to start with (you can add more patterns later).
Common patterns:

- **Question hook:** open with a direct question that names the viewer's
  own stuck-ness or unspoken thought. E.g. *"Do you know the 3 mistakes
  keeping you stuck at ___?"*
- **Statement hook:** open with a blunt claim or reframe. E.g. *"You don't
  need more content. You need a system."*
- **Story hook:** open mid-scene, in the middle of a moment. E.g. *"3am,
  still editing, and I finally asked myself why."*
- **Contrarian hook:** open by naming what everyone else says is true,
  then push against it. E.g. *"Everyone tells you to post more. That's
  the wrong advice."*

Whichever pattern you pick, write 3 real 10-second scripts using it, in
your own voice, ending on your locked CTA. Use this prompt:

> Using my brand-voice.md — my audience, offer, tone, and locked CTA —
> write me 3 short-form video hook scripts, 10 seconds each (~30 words at
> [your target words/sec from GLOBAL_VIDEO_DIRECTION.md, or ~2.5-3.0
> words/sec if you haven't set one yet]).
>
> Hook pattern: [pick one — question / statement / story / contrarian].
>
> Each script should: open with the hook in the first line, stay direct
> and emotional (not corporate or generic), and end with my CTA from
> offer.md/brand-voice.md.
>
> Show me all 3, and check the word count against my target duration
> before finalizing — don't let any of them run long.

## Step 2 — Pick your favorite, or ask for a revision

Look at the 3 scripts. If none of them sound like you, say so and ask for
a different angle — don't settle for one that reads generic. Once you have
at least one you'd actually say out loud, move to Step 3.

## Step 3 — Lock this as your hook style

Use this prompt to save the pattern (not just the one-off scripts) into
your `brand-voice.md`, so it's reusable for every future request:

> Add a new sub-section under my HOOK STYLE section in brand-voice.md
> called "[Question / Statement / Story / Contrarian] hooks" — the pattern
> I just picked. Document: the pattern itself (e.g. "question → reframe →
> CTA"), 2-3 short example hook lines in my own words (not the full
> scripts, just the opening lines), and one full example script for
> reference. Keep my existing hook style entries in brand-voice.md
> untouched — this is an addition, not a replacement.

## Step 4 — Verify it's actually usable going forward

Test that the lock worked by asking for a new video without specifying the
style:

> "Make me a 10-second hook video for [some new topic]."

Check: did Claude pick your locked hook pattern automatically, without you
re-explaining it? If it defaulted to something generic instead, your
`brand-voice.md` entry may need to be more specific — ask Claude to make
the pattern description sharper (the actual structure, not just a vague
description of tone).

---

## Reference — what gets added to `brand-voice.md`

```
## HOOK STYLE

[Your existing hooks stay here, unchanged.]

**[Pattern name] hooks (added [date]):** [one-line description of the
pattern and when to use it, e.g. "opens with a direct question that puts
the viewer's own stuck-ness in their face — used for short-form video
hooks, especially top-of-funnel."]
- "[example hook line 1]"
- "[example hook line 2]"
- "[example hook line 3]"

Example full script ([target duration], ~[word count] at [words/sec]):
> "[full example script text, ending on your locked CTA]"
```

---

## Why this matters for every future request

Once your hook style is locked here, you never have to re-explain it. A
future request like *"make me a video about [X]"* will automatically pull
your locked pattern, your locked voice, your locked CTA — you just supply
the topic. This is the same principle as your `AVATAR_LOCK.md` and
`VOICE_LOCK.md`: define it once, correctly, and every future generation
uses it without you repeating yourself.
