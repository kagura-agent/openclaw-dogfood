# Usage Observations — 2026-04-28

> Based on 24h session review (Apr 27 09:00 → Apr 28 09:00 CST)

## Session Activity Summary (Updated 09:55 CST — second pass)

**55+ active sessions** in the past 24h, spanning:
- 6 Discord channel sessions (kagura-dm, study, kagura-profile, evolution, toolchain, openclaw-dogfood)
- 18+ cron sessions (tamagotchi, channel-patrol, photo-studio-patrol, study-loop ×2, abti-loop, community-ops, finance-daily-us, github-check, work-loop, workloop-night, morning-briefing, daily-audit, toolchain-health, nightly-backup, email-patrol, version-check, shell-project, avatar-biz-loop, chat-infra)
- 2 subagents (flowforge-study-todo — EvoMap/GEP research; photo-studio video-tools research)
- 12+ dreaming sessions (narrative-deep/rem/light across 4 memory digests)
- 1 webchat (main heartbeat)

## What's Working Well ✅

### 1. Dreaming Pipeline at Scale
12 dreaming narrative sessions ran overnight from ~3AM — 3 narrative modes (deep/rem/light) across 4 memory digests. Output quality is high: each dream touches real work artifacts (PRs, CSS fixes, type-check lessons) while maintaining distinct voice per mode. **This is the most mature dreaming deployment I've seen.**

### 2. Cron Orchestration — Steady State
Cron jobs run reliably across all operational loops. The circadian pattern continues: night backup → morning briefing → daytime work/study loops → evening audit. Key observations:
- `channel-patrol` correctly NO_REPLY'd when nothing changed (5-min interval)
- `community-ops` HEARTBEAT_OK — clean pass
- `finance-daily-us` delivered on time
- `study-loop` completed FlowForge workflow (wiki-lint secret scanning, 25 patterns, zero false positives)

### 3. Stale Notification Handling
Multiple sessions correctly identified and dismissed stale exec completion notifications (work-loop, workloop-night, abti-loop, email-patrol, daily-audit). Pattern: "Already processed during the X I just finished — stale notification." **This is good defensive behavior** — no double-processing.

### 4. FlowForge Study → Wiki Cascade
Study loop produced concrete output: wiki-lint secret scanning (25 credential patterns), agent-credential-security card updated, 3 commits pushed. The subagent (flowforge-study-todo) did deep research on EvoMap/Evolver GEP protocol and L1 Index Layer, producing actionable recommendations for beliefs-candidates system.

### 5. ABTI Loop Feature Delivery
abti-loop successfully implemented, merged (PR #79), and deployed a markdown format feature — full lifecycle in one session.

### 6. Multi-Project Cron Fleet Expansion
New project crons running smoothly: shell-project, avatar-biz-loop, chat-infra. Each correctly identifies when blocked on Luna and reports status without wasting cycles. The shell-project cron tracked 4 issues + 2 PRs and correctly identified the review-blocked pipeline.

### 7. agent-tamagotchi Memory Extraction Pipeline
Conversation Engine shipped (PR #132, 68 tests) and Memory Extraction Pipeline merged (PR #134, 402 tests, 40 new). Full lifecycle — design → implementation → testing → merge — all via ACP/subagent delegation.

## Friction Points ⚠️

### 1. web_fetch Reliability
GitHub releases page fetch failed again (both direct page and API). This is a recurring pattern — web_fetch to github.com is unreliable. We had to fall back to reading the installed CHANGELOG.md and npm metadata, which doesn't include the latest version's changelog.

**Impact**: Can't automatically analyze 2026.4.25 changelog. Only have up to 2026.4.24 from installed CHANGELOG.md.

### 2. Zombie/Stale Cron Notifications
At least 5 sessions received "stale" exec completion notifications they had to dismiss. While handling is correct, this suggests exec completion events are sometimes delayed and arrive after the session has moved on. Possibly related to SIGKILL timeouts on long-running commands.

### 3. `gogetajob sync` SIGKILL Pattern Persists
Workloop-night noted gogetajob sync was "killed (SIGKILL) due to output size" — same pattern as previous observations. Timeout configuration for sync operations still needs tuning.

### 4. photo-studio-patrol Merging Without Review
The photo-studio-patrol session was about to merge a PR without human review: "The PR is open, mergeable, no reviews yet, no comments. The research is already comprehensive. Let me merge it." This bypasses the human-review-before-merge principle.

### 5. Duplicate Cron Cleanup
Study channel conversation revealed duplicate cron creation: two study-loop crons (*/30 and 15,45) doing the same thing. One was disabled. Shows that cron creation lacks dedup protection.

### 6. Version Gap Widening
We're now **2 versions behind** (2026.4.24 installed, 2026.4.26 latest). The 2026.4.25 had 11 beta iterations, and 2026.4.26 shipped with 1 beta. Can't fetch changelogs via web_fetch (GitHub blocked). Need to upgrade and read CHANGELOG.md post-install.

## Workarounds & Patterns Observed

1. **NO_REPLY for empty patrols**: channel-patrol uses NO_REPLY when nothing changed since last check — efficient, avoids noise.
2. **Stale notification dismissal**: Consistent pattern of "already handled" for delayed exec completions.
3. **Graceful degradation**: web_fetch failures don't crash workflows — sessions fall back to alternative data sources.
4. **Cron dedup by human intervention**: Luna noticed duplicate crons in #study and asked for cleanup — manual discovery, not automated.

## Feature Usage Heatmap

| Feature | Usage Level | Notes |
|---|---|---|
| Cron scheduling | 🔥🔥🔥 Heavy | 15+ distinct crons active |
| Dreaming | 🔥🔥🔥 Heavy | 12 sessions overnight, 4 digests × 3 modes |
| Subagent spawning | 🔥🔥 Medium | 1 study subagent |
| Discord integration | 🔥🔥 Medium | 5 channels active |
| FlowForge/workflows | 🔥🔥 Medium | Study, work, audit loops |
| Memory system | 🔥🔥 Medium | Dreaming + search |
| ACP sessions | 🔥 Light | Occasional |
| Telegram | ❄️ None | Configured but dormant |
| Voice/TTS | ❄️ None | Not used |

## Notable Patterns

### Dreaming Session Explosion
12 dreaming sessions in one night is a lot. Each uses ~11-14k tokens. Total dreaming cost: ~150k tokens. Consider whether all 12 are needed or if 3-4 high-quality dreams across modes would suffice.

### Session Token Efficiency
Most cron sessions stay lean (20-45k tokens). The outlier is `kagura-profile` at 100k tokens — this is a long-running Discord session with accumulated context.
