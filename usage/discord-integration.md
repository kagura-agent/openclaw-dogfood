# Discord Integration

> Primary messaging surface — 20 channels, allowlist mode, streaming enabled.

## Architecture

We migrated from Feishu to Discord on 2026-04-09. Discord is now the sole messaging surface for Kagura × Luna.

### Channel Model
- **One session per channel** — each Discord channel maintains its own OpenClaw session with independent context
- **Cron → channel delivery** — 39 cron jobs deliver output to target channels via `announce`
- **Thread model** — long-running work spawns a Discord thread; one work unit = one thread
- **Pin as kanban** — each channel uses pinned messages as a status board

### 3-Tier Channel Architecture

**Top-level (private comms)**
| Channel | Purpose |
|---|---|
| #kagura-dm | Main comms with Luna. Heartbeat every 30m |
| #luna-private | Luna-only, Kagura doesn't post |

**Daily (routine operations)**
| Channel | Purpose | Cron |
|---|---|---|
| #work | Open source contributions | Hourly :02, 8-20 |
| #study | Research & learning | 2×/h, 8-22 |
| #community | Community ops | Every 2h :40 |
| #general | General | — |

**Project (dedicated spaces)** — 14 channels for specific projects (abti, hermes, memex, chat-infra, memory-eval, shell-project, agent-identity, openclaw-dogfood, toolchain, agent-memes, workshop, moltbook, luna-biz, finance)

## Configuration

### Allowlist Mode
Discord channels operate in allowlist mode — Kagura only responds in explicitly configured channels. New channels must be added to the allowlist.

### Streaming
Partial streaming is enabled for Discord — Kagura's responses appear incrementally as they're generated, rather than waiting for the full response.

### Bot Setup
- **Bot user**: Kagura (`1480846428266823803`)
- **Guild**: `1490989630382931980`
- **Luna's Discord ID**: `1359351419181863053`

## Operational Patterns

### Pin-Based Status Tracking
Key channels use pinned messages for persistent state:
- #kagura-dm: TODO pin, North Star pin, Config pin
- #work: Work status pin
- #study: Study status pin
- #community: Community status pin

The `todo-pin-sync` hook automatically syncs TODO.md to the pinned message in #kagura-dm.

### Channel-Specific Cron
Each project channel has its own cron schedule (see `usage/cron.md`). Cron output is delivered directly to the channel, creating a self-contained workspace.

## Known Issues

1. **No markdown tables in Discord** — Discord doesn't render markdown tables well. Use bullet lists instead.

2. **Link embeds** — Multiple links cause embed spam. Wrap in `<>` to suppress: `<https://example.com>`

3. **Thread management** — Threads accumulate and there's no automatic archival. Manual cleanup needed.

4. **Channel session isolation** — Each channel is a separate session. Context from #work isn't available in #study unless explicitly shared via files.

5. **Rate limits** — Discord API rate limits can hit during high-activity periods (many cron jobs firing close together).
