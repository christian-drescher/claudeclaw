This is my public fork of <a href="https://github.com/moazbuilds/claudeclaw/">moazbuilds/claudeclaw</a>, a lightweight, open-source OpenClaw variant built into Claude Code. It turns your Claude Code into a personal assistant that never sleeps. It runs as a background daemon, executing tasks on a schedule, responding to messages on Telegram, and integrating with any service you need.

## How does this vary from upstream?

I started this fork to submit a pull request against upstream when I realized that some other PRs are also awaiting integration that I didn't want to wait for.  I also plan to adjust the project more to my specific needs and learn along the way. Current differences:
- **Telegram only**
- **No fallback model**, resort to *extra usage* for paid Claude plans instead
- **No audio transciption** (should be handled via skills or MCP)
- **File attachment support**
- **Reporting Claude errors**

## Getting Started

```bash
claude plugin marketplace add christian-drescher/claudeclaw
claude plugin install claudeclaw
```
Then open a Claude Code session and run:
```
/claudeclaw:start
```
The setup wizard walks you through model, heartbeat, Telegram, and security, then your daemon is live with a web dashboard.

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

## Next steps
- Learn more about the plugin's architecture, and use of `prompts/`
- Consider adding **file response**; see PR<a href="https://github.com/moazbuilds/claudeclaw/pull/23">23</a>
- Find out how this relates to <a href="https://code.claude.com/docs/en/channels">channels</a> in Claude Code (currently in research preview)