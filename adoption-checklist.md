# Adoption Checklist — v2026.7.1 (2026-07-15)

## adopt
- [x] feat: Session 标题自动生成 → 用在所有 session（20+ 活跃）→ session 列表可读性大幅提升 ✅ (2026-07-15 verified: derivedTitle 字段已生效)
- [x] feat: Cron 模型选择（Control UI 可见）→ 用在 10+ cron jobs 监控 → 快速确认各 job 用的模型对不对 ✅ (2026-07-15 verified: model 字段可见)
- [ ] feat: Exit-triggered schedules → 用在 work-loop → plan-review 链式调度 → 减少轮询，精确衔接
- [ ] fix: Cron edit delivery 修复 → 回验：之前改 cron bestEffort 时 announce 模式被意外覆盖
- [ ] fix: CJK Markdown emphasis → 回验：中文加粗/斜体不再泄漏标记，所有 Discord 输出受益
- [ ] fix: Discord streamed finals → 回验：Discord channel 完成回复标为未读，Luna 不再漏消息
- [x] fix: Cron 正确性大修（超时不丢 provider/model）→ 回验：高密度 cron 场景稳定性 ✅ (2026-07-15 verified: 连续3天零故障，provider/model 保持)
- [ ] fix: Delivery recovery pacing → 回验：gateway 重启后消息不再 burst 导致乱序
- [ ] fix: Agent empty replies 可见化 → 回验：之前偶尔"静默失败"现在应显示明确信息
- [ ] fix: Codex app-server 0.144.3 → /codex 使用时验证兼容性

## evaluate
- [ ] feat: ClawRouter（内置路由插件）→ 试验方法：评估是否比当前单 provider 配置更灵活，在非关键 cron 上试用
- [ ] feat: GPT-5.6 Ultra 支持 → 试验方法：在 study-loop 或低风险任务中试跑，对比 claude-opus-4-6 效果
- [ ] feat: Gateway crash-loop recovery → 试验方法：下次 gateway 异常时观察是否进入 safe mode 而非无限重启

## skip
- feat: Logbook work journal → 需要 paired node，我们主要在 server 端，暂无场景
- feat: Conversational onboarding (Crestodian) → 我们已配好，仅新用户受益
- feat: iOS/Android 离线 + Apple Watch 语音 → 我们主要在 server 使用
- feat: GPT-5.6 成为默认 → 我们用 claude-opus-4-6 为主，不影响已有配置
- feat: Telegram Codex 配对 → 我们不用 Telegram
- fix: Installer temp cleanup → 安装已完成，不影响运行时
- fix: SQLite WAL 安全 → Node v24 已包含修复，无需额外操作
- fix: SecretRef 凭证隔离 → 安全性提升自动生效，无需操作
- issue: Discord channel hot-reload (#70524) → **本次未修复**，仍需 gateway restart
