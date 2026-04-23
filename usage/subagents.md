# Subagents

> Background task delegation — Kagura orchestrates, Claude Code implements.

## What Are Subagents

Subagents are background sessions spawned by the main agent to handle specific tasks. The main session stays responsive to Luna while subagents work independently.

## Coding Agent Pattern

The primary subagent pattern: Kagura never writes code directly, always delegates to Claude Code.

### Via coding-agent Skill
```bash
cd /project && claude --print --permission-mode bypassPermissions "task description"
```

Key flags:
- `--print` — output mode (no interactive UI)
- `--permission-mode bypassPermissions` — skip permission prompts
- No PTY needed for Claude Code (unlike Codex/Pi which need `pty: true`)

### Via sessions_spawn
For thread-bound work or ACP sessions:
```
sessions_spawn(runtime: "acp", agent: "claude-code", ...)
```

## Our Subagent Architecture

### Division of Labor
- **Kagura (main)**: Orchestration, research, planning, non-code tasks
- **Claude Code (subagent)**: All code writing, modification, testing
- **Haru (dev agent)**: Team-lead workflow implementation
- **Ren (QA agent)**: Team-lead workflow testing

### Rules (from AGENTS.md)
1. Code implementation MUST use Claude Code — subagents don't write code themselves
2. Any task can be a subagent — long tasks are the design intent
3. Main session stays free for Luna
4. Push-based completion — results auto-announce when done

## Execution Patterns

### Simple Code Task
```
Main agent → spawns Claude Code → Claude Code writes/tests code → result auto-announces
```

### Team-Lead Workflow
```
Kagura → creates GitHub issue → assigns to Haru (dev)
Haru → implements via Claude Code → opens PR
Kagura → assigns to Ren (QA) → Ren tests
Kagura → reviews and merges
```

### FlowForge Workflow
```
FlowForge step → spawns subagent for step execution → result feeds next step
```

## Known Issues

1. **Copilot API timeout** — ~60s streaming idle timeout. If the model thinks for too long without producing tokens, the connection drops. Workaround: main agent takes over.

2. **Context limitations** — Subagents don't inherit the parent session's conversation history. Task descriptions must be self-contained with all necessary context.

3. **No shared memory** — Subagents can read workspace files but their session context is isolated. They can't see what the main agent discussed with Luna.

4. **Depth limits** — Subagent nesting has limits (currently max depth configured per deployment). Our setup uses depth 1 primarily.

5. **Verification discipline** — When a subagent reports "done", the main agent must verify (check code, run tests). "Trust but verify" — subagent output is not automatically trusted.
