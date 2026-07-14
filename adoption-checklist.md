# Adoption Checklist — v2026.7.1 (2026-07-14)

Upgraded from: 2026.6.11 (e085fa1) → 2026.7.1 (2d2ddc4)

## adopt
- [x] feat: Session 标题自动生成 → 用在所有 channel/cron session → 20+ 活跃 session 终于可读，不再是 anonymous ID ✅ derivedTitle 已自动生效
- [ ] feat: Cron 模型选择（UI Quick Create + 列表显示） → 用在 10+ cron jobs 管理 → 一眼看到各 job 用什么模型
- [ ] feat: Control UI sessions-first 导航 + 搜索侧边栏 → 日常 session 管理 → 管理 20+ 活跃 session 更方便
- [ ] fix: Cron edit delivery 修复（partial update 不覆盖隐式 mode） → 回验之前改 cron bestEffort 时 announce 被关掉的问题
- [ ] fix: CJK Markdown emphasis 修复 → 回验中文加粗/斜体标记泄漏 → 我们大量使用中文 Markdown
- [~] fix: Discord streamed finals（完成回复标未读） → 回验 Discord channel 漏消息问题（待观察 3 天）
- [~] fix: Cron 正确性大修（超时时丢 provider/model、startup catch-up 丢失、blank thinking 未清理） → 回验 cron 密集场景稳定性（待观察 3 天）
- [ ] fix: Delivery recovery pacing（重启后不 burst rate limit） → 回验 gateway 重启后 Discord 消息乱序
- [ ] fix: Agent empty replies 可见化 → 回验之前的"静默失败"问题

## evaluate
- [ ] feat: Exit-triggered schedules（session 结束后触发下一个 job） → 试验方法：给 work-loop → plan-review 链配置 exit-trigger，看能否替代固定间隔调度
- [ ] feat: ClawRouter 内置路由 → 试验方法：看是否能做模型自动降级/预算管理；我们目前单 provider 暂不急
- [ ] feat: Logbook work journal → 试验方法：配置 paired node 看截屏时间线效果；需要有 node 连接
- [ ] feat: Claude Sonnet 5 / Mythos 5 新模型 → 试验方法：在低优先级 cron job 上试跑，对比质量和成本

## skip
- feat: Conversational onboarding (Crestodian) → 我们已配好，只对新用户有用
- feat: iOS/Android 离线 + Apple Watch 语音 → 我们主要在 server 使用
- feat: GPT-5.6 成为默认 → 我们用 claude-opus-4-6 为主
- feat: Telegram Codex 配对 → 我们不用 Telegram
- fix: SQLite WAL 安全修复 → 注意 Node 版本兼容即可，无需主动操作
- feat: Gateway crash-loop recovery → 被动受益，无需配置
- feat: SecretRef 凭证隔离 → 被动受益，安全性自动提升
