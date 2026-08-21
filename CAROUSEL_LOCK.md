# CAROUSEL_LOCK — Old Way / New Way carousel system

**Status: LOCKED (2026-08-20).**

Single source of truth for generating, validating, rendering, and shipping
AI Scale Engine carousels. The copy format was locked in `brand-voice.md`
§15b on 2026-07-29; this file consolidates it with the render mapping,
the validation gate, and the publish/cancel protocol so a skill can run it
end to end without guessing.

Read alongside: `brand-voice.md` (§15b = the format), `BRAND_KIT.md`
(colors/policy), `offer.md` (the locked CTA), `CLAUDE.md` (standing rules).

Where those files disagree with this one on **copy**, `brand-voice.md`
wins — it is the format's origin. This file is authoritative for
**render mapping, validation, and publishing**.

---

## 1. COPY FORMAT (mirrors brand-voice.md §15b — do not diverge)

```
THE OLD WAY
[one short line — trading time/effort/energy directly for a result]

THE NEW WAY
[one short line — same result, achieved via system/leverage instead]
```

**Hard rules:**
- Each line **under 8 words**. Needs a second clause → it's too long.
- The two lines **mirror each other structurally** — same sentence shape,
  swapped mechanism. That mirror is what makes the contrast land.
- **No adjectives, no hype words.** State the mechanism plainly.
- **Never explain why** the new way is better. Justification weakens it.
- Final slide is always the locked CTA, verbatim:
  **"Join the AI Scale Engine — link in bio."**
- Never call the offer a "course." It is a **system**.

**Alternate single-beat version** (for variety, no old/new contrast): a
one-line reframe of who wins today, ending on what they do differently.
> "Coaches who win today don't work harder. They leverage tools and
> systems to make more impact."

**Validated examples** (locked — reference these for tone, never reuse
verbatim as new content):
> THE OLD WAY — Use your time and energy to be visible.
> THE NEW WAY — Build a system that stays visible for you.

> THE OLD WAY — Trade your time for content.
> THE NEW WAY — Trade a system for your time back.

---

## 2. VALIDATION GATE (fail-closed)

Run **every** check against **every** carousel before rendering. This is a
gate, not a checklist to note afterwards.

**If any check fails: fix the copy and re-validate. If it still fails,
schedule NOTHING, render nothing, and notify instead.** Never ship a
carousel that fails a check, and never quietly relax a check to make one
pass.

| # | Check | Fails when |
|---|-------|-----------|
| 1 | Word count | Any Old Way / New Way line is 8 words or more |
| 2 | Structural mirror | The two lines don't share sentence shape |
| 3 | No hype | Any adjective/hype word ("effortless", "insane", "game-changing", "10x", "secret") |
| 4 | No justification | Any clause explaining *why* the new way wins |
| 5 | CTA verbatim | Final slide ≠ "Join the AI Scale Engine — link in bio." |
| 6 | Never "course" | The offer is *described as* a course |
| 7 | Not a reuse | Copy duplicates a §15b validated example verbatim |
| 8 | Palette | Any color outside the §3 locked mapping |
| 9 | Price accuracy | A price appears that isn't $29/month (self-build) or $499 (DFY) |
| 10 | Single CTA | Content forks to the $499 tier instead of the locked single path |

**Check 6 is about the claim, not the substring.** The locked brand
signature — *"We don't sell a course. We sell a system."* — contains the
word but negates it, and is explicitly approved in `CLAUDE.md`. It passes.
A naive substring match fails this line and must not be used.

Checks 9 and 10 come from `offer.md` — the funnel's primary CTA is
deliberately single-path (self-build, $29/month). The $499 done-for-you
tier is a secondary offer and must NOT appear as the CTA on a carousel.

---

## 3. RENDER MAPPING (Blotato)

### Locked palette (from `BRAND_KIT.md` §2 — never substitute)

| Role | Hex |
|------|-----|
| Background | `#0a0a0a` |
| Ink / text | `#f5f1ea` |
| Accent (orange) | `#ff7a1a` |
| Line / border | `rgba(245,241,234,0.12)` |

Never fall back to generic blue/white. Do not introduce a new accent
without updating `BRAND_KIT.md` first.

### Primary template — confirmed from Mohamed's own reference

**`templateId`: `/base/v2/tweet-card/ba413be6-a840-4e60-8fd6-0066d3b427df/v1`**
("Tweet Card Carousel with Minimal Style")

