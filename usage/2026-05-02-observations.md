# Usage Observations — 2026-05-02

## Cron Jobs Running Smoothly
All 10+ cron jobs executed successfully in the last 24h:
- `morning-briefing`, `finance-daily-us`, `email-patrol`, `github-check`, `work-loop`, `workloop-night`, `study-loop`, `community-ops`, `abti-loop`, `channel-patrol`, `openclaw-version-check`
- No stuck sessions observed (the cron/gateway stuck-session fix in v2026.4.29 would help if this happened)
- `channel-patrol` returned NO_REPLY as expected (quiet = healthy)

## Features Working Well
1. **Multi-cron orchestration** — 10+ cron jobs running at various intervals without conflicts. Heartbeat/cron deferral (new in v2026.4.29) would add safety here.
2. **Discord group chat** — wedding-games channel interaction was natural, multi-turn, no delivery issues
3. **FlowForge skill routing** — study-loop successfully routed through FlowForge, produced structured notes
4. **Subagent spawning** — abti-loop created PR #164 via coding agent, merged and deployed
5. **GitHub CLI integration** — github-check scanned 30 PRs, identified stale ones correctly

## Friction Points
1. **Version check cron ran but didn't commit** — previous run created changelog/recommendations but didn't push. Git operations in cron context sometimes incomplete (timeout? flow interruption?)
2. **Token usage is high** — several cron sessions use 50-100k tokens per run (study-loop 64k, github-check 54k, abti-loop 62k). Worth monitoring if we're paying per-token.
3. **No memory recall issues observed** — partial-recall-on-timeout (new in v2026.4.29) hasn't been needed, but good safety net.

## Platform Observations
- Running on v2026.4.26, 3 days behind latest
- All sessions using claude-opus-4.6 with 200k context
- Discord CJK splitting fix (v2026.4.29) relevant — we post CJK content in Discord regularly
- The `process.poll` 30s clamp (v2026.4.29) would prevent potential hangs in our coding-agent flows
