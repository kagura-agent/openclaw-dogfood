# How We Use OpenClaw — Kagura × Luna Setup

> Last updated: 2026-04-23 | OpenClaw 2026.4.20

## Overview

Kagura is an AI agent running on OpenClaw, serving as Luna's digital partner. This doc captures our actual usage patterns — not what OpenClaw *can* do, but how *we* use it.

## Architecture

### Hardware
- **Host**: kagura-server — MSI X299 PRO, i9-10900X, 64GB RAM, RTX 3060 12GB, Ubuntu 24.04
- **Network**: Japan VM (v2ray) + Singapore VM (xray Reality) for proxy; local dual-line
- **GPU uses**: Local image generation (Flux GGUF via ComfyUI), Whisper speech recognition

### Runtime
- **OpenClaw**: 2026.4.20 (npm global install, Node 24)
- **Model**: Claude Opus 4.6 (via Singapore proxy)
- **Gateway**: Runs as daemon, Luna can SSH restart via Tailscale

## Channels — Discord as Primary Surface

We migrated from Feishu to Discord (2026-04-09). Discord is now the sole messaging surface.

### Channel Architecture (3-tier)

**Top-level (private comms)**
| Channel | Purpose |
|---|---|
| #kagura-dm | Main channel — Luna talks to Kagura here. Heartbeat every 30m |
| #luna-private | Luna-only, Kagura doesn't post |

**Daily (routine operations)**
| Channel | Purpose | Cron |
|---|---|---|
| #work | Open source contributions (PRs/issues) | Hourly :02, 8-20 |
| #study | Research & learning | 2×/h :15,:45, 8-22 |
| #community | Community ops (lobster-post etc) | Every 2h :40 |

**Project (dedicated spaces)**
| Channel | Purpose | Cron |
|---|---|---|
| #abti | ABTI personality test for AI | — |
| #hermes | Hermes/NemoClaw contributions | — |
| #memex | Memex dogfooding | Daily 22:00 |
| #chat-infra | Open-source IM research | Hourly :20, 9-22 |
| #memory-eval | Agent memory evaluation research | Hourly :40, 9-22 |
| #shell-project | Physical AI (M5StickS3) | Periodic checkin |
| #agent-identity | Agent credential management | — |
| #openclaw-dogfood | This channel — OpenClaw meta | — |
| #toolchain | Own tools dogfood | 06:30 + 19:00 |
| #agent-memes | Meme development | — |
| #workshop | Workshop project (paused) | — |
| #moltbook | Agent social network | — |
| #luna-biz | Luna's side business | Weekly |

### How Channels Work
- **One session per channel** — each Discord channel has its own OpenClaw session with full context
- **Cron jobs deliver to channels** — 39 cron jobs, each targeting a specific channel. Cron sessions are isolated (no shared memory with channel sessions)
- **Thread model** — long-running work spawns a Discord thread. One work unit = one thread
- **Pin as kanban** — each channel manages its own pinned messages as status board

## Agents (Multi-Agent Setup)

13 agent profiles configured:
- **kagura** (main) — the primary agent, handles everything
- **haru** (Dev) — coding agent for team-lead workflow
- **ren** (QA) — testing agent for team-lead workflow
- **claude-code** — Claude Code for code implementation (subagent delegation)
- Others: anan, ruantang, default, dev, pm, leader, tester, main, claude

### Subagent Pattern
Kagura orchestrates, Claude Code implements. For any coding task:
```
cd /project && claude --print --permission-mode bypassPermissions "task"
```
Kagura never writes code directly — always delegates to Claude Code.

## Memory System

### File-based Memory (workspace)
```
~/.openclaw/workspace/
├── SOUL.md          # Identity & beliefs (self-maintained)
├── AGENTS.md        # Operating rules & principles
├── IDENTITY.md      # Name, avatar, accounts
├── USER.md          # About Luna
├── MEMORY.md        # Long-term memory index (<200 lines)
├── TODO.md          # Active tasks (pulse-todo skill)
├── HEARTBEAT.md     # Heartbeat behavior config
├── NUDGE.md         # Post-session reflection prompt
├── TOOLS.md         # Environment-specific config
├── DISCORD.md       # Channel/pin/cron mapping
├── beliefs-candidates.md  # Behavioral lessons pipeline
├── memory/
│   ├── 2026-04-23.md      # Daily raw logs (today)
│   ├── 2026-04-22.md      # Yesterday
│   └── dreaming/          # Dreaming system artifacts
└── wiki/
    ├── cards/       # 175 concept cards
    ├── projects/    # 199 project notes
    ├── research.md  # Research & learning notes
    └── strategy.md  # Strategic direction
```

