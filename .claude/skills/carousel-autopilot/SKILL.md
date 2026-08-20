---
name: carousel-autopilot
description: |
  Daily carousel pipeline for AI Scale Engine: researches the niche
  (AI avatars, daily content without filming, faceless content for
  coaches), writes TWO carousels in the locked Old Way / New Way format,
  validates them against the brand files as a fail-closed gate, renders
  each via Blotato using the locked template and brand colors, SCHEDULES
  them to Instagram @aiscale_engine and TikTok @aiscaleengine (12:00 and
  18:00 Europe/Paris), then notifies Mohamed with the copy, times, and
  post IDs so he has a real window to cancel. Use when: "run carousel
  autopilot", "make today's carousels", "run the carousel pipeline", or
  on a schedule. NOT for: publishing immediately, avatar/talking-head
  video (use `avatar-video` or `daily-content-pipeline`), or any carousel
  format other than the locked Old Way / New Way.
argument-hint: "[--topic override] [--skip-research] [--dry-run] [--no-schedule]"
allowed-tools: Read, Write, Bash, WebSearch, WebFetch, SendUserFile, PushNotification, mcp__Blotato__blotato_list_accounts, mcp__Blotato__blotato_list_visual_templates, mcp__Blotato__blotato_create_visual, mcp__Blotato__blotato_get_visual_status, mcp__Blotato__blotato_create_post, mcp__Blotato__blotato_get_post_status, mcp__Blotato__blotato_list_schedules, mcp__Blotato__blotato_delete_schedule, mcp__Blotato__blotato_list_conversations, mcp__Blotato__blotato_list_messages, mcp__Blotato__blotato_send_message, mcp__Blotato__blotato_get_credits
---

# Carousel autopilot (AI Scale Engine)

Research → write 2 carousels → validate → render → schedule → notify.

Unlike `daily-content-pipeline` (which hard-stops for approval before any
publish), this pipeline **schedules for later and gives Mohamed a cancel
window instead of a pre-approval gate.** That is a deliberate, narrower
carve-out and it is only safe because of two invariants:

1. Posts are **always scheduled**, never published immediately.
2. A **working notification channel must exist**, or the schedule is
   cancelled.

Static carousel copy carries far less brand risk than video under
Mohamed's face and cloned voice — which is why the video pipeline keeps
its stricter gate and this one doesn't. Do not "harmonise" the two.

## Read these first, every run

Read the real files — they change independently of this skill. Paths are
relative to the repo root:

1. `CAROUSEL_LOCK.md` — **authoritative** for format, validation, render
   mapping, scheduling, notify/cancel protocol
2. `brand-voice.md` — §15b is the format's origin; wins on copy
3. `offer.md` — the locked CTA and pricing
4. `BRAND_KIT.md` — palette and policy text
5. `CLAUDE.md` — standing rules

Do not work from this file's summary of them.

## Step 0 — Preflight

- `blotato_list_accounts` → resolve the Instagram and TikTok account IDs
  and read each platform's `requiredFields`. Never hardcode IDs.
- `blotato_get_credits` → confirm credits remain. Each carousel render
  costs credits; with none, stop and notify rather than half-running.
- If the Blotato MCP tools are unavailable, **do not improvise another
  publishing route.** Send a `PushNotification` saying the run could not
  proceed, and stop.

## Step 1 — Research the niche

One `WebSearch` pass. Topics: making money with an AI avatar, creating
daily content without filming or editing, faceless/AI-clone content for
coaches, AI content automation.

Put recency in the query (current month/year). Look for what the hook
actually said, what pain it named, what the comments pushed back on.
Prefer specifics — a number, a claim, an objection — over themes.

Record the source and one sentence on why it worked, for the notification.

**If research returns nothing usable:** say so plainly and fall back to a
strong evergreen angle from `offer.md` / `conversion-engine.md`. Flag the
fallback. **Never invent a trend, statistic, or competitor quote.**

