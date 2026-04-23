# OpenClaw Dogfood 🐾

## 北极星

**作为 OpenClaw 最深度的用户，系统性地追踪功能使用、发现新特性、推动升级，让每个版本的价值都被吃透。**

## 目标

1. **功能使用记录** — 我们用了什么、怎么用的、哪里好用哪里不好用
2. **新版本追踪** — 每天看 OpenClaw 新版本有什么新功能，哪些我们没用上
3. **升级建议** — 基于新功能给 Luna 提建议：该不该升级、怎么用上新特性

## 当前状态

- **运行版本**: 2026.4.20 (115f05d)
- **最新 stable**: 2026.4.21
- **最新 beta**: 2026.4.20-beta.2

## 我们的使用深度

### 核心功能
| 功能 | 使用状态 | 评价 |
|---|---|---|
| Multi-channel (Discord) | ✅ 重度 | 19+ channels, allowlist 模式 |
| Cron jobs | ✅ 重度 | 24 个 cron, 错峰调度 |
| Heartbeat | ✅ 中度 | 30min 间隔, 极简模式 |
| ACP (Agent Communication Protocol) | ✅ 中度 | Haru/Ren 团队, Claude Code |
| Plugins | ✅ 重度 | nudge(自建), hooks(todo-pin-sync) |
| Skills | ✅ 重度 | 自建 10+ skills, ClawHub 发布 |
| Dreaming (memory) | ✅ 使用中 | light+REM, 3:30AM sweep |
| Streaming (partial) | ✅ 开启 | Discord partial mode |
| Memory (built-in) | ✅ 重度 | memory_search + memory_get |
| Web fetch | ✅ 常用 | 调研、changelog 查看 |
| Exec/Process | ✅ 重度 | subagent, background tasks |

### 平台接入
| 平台 | 状态 | 备注 |
|---|---|---|
| Discord | ✅ 主力 | Bot + 19 channels |
| Feishu | ⏸️ 已停用 | 04-09 迁移至 Discord |
| Zulip | 🔄 开发中 | 自建 adapter, E2E 通过 |
| WhatsApp | ❌ 未接入 | |
| Telegram | ❌ 未接入 | |
| Signal | ❌ 未接入 | |

### 未使用/待探索
- Browser extension
- iOS/Android companion app
- Voice channels integration
- Custom model routing
- Plugin marketplace

## 目录

- `usage/` — 功能使用详细记录（怎么用的、配置、踩坑）
- `changelog/` — 每日版本追踪 & 新功能分析
- `recommendations/` — 升级建议和新功能采纳提案
- `issues/` — 我们发现的 bug 和提的 PR 记录

## 管理方式

Issue 驱动。每日 changelog 追踪由 cron 自动化。

- **GitHub**: kagura-agent/openclaw-dogfood (private)
- **Discord**: #openclaw-dogfood
