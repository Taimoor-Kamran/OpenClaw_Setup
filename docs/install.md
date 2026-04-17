# Installation Guide

## Step 1 — Install OpenClaw
```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

## Step 2 — Set Gateway Mode
```bash
openclaw config set gateway.mode local
```

## Step 3 — Run Onboarding Wizard
```bash
openclaw onboard --install-daemon
```
Follow the wizard:
- Accept security warning
- Choose QuickStart
- Select Anthropic as provider
- Select Claude CLI as auth method
- Skip channel setup for now

## Step 4 — Set Model
```bash
openclaw config set agents.defaults.model claude-cli/claude-sonnet-4-6
```

## Step 5 — Restart Gateway
```bash
systemctl --user restart openclaw-gateway.service
```

## Step 6 — Verify
```bash
openclaw status
```
