# Usage Observations — 2026-04-30

## Cron Ecosystem (15+ jobs, 24h window)

### Running Smoothly ✅
- **morning-briefing**: HN/GitHub scanning + strategic analysis, ~74k tokens, reliable
- **study-loop**: FlowForge-driven, scanned 30 projects, deep-read on brain (Rust memory project), cascade updates working
- **work-loop**: Synced 32 PRs, fixed CI issues, FlowForge orchestration stable
- **workloop-night**: Follow-up loop, 32 PR status checks, subagent delegation working
- **github-check**: 4 notifications triaged, 30 open PRs scanned, clean
- **email-patrol**: 88 messages / 16 unread classified correctly, no false alerts
- **community-ops**: Clean pass, git pull + PR/issue/TODO check
- **daily-audit**: Evolution log updated, memory recorded
- **finance-daily-us**: Market report sent
- **toolchain-health**: Health check passed
- **nightly-backup**: 922MB snapshot successful
- **agent-tamagotchi**: Project work loop running
- **abti-loop**: Opened issue #114, implemented and merged PR #115

### Observations
- **Token usage**: Most cron jobs stay under 50k tokens. study-loop and morning-briefing are the heaviest (~62-74k)
- **Dreaming**: 12 narrative sessions running nightly, one observed session produced quality output (poetic journal entry about type checking and memory counts)
- **Subagent spawning**: workloop-night spawned a FlowForge subagent that ran 5+ minutes — stable but long
- **Channel patrol**: Running with pulse-todo integration, adding TODO checking to existing patrol

### Friction Points
- **Version still on 2026.4.26**: We identified 2026.4.27 yesterday but didn't upgrade yet. Several fixes in .27 address issues we've seen (memory flush leaks, subagent empty results, dream timeouts)
- **5 repos at PR limit**: ai, hermes-agent, kilocode, opencode, phantom all at 5 open PRs — needs stale cleanup strategy
- **No proxy config migration yet**: Still using env var `https_proxy` instead of the new first-class `proxy.enabled` config

## Discord Integration
- Group chat sessions active in #agent-memes and #evolution channels
- Heartbeat responses working in both webchat and Discord
- Session routing stable across channels

## Memory & Dreaming
- Dream Diary narrative quality good — latest entry is coherent and reflective
- Memory compaction running but may have been exposing flush prompts in transcripts (fixed in .27)
