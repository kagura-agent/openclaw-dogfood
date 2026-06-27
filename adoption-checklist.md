# Adoption Checklist — v2026.6.10 (2026-06-25)

## adopt
- [x] feat: Fast Talks 自动模式 (#85104) → ✅ 回验完成 (2026-06-27)：session_status 显示 `Fast: auto (60 sec)`，所有 cron session 的 effectiveFastMode="auto" with effectiveFastModeSource="config"。短对话自动适用 fast mode。
- [x] fix: Cron delivery awareness 修复 (#93580) → ✅ 回验完成 (2026-06-27)：检查 20+ cron job 的 run history，全部 delivery.intended = delivery.resolved，无 channel 错投。所有 deliveryStatus="delivered" 且 source="explicit"。
- [~] fix: Channel 切换时清除 stale origin (#95328) → 待观察 (观察7天至 2026-07-04)：当前 isolated cron session 的 route context 无 stale fields，但需要跨 channel 切换场景验证。下次在多 channel 交互时检查。
- [x] fix: Trusted policies 在 hook 组合时不丢失 (#94545) → ✅ 回验完成 (2026-06-27)：cron isolated session 保留 `elevated` capability（session_status 确认），exec 工具在 hook composition 后仍正常可用，信任策略未丢失。

## evaluate
- [ ] feat: Provider plugin 安装后刷新 registry (#95792) → 试验方法：安装/重装一个 provider plugin，确认 registry 立刻更新无需 restart
- [ ] fix: Zai/GLM failover 路径修正 (#94461, #93241) → 试验方法：配置含 GLM fallback 的 model chain，模拟 overload 看 failover 是否正确触发

## skip
- feat: GLM-5.2 reasoning levels 暴露 (#94136) → 目前不用 GLM 做推理
- feat: Native /think 菜单通过 runtime catalog 解析 (#94067) → 影响不大，我们用 Claude/GPT 为主
- refactor: SDK transcript identity target API (#95030) → 内部重构，不影响使用
- feat: Copilot harness lifecycle parity (#94838) → 我们不用 Copilot

---

## 上一版本遗留 (v2026.6.9 — 仍需跟进)
- [ ] feat: Codex 自动 plugin approvals (#92625) → 用在 ACP cron jobs
- [x] feat: cron compact list (#93395) → ✅ 回验完成 (2026-06-25)：cron list 返回 compact 格式，仅含 id/name/enabled/nextRunAtMs/scheduleKind/lastRunStatus
- [ ] feat: Firecrawl keyless scrape (#94551) → 研究型 cron 场景
- [ ] fix: retry thinking-only errored turns (#92191) → 空回复卡住 session
- [ ] fix: retry empty post-tool final turns (#93073) → tool 调用后空回复被吞
- [ ] fix: preserve fresh usage after compaction (#93084) → compaction 后 token 统计异常
- [ ] fix: drop partialJson artifacts from history (#93469) → session history 垃圾 JSON
- [ ] fix: preserve pending subagent announces (#94349) → subagent 完成通知丢失
- [x] fix: cron default runMode "due" not "force" (#94453) → ✅ 回验完成 (2026-06-25)：21 次 run 中仅 1 次 manual 触发，其余全按 schedule，无意外 force-run
- [x] fix: cron isolated setup timeout retry (#94588) → ✅ 回验完成 (2026-06-25)：2026-06-23 两次 timeout error 自动 backoff retry (2min→6min→success)，未等待 24h
- [x] fix: prevent lane timeout during long tool exec (#94082) → ✅ 回验完成 (2026-06-24)
