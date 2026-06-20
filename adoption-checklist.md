# Adoption Checklist — v2026.6.8 (2026-06-19)

## adopt
- [ ] feat: 原生 /usage footer 渲染器 + 默认模板 (#92657, #89835, #89629) → 用在 cron 任务 token 消耗监控 → Discord 投递中直接看到每次 run 的消耗，不用手动跟踪
- [x] feat: Session identity 暴露到 runtime prompt (#92468) → 用在 multi-channel 架构 → agent 自动感知当前 session，减少 prompt 工程 ✅ 2026-06-20: 确认 runtime prompt 已包含完整 session identity (agent=kagura | session=agent:kagura:cron:... | sessionId=...)
- [ ] feat: Subagent thinking override clamp (#92914) → 用在 code-review / workloop 的 subagent spawn → 防止重型 subagent 消耗过多 token（如 #cove PR#409 的 5.2M token 场景）
- [ ] feat: Cron timezone preserve on expression edits → 用在 10+ cron 维护 → 编辑 cron 表达式时时区不丢失
- [ ] feat: OpenAI embedding batch split 防 431 → 用在 memory indexing → 大批量 embedding 场景下的保护
- [ ] fix: Yielded subagent runs 在 abort 时正确 pause (#92631) → 回验 subagent 被 kill 后的恢复 → 之前 restart 时 subagent 可能丢失
- [ ] fix: Reset archive fallback 恢复 (#92879) → 回验 #cove 等长期 session 的 context 恢复 → 之前 transcript 损坏问题
- [~] fix: 主 session heartbeat 事件去重 (#91287) → 回验 10+ cron 场景的 token 消耗 → 之前重复 heartbeat 浪费 token（观察3天，到 2026-06-23 确认 token 消耗是否下降）
- [ ] fix: Discord auto-thread title timeout + reasoning cap (#64734) → 回验 Discord thread 创建 → 之前偶尔卡住
- [x] fix: memory_search 在 transient QMD mode 下保持可用 (#92618, #92639) → 回验 cron isolated session 的 memory_search → 之前 transient 模式下 disabled ✅ 2026-06-20: cron isolated session 中 memory_search 正常返回结果 (2077ms, score 0.609)

## evaluate
- [ ] feat: /btw 支持 CLI-backed sessions (#92669) → 试验：在下次 ACP session 运行中用 /btw 发送补充信息
- [ ] feat: Browser --labels overlay 扩展到 full-page/element captures (#92834) → 试验：下次 browser-automation 时测试截图标注精度
- [ ] feat: Claude Haiku 4.5 支持 → 试验：考虑用 Haiku 4.5 替代部分轻量 subagent 任务降低成本

## skip
- feat: GLM-5.2 支持 → 暂不需要新模型
- feat: Telegram 富文本消息 → 我们主用 Discord
- feat: WhatsApp ACP binding → 不适用
- feat: Key-free web search opt-in → 自动生效，无需操作
- feat: Workspace files collapsed by default → UI 改善，自动生效
- feat: WebChat backscroll 保持 → UI 改善，自动生效
- feat: Feishu dynamic agent route 修复 → 不适用
- fix: SQLite NFS WAL avoidance (#91247) → 我们不用 NFS
