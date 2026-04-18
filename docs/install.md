# Full Installation Guide

This guide walks you through installing OpenClaw from scratch on WSL2 (Ubuntu). Follow every step in order.

---

## Prerequisites

Before you begin, make sure you have:

- Windows 10/11 with WSL2 installed
- Ubuntu 22.04 or 24.04 running inside WSL2
- Node.js v18 or higher (`node --version` to check)
- npm v10 or higher (`npm --version` to check)
- Claude CLI installed and authenticated (`claude --version` to check)

If you do not have Claude CLI yet, install it first:

```bash
npm install -g @anthropic-ai/claude-code
claude
```

---

## Step 1 — Install OpenClaw

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

This downloads and installs the `openclaw` binary. After it finishes, close and reopen your terminal so the PATH updates.

Verify the install:

```bash
openclaw --version
```

---

## Step 2 — Set Gateway Mode to Local

```bash
openclaw config set gateway.mode local
```

This tells OpenClaw to run as a local gateway on your machine instead of connecting to a remote server.

---

## Step 3 — Run the Onboarding Wizard

```bash
openclaw onboard --install-daemon
```

The wizard will guide you step by step. When prompted:

1. **Accept** the security warning
2. Choose **QuickStart** (not manual setup)
3. Select **Anthropic** as the AI provider
4. Select **Claude CLI** as the authentication method
5. **Skip** channel setup for now (we set up channels separately)

The wizard will also install a systemd daemon so OpenClaw starts automatically.

---

## Step 4 — Set the Default Model

```bash
openclaw config set agents.defaults.model claude-cli/claude-sonnet-4-6
```

This sets Claude Sonnet 4.6 as the default AI model for your bot.

---

## Step 5 — Restart the Gateway Service

```bash
systemctl --user restart openclaw-gateway.service
```

Whenever you change config, always restart the service so the changes take effect.

---

## Step 6 — Verify Everything is Running

```bash
openclaw status
```

You should see something like:

```
Gateway   │ running
Channels  │ none connected
```

If you see `Gateway: running`, the install worked. Now go set up your first channel.

---

## Next Steps

- [WhatsApp Setup](whatsapp.md)
- [Discord Setup](discord.md)
- [Telegram Setup](telegram.md)
