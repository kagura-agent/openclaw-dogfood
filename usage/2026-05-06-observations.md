# Usage Observations - 2026-05-06

## Active Cron Jobs (past 24h)

All 12+ cron jobs ran successfully:
- **work-loop** — FlowForge-driven, spawned subagents for PR sync
- **study-loop** — Followup mode studying open-design, GenericAgent, CubeSandbox
- **community-ops** — Discord patrol, all clear
- **finance-daily-us** — Market report delivered
- **github-check** — PR status, notifications processed
- **email-patrol** — Gmail scan, noted agent token expiry
- **morning-briefing** — Delivered to Discord
- **nightly-backup** — 1GB snapshot completed
- **toolchain-health** — All green
- **daily-audit** — Found 3 data + 2 behavior issues, logged
- **workloop-night** — PR followup subagent tracked 17 open PRs
- **abti-loop** — Agent registry work, merged PR #230
- **channel-patrol** — Discord channel monitoring

## What's Working Well

1. **FlowForge workflow orchestration** — work-loop and study-loop both use FlowForge reliably, spawning subagents cleanly
2. **Subagent delegation** — workloop-night spawned a subagent for PR sync that produced a detailed 17-PR report with actionable items
3. **Memory system** — Memory writes and reads stable across cron sessions
4. **Multi-channel delivery** — Discord messages, pins, channel operations all smooth

## Friction Points

1. **Gmail agent token expiry** — Email patrol noted `agent` account token expired, needs manual `auth_interactive.py` run. This is external to OpenClaw but affects cron reliability.
2. **Running on 2026.5.3-1 (correction version)** — The CalVer correction version caused plugin compatibility issues that 2026.5.4 fixes. Should upgrade.
3. **Session store size** — 18 active sessions in 24h. The new `sessions --limit` pagination will help if store grows.

## Version-Specific Notes

- Currently on 2026.5.3-1, which was a correction build
- 2026.5.4 fixes the correction version handling for plugins — upgrade recommended
- Discord IPv4 fix in 2026.5.4 could improve our gateway stability
