# Hooks & Plugins

> Extending OpenClaw behavior with post-session hooks and plugins.

## Hooks

Hooks are triggered at specific lifecycle points (e.g., `agent_end` — after each agent session completes).

### todo-pin-sync

**Trigger**: `agent_end` (runs after every session)

**What it does**: Syncs workspace files to pinned messages in Discord channels.

**Mappings**:
| File | Pin ID | Channel |
|---|---|---|
| TODO.md | `1491651533492850769` | #kagura-dm |
| wiki/strategy.md | `1491658212816982066` | #kagura-dm |

**Implementation**: TypeScript handler in `~/.openclaw/workspace/hooks/todo-pin-sync/`

**How it works**: After each session, the hook reads the mapped files and updates the corresponding Discord pinned messages with their current content. This keeps the "kanban" pins always in sync.

## Plugins

### Nudge Plugin

**Trigger**: Every 5th `agent_end` event

**What it does**: Injects `NUDGE.md` as a reflection prompt, triggering:
1. **Meme check** — Were there moments that deserved a meme reaction?
2. **Memory triage** — Anything worth logging? Route to the right file:
   - Daily events → `memory/YYYY-MM-DD.md`
   - Reusable lessons → `beliefs-candidates.md`
   - Domain knowledge → `wiki/`
3. **Gradient capture** — Did Luna give feedback? Corrections? Preferences?

**Config**: NUDGE.md in workspace root defines the reflection prompt.

**Why every 5th**: Running reflection after every session would be too frequent and token-expensive. Every 5th strikes a balance between capturing lessons and efficiency.

## Known Issues

1. **Hook execution is silent** — Hooks run in the background. If they fail, there's no visible error in the chat. Check logs for failures.

2. **Pin size limits** — Discord messages have a 2000-character limit. If TODO.md grows beyond that, the pin sync truncates.

3. **Nudge token cost** — Each nudge reflection adds ~500-1000 tokens. With frequent sessions, this adds up.

4. **No hook editing UI** — Hooks are configured via files. No CLI for managing hooks (unlike cron which has `openclaw cron`).
