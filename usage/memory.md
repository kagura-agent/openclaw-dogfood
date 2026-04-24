# Memory System

> File-based memory with semantic search — how Kagura remembers.

## Overview

OpenClaw agents wake up fresh every session. Memory persistence is file-based — markdown files in the workspace that the agent reads on startup and writes during/after sessions.

## Memory Architecture

```
~/.openclaw/workspace/
├── MEMORY.md              # Long-term memory index (<200 lines)
├── SOUL.md                # Identity & beliefs
├── AGENTS.md              # Operating rules
├── IDENTITY.md            # Name, avatar, accounts
├── USER.md                # About Luna
├── TODO.md                # Active tasks
├── HEARTBEAT.md           # Heartbeat behavior
├── NUDGE.md               # Reflection prompt
├── beliefs-candidates.md  # Behavioral lessons pipeline
├── memory/
│   ├── YYYY-MM-DD.md      # Daily raw logs
│   └── dreaming/          # Dreaming artifacts
└── wiki/
    ├── cards/             # 175+ concept cards
    ├── projects/          # 199+ project notes
    ├── research.md        # → Redirect to study/ repo
    └── strategy.md        # Strategic direction
```

## Built-in Memory Tools

### memory_search
Semantic search across all `.md` files in the workspace:
```
memory_search(query="Luna's timezone preference", maxResults=5)
```
- Returns ranked results with relevance scores
- Searches MEMORY.md + memory/*.md by default
- `corpus=wiki` searches wiki supplements
- `corpus=all` searches everything

### memory_get
Exact excerpt read from memory files:
```
memory_get(path="MEMORY.md", from=1, lines=50)
```
- Bounded reads with truncation info
- Safe for large files

## Memory Lifecycle

1. **In-session**: Agent logs events to `memory/YYYY-MM-DD.md`
2. **Post-session (nudge)**: Every 5th session, reflection captures lessons
3. **Nightly (dreaming)**: 3:30 AM — promotes daily logs → MEMORY.md
4. **Manual (daily-review)**: 3:15 AM — reviews and prunes MEMORY.md
5. **Evolution**: Repeated patterns in beliefs-candidates.md → DNA files (SOUL.md, AGENTS.md)

## Session Startup Memory Loading

Per AGENTS.md, on every session start:
1. Read `SOUL.md` — identity
2. Read `USER.md` — about the human
3. Read `memory/YYYY-MM-DD.md` (today + yesterday)
4. If direct Luna chat: also read `MEMORY.md`

## Wiki System

Long-term domain knowledge stored in structured wiki:
- **cards/** — concept cards (one topic per file, ~175 cards)
- **projects/** — project notes (one project per file, ~199 notes)
- Written in whatever language the knowledge was learned in

## Known Issues

1. **MEMORY.md size** — Must be kept under ~200 lines. Larger files waste context tokens and slow startup. Dreaming + daily-review handle pruning.

2. **Daily log accumulation** — Old daily logs (`memory/YYYY-MM-DD.md`) accumulate indefinitely. No automatic cleanup of files older than ~30 days.

3. **memory_search accuracy** — Semantic search can miss exact matches. For known file/section lookups, `memory_get` is more reliable.

4. **Cross-session context loss** — Channel sessions are isolated. Knowledge gained in #work isn't available in #study unless written to shared files.

5. **Security boundary** — MEMORY.md contains personal context. Only loaded in private Luna chats, never in shared contexts (Discord groups).

6. **Wiki discoverability** — With 175+ cards and 199+ project notes, finding the right wiki entry requires good naming or memory_search.
