# Memory Dreaming

> Automated memory consolidation — promotes daily logs into long-term memory.

## What It Is

OpenClaw's dreaming system runs during off-hours to process recent daily memory logs (`memory/YYYY-MM-DD.md`) and promote significant entries into `MEMORY.md` (long-term memory). It mimics biological memory consolidation during sleep.

## Configuration

Dreaming is configured in OpenClaw's config:
- **Schedule**: Runs as a cron job at 3:30 AM (`Memory Dreaming Promotion`)
- **Target**: `main` session (unique — most crons use `isolated`)
- **Modes**: `light` + `REM` (both enabled)

### Dreaming Modes
- **Light sleep**: Quick scan of recent daily logs, extracts key facts and events
- **REM sleep**: Deeper processing — finds patterns, connections, and promotes insights to MEMORY.md

## Our Setup

- **Cron**: `cron 30 3 * * * @ Asia/Shanghai`
- **Target**: main (needs write access to MEMORY.md)
- **Artifacts stored in**: `memory/dreaming/`

### Memory Lifecycle
1. **During sessions**: Events logged to `memory/YYYY-MM-DD.md`
2. **3:30 AM dreaming**: Scans recent daily logs → promotes to `MEMORY.md`
3. **MEMORY.md cap**: Kept under ~200 lines — older entries pruned or archived
4. **Wiki promotion**: Domain knowledge extracted to `wiki/cards/` or `wiki/projects/`

## Actual Effects

- MEMORY.md stays current with important events without manual curation
- Cross-day patterns get surfaced (e.g., "Luna mentioned X three times this week")
- Reduces daily log noise — only significant items survive to long-term memory

## Known Issues

1. **Main target requirement** — Dreaming must run as `main` target to write MEMORY.md. If it ran as `isolated`, it couldn't persist changes properly.

2. **MEMORY.md bloat** — Without active pruning, MEMORY.md grows past its useful size. The dreaming system handles some pruning but manual review (in daily-review at 3:15 AM) catches what it misses.

3. **No selective replay** — Can't tell dreaming to focus on specific topics. It processes everything in recent daily logs equally.

4. **Dreaming artifacts** — The `memory/dreaming/` directory accumulates artifacts. No automatic cleanup.
