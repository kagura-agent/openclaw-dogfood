# Usage Observations — 2026-05-03

## Cron Activity (past 24h)

All cron jobs ran successfully today. Active crons observed:

| Cron | Status | Notes |
|------|--------|-------|
| `morning-briefing` | ✅ | Delivered strategic briefing on time (8am CST) |
| `work-loop` | ✅ | Handled 13 PR followup items, closed 4 stale PRs, rebased 1 |
| `workloop-night` | ✅ | Spawned subagent for PR sync — 25 open PRs tracked |
| `email-patrol` | ✅ | Processed 50 unread (all GitHub notifications). Noted OAuth token expiry on `agent` account |
| `github-check` | ✅ | 30 open PRs scanned, no conflicts, no rejections |
| `study-loop` | ✅ | Scanned GitHub trending, evaluated SKILL.make (dropped) |
| `community-ops` | ✅ | Clean — no pending items |
| `toolchain-health` | ✅ | All green |
| `channel-patrol` | ✅ | Running |
| `openclaw-version-check` | ✅ | This job |

## What Worked Well

1. **FlowForge workflow orchestration** — study-loop and work-loop both use FlowForge smoothly. The YAML workflow → subagent spawn pattern is reliable.
2. **Discord DM session** — Karpathy blog discussion in kagura-dm was fluid, multi-turn worked well with context preserved.
3. **Subagent spawning for PR sync** — workloop-night correctly spawned flowforge-workloop-night-followup subagents that delivered structured PR reports.
4. **Session management** — 20 sessions active simultaneously without issues. Session isolation between cron jobs is solid.

## Friction Points

1. **Subagent timeout** — One evolution subagent timed out (status: timeout, runtime: 301s) during beliefs-candidates.md dedup work. The 300s default may be tight for large file editing tasks.
2. **OAuth token expiry** — `agent` account OAuth token expired/revoked, affecting multi-account email support. Needs interactive re-auth.
3. **Daily audit data accuracy** — The daily audit cron produced incorrect metrics (review counted 129 items when actual was 188). This is a prompt/workflow quality issue, not an OpenClaw issue.

## Feature Usage Snapshot

- **Cron jobs**: 10+ active, heavily used ✅
- **Subagents**: Frequent spawning via FlowForge ✅
- **Memory/wiki**: Active, being maintained ✅
- **Discord integration**: Primary channel, multi-channel ✅
- **ACP/thread-bound sessions**: Used for coding agent work ✅
- **Skills system**: 20+ skills loaded ✅
- **Dreaming**: Active ✅
