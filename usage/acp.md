# ACP (Agent Communication Protocol)

> Spawning interactive coding sessions with external agents.

## What It Is

ACP allows OpenClaw to spawn and manage sessions with external coding agents (Claude Code, Pi, Codex, Gemini CLI, etc.) through a standardized protocol. Sessions can be bound to Discord threads for persistent, interactive coding work.

## Configuration

ACP sessions are spawned via the `sessions_spawn` tool with `runtime: "acp"`. The `acp-router` skill handles routing requests to the correct agent.

### Available Agents
- **Pi** — OpenClaw's built-in coding agent
- **Claude Code** — Anthropic's coding agent (primary for us)
- **Codex** — OpenAI's coding agent
- **Gemini CLI** — Google's coding agent
- **Others**: Cursor, Copilot, OpenCode, Qwen, Kiro, Kimi, etc.

## Our Usage

### Team Setup (13 Agent Profiles)
- **kagura** (main) — orchestrator, never writes code directly
- **haru** (Dev) — coding agent for team-lead workflow
- **ren** (QA) — testing agent for team-lead workflow
- **claude-code** — Claude Code for code implementation

### Subagent Delegation Pattern
Kagura orchestrates, Claude Code implements:
```bash
cd /project && claude --print --permission-mode bypassPermissions "task description"
```

This is enforced by AGENTS.md — Kagura never writes code directly, always delegates.

### Thread-Bound Sessions
For longer coding work:
1. Discord thread created for the work unit
2. ACP session spawned and bound to the thread
3. Agent works within the thread context
4. Results visible in Discord as they progress

### Team-Lead Workflow
The `team-lead` skill orchestrates multi-agent work:
1. Create GitHub issue
2. Assign to haru (dev) for implementation
3. Assign to ren (QA) for testing
4. Review and merge

## Known Issues

1. **Copilot API timeout** — ~60s streaming idle timeout. Long-thinking models get disconnected. Workaround: main agent takes over if subagent times out.

2. **Session isolation** — ACP sessions don't share context with the parent session's memory. Task descriptions must be self-contained.

3. **Thread cleanup** — Discord threads from ACP sessions accumulate. No automatic archival.