`--skip-research` skips this. `--topic "..."` replaces it.

## Step 2 — Write TWO carousels

Follow `CAROUSEL_LOCK.md` §1 exactly. Two distinct angles — not one angle
phrased two ways. Carousel 1 goes to the 12:00 slot, carousel 2 to 18:00.

For each: a hook line (the `mainTitle`, under 50 chars), one or more Old
Way / New Way pairs, and the locked CTA closing slide.

Voice per `brand-voice.md`: direct, high-energy, operator. Short
sentences. No mentor tone, no hype padding.

## Step 3 — VALIDATE (fail-closed gate)

Run all 10 checks in `CAROUSEL_LOCK.md` §2 against **both** carousels,
plus the template's own length constraints from §3.

State each check's result explicitly — do not assert "validated" in bulk.

**If any check fails:** fix the copy and re-validate. If it still fails,
**schedule NOTHING, render nothing**, send a `PushNotification` explaining
which check failed and why, and stop. Never relax a check to make copy
pass.

## Step 4 — Render

For each carousel, call `blotato_create_visual` with the locked
`templateId` and **explicit `inputs`** per `CAROUSEL_LOCK.md` §3.

**Never pass a bare `prompt` with empty `inputs`** — that lets the model
invent copy and colors, defeating both locks.

Poll `blotato_get_visual_status`, **≥15s between polls**. On `done`,
collect `imageUrls`. On `creation-from-template-failed` or
`insufficient-credits`, stop and notify — do not silently retry with a
different template or drop to the fallback without saying so.

## Step 5 — Schedule (never publish immediately)

Convert the Paris slot times to UTC against the offset in effect that day
(§4). Always pass `scheduledTime`.

Instagram: `mediaUrls` = the carousel `imageUrls`.

TikTok: same media, plus every field in the account's `requiredFields`,
including **`isAiGenerated: true`**.

Capture every `postSubmissionId`.

If a post fails to schedule, report it and continue with the others —
then make sure the notification says exactly which ones are live and which
are not.

## Step 6 — Notify (mandatory, both paths)

Per `CAROUSEL_LOCK.md` §5:

- **`PushNotification` always fires**, success or failure. It is the
  primary channel and the only one that reliably reaches an unattended
  run. Wrap the summary in `<routine_summary>` tags.
- **DM is a best-effort duplicate.** Resolve the recipient at runtime via
  `blotato_list_conversations` → `blotato_list_messages`; use an incoming
  message's `senderId`. Never hardcode. Check the newest inbound message
  first — if it is **older than 24h the window is closed** and the send
  will fail; skip it and say so rather than burning the run on a failure.

Both messages carry: both carousels' copy, the scheduled times **in
Europe/Paris**, every `postSubmissionId`, and how to cancel.

**If no channel confirms delivery, cancel the scheduled posts**
(`blotato_list_schedules` → `blotato_delete_schedule`) and report that
nothing is queued. An uncancellable scheduled post is worse than no post.

## Flags

- `--dry-run` — research, write, validate. **No render, no schedule.**
  Use this to test copy changes cheaply (spends no Blotato credits).
- `--no-schedule` — render and show the images, but don't schedule. Use
  when validating the visual template mapping.
- `--topic "..."` / `--skip-research` — see Step 1.

## Failure handling

Report failures plainly with the actual error. Do not silently retry a
different approach, and do not present a partial result as complete.

Real cases:
- **Blotato MCP unavailable** — stop, `PushNotification`, no improvised
  publishing route.
- **Insufficient credits** — stop before scheduling; report the balance.
- **Template render failed** — report it; use the §3 fallback template
  only if you also visually verify contrast and say that you did.
- **DM window closed (>24h)** — expected on unattended runs. Not a
  failure of the run; `PushNotification` covers it.
- **Scheduled but nobody notified** — cancel the schedules. This is the
  one case where undoing your own work is correct.
