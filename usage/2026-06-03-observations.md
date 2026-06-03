# 使用观察 — 2026-06-03

## 运行概况
- **活跃 session**: 26 个（含 cron、subagent、dreaming、Discord channel）
- **Cron 全线正常**: version-check, cove-patrol, auto-trader, study-loop, work-loop, workloop-night, morning-briefing, channel-patrol, email-patrol, github-check, abti-loop, daily-audit, toolchain-health, community-ops, finance-daily, garden-watering, code-review-pr-tracking — 全部 OK
- **consecutiveErrors**: 0（version-check cron）

## ✅ 顺畅的

1. **Subagent spawn + completion 可靠**
   - work-loop spawn code review subagent（NemoClaw #4623 分析，评分 8/10，15s 完成）
   - workloop-night spawn PR followup subagent（30 PR 全量扫描，159s 完成）
   - 两个都正确返回结果和 delivery

2. **Dreaming 管线健康** — deep + rem narrative 都正常产出，内容质量好

3. **跨 channel 投递正常** — email-patrol 向 kagura-dm @ Luna 发安全提醒，server-health 回复 channel 问题，均无投递失败

4. **FlowForge 编排稳定** — work-loop 通过 FlowForge 完成 issue 分析→study→plan→code review 完整流程

5. **Cron 执行效率提升** — version-check 从之前常见的 100-200s 降到 62s（昨天），说明 lightContext 和流程优化生效

## ⚠️ 摩擦点

1. **web_search 故障** — morning-briefing 报告 kimi provider API key 缺失，HN/Twitter/arxiv 扫描跳过。需要修 config 或换 search provider
2. **NemoClaw #4545 执行跟进失败** — daily-audit 连续 2 天发现 assigned 6 天无 PR，但"今天 PR 或 unassign"的最后通牒未执行。审计→执行的闭环断裂
3. **cc-connect 4 PR approved 但不 merge** — 已 ping 3 次，maintainer 无反应。属于外部依赖

## 📊 Token 使用（按 session）
- work-loop: 109K（最高，含 issue 分析全流程）
- daily-audit: 75K
- github-check: 74K
- email-patrol: 59K
- channel-patrol: 57K
- morning-briefing: 54K
- 其他 cron: 25-47K

## 🔧 Platform 表现
- v2026.5.28 运行第 6 天，零 platform regression
- Isolated cron narrow grant 仍限制 cross-cron 可观测性（已知限制）
- Heartbeat 正常，community-ops + main session 均 HEARTBEAT_OK
