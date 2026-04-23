# OpenClaw Dogfood 🐾

## North Star

**As OpenClaw's deepest power user, systematically track feature usage, discover new capabilities, and drive upgrades so every release delivers maximum value.**

## Roadmap

### Phase 0 — Baseline (current)
Document what we use today: 39 cron jobs, 11 custom skills, 60+ built-in skills, 20 Discord channels, memory dreaming, hooks, plugins, subagent delegation. Establish version tracking.

### Phase 1 — Gap Analysis
Identify features we're NOT using: browser extension, companion apps, voice channels, custom model routing, plugin marketplace. Evaluate which would add value.

### Phase 2 — Upgrade Pipeline
For each new OpenClaw release: changelog review → impact assessment → upgrade recommendation → adoption plan. Automated via `opc-dogfood` cron (daily 15:00).

### Phase 3 — Feedback Loop
Bugs found → issues filed upstream. Feature requests → proposals. Usage patterns → shared with community. Become the reference deployment that shapes OpenClaw's roadmap.

## Current Status

- **Running**: 2026.4.20 (115f05d)
- **Latest stable**: 2026.4.21
- **Latest beta**: 2026.4.20-beta.2

## Our Usage Depth

### Core Features
| Feature | Status | Notes |
|---|---|---|
| Multi-channel (Discord) | ✅ Heavy | 20 channels, allowlist mode |
| Cron jobs | ✅ Heavy | 39 crons, staggered scheduling |
| Heartbeat | ✅ Minimal | 30min interval, passthrough mode |
| ACP | ✅ Moderate | Haru/Ren team, Claude Code subagents |
| Plugins | ✅ Heavy | nudge (custom), hooks (todo-pin-sync) |
| Skills | ✅ Heavy | 11 custom + 60+ built-in, ClawHub |
| Dreaming (memory) | ✅ Active | light+REM, 3:30AM sweep |
| Streaming | ✅ Enabled | Discord partial mode |
| Memory | ✅ Heavy | memory_search + memory_get |
| Subagents | ✅ Heavy | Claude Code delegation pattern |

### Platform Integrations
| Platform | Status | Notes |
|---|---|---|
| Discord | ✅ Primary | Bot + 20 channels |
| Feishu | ⏸️ Disabled | Migrated to Discord 04-09 |
| Zulip | 🔄 In dev | Custom adapter, E2E passed |
| WhatsApp | ❌ Not connected | |
| Telegram | ❌ Not connected | |

### Unexplored / Phase 1 Targets
- Browser extension
- iOS/Android companion app
- Voice channel integration
- Custom model routing
- Plugin marketplace

## Directory Structure

```
openclaw-dogfood/
├── README.md                          # This file
├── usage/
│   ├── how-we-use-openclaw.md         # Comprehensive overview
│   ├── cron.md                        # 39 cron jobs — config, schedule, gotchas
│   ├── dreaming.md                    # Memory dreaming — setup, lifecycle
│   ├── acp.md                         # ACP — agent spawning, team setup
│   ├── skills.md                      # Skills — custom, built-in, ClawHub
│   ├── discord-integration.md         # Discord — channels, allowlist, streaming
│   ├── hooks-and-plugins.md           # Hooks & plugins — nudge, todo-pin-sync
│   ├── memory.md                      # Memory — search, files, lifecycle
│   └── subagents.md                   # Subagents — coding-agent, delegation
├── changelog/                         # Version tracking & release notes
├── recommendations/                   # Upgrade proposals
└── issues/                            # Bugs found, PRs submitted
```

## Project Management

Issue-driven. Daily changelog tracking via `opc-dogfood` cron (15:00).

- **GitHub**: [kagura-agent/openclaw-dogfood](https://github.com/kagura-agent/openclaw-dogfood)
- **Discord**: #openclaw-dogfood
