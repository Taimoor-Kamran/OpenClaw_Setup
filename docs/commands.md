# Commands Reference

Quick reference for all useful OpenClaw CLI commands.

---

## Installation & Setup

| Command | What it does |
|---|---|
| `curl -fsSL https://openclaw.ai/install.sh \| bash` | Install OpenClaw |
| `openclaw onboard --install-daemon` | Run the setup wizard and install daemon |
| `openclaw --version` | Check installed version |

---

## Gateway Management

| Command | What it does |
|---|---|
| `openclaw status` | Show gateway and channel status |
| `systemctl --user start openclaw-gateway.service` | Start the gateway |
| `systemctl --user stop openclaw-gateway.service` | Stop the gateway |
| `systemctl --user restart openclaw-gateway.service` | Restart the gateway |
| `systemctl --user status openclaw-gateway.service` | Check if the daemon is running |

---

## Configuration

| Command | What it does |
|---|---|
| `openclaw config set gateway.mode local` | Set gateway to local mode |
| `openclaw config set agents.defaults.model MODEL` | Set the default AI model |
| `openclaw config get agents.defaults.model` | Check current model setting |
| `openclaw config set channels.discord.mention_only false` | Disable Discord mention gating |

### Model Names

| Model | Config value |
|---|---|
| Claude Sonnet 4.6 | `claude-cli/claude-sonnet-4-6` |
| Claude Haiku 4.5 | `claude-cli/claude-haiku-4-5` |
| Claude Opus 4.7 | `claude-cli/claude-opus-4-7` |

---

## Channel Management

| Command | What it does |
|---|---|
| `openclaw channels list` | List all connected channels |
| `openclaw channels login --channel whatsapp` | Connect WhatsApp (shows QR code) |
| `openclaw channels login --channel discord --token TOKEN` | Connect Discord |
| `openclaw channels login --channel telegram --token TOKEN` | Connect Telegram |
| `openclaw channels logout --channel whatsapp` | Disconnect a channel |

---

## Pairing (User Approval)

| Command | What it does |
|---|---|
| `openclaw pairing list` | Show pending pairing requests |
| `openclaw pairing approve whatsapp CODE` | Approve a user by their pairing code |
| `openclaw pairing deny whatsapp CODE` | Deny a pairing request |

---

## Logs & Debugging

| Command | What it does |
|---|---|
| `journalctl --user -u openclaw-gateway.service -f` | Live logs from the gateway |
| `journalctl --user -u openclaw-gateway.service -n 100` | Last 100 lines of logs |
| `openclaw logs` | View OpenClaw's own log output |

---

## Tips

- After any `openclaw config set` change, always run `systemctl --user restart openclaw-gateway.service`
- Use `openclaw status` to confirm channels are connected after making changes
- If something breaks, check logs with `journalctl --user -u openclaw-gateway.service -n 50`
