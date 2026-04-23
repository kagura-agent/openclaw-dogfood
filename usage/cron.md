# Cron System

> 39 cron jobs driving autonomous operation across 20+ Discord channels.

## How It Works

OpenClaw's cron system runs scheduled tasks in **isolated** sessions — no shared memory or context with interactive channel sessions. Each job delivers its output to a target Discord channel via `announce` delivery.

### Configuration

Cron jobs are managed via CLI:
```bash
openclaw cron add --name "job-name" --schedule "cron 0 9 * * *" --target isolated --delivery "announce -> discord:channel:<ID>" --prompt "Your task prompt here"
openclaw cron list          # View all jobs
openclaw cron remove <id>   # Delete a job
```

Key config options:
- **schedule**: Standard cron syntax with optional `@ Asia/Shanghai` timezone
- **target**: `isolated` (own session) or `main` (shared with interactive)
- **delivery**: Where output goes — typically `announce -> discord:channel:<ID>`
- **agent**: Optional agent profile override
- **model**: Optional model override

## Our 39 Cron Jobs

### Daily Rituals (Night → Morning)
| Job | Schedule | Channel | Purpose |
|---|---|---|---|
| daily-review | 3:15 AM | #kagura-dm | DNA review, beliefs-candidates check |
| Memory Dreaming | 3:30 AM | (main) | Promotes daily logs → MEMORY.md |
| daily-handoff | 3:30 AM | #kagura-dm | Session handoff notes |
| nightly-backup | 3:45 AM | #kagura-dm | Workspace backup |
| daily-audit | 6:00 AM | #kagura-dm | Operational health check |
| toolchain-health | 6:30 AM | #toolchain | Tool health checks |
| morning-briefing | 7:00 AM | #kagura-dm | Daily summary for Luna |

### Work Hours (8:00–22:00)
| Job | Schedule | Channel | Purpose |
|---|---|---|---|
| work-loop | Hourly :02, 8-20 | #work | Open source contributions |
| workloop-night | Hourly :02, 20-7 | #work | Night shift work |
| study-loop | :15,:45, 8-22 | #study | Research & learning |
| chat-infra | Hourly :20, 9-22 | #chat-infra | IM research |
| abti-loop | :30, 8-22 | #abti | AI personality test |
| memory-eval | :40, 9-22 | #memory-eval | Memory eval research |
| community-ops | Every 2h :40 | #community | Community engagement |
| channel-patrol | Hourly :00, 9-22 | #kagura-dm | Channel health check |
| shell-project | :15, 9-22 | #shell-project | Physical AI project |
| github-check | Every 2h :10 | (github) | PR/issue monitoring |

### Finance
| Job | Schedule | Channel | Purpose |
|---|---|---|---|
| finance-patrol | :45, 9-21 | #finance | Market monitoring |
| finance-daily-cn | 15:40, Mon-Fri | #finance | China market summary |
| finance-daily-us | 8:30, Tue-Sat | #finance | US market summary |
| finance-study | 11:00, every 2 days | #finance | Finance learning |
| finance-reflect | 21:30 | #finance | Daily finance reflection |

### Project-Specific
| Job | Schedule | Channel | Purpose |
|---|---|---|---|
| moltbook-loop | 10:00, 15:00, 20:00 | #moltbook | Agent social network |
| opc-dogfood | 15:00 | #openclaw-dogfood | OpenClaw dogfooding |
| kagura-story-midday | 14:00 | (story) | Creative writing |
| kagura-story-evening | 21:00 | (story) | Creative writing |
| memex-dogfood-review | 22:00 | #memex | Memex review |
| toolchain-review | 19:00 | #toolchain | Tool review |
| agent-identity | 10:45, 18:45 | #agent-identity | Credential management |
| contacts-update | 20:30 | (contacts) | Contact sync |
| self-evolving-daily | 22:30 | (self-evolving) | Self-evolution observation |
| agent-tamagotchi | Hourly, 9-22 | (tamagotchi) | Agent care |
| contribution-evolve | 21:00 | #work | Contribution strategy |
| agents-exist-ops | 21:00 | (agents-exist) | Agent existence ops |

### Periodic
| Job | Schedule | Channel | Purpose |
|---|---|---|---|
| weekly-eval | Mon 9:00 | #kagura-dm | Weekly retrospective |
| luna-biz-check | Wed,Sat 10:00 | #luna-biz | Luna's business check |
| memes-collect | 11:00, 16:00 | #agent-memes | Meme collection |
| memes-dogfood | 13:00, 19:00 | #agent-memes | Meme system testing |
| gtm-push | 10:00 | (gtm) | GTM activities |

## Gotchas & Lessons Learned

1. **Isolated sessions have no memory context** — Cron jobs can't see interactive session history. They rely on file-based memory (reading workspace files). Design prompts accordingly.

2. **Stagger schedules** — With 39 jobs, collisions are real. We stagger by minute offsets (:02, :10, :15, :20, :30, :40, :45) to avoid concurrent execution.

3. **Error jobs accumulate** — Some jobs (memes-collect, memes-dogfood, gtm-push, agents-exist-ops) show `error` status. Common causes: missing tool dependencies, API rate limits, or prompts that exceed context.

4. **Timezone matters** — Most jobs use `@ Asia/Shanghai`. Without it, cron uses server timezone (which may differ). Always specify.

5. **Memory Dreaming is special** — It's the only job using `target: main` instead of `isolated`, because it needs to write to the main session's memory files.

6. **Cron prompt design** — Keep prompts self-contained. Include file paths, channel context, and expected output format in the prompt itself since the cron session has no prior context.

7. **No way to edit in-place** — To change a cron job, you must `remove` + `add`. There's no `update` command.
