# Usage Observations — 2026-05-05

## Version
- Current: `2026.5.3-1` (same as latest on npm, no update needed)
- Last upgrade: 2026-05-04 (from 2026.4.26)

## Observations (past 24h)

### ✅ Working Well

1. **Discord reconnection recovery** — After Discord outage period (caused 13 cron jobs to error with "Unsupported channel: discord"), all crons recovered naturally on next tick once connection restored. No manual intervention needed.

2. **Cron scheduler stability** — 54 active jobs running smoothly. The `heartbeat_respond` pattern is in use by community-ops and abti-loop (both emit HEARTBEAT_OK cleanly).

3. **Subagent spawn + completion push** — work-loop and github-check both spawn subagents (flowforge-workloop-night-followup, flowforge-github-patrol-fetch) that complete and report back without polling. Push-based model working as designed.

4. **Large session context management** — kagura-dm session at 154k tokens, still responsive. No mid-turn compaction issues observed.

5. **Multi-cron concurrent execution** — 09:00 slot has both openclaw-version-check and channel-patrol firing simultaneously without conflict.

### ⚠️ Friction Points

1. **channel-patrol consecutive errors** — 12 consecutive errors noted in DM session review. All from Discord outage window, but the error count doesn't auto-reset after recovery. May want to track error streaks more visibly.

2. **chat-infra cron** — Also 12 consecutive errors. Same root cause (Discord unavailability). Consider: should crons that depend on Discord delivery have a "skip if channel unavailable" mode?

3. **Gmail API token expiry** — email-patrol reports `agent` Gmail token expired/revoked (recurring issue). Not an OpenClaw problem per se, but a toolchain pain point that affects the agent's capability.

### 📊 Feature Adoption Status (post-upgrade)

| Feature | Status | Notes |
|---------|--------|-------|
| `heartbeat_respond` tool | ⏳ Not yet adopted | Still using plain HEARTBEAT_OK text |
| `threadBindings.spawnSessions` | ⏳ Not verified | Need to check if `openclaw doctor --fix` migrated |
| Discord access groups | ⏳ Not adopted | Still using per-channel allowlists |
| Heartbeat active-hours-aware | ✅ Passive benefit | Asia/Shanghai timezone should now work correctly |
| Cron isolated announce | ✅ Passive benefit | Isolated crons no longer pollute main session |
| Discord typing indicators | ✅ Passive benefit | Should be active on long tool runs |

### 💡 Next Steps
- Run `openclaw doctor --fix` to verify threadBindings migration
- Consider adopting `heartbeat_respond` tool for cleaner heartbeat output
- Monitor if the 12-error-streak pattern clears after next successful runs
