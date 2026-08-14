---
name: daily-content-pipeline
description: |
  End-to-end daily content pipeline for AI Scale Engine: finds what is
  working right now in Mohamed's niche (making money with an AI avatar,
  creating daily content without filming or editing, faceless/AI-clone
  content for coaches), rewrites the winning angle into a 15-second script
  in Mohamed's locked voice and hook style, generates the avatar video with
  his locked identity and voice, appends the locked closing outro, then
  STOPS and presents the finished video for approval before anything is
  published to Instagram or TikTok. Use when: "run the daily content
  pipeline", "make today's video", "find a viral angle and build the video",
  or when triggered on a schedule. NOT for: publishing without approval,
  one-off videos from a script Mohamed already wrote (use `avatar-video`
  directly for that), or Remotion motion-graphics videos (no avatar).
argument-hint: "[--topic override] [--skip-research] [--dry-run]"
allowed-tools: Read, Write, Bash, WebSearch, WebFetch, AskUserQuestion, SendUserFile, Skill, mcp__fbc7be1f-a61a-40a8-b9df-6066b4219553__generate_video, mcp__fbc7be1f-a61a-40a8-b9df-6066b4219553__explainer_video, mcp__fbc7be1f-a61a-40a8-b9df-6066b4219553__job_display, mcp__fbc7be1f-a61a-40a8-b9df-6066b4219553__show_generations, mcp__0831e30c-1d8e-4129-8cb5-ca64071f8895__blotato_create_post, mcp__0831e30c-1d8e-4129-8cb5-ca64071f8895__blotato_list_accounts, mcp__0831e30c-1d8e-4129-8cb5-ca64071f8895__blotato_get_post_status
---

# Daily content pipeline (AI Scale Engine)

Runs the full loop from "what's working in the niche today" to "finished
video waiting for Mohamed's yes". **Never publishes on its own.**

## Hard rule — approval gate

This pipeline **always stops** after the video is rendered and before any
post is created. Publishing is a separate, explicit step that only happens
after Mohamed says yes in chat. Do not call any `blotato_create_post`,
`tiktok_publish`, or equivalent before that approval exists in the current
conversation.

This overrides the project's general "don't force unnecessary approval
steps" default in `CLAUDE.md` — that rule is about not blocking on
approval-for-approval's-sake, not about auto-posting AI-generated video to
live brand accounts. Video going out under Mohamed's face and voice is
exactly the "brand-risky or irreversible" case that rule carves out.

## Read these first, every run

Do not work from memory or from this file's summary — read the real files,
they change independently. Paths are relative to the repo root (this skill
ships inside the repo so cloud agents can discover it):

1. `CLAUDE.md` — standing rules
2. `HOOK.md` — locked hook pattern
3. `brand-voice.md` — how the brand talks
4. `offer.md` — the locked CTA
5. `BRAND_KIT.md` — colors, policy text
6. `SEEDANCE.md` — video bible (read by `avatar-video`, but read it here
   too so the script is written to fit the pacing math)

When running locally from `ThefounderStudio/`, prefix each with
`ai-scale-engine-mo-test-3/`.

## Step 1 — Find the angle

Goal: identify one angle that is demonstrably working right now in the
niche, not a generic evergreen take.

Search for recent, high-engagement content on: making money with an AI
avatar, creating daily content without filming or editing, AI content
automation for coaches, faceless content systems, AI clone creators.

Use `WebSearch` with recency in the query (the current month/year). Look
for: what the hook actually said, what pain it named, what the comments
pushed back on. Prefer specifics (a number, a claim, an objection) over
themes.

Record for the summary later: the source, the angle, and one sentence on
why it worked.

**If research returns nothing usable** — say so plainly and fall back to a
strong evergreen angle from `offer.md`/`conversion-engine.md`. Do not
invent a fake trend, a fake statistic, or a fake competitor quote. A
flagged fallback is fine; a fabricated trend is not.

`--skip-research` skips this step. `--topic "..."` replaces it.

## Step 2 — Write 3 hook options

`CLAUDE.md` has a standing rule: before generating any video, propose 3
hook scripts and wait for Mohamed to pick. **That rule applies here.**

Write 3 different 15-second scripts on the chosen angle:

- ~45 words each (15s at 3.0 words/sec — pacing math per `SEEDANCE.md`)
- Open with a **question hook** in the locked `HOOK.md` pattern — a new
  question each time, never a reuse of the three locked examples
- Structure: question → one-line reframe → CTA
- Voice per `brand-voice.md`: direct, high-energy, operator. Short
  sentences. No mentor tone, no hype padding.
- Never call the offer a "course" — it is a system
- End on the locked Stage 4 CTA from `offer.md`
- Commas sparingly, only where a real spoken pause belongs

Present all 3. Wait for a pick. Do not generate video before Mohamed
chooses or approves one.

## Step 3 — Generate the video

Invoke the existing `avatar-video` skill with the approved script. Do not
rebuild its prompt logic here — it already enforces `SEEDANCE.md`,
`AVATAR_LOCK.md` (Element `9cf95684-c068-4807-bfa8-08aaa3add7c5`), and
`VOICE_LOCK.md` (voice media_id `af1371ee-64cf-4e40-b7d8-13296b214095`).

If `avatar-video` is unavailable, stop and say so — do not fall back to
generating Mohamed's likeness some other way. Identity is locked.

## Step 4 — Append the locked outro

Per the standing rule in `CLAUDE.md`, every video ends with the locked
closing outro: `assets/video/closing-outro-9x16.mp4` (1080x1920, ~5.5s)
for vertical content — same path convention as the read-list above.

Per the CapCut reference rule, the outro carries the starfield-particle
overlay and subtle letterbox treatment. If the outro asset already has
this baked in, use it as-is — do not re-add the effect twice.

## Step 5 — STOP. Present for approval.

Send the finished video to Mohamed with `SendUserFile`, plus a short
summary:

- The angle found, and the source it came from
- Which of the 3 hooks was used
- The final script as spoken
- Runtime
- Proposed caption + hashtags for Instagram and TikTok, adapted per
  platform (per the `CLAUDE.md` per-platform rule) — written but **not
  posted**

Then ask, explicitly, whether to publish. End the turn there.

Do not pre-create drafts, scheduled posts, or "ready to send" items on
Blotato as a shortcut — a scheduled post is a published decision.

## Step 6 — Publish (only after an explicit yes)

Only runs when Mohamed has said yes in this conversation.

Target accounts: Instagram `@aiscale_engine`, TikTok `@aiscaleengine`.
Confirm with `blotato_list_accounts` that the intended accounts are the
ones connected before posting — do not assume account IDs from memory.

Post via Blotato with the approved caption per platform. Report back the
post status and links.

If Mohamed approves only one platform, publish only that one.

## Failure handling

Report failures plainly, with the actual error. Do not silently retry a
different approach, and do not present a partial result as a finished one.

Common real cases:
- **Higgsfield MCP disconnected** — `generate_video` unavailable. Stop and
  say so; the identity lock lives there and has no REST equivalent with
  Element + voice support.
- **Rate limit** — report the limit and the retry window from the error.
- **Video generated but outro append failed** — present the raw video,
  flag that the outro is missing, do not publish it as complete.

## Scheduling note

When run unattended (cron / `/loop`), the pipeline still stops at Step 5.
An unattended run produces a video waiting for review, not a published
post. If nobody approves, nothing goes out — that is the intended
behavior, not a bug.
