# Adoption Checklist — v2026.6.5 (2026-06-10)

## adopt
- [ ] feat: MCP tool result 自动类型转换 → 用在 Notion/Obsidian MCP 工具调用场景 → 根治神秘 400 错误
- [ ] feat: Anthropic extended-thinking 会话恢复 → 用在日常 thinking mode session → Gateway 重启后不再卡死
- [ ] fix: config.patch 数组替换语义修复 → 回验 tools.allow/deny 配置变更 → 旧条目不再残留
- [ ] fix: Cron legacy JSON → SQLite 自动迁移 → 回验升级后 cron 数据完整性
- [ ] fix: TUI 消息稳定性修复 → 回验 TUI 发消息后不再出现幽灵消息

## evaluate
- [ ] feat: Parallel 作为内置 web_search provider → 试验方法：配置 PARALLEL_API_KEY，对比搜索质量
- [ ] feat: ClawHub GitHub 仓库技能安装 → 试验方法：尝试从 GitHub repo 安装一个社区 skill

## skip
- fix: QQBot/频道 thinking 标签泄漏 → 我们 QQBot channel 用量极低，非优先
- fix: macOS node 不再静默断开健康连接 → 我们没有 Mac 节点
- feat: State/Storage 全面 SQLite 化 → 自动生效，无需主动采用
- feat: Google Chat 原生审批卡片 → 我们未接入 Google Chat
- feat: 内联图片 data URL 脱敏 → 自动生效，无需主动配置
