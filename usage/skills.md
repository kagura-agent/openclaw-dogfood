# Skills System

> 11 custom + 60+ built-in skills, loaded via system prompt injection.

## How Skills Work

Skills are structured directories containing a `SKILL.md` file that gets injected into the agent's system prompt. When a task matches a skill's description, the agent reads the SKILL.md and follows its instructions.

### Skill Loading
- **Built-in skills**: Shipped with the OpenClaw npm package (`~/.nvm/versions/node/v24.14.1/lib/node_modules/openclaw/skills/`)
- **Custom skills**: Loaded from workspace via `skills.load.extraDirs` config pointing to `~/.openclaw/workspace/skills/`
- **Auto-scan**: OpenClaw scans skill directories at startup and injects descriptions into the system prompt
- **Lazy loading**: Only the matching skill's SKILL.md is read when a task triggers it

## Custom Skills (11)

| Skill | Purpose |
|---|---|
| agent-memes | Send reaction memes in chat (Discord, Feishu, Telegram) |
| discord-ops | Discord server management (channels, pins, allowlists) |
| flowforge | Workflow engine — mandatory for work/study/reflect tasks |
| gogetajob | Open source contribution CLI & workflow |
| kagura-storyteller | Creative writing, journal entries, podcasts |
| memos-memory-guide | Guide for writing memory entries |
| pulse-todo | Task management with pin sync |
| self-portrait | Identity expression and self-construction |
| team-lead | Multi-agent team management (dev + QA) |

### Custom Skill Location
All in `~/.openclaw/workspace/skills/<skill-name>/SKILL.md`

## Built-in Skills (60+)

Key ones we use regularly:
| Skill | Usage |
|---|---|
| github | GitHub ops via gh CLI |
| coding-agent | Delegate coding to Claude Code / Codex / Pi |
| gh-issues | Fetch issues, spawn fix agents, open PRs |
| clawhub | Skill marketplace — search, install, publish |
| session-logs | Search own session history via jq |
| weather | Weather via wttr.in |
| healthcheck | Host security hardening |
| skill-creator | Create and audit skills |
| tmux | Remote-control tmux sessions |
| taskflow | Durable task flow substrate |
| video-frames | Extract frames from video |
| web_fetch | (built-in tool, not a skill) |

Full list includes: 1password, apple-notes, bear-notes, blucli, camsnap, discord, gemini, gog, himalaya, notion, obsidian, openai-whisper, sag (TTS), slack, spotify-player, trello, voice-call, wacli, and many more.

## ClawHub

ClawHub (`clawhub.com`) is the skill marketplace:
```bash
clawhub search <query>     # Find skills
clawhub install <skill>    # Install a skill
clawhub publish <dir>      # Publish a skill
clawhub update <skill>     # Update to latest
```

We've published several custom skills to ClawHub for community use.

## Known Issues

1. **System prompt bloat** — All skill descriptions are injected into every session's system prompt. With 60+ skills, this adds significant token overhead. Only the description is injected though, not the full SKILL.md.

2. **Skill conflicts** — When multiple skills could match a task, the agent picks the "most specific" one. This heuristic sometimes picks wrong.

3. **No skill versioning in workspace** — Custom skills in workspace/ have no version tracking beyond git. ClawHub skills have versions.

4. **Skill loading order** — Custom skills override built-in skills with the same name. This is useful but can cause confusion.
