# Setup — Daily Content Pipeline (AI Scale Engine)

**Last updated:** 2026-08-14  
**Status:** Ready for terminal-based work  
**Repo:** [github.com/herichi/ai-scale-engine](https://github.com/herichi/ai-scale-engine)

---

## What's done

✅ **Skill** `daily-content-pipeline` shipped in `.claude/skills/daily-content-pipeline/SKILL.md` — orchestrates viral research → 3 hook scripts → avatar video generation → validation gate → social publishing (Blotato).

✅ **Skills in repo** — both `avatar-video` and `daily-content-pipeline` are now versionned inside `.claude/skills/` so any Claude agent (cloud, local, terminal) can discover them after cloning. Local copy at `ThefounderStudio/.claude/skills/` is now a symlink to the repo copy — single source of truth.

✅ **Locked assets tracked** — `assets/video/closing-outro-9x16.mp4` (3.1 MB), `assets/audio/closing-bg-music.mp3` (8.8 MB), and `assets/voice/voice-reference.mp3` are in git. Remotion workspaces and large intermediates are gitignored.

✅ **Architecture documented** — `CLAUDE.md` updated with the permanent rule: daily pipeline runs in Claude with approval gate before publishing.

✅ **Pushed to GitHub** — all commits on `main`, remote configured, ready for cloud agents.

---

## What's blocked (needs web action)

Three things remain, **to be done before the cloud routine can run end-to-end:**

### 1. Connect GitHub Integration (claude.ai)
**Where:** Settings → Connectors → GitHub Integration → **Connect**  
**Why:** The cloud routine needs to clone the repo and push branches. Right now the API returns `authentication_error: Connect your GitHub account before saving a routine...`  
**Action:** Click Connect, authorize `herichi/ai-scale-engine` access.

### 2. Get Blotato's MCP URL
**Where:** Settings → Connectors → Blotato (find the details like you showed for Higgsfield)  
**Current state:** Higgsfield MCP URL is `https://mcp.higgsfield.ai/mcp`. Blotato's is unknown.  
**Why:** The cloud routine needs to wire up both connectors explicitly. Without it, `blotato_create_post` will be unavailable in cloud runs.  
**Action:** Send a screenshot of Blotato's connector panel, showing the MCP URL (if visible).

### 3. Decide: "Generate Video" permission level
**Where:** Settings → Connectors → Higgsfield → Tool permissions → Generate Video  
**Current state:** Marked with a raised-hand icon (ask each time).  
**Trade-off:**
- **Keep raised-hand:** Cloud routine will block at video generation, waiting for approval nobody will give at 6am. Useful only if you want to run the pipeline manually and select a hook first, then approve video gen.
- **Change to ✓ (allowed):** Cloud routine generates video fully unattended. Video is ready for review when you wake up, no approval step needed. You review the video AFTER it's generated, decide to publish or not.

**Current design:** The pipeline is built to stop *after* video generation and *before* publishing — that approval gate is hard-coded. So the permission setting controls whether you approve the video generation step, not whether the video gets posted.

---

## How to run locally (now)

From `~/ThefounderStudio/`:

```bash
claude -p "run the daily content pipeline"
```

Claude will clone/read the project context from `ai-scale-engine-mo-test-3/CLAUDE.md`, discover the skill, and execute it. The pipeline will:
1. Search for viral angles in your niche
2. Write 3 hook scripts
3. Ask you to pick one
4. Generate the avatar video with your locked Element + voice
5. Append the locked outro
6. Send you the finished video + proposed captions
7. Ask: publish to Instagram/TikTok?

If you say yes, it publishes via Blotato. If no, the video stays local and you can reshoot/edit.

---

## How to run on cloud schedule (when blocked items are fixed)

Once you complete the three actions above, I will:

1. Create a remote routine with this config:
   - **Cron:** `0 6 * * 1-5` (Monday–Friday, 6am UTC)
   - **Clone:** `herichi/ai-scale-engine` latest `main`
   - **Run:** the skill `daily-content-pipeline`
   - **Prompt:** find the angle, write 3 scripts, save to `content-queue/YYYY-MM-DD.md`, commit + push branch `content/YYYY-MM-DD`
   - **Stop:** do NOT generate video or publish (those are local steps, you pick the hook and approve generation)

2. Schedule outcome: every morning at 6am UTC, a new branch appears on GitHub with three scripts ready. You pull, pick a hook, run `claude -p "run the daily content pipeline --topic ..."` locally, and the video is done.

---

## File map

**Core rules & locks:**
- `CLAUDE.md` — standing rules, updated with daily-pipeline rule
- `HOOK.md` — locked question-hook pattern (3 examples)
- `brand-voice.md` — how the brand talks (direct, high-energy, operator)
- `offer.md` — locked CTA: "Join the AI Scale Engine — link in bio. $29/month."
- `BRAND_KIT.md` — colors (#0a0a0a bg, #ff7a1a accent), typography, templates
- `SEEDANCE.md` — video pacing bible (3.0 words/sec, gesture bank, lighting rules)

**Locked assets:**
- `assets/video/closing-outro-9x16.mp4` (1080×1920, 5.5s, has starfield + letterbox per CapCut rule)
- `assets/audio/closing-bg-music.mp3` (dark pagan/Norse, Pixabay, louder mix -10 to -20 dB RMS)
- `assets/voice/voice-reference.mp3` (for voice cloning in Higgsfield)

**Skills:**
- `.claude/skills/avatar-video/SKILL.md` — generates 15s video with locked identity + voice
- `.claude/skills/daily-content-pipeline/SKILL.md` — orchestrates the full loop

**Workflow template (for reference, used in earlier n8n experiments):**
- `assets/n8n/3_hackernews_to_ai_clone_videos_HIGGSFIELD.json` — n8n workflow (not used for production anymore)

**Student resources:**
- `student-resources/` — templates for new creators to build their own brand kits and avatar video pipelines (not used by Mohamed's pipeline, kept for teaching)

---

## Decisions made (and why)

### Q: Why did we abandon n8n for production?
**A:** n8n's REST APIs can't call Higgsfield's Element-lock or voice-reference features — those are MCP-only. The canvas is also not automatable from Claude Code (Vue Flow synthetic events don't work). For Mohamed's production use, Claude orchestration with MCP tools is cleaner, faster, and keeps identity/voice locked.

n8n remains useful as a teaching artifact for students (REST-based workflows are more portable) and as a handoff when other systems need to trigger the pipeline.

### Q: Why does the pipeline stop before publishing?
**A:** Mohamed's avatar and voice are locked to public accounts (@aiscale_engine on Instagram/TikTok). A video going out under his face is an irreversible brand decision. The "stop for approval" rule is not about blocking on approval-for-approval's-sake (that's what `CLAUDE.md` discourages) — it's about brand-risky, irreversible actions. Confirmed with Mohamed: "je veux bien qu'il s'arrête pour valider la vidéo avant l'envoi" (for testing, I want it to stop before sending to validate the video).

### Q: Why isn't the cloud routine generating video end-to-end?
**A:** Higgsfield MCP is a remote server (`https://mcp.higgsfield.ai/mcp`), so cloud agents *can* reach it. But I have no programmatic way to retrieve the `connector_uuid` for custom MCP connectors — they're absent from the registry. Rather than create a routine that fails silently every morning, I built what marches: research + scripts, saved to the repo. You approve the angle + hook locally, then the video generates on your machine with full MCP access. The work that doesn't need you (research, writing) is automated; the work that needs your identity (video + approval) is local.

If you find the Blotato MCP URL and give me explicit permission to wire both connectors into the routine, I can extend it to generate video in cloud too — but that's optional given the current setup works fine.

---

## Next steps (in order)

1. **Web actions** (you): Connect GitHub Integration, find Blotato MCP URL, decide on Generate Video permission.
2. **Terminal work** (you): Test locally — `claude -p "run the daily content pipeline"`.
3. **Cloud setup** (me): Once actions 1 is done, wire up the remote routine and test with a manual trigger.
4. **Schedule** (me): Enable cron for 6am UTC, Mon–Fri.
5. **Monitor** (you): Each morning, a branch with 3 scripts. Pull, pick one, generate locally.

---

## Quick reference

**Local run:**
```bash
cd ~/ThefounderStudio/ai-scale-engine-mo-test-3
claude -p "run the daily content pipeline"
```

**Override topic (skip research):**
```bash
claude -p "run the daily content pipeline --topic 'how to scale a one-person business with AI content'"
```

**Repo URL:** `https://github.com/herichi/ai-scale-engine`  
**Branch:** `main` (production)  
**Content queue:** `content/YYYY-MM-DD` branches (one per day after cloud run)

---

## Connector UUIDs (needed for cloud wiring)

Once you provide the screenshots:

- **Higgsfield MCP:** `https://mcp.higgsfield.ai/mcp` ✓
- **Blotato MCP:** `[TBD — need screenshot]`

(These will be fed into the remote routine's `mcp_connections` field once retrieved.)
