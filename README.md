# OpenClaw Dogfood 🐾

## North Star

**As OpenClaw's deepest power user, systematically track feature usage, discover new capabilities, and drive upgrades so every release delivers maximum value.**

## Goals

1. **Feature usage log** — What we use, how we use it, what works well, what doesn't
2. **Version tracking** — Daily check on new OpenClaw releases and features we're not using yet
3. **Upgrade recommendations** — Based on new features, advise Luna: should we upgrade? How to adopt new capabilities?

## Current Status

- **Running**: 2026.4.20 (115f05d)
- **Latest stable**: 2026.4.21
- **Latest beta**: 2026.4.20-beta.2

## Our Usage Depth

### Core Features
| Feature | Status | Notes |
|---|---|---|
| Multi-channel (Discord) | ✅ Heavy | 19+ channels, allowlist mode |
| Cron jobs | ✅ Heavy | 24 crons, staggered scheduling |
| Heartbeat | ✅ Moderate | 30min interval, minimal mode |
| ACP (Agent Communication Protocol) | ✅ Moderate | Haru/Ren team, Claude Code |
| Plugins | ✅ Heavy | nudge (custom), hooks (todo-pin-sync) |
| Skills | ✅ Heavy | 10+ custom skills, ClawHub publishing |
| Dreaming (memory) | ✅ Active | light+REM, 3:30AM sweep |
| Streaming (partial) | ✅ Enabled | Discord partial mode |
| Memory (built-in) | ✅ Heavy | memory_search + memory_get |
| Web fetch | ✅ Regular | Research, changelog review |
| Exec/Process | ✅ Heavy | Subagents, background tasks |

### Platform Integrations
| Platform | Status | Notes |
|---|---|---|
| Discord | ✅ Primary | Bot + 19 channels |
| Feishu | ⏸️ Disabled | Migrated to Discord 04-09 |
| Zulip | 🔄 In dev | Custom adapter, E2E passed |
| WhatsApp | ❌ Not connected | |
| Telegram | ❌ Not connected | |
| Signal | ❌ Not connected | |

### Unexplored / To Investigate
- Browser extension
- iOS/Android companion app
- Voice channel integration
- Custom model routing
- Plugin marketplace

## Directory Structure

- `usage/` — Detailed feature usage notes (config, setup, gotchas)
- `changelog/` — Daily version tracking & new feature analysis
- `recommendations/` — Upgrade proposals and feature adoption plans
- `issues/` — Bugs we've found and PRs we've submitted

## Project Management

Issue-driven. Daily changelog tracking automated via cron.

- **GitHub**: kagura-agent/openclaw-dogfood (private)
- **Discord**: #openclaw-dogfood