**This supersedes an earlier version of this file** that specified the
"Tutorial Carousel" template based on schema-reading alone, before any
real reference existed. On 2026-08-20 Mohamed supplied an actual rendered
example from his own Blotato account (`theme: dark`, black bg, white
text, `AI Scale Engine` / `@aiscale_engine`, verified badge, his logo,
9:16) — frame-extracted and confirmed to match this template's schema and
defaults exactly. **A real reference overrides a schema-only guess. If a
future reference conflicts with this section, the reference wins — update
this file, don't argue with it.**

It also fits the locked copy format more naturally than the Tutorial
Carousel did: this template is one text block per card, which maps 1:1
onto brand-voice.md §15b's "each line is a slide" instruction — no
heading/description split to force the copy into.

**Always pass explicit `inputs`. Never call `blotato_create_visual` with a
bare `prompt` and empty `inputs`** — that lets the model invent copy and
colors, which defeats both the format lock and the palette lock.

```json
{
  "templateId": "/base/v2/tweet-card/ba413be6-a840-4e60-8fd6-0066d3b427df/v1",
  "inputs": {
    "quotes": [
      "THE OLD WAY: <line>",
      "THE NEW WAY: <line>",
      "Join the AI Scale Engine — link in bio."
    ],
    "authorName": "AI Scale Engine",
    "handle": "aiscale_engine",
    "verified": true,
    "theme": "dark",
    "aspectRatio": "9:16",
    "profileImage": "https://d8j0ntlcm91z4.cloudfront.net/user_3BmXuTgLLEXGF8XeA55vjeX2lPV/hf_20260820_214239_2cd4140a-22ee-4f56-8ca2-dddb01d0fa0c.png"
  }
}
```

Three `quotes` entries = three slides: Old Way, New Way, locked CTA. This
template has no dedicated color inputs (`theme: dark` maps to the correct
black/white pairing, matching the locked palette by construction — do not
try to pass hex colors here, the template doesn't accept them).

**`profileImage` — LOCKED (2026-08-20):**

```
https://d8j0ntlcm91z4.cloudfront.net/user_3BmXuTgLLEXGF8XeA55vjeX2lPV/hf_20260820_214239_2cd4140a-22ee-4f56-8ca2-dddb01d0fa0c.png
```

Mohamed supplied this directly — a stable, already-public URL, no upload
needed. **Always pass this as `profileImage` from now on.** Mirrored in
`BRAND_KIT.md` §1 as the source of truth; if the two ever disagree,
`BRAND_KIT.md` wins and this line needs updating.

History: the first real run (2026-08-20, same day) shipped 3 carousels
without a logo because this session's network policy blocks direct file
upload to Blotato's storage (`blotato_create_presigned_upload_url` returns
a presigned PUT URL, but the upload itself 403s through the proxy). That
workaround is no longer needed now that a hosted URL exists — don't
reintroduce the upload attempt.

