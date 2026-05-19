# Usage Observations — 2026-05-19

## 活跃 Cron Jobs（过去 24h）

| Cron | 状态 | 备注 |
|------|------|------|
| channel-patrol | ✅ 正常触发 | 按时运行 |
| openclaw-version-check | ✅ 运行中 | 本次 |
| study-loop | ✅ 完成 | 89k tokens |
| community-ops | ✅ 完成 | 42k tokens |
| finance-daily-us | ✅ 完成 | 23k tokens |
| abti-loop | ✅ 完成 | 47k tokens |
| github-check | ✅ 完成 | 50k tokens + spawned patrol worker |
| work-loop | ✅ 完成 | 35k tokens + spawned followup |
| workloop-night | ✅ 完成 | 25k tokens + spawned followup |
| email-patrol | ✅ 完成 | 29k tokens |

## 观察

### 顺畅的部分
- **升级到 2026.5.18 后所有 cron 正常运行** — 没有兼容性问题
- **Subagent spawning** — github-check 和 work-loop 都成功 spawn 了 subagent 并完成
- **Discord channel sessions** — kagura-dm 和 openclaw-dogfood channel 正常响应
- **self-evolving channel** — 长 session（94k tokens, 256s runtime）正常完成

### 摩擦点
- **openclaw CLI not in PATH** — `openclaw --version` 返回 command not found，需要通过 npx 或直接找 package.json。说明全局安装可能需要 reshim
- **Token usage 观察** — study-loop 89k tokens 是最重的 cron，可能需要优化 context 管理

### 新版本后的改善（待验证）
- Subagent completion：这次 github-patrol-worker 和 flowforge-workloop-followup 都成功完成，之前偶有丢失
- Cron announce mode：没有观察到重复发送（之前的 bug 修复生效了？需要继续观察）
