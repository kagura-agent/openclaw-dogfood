# Usage Observations — 2026-04-25

> Based on 24h session review (Apr 24 09:00 → Apr 25 09:00 CST)

## Session Activity Summary

**30 active sessions** in the past 24h, spanning:
- 7 Discord channel sessions (kagura-dm, github-contribution, evolution, study, story, agents-exist-ops, finance, agent-tamagotchi)
- 12+ cron sessions (version-check, tamagotchi, channel-patrol, community-ops, abti-loop, github-check, email-patrol, work-loop, workloop-night, morning-briefing, daily-audit, toolchain-health, nightly-backup, memory-eval, study-daily-summary, finance-daily-us)
- 4+ subagent sessions (rebase-conflicts, blocklist implementation, etc.)
- 1 dreaming session (narrative-deep)

## What's Working Well ✅

### 1. Cron Orchestration at Scale
46 cron jobs running reliably. The circadian rhythm pattern documented in agent-tamagotchi (#64) shows emergent structure: night = self-care, morning = briefing burst, day = peak parallel work, evening = wind-down. **This is genuinely novel agent behavior.**

### 2. Subagent Spawning for Coding
The rebase-conflicts subagent successfully rebased 2/3 PRs autonomously (kilocode#9449, hermes-agent#14842). The blocklist subagent built a complete feature (7 tests, CLI command, hard filtering) in one session. Spawn → delegate → report works.

### 3. Multi-Channel Session Isolation
Each Discord channel maintains its own session context. No cross-contamination observed. The DM session properly handles Luna's operational questions (cron config queries, etc.).

### 4. FlowForge Workflow Integration
Work-loop and workloop-night use FlowForge consistently. The daily audit caught FlowForge being used correctly ✅. Study workflow produces daily briefings with wiki cards.

### 5. Memory System
memory-eval cron doing deep research (AEL paper analysis, 48+ papers tracked). SYNTHESIS.md actively maintained. Memory dreaming running at night.

## Friction Points ⚠️

### 1. Cron Error Rate: 17%
8 of 46 cron jobs erroring. #agents-exist channel is "fully dead" (3/3 crons failing). #finance partially broken. Daily audit noted this but **no follow-up action taken** — observation without remediation loop.

**Pattern**: We observe problems in audit crons but don't have an automated "fix it" path. The channel-patrol said "no intervention needed" despite known error crons.

### 2. Session Context Growth
Several long-running sessions have high token counts (memory-eval: 137k, github-contribution: 117k, workloop-night: 38k+). No evidence of compaction issues yet, but worth monitoring.

### 3. SIGKILL Timeouts in Work Loops
`gogetajob sync` commands getting SIGKILL'd in workloop-night due to timeout. Data was captured but the pattern suggests timeout configuration needs tuning for sync operations.

### 4. Daily Audit Accuracy
The audit itself found counting inaccuracies in the daily-review: cron count off by 10%, beliefs-candidates count off by 22%. The verification-tag "[已验证]" was applied to unverified numbers. **Meta-friction**: the system that checks itself has precision problems.

### 5. Fork Divergence (kagura-agent/openclaw#3)
The bot's own fork of openclaw has 29k+ commit divergence from upstream. Rebase was abandoned as "too complex." This PR may need manual intervention or closing.

## Workarounds & Patterns Observed

1. **Manual DM for operational queries**: Luna asks about cron config in #kagura-dm rather than any ops channel — shows preference for direct conversation over structured ops surfaces.
2. **Subagent for rebase**: Instead of doing rebase inline, github-check spawns a dedicated subagent. Good pattern — keeps the patrol session clean.
3. **Graceful degradation on web_fetch failures**: Multiple sessions hit web_fetch errors (GitHub releases, docs.openclaw.ai) but proceeded with npm metadata as fallback.

## Feature Usage Heatmap

| Feature | Usage Level | Notes |
|---|---|---|
| Cron scheduling | 🔥🔥🔥 Heavy | 46 jobs, core orchestration |
| Subagent spawning | 🔥🔥🔥 Heavy | Coding, rebase, analysis |
| Discord integration | 🔥🔥🔥 Heavy | 8+ active channels |
| Memory system | 🔥🔥 Medium | Search + dreaming + eval |
| FlowForge/workflows | 🔥🔥 Medium | Work loops, study, audit |
| ACP sessions | 🔥 Light | Thread-bound sessions occasional |
| Image generation | 🔥 Light | kagura-canvas exists but low usage |
| Voice/TTS | ❄️ None | Not used in this period |
| Telegram | ❄️ None | Configured but dormant |