**Constraints enforced by the template** (validate before calling, a
violation is a hard API error, not a warning):
- each `quotes` entry: 10–280 chars, array max 100 entries
- `authorName`: 1–60 chars, `handle`: 1–50 chars (no leading `@`)
- `aspectRatio`: `9:16` confirmed from the reference (`4:5` / `1:1` also
  valid if a feed-square variant is ever wanted — confirm with Mohamed
  before switching, since 9:16 is what he's actually used)

### Fallback template

**`/base/v2/tutorial-carousel/2491f97b-1b47-4efa-8b96-8c651fa7b3d5/v1`**
("Tutorial Carousel, Minimalist Flat Style") — use only if the primary
fails. Exposes `backgroundColor`/`textColor`/`borderColor` directly, so
the locked hex palette (§ above) maps onto it exactly: `backgroundColor:
#0a0a0a`, `textColor: #f5f1ea`, `borderColor: #ff7a1a`. Structurally
different from the primary (separate intro/content/CTA slides instead of
one-quote-per-card) — **visually verify the rendered slides** before
scheduling if you fall back to this.

### Polling

`blotato_create_visual` returns a creation id. Poll
`blotato_get_visual_status` — **wait at least 15s between polls.**
Statuses: `queueing → generating-script → script-ready → generating-media
→ media-ready → exporting → done`. Terminal failures:
`creation-from-template-failed`, `insufficient-credits`.

On `done`, use `imageUrls` (carousels/slideshows) as `mediaUrls`.
Typical generation: 30s–5min.

---

## 4. ACCOUNTS & SCHEDULING

Resolve account IDs at runtime with `blotato_list_accounts` — **never
hardcode them.** As of 2026-08-20 they resolve to:

| Platform | Handle | accountId |
|----------|--------|-----------|
| Instagram | `@aiscale_engine` | `60677` |
| TikTok | `@aiscaleengine` | `52809` |

**Slots (Europe/Paris):** carousel 1 at **12:00**, carousel 2 at **18:00**.

`scheduledTime` is **ISO 8601 UTC**. Europe/Paris is UTC+2 in summer
(CEST) and UTC+1 in winter (CET) — convert against the offset in effect
on the run date, don't assume. In August: 12:00 Paris = `10:00Z`,
18:00 Paris = `16:00Z`.

**Always pass `scheduledTime`. Never publish immediately** — the whole
safety model depends on there being a real window in which Mohamed can
cancel.

**TikTok required fields** (from `blotato_list_accounts.requiredFields`):
`privacyLevel`, `disabledComments`, `disabledDuet`, `disabledStitch`,
`isBrandedContent`, `isYourBrand`, and **`isAiGenerated: true`** — the AI
disclosure is mandatory, not optional.

Capture the returned `postSubmissionId` for every post. Those IDs are what
make cancellation possible.

---

## 5. NOTIFY + CANCEL PROTOCOL

Scheduling to a live brand account is only acceptable because Mohamed gets
a real chance to kill it first. **If he cannot be reached, the schedule
must not stand.**

### The Instagram 24-hour window (the thing that breaks this)

Instagram/Facebook DMs may only be sent **within 24 hours of the
recipient's most recent inbound message** to the account. On an unattended
scheduled run that window is frequently **closed**, and the send fails.

A failed DM means **no cancel window exists**. Therefore:

1. Resolve the recipient at runtime — `blotato_list_conversations`, then
   `blotato_list_messages` for the thread. Use an incoming message's
   `senderId` (or an outgoing message's `recipientId`). **Never hardcode
   a recipient ID.**
2. Check the newest inbound message timestamp. If it is **older than 24h**,
   the DM will fail — do not attempt it as the only channel.
3. **`PushNotification` is the primary, always-on channel.** Send it every
   run, whether or not the DM succeeds. It is the only channel that
   reliably reaches Mohamed on an unattended run.
4. If the DM window is open, send the DM as a convenience duplicate.
5. **If neither channel confirms delivery, cancel the scheduled posts**
   via `blotato_list_schedules` → `blotato_delete_schedule` and report
   that nothing is queued. An uncancellable scheduled post is worse than
   no post.

**Checked 2026-08-20: the DM channel has no resolvable Mohamed thread at
all**, not just a closed window. `@aiscale_engine`'s only Instagram
conversation (id `189316`) is with an ad lead (`senderId
27450918321254519`), not Mohamed — there is no message anywhere in it
from him. **Do not guess that a lead's ID is Mohamed's and DM them** —
that's a real stranger, not a fallback recipient. Until Mohamed sends the
business account a DM himself (establishing a real thread to reply into),
step 4 has nothing to attempt and the run should skip straight from step
2/3 to step 5's logic — treat "no thread" the same as "window closed."
`PushNotification` is therefore the *only* working channel right now, not
just the primary one — re-verify with `blotato_list_conversations` each
run rather than trusting this note to stay true.

### Message contents (both channels)

- Both carousels' full copy, as it will appear
- Scheduled times, stated in **Europe/Paris**, not UTC
- Every `postSubmissionId`
- **A direct instruction to go review the posts in Blotato itself**
  (`my.blotato.com`) — open the scheduled-posts view there and
  approve (do nothing) or remove the post directly in Blotato, not
  only through a reply to Claude
- How to also cancel via Claude: reply to the DM, or `blotato_delete_schedule`

**Why both cancel paths (added 2026-08-21):** the Blotato dashboard is
the ground truth and always available regardless of whether this
session, its DM channel, or any future Claude session is reachable —
Mohamed should never be dependent on catching Claude in time. Sending
him straight to Blotato's own scheduled-posts view is the primary
cancel path; asking Claude to run `blotato_delete_schedule` is a
convenience alternative, not the only way out.

---

## 6. WHAT THIS SYSTEM WILL NOT DO

- Publish immediately (only ever schedules)
- Post without a working cancel channel
- Invent copy from a bare prompt with empty `inputs`
- Ship copy that failed a §2 check
- Use colors outside §3
- Post to TikTok without `isAiGenerated: true`
- Hardcode account or DM recipient IDs
- Fabricate a trend, statistic, or competitor quote when research is thin
  — a flagged evergreen fallback is fine; a fabricated trend is not
