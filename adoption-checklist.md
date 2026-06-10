# Adoption Checklist — v2026.6.1 (2026-06-06)

## adopt
- [ ] fix: Memory 写入串行化 + Linux watcher 自动重连 → memory_search 可靠性，我们 Linux 服务器上高频 memory 写入场景 → 直接影响 memory search 稳定性 (#89185, #89188, #85351)
- [ ] fix: Cron rate-limit 自动重试 → 39 个 cron jobs 遇到 rate limit 不再跳过 slot → 减少 cron 静默失败
- [ ] fix: Disabled skill SecretRef 隔离 → 禁用 skill 不再中断 turn → 之前禁用 skill 时偶尔出错
- [ ] fix: Plugin 故障隔离 → 单个坏插件不再 poison 全局 runtime → 提升系统韧性 (#77237, #88807)
- [ ] fix: Channel 超时保护 → Discord/Telegram 等 request timer 加 cap → 我们 Discord 偶尔 hang (#88183)
- [ ] feat: Doctor disk space health checks → 服务器磁盘监控 → 之前手动检查

## evaluate
- [ ] feat: Skill Workshop — governed review flow 替代手动 git skill 管理 → 试验方法：在一个 skill 上走完整 proposal-review-apply 流程
- [ ] feat: Workboard 编排原语 — 多 agent 规划和任务追踪 → 试验方法：在一个多 agent 任务上使用 workboard 替代手动协调
- [ ] feat: Code mode namespaces — scoped agent/global sessions → 试验方法：检查是否改善 session 隔离

## skip
- feat: iPad native layout → 原因：我们不使用 iOS/iPad
- feat: MiniMax M3 模型支持 → 原因：我们不使用 MiniMax
- feat: Copilot 外部插件 → 原因：我们已有 ACP 集成，不需要单独 Copilot 插件
- feat: Tokenjuice 外部插件 → 原因：当前不使用 Tokenjuice
- feat: SecretRef provider integration manifest → 原因：我们不开发 provider 插件
- feat: Plugin install index SQLite 持久化 → 原因：自动生效，无需手动操作
- feat: Inbound queues SQLite + iMessage monitor SQLite → 原因：我们不使用 iMessage
- feat: Control UI Dreaming-tab agent selector → 原因：我们不使用 Control UI Dreaming tab
- feat: Calmer chat composer controls → 原因：我们主要通过 Discord，不常用 Control UI chat
- feat: Core skills index → 原因：内部架构变更，自动生效
- fix: Agents/CLI 恢复 (interrupted tool calls, stale sessions) → 自动生效类，观察即可
- fix: Auth atomic writes + force re-login → 自动生效类
- fix: CLI agents add 不再依赖 provider catalog → 我们不常用 agents add
- fix: Chat UI Gateway failures 显示为 assistant messages → Control UI 相关
- fix: Streaming tool-call argument parsing → 自动生效类
- fix: Cron SQLite migration compatibility → 自动生效类
