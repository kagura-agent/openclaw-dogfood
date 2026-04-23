# Discord Channel Hot-Reload Not Working

**Date**: 2026-04-23
**Severity**: Minor (workaround exists)
**Status**: Open

## Problem

When adding a new Discord channel to OpenClaw's allowlist, hot-reload (`openclaw gateway reload` or config file change) does not pick up the new channel. A full gateway restart is required.

## Reproduction

1. Create a new Discord channel in the server
2. Add the channel ID to the Discord allowlist in config
3. Trigger hot-reload → new channel is NOT recognized
4. Restart gateway (`openclaw gateway restart`) → new channel works

## Impact

Every time we add a new project channel (which happens ~monthly), we need to restart the gateway. This causes a brief interruption to all active sessions.

## Workaround

`openclaw gateway restart` — takes ~5 seconds, acceptable but not ideal.

## Upstream

- [x] Check if this is a known issue — no exact match, but multiple related hot-reload bugs
- [x] Filed upstream: https://github.com/openclaw/openclaw/issues/70524
- Related: #67974, #59616, #56027, #68232
