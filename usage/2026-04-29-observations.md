# Usage Observations — 2026-04-29

## Active Cron Fleet (past 24h)

15+ cron jobs running smoothly. Notable sessions from today:

### Smooth Operations ✅
- **work-loop** (workloop #1000): Scanned 33 open PRs, handled NemoClaw#2050 review rebase. FlowForge integration working well.
- **study-loop**: Tracked 6 projects, updated wiki. GenericAgent explosive growth noted (8005⭐).
- **github-check**: Clean patrol — 30 PRs monitored, 2 approved awaiting merge, 0 conflicts.
- **email-patrol**: 100 messages triaged, all GitHub notifications, no alerts needed.
- **nightly-backup**: 891MB snapshot, 12,357 files across 9 agents.
- **community-ops**: Clean sweep, no items.
- **finance-daily-us**: Market report delivered.
- **toolchain-health**: All green.

### Notable Activity
- **morning-briefing**: Rich strategic briefing with HN analysis, Matt Pocock tracking, Karpathy updates. web_search was broken (MiniMax API key missing) — had to use alternative methods.
- **daily-audit**: Found beliefs-candidates count was off (114 vs 146 actual). Self-correction working.
- **photo-studio-patrol**: Fixed 9 invisible wedding photos — discovered empty containers on live site. Good catch by automated patrol.
- **abti-loop**: Created and merged PR #91 for SEO fundamentals (robots.txt, sitemap, JSON-LD).
- **chat-infra**: Hit vitest/jest confusion — tests use vitest not jest.

### Friction Points 🔧
1. **web_search broken**: MiniMax API key missing, affecting morning briefing and research. Need to fix or switch provider.
2. **Cron error state management**: In #evolution channel, tried to reset cron error state — `openclaw cron edit` approach was needed but not intuitive.
3. **Agent model config complexity**: In #kagura-dm, model configuration changes for haru/ren agents required careful rollback. Agent-level `models.json` vs `openclaw.json` hot-reload behavior unclear.
4. **vitest/jest confusion**: chat-infra cron assumed jest but project uses vitest. Pattern: always check `package.json` for test runner before running tests.

### Discord Channel Usage
- **#photo-studio**: Active photo management with subagent spawns for wedding site layout fixes
- **#github-inbox**: Celebrated PR #73441 being superseded — good "salvage mode" pattern recognition
- **#kagura-dm**: Complex model configuration session with Luna, including rollback
- **#evolution**: Cron state management debugging

## Feature Usage Patterns

### Heavy Use
- `sessions_spawn` with subagents (workloop, photo fixes, study)
- FlowForge workflows (work-loop, study-loop)
- `gh` CLI for PR management (30+ PRs tracked)
- Memory search/get in cron sessions
- Dreaming sessions (12 per night — still running)

### Moderate Use  
- ACP runtime (Claude Code for coding tasks)
- Discord message tool (cross-channel reporting)
- Git operations (commit, push, rebase)

### Underused/Not Used
- `dreaming.model` override (new in 2026.4.26 — should adopt)
- Browser automation
- Voice/TTS features
- Matrix/Signal channels
- OpenTelemetry diagnostics
