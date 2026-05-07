# Usage Observations - 2026-05-07

## 24h Cron Activity Summary

Active crons in the last 24h (all running smoothly):

| Cron Job | Status | Notes |
|----------|--------|-------|
| channel-patrol | ✅ Running | Normal |
| github-check | ✅ 38K tokens | Processed 8 notifications, 30 open PRs tracked |
| community-ops | ✅ Heartbeat | Normal |
| abti-loop | ✅ 43K tokens | Added GLM-4 9B to registry (now 49 agents) |
| finance-daily-us | ✅ 21K tokens | Market report delivered cleanly |
| study-loop | ✅ 106K tokens | Heavy session — FlowForge study with MemOS deep read |
| work-loop | ✅ 68K tokens | Submitted PR #78679 to openclaw |
| email-patrol | ✅ 22K tokens | 20 unread, all GitHub noise |
| workloop-night | ✅ 25K tokens | Spawned PR sync subagent successfully |
| morning-briefing | ✅ 76K tokens | Delivered to Discord |
| toolchain-health | ✅ 24K tokens | All green |
| daily-audit | ✅ 31K tokens | No behavioral violations found |
| memes-dogfood | ✅ Running | New strategy audit format deployed |
| openclaw-version-check | 🔄 Running | This session |

## What's Working Well

1. **Subagent spawning from cron** — workloop-night spawned a PR sync subagent that produced a comprehensive 21-PR report. Subagent completion and result collection worked flawlessly.
2. **FlowForge orchestration** — study-loop ran patrol → followup → deep-read pipeline without issues. 106K tokens is heavy but within budget.
3. **Memory search** — `corpus=all` fix in v2026.5.4 already deployed; memory recall quality seems improved (no complaints from study/audit crons).
4. **Discord delivery** — All Discord-targeted crons delivered successfully. No ghost replies observed today.

## Friction Points

1. **Version lag** — We're on 2026.5.3-1 while 2026.5.6 is out. Three versions behind. The correction version plugin compatibility fix in 2026.5.4 is particularly relevant since we're running a correction build.
2. **Wiki lint CI** — Still failing on main (reported by email-patrol and github-check). Not an OpenClaw issue but shows up as noise in our patrol crons.
3. **Hermes CI** — All 5 hermes-agent PRs have failing CI. Systemic infrastructure issue on their end, not our code.

## Token Usage Estimate (24h)

Total across all crons: ~495K tokens (Claude Opus 4.6)
Heaviest: study-loop (106K), morning-briefing (76K), memes-dogfood session (74K)
