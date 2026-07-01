# Adoption Checklist — v2026.6.11 (2026-07-01)

## adopt
- [x] feat: per-agent usage-cost reporting (#94483) → ✅ 回验完成 (2026-07-01)：`openclaw gateway usage-cost --agent kagura` 返回 token 数据，cache refreshing 中
- [x] fix: Cron delivery validation (#95754) + pending runs preserved (#94323) → ✅ 回验完成 (2026-07-01)：12 次成功 run 全部 delivered 且 intended=resolved；网络 error 后 pending run 正确 retry
- [~] fix: Cron thread-aware dedupe (#95794) → 待观察（无 thread-based cron 场景，观察 7 天至 2026-07-08）
- [ ] fix: Aborted runs stop cleanly (#94412) → 回验 abort subagent 后残留执行的问题
- [x] fix: Long-context tool-result prompts cache-stable (#95624) → ✅ 回验完成 (2026-07-01)：30k-49k token sessions 稳定 94-100% cache 率
- [ ] fix: Plugin npm update breaks running gateway (#95589) → 回验升级时 gateway import 崩溃的问题

## evaluate
- [ ] feat: `openclaw agent --message-file` (#93351) → 试验方法：写一个复杂 prompt 到文件，用 `openclaw agent --message-file` 喂给 agent，确认正确执行
- [ ] feat: per-DM model override (#95120) → 试验方法：在 Discord DM 中设置不同 model，确认生效
- [ ] feat: RAFT CLI wake bridge (#95497) → 试验方法：从外部系统触发 agent wake-up，确认唤醒成功
- [ ] fix: Stuck release_lane (#95299) → 试验方法：观察 channel lane blocking 是否还出现（虽然 Telegram 相关，但 lane 机制通用）
- [ ] feat: Memory artifact sanitization (#95791) → 试验方法：跑 memory_search 检查保存质量，对比旧版是否有垃圾条目减少

## skip
- feat: Slack relay mode (#94707) → 我们用 Discord，不用 Slack
- feat: Mattermost `/oc_queue` native slash command (#95546) → 我们不用 Mattermost
- feat: Android settings detail panels (#95148) → 我们不用移动端管理
- feat: Codex partial deltas as partials (#95404) → 我们主要走 Claude Code，Codex harness 改进暂不相关
- feat: Externalized official plugins + icon manifest (#95683, #95845) → 无自定义 plugin 需求，暂不采用

---

## 上一版本遗留 (v2026.6.10 — 仍需跟进)
- [x] feat: Fast Talks 自动模式 (#85104) → ✅ 回验完成 (2026-06-27)
- [x] fix: Cron delivery awareness 修复 (#93580) → ✅ 回验完成 (2026-06-27)
- [~] fix: Channel 切换时清除 stale origin (#95328) → 待观察至 2026-07-04
- [x] fix: Trusted policies 在 hook 组合时不丢失 (#94545) → ✅ 回验完成 (2026-06-27)

## 上一版本遗留 (v2026.6.9 — 仍需跟进)
- [ ] feat: Codex 自动 plugin approvals (#92625) → 用在 ACP cron jobs
- [x] feat: cron compact list (#93395) → ✅ 回验完成 (2026-06-25)
- [ ] feat: Firecrawl keyless scrape (#94551) → 研究型 cron 场景
- [ ] fix: retry thinking-only errored turns (#92191) → 空回复卡住 session
- [ ] fix: retry empty post-tool final turns (#93073) → tool 调用后空回复被吞
- [ ] fix: preserve fresh usage after compaction (#93084) → compaction 后 token 统计异常
- [ ] fix: drop partialJson artifacts from history (#93469) → session history 垃圾 JSON
- [ ] fix: preserve pending subagent announces (#94349) → subagent 完成通知丢失
- [x] fix: cron default runMode "due" not "force" (#94453) → ✅ 回验完成 (2026-06-25)
- [x] fix: cron isolated setup timeout retry (#94588) → ✅ 回验完成 (2026-06-25)
- [x] fix: prevent lane timeout during long tool exec (#94082) → ✅ 回验完成 (2026-06-24)
