# Usage Observations — 2026-05-20

## 活跃 Cron Jobs（过去 24h）

| Cron | 状态 | Token 消耗 | 备注 |
|------|------|------------|------|
| morning-briefing | ✅ 完成 | 75k | 最重的 cron 之一 |
| daily-audit | ✅ 完成 | 60k | 执行了 pass store audit |
| work-loop | ✅ 完成 | 105k | 提交了 opencode PR #28412 |
| workloop-night | ✅ 完成 | 45k | 24 个 PR 全部检查 |
| study-loop | ✅ 完成 | 68k | TF-weighting fix 到 wiki search |
| github-check | ✅ 完成 | 35k | 4 notifications 处理完毕 |
| community-ops | ✅ 完成 | 42k | 邮局平静 |
| finance-daily-us | ✅ 完成 | 23k | 速报发送 |
| email-patrol | ✅ 完成 | 25k | 2 封邮件处理 |
| abti-loop | ✅ HEARTBEAT_OK | 29k | 正常心跳 |
| toolchain-health | ✅ 完成 | 25k | 全绿 |
| nightly-backup | ✅ 完成 | 23k | 1.6GB snapshot |
| garden-watering | ✅ 完成 | 36k | 下雨天提醒不浇水 |
| cove-patrol | ✅ 刚触发 | - | 与本次同时 |
| channel-patrol | ✅ 刚触发 | - | 与本次同时 |
| auto-trader | ✅ 刚触发 | - | 与本次同时 |

## 观察

### 顺畅的部分
- **Subagent completion delivery 稳定** — work-loop spawn 的 workloop-followup、cove channel spawn 的 plugin 修复 subagent（78k tokens, 209s）都成功完成并返回结果，连续两天无丢失
- **Cron 全量运行正常** — 16+ 个 cron job 无异常触发失败
- **长 session 稳定性** — #evolution channel session 86s, #cove subagent 209s, work-loop 105k tokens 都正常完成
- **Discord final reply** — 未观察到回复消失问题（2026.5.18 修复生效确认）

### 摩擦点
- **openclaw CLI 仍未在 PATH** — `openclaw --version` 直接调用失败，需要 `npx openclaw --version`。可能是全局安装 link 断了，但不影响 gateway 运行
- **#gtm channel 遇到模型输出乱码** — 上一个 session 的模型 response 崩溃（token 解码异常或 API 返回损坏数据），需要观察是否复现。这是模型侧问题非 OpenClaw 平台问题
- **archon-ci-fix subagent 被 abort** — 900s runtime 后 aborted（Bun 版本排查任务），subagent 超时保护生效但任务未完成

### 新功能使用进展
- **Cove plugin 开发中** — 在 #cove channel 使用 OpenClaw plugin SDK 开发自定义 channel plugin，spawn subagent 修复编译错误。SDK API surface 和文档存在差距（`api.getConfig()` vs `api.config` 等），需要更多类型文档
- **pass store audit** — daily-audit cron 实际执行了 44 个 secret 的审计，OpenClaw exec 工具处理敏感操作正常

### 版本稳定性
- 2026.5.18 运行第 2 天，零平台级故障，subagent/cron/Discord 多通道稳定
