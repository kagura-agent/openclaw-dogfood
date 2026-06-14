# Adoption Checklist — v2026.6.6 (2026-06-13)

## adopt
- [ ] feat: Trusted diagnostics channel 可捕获 tool I/O (#91256) → 用在 subagent 调试、cron 排查 → 复杂 subagent 链出问题时能看到完整 tool 调用，不用猜
- [ ] feat: 启动和首回复延迟优化 (#91531, #91538, #91568) → 全局生效 → TUI 响应更快，减少等待
- [ ] fix: Cron 任务取消/超时状态正确保留 (#90666, #90678) → 回验 12+ 个活跃 cron → 之前偶尔看到 cron 超时后状态不一致
- [ ] fix: Cron no-deliver tool warnings 恢复而非静默丢失 (#90678) → 回验 cron 投递 → 之前偶尔 cron 运行但无输出
- [ ] fix: Config patch 中数组显式替换 (#91551) → 回验 config.patch 操作 → 之前配置更新数组时行为不可预测
- [ ] fix: Compaction timeout 降至 180s 并尊重显式配置 (#91361) → 回验长会话 compaction → 更合理的超时

## evaluate
- [ ] feat: OpenRouter OAuth 入驻 (#91830) → 试验：检查是否能简化我们 code-review 多模型 provider 配置
- [ ] feat: Claude Fable 5 自适应 thinking (#91882) → 试验：在一个 subagent 任务中试用 Fable 5，对比推理质量
- [ ] feat: ClawHub dry-run 跳过 publish approval (#91591) → 试验：下次发布 skill 时用 dry-run 验证

## skip
- feat: iMessage 恢复和交付改进 → 我们不用 iMessage channel
- feat: Telegram 投递安全和一致性改进 → 我们主要用 Discord
- feat: Browser CDP 支持现有会话 → 当前无需连接已有浏览器
- feat: Gemma 4 reasoning replay 保留 → 我们不用本地 Gemma 模型
- fix: Session rebind 后清理过期 approval follow-ups (#85679) → 低频场景，自动生效无需特别操作
- security: 安全边界收紧（transcript/sandbox/exec） → 基础设施级别，自动生效
