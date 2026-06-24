# Adoption Checklist — v2026.6.9 (2026-06-22)

## adopt
- [ ] feat: Codex 自动 plugin approvals (#92625) → 用在 ACP cron jobs (gogetajob, code-review 等) → 减少 plugin 批准卡住导致 cron 超时
- [ ] feat: cron compact list (#93395) → 用在日常 cron 管理 → 30+ job 查看更清晰
- [ ] feat: Firecrawl keyless scrape (#94551) → 用在研究型 cron (study workflow, web_fetch 场景) → 无需配 API key 即可抓取
- [ ] fix: retry thinking-only errored turns (#92191) → 回验 thinking-only 空回复卡住 session 的问题
- [ ] fix: retry empty post-tool final turns (#93073) → 回验 6/18 日报中 tool 调用后空回复被吞
- [ ] fix: preserve fresh usage after compaction (#93084) → 回验 compaction 后 token 统计异常
- [ ] fix: drop partialJson artifacts from history (#93469) → 回验 session history 偶现垃圾 JSON 片段
- [ ] fix: preserve pending subagent announces (#94349) → 回验 gogetajob 流程 subagent 完成通知丢失
- [ ] fix: cron default runMode "due" not "force" (#94453) → 回验 cron 意外重跑问题
- [ ] fix: cron isolated setup timeout retry (#94588) → 回验 isolated cron setup 超时后直接 fail
- [x] fix: prevent lane timeout during long tool exec (#94082) → ✅ 回验完成 (2026-06-24)：work-loop 连续 3 天零错误

## evaluate
- [ ] feat: Standalone 官方 provider plugins (#93470) → 试验方法：检查 gateway 启动日志看是否自动发现 provider 插件
- [ ] feat: Codex Hosted Search (#93446) → 试验方法：在 Codex ACP session 中测试 web_search 是否无需额外配置
- [ ] feat: Codex remote-node exec (#93654) → 试验方法：在 Codex session 中尝试操作 macOS node
- [ ] feat: Codex app-server SecretRefs (#94324) → 试验方法：尝试声明式传递 secret 给 Codex session
- [ ] feat: OTEL log export (#94561) → 试验方法：配置 OTEL endpoint 查看是否有日志输出

## skip
- feat: ClawRouter managed proxy (#93832→reverted) → 已回滚，等稳定
- feat: iOS Watch controls (#93387) → 非刚需，无 Apple Watch 使用场景
- feat: Session workspace rail (#92856) → UI 组件，等有需求再探索
- feat: Cohere provider plugin (#24661) → 当前无 Cohere 使用需求
- feat: SIEM security events (#93945) → 企业级安全审计，个人使用不需要
- fix: Discord tool status emoji ordering (#93488) → 不影响功能，cosmetic fix
- fix: preserve CJK IME composition (#93498) → WebChat 场景，我们主要用 Discord/CLI
