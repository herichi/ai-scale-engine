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

### Primary template — full brand-color control

**`templateId`: `/base/v2/tutorial-carousel/2491f97b-1b47-4efa-8b96-8c651fa7b3d5/v1`**
("Tutorial Carousel with Minimalist Flat Style")

Chosen because it exposes `backgroundColor`, `textColor`, **and**
`borderColor` as explicit inputs — all three locked brand colors are
controllable. Templates that only expose a background color cannot honour
the palette and must not be used as primary.

**Always pass explicit `inputs`. Never call `blotato_create_visual` with a
bare `prompt` and empty `inputs`** — that lets the model invent copy and
colors, which defeats both the format lock and the palette lock.

```json
{
  "templateId": "/base/v2/tutorial-carousel/2491f97b-1b47-4efa-8b96-8c651fa7b3d5/v1",
  "inputs": {
    "font": "font-oswald",
    "mainTitle": "<hook line, under 50 chars>",
    "authorName": "Mohamed",
    "ctaButtonText": "Swipe",
    "contentItems": [
      "THE OLD WAY\n<line>\n\nTHE NEW WAY\n<line>"
    ],
    "backgroundColor": "#0a0a0a",
    "textColor": "#f5f1ea",
    "borderColor": "#ff7a1a",
    "ctaTitle": "Join the AI Scale Engine — link in bio.",
    "ctaActions": ["Follow", "Share"],
    "profileName": "Mohamed",
    "profileTitle": "AI Scale Engine",
    "profileDescription": "We don't sell a course. We sell a system.",
    "profileCta": "Link in bio",
    "aspectRatio": "4:5"
  }
}
```

**Constraints enforced by the template** (validate before calling, a
violation is a hard API error, not a warning):
- `mainTitle`: 5–50 chars
- each `contentItems` entry: 10–300 chars
- `ctaTitle`: 5–150 chars
- `profileDescription`: 10–250 chars
- `aspectRatio`: `4:5` for feed carousels (`1:1` / `9:16` also valid)

Each `contentItems` entry carries **one complete Old Way / New Way pair**
so the contrast is fully visible on a single slide rather than split
across a swipe.

### Fallback template

**`/base/v2/tutorial-carousel/e095104b-e6c5-4a81-a89d-b0df3d7c5baf/v1`**
("Monocolor Background") — use only if the primary fails. It exposes
`introBackgroundColor`, `contentBackgroundColor`, `accentColor` but **no
`textColor`**, so text contrast is not guaranteed. Map bg → `#0a0a0a`,
accent → `#ff7a1a`, and **visually verify the rendered slides** before
scheduling.

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

### Message contents (both channels)

- Both carousels' full copy, as it will appear
- Scheduled times, stated in **Europe/Paris**, not UTC
- Every `postSubmissionId`
- How to cancel: reply to the DM, or `blotato_delete_schedule`

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