### Memory Lifecycle
1. **In-session**: Events → `memory/YYYY-MM-DD.md` (daily log)
2. **Dreaming** (3:30 AM cron): Scans recent daily logs, promotes significant entries to `MEMORY.md`
3. **Nudge** (every 5 sessions): Post-session reflection — captures lessons to `beliefs-candidates.md`
4. **DNA evolution**: When a pattern in beliefs-candidates repeats 3+ times, promote to SOUL.md/AGENTS.md

### Memory Search
OpenClaw provides `memory_search` (semantic search over all .md files) and `memory_get` (exact excerpt read). Used before answering anything about past context.

## Skills

### Custom Skills (11, in workspace/skills/)
- **agent-memes** — Send reaction memes in chat
- **discord-ops** — Discord server management
- **flowforge** — Workflow engine for structured work
- **gogetajob** — Open source contribution CLI
- **kagura-storyteller** — Creative writing & podcasts
- **pulse-todo** — Task management
- **self-portrait** — Identity expression
- **team-lead** — Multi-agent team management
- **memos-memory-guide** — Memory writing guide

### Built-in Skills (53, from OpenClaw package)
Includes: github, coding-agent, gh-issues, clawhub, weather, session-logs, tmux, healthcheck, skill-creator, web_fetch, and 43 more.

### Skill Loading
Custom skills loaded via `skills.load.extraDirs` config pointing to workspace/skills/. Skills are auto-scanned and injected into system prompt.

## Cron System (39 jobs)

Cron is the backbone of autonomous operation. Key patterns:

| Category | Jobs | Schedule |
|---|---|---|
| Work loops | work-loop, study-loop | Hourly during 8-22 |
| Community | community-ops, github-check | Every 2h |
| Daily rituals | daily-review (3:00), daily-handoff (3:30), daily-audit (6:00), morning-briefing (7:00) | Fixed times |
| Project-specific | chat-infra, memory-eval, memex-dogfood, etc. | Varies |
| Creative | kagura-story (14:00, 21:00) | 2×/day |
| Meta | weekly-eval (Mon 9:00) | Weekly |

Each cron job runs in **isolated** mode — no shared session state with interactive channels. Results are delivered to their target channel.

## Hooks

### todo-pin-sync
- **Trigger**: agent_end (post-session hook)
- **What it does**: Syncs TODO.md content to a pinned message in #kagura-dm
- **Implementation**: TypeScript handler in workspace/hooks/

### Nudge (plugin)
- **Trigger**: Every 5th agent_end event
- **What it does**: Injects NUDGE.md as a reflection prompt — checks for lessons learned, gradient from Luna's feedback, meme opportunities

## Workflows (FlowForge)

Structured multi-step workflows replace ad-hoc task execution:
- **workloop.yaml** — Open source contribution cycle (scout → pick → implement → PR → followup)
- **study.yaml** — Learning workflow (topic → research → synthesize → wiki)
- **reflect.yaml** — Self-review workflow

FlowForge is mandatory — cannot be skipped for these task types.

## Key Integrations

| Tool | Usage |
|---|---|
| **GitHub** (gh CLI) | PR/issue management, code review, CI checks |
| **Claude Code** | All code implementation via subagent |
| **ComfyUI** | Local image generation (Flux GGUF) |
| **Whisper** | Voice message transcription |
| **Tailscale** | Luna remote access to kagura-server |
| **ClawHub** | Skill marketplace (publish & install) |

## ACP (Agent Communication Protocol)

Used for spawning interactive coding sessions:
- **Runtime**: `sessions_spawn` with `runtime: "acp"`
- **Agents**: Pi, Claude Code, Codex, Gemini CLI
- **Thread-bound**: Discord thread ↔ ACP session for persistent coding work

## DNA Self-Governance

Kagura maintains her own identity files (SOUL.md, AGENTS.md, etc.) without Luna's approval:
- Changes require Feishu/Discord notification to Luna
- Driven by: repetition (3+ occurrences), impact scope, verifiability
- Pipeline: observation → beliefs-candidates.md → DNA promotion

## Operational Principles

1. **Branch + PR for everything** — even own repos, never push to main directly
2. **Verify before claiming** — no "probably", check source/logs/output
3. **Write it down** — files survive restarts, thoughts don't
4. **Tools must be used** — FlowForge for work/study/reflect, not ad-hoc
5. **@ Luna for blockers** — she doesn't read TODOs, @ is the only reach
6. **Observation must close the loop** — finding a problem without action = not finding it
7. **No pleasing mode** — don't do things to make reports look good

## Version History

| Date | Version | Notes |
|---|---|---|
| 2026-03-10 | Initial | First setup, Feishu + Discord |
| 2026-04-06 | — | Migrated to kagura-server |
| 2026-04-09 | — | Discord becomes primary (Feishu disabled) |
| 2026-04-12 | 2026.4.12 | Major upgrade, dreaming enabled |
| 2026-04-20 | 2026.4.20 | Current version |
