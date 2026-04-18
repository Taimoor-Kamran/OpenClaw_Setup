# OpenClaw Setup Guide

AI assistant bot connected to WhatsApp, Telegram, Discord and more — powered by Claude AI on WSL Ubuntu.

---

## What is OpenClaw?

OpenClaw is an open-source AI gateway that lets you connect Claude AI to messaging platforms like WhatsApp, Telegram, and Discord. Once set up, anyone can message your bot and get AI-powered responses — without needing to install anything on their phone.

---

## Requirements

| Requirement | Version |
|---|---|
| Windows with WSL2 (Ubuntu) | Ubuntu 22+ |
| Node.js | v18+ |
| npm | v10+ |
| Claude CLI | installed and authenticated |

---

## Channel Status

| Channel | Status | Notes |
|---|---|---|
| WhatsApp | Working | QR code scan required |
| Discord | Working | Mention gating applies |
| Telegram | Blocked in Pakistan | Requires VPN |
| Microsoft Teams | Not tested | — |

---

## Quick Start

```bash
# Install OpenClaw
curl -fsSL https://openclaw.ai/install.sh | bash

# Run onboarding
openclaw onboard --install-daemon
```

Follow the wizard:
- Accept the security warning
- Choose **QuickStart**
- Select **Anthropic** as provider
- Select **Claude CLI** as auth method

Then set the model and restart:

```bash
openclaw config set agents.defaults.model claude-cli/claude-sonnet-4-6
systemctl --user restart openclaw-gateway.service
openclaw status
```

---

## Documentation

- [Full Installation Guide](docs/install.md)
- [WhatsApp Setup](docs/whatsapp.md)
- [Discord Setup](docs/discord.md)
- [Telegram Setup](docs/telegram.md)
- [Commands Reference](docs/commands.md)
- [Troubleshooting](docs/troubleshooting.md)
- [Push to GitHub](docs/github-setup.md)

---

## Who Made This?

This setup was documented by students at a university lab. It is intended to be beginner-friendly for anyone running OpenClaw on WSL for the first time.
