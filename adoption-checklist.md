# Adoption Checklist — v2026.6.1 (2026-06-04)

## adopt
- [x] feat: Cron 重试机制改进 → 用在所有 cron job → 解决偶发 rate limit 导致 job 静默跳过的问题，无需配置变更，自动生效
- [x] fix: Memory 系统稳定性大修（写入串行化、watcher fan-out 减少、transient read 重试） → 回验之前 memory search 结果不稳定的情况
- [x] fix: Disabled skill SecretRef 不再中断 turn → 回验之前偶尔的莫名 turn 失败
- [ ] fix: 插件加载失败隔离 → 更安全的插件管理，无需操作
- [ ] fix: Channel 超时保护增强 → 回验 Discord 集成稳定性
- [ ] fix: Agent 中断恢复改进 → 回验长时间 subagent/ACP session 中断恢复

## evaluate
- [ ] feat: Skill Workshop 全面上线 → 试验方法：用 `skill_workshop` tool 替代手动 git 管理一个 skill 的修改和审核流程
- [ ] feat: Workboard 编排原语 → 试验方法：在 team-lead workflow 中尝试用 Workboard 追踪一次多 agent 任务
- [ ] feat: MiniMax M3 模型支持 → 试验方法：在某个低风险 cron job 中配置为 fallback model
- [ ] feat: Chat UI 增量流式输出 → 升级后自动生效，观察 Control UI 长回复体验

## skip
- feat: Code mode 内部命名空间 → 我们当前 multi-agent 场景不需要 scoped namespaces
- feat: Copilot 插件外部化 → 我们不使用 GitHub Copilot agent
- feat: Tokenjuice 插件外部化 → 我们不使用 Tokenjuice
- feat: iPad 原生布局 → 我们不在 iPad 上使用 OpenClaw
- feat: iMessage/Channel SQLite 迁移 → 我们不使用 iMessage channel
- feat: Control UI Dreaming 标签 agent 选择器 → 低优先级 UI 改进
