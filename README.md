This is my public fork of <a href="https://github.com/moazbuilds/claudeclaw/">moazbuilds/claudeclaw</a>, a lightweight, open-source OpenClaw variant built into Claude Code. It turns your Claude Code into a personal assistant that never sleeps. It runs as a background daemon, executing tasks on a schedule, responding to messages on Telegram, and integrating with any service you need.

## How does this vary from upstream?

I started this fork to submit pull requests against upstream when I realized that some other PRs are also awaiting integration that I didn't want to wait for. I also plan to adjust the project more to my specific needs and learn along the way. Current differences:
- **IDENTITY.md** in the agent's project directory is elevated to system prompt level at every invocation; not using `CLAUDE.md` for persisting assistant's identity
- **Telegram only**
- **No fallback model**, resort to *extra usage* for paid Claude plans instead
- **No audio transciption** (should be handled via skills or MCP)
- **File attachment support**
- **Reporting Claude errors**
- **Fixes** empty prompt templates in system prompt
- **Fixes** `HEARTBEAT_OK` from leaking into Telegram channel

## Getting Started

I suggest installing the assistant only in local scope inside its own workspace.

1. Create a workspace
```bash
mkdir workspace && cd workspace
```

2. Install marketplace and plugin with local scope
```bash
claude plugin marketplace add christian-drescher/claudeclaw --scope local
claude plugin install claudeclaw --scope local
```
Then open a Claude Code session and run:
```
/claudeclaw:start
```
The setup wizard walks you through model, heartbeat, Telegram, and security, then your daemon is live with a web dashboard.

### First Steps
- Verify `IDENTITY.md`, edit `CLAUDE.md` for workspace structure
- Consider moving auto-memory into `memory/` in the agent's workspace; set <a href="https://code.claude.com/docs/en/memory#storage-location">autoMemoryDirectory</a> in `.claude/settings.local.json`

### Useful tools/skills (Linux)
- Web search via the Brave Search API
- Web browsing via `playwright` in docker
- Calendar access via `vdirsyncer` and `khal`
- Shared notes via `obsidian-headless`
- Smart home integration via `mosquitto` (MQTT client)
- Integration with other cloud LLMs or image generation via openrouter
- Local image generation via Stable Diffusion (**TODO** move to *SD.next*)
- Documentation for popular third-party libraries, SDK or API, via `chub`

## Update

Change directory into the assistant's workspace and then

```bash
claude plugin marketplace update claudeclaw
claude plugin update claudeclaw@claudeclaw --scope local
```

## Features

### Automation
- **Heartbeat:** Periodic check-ins with configurable intervals, quiet hours, and editable prompts.
- **Cron Jobs:** Timezone-aware schedules for repeating or one-time tasks with reliable execution.

### Communication
- **Telegram:** Text, image, and file attachment support.
- **Time Awareness:** Message time prefixes help the agent understand delays and daily patterns.

### Reliability and Control
- **Web Dashboard:** Manage jobs, monitor runs, and inspect logs in real time.
- **Security Levels:** Four access levels from read-only to full system access.
- **Model Selection:** Switch models based on your workload.

## Future Work / TODO
- Memory get's cluttered over time. Define a skill to clean this up.
- Find out how this relates to <a href="https://code.claude.com/docs/en/channels">channels</a> in Claude Code (currently in research preview)