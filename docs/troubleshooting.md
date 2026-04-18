# Troubleshooting

Common errors and fixes encountered during setup.

---

## Error: "Gateway pairing required"

**Symptom:** A user messages your WhatsApp/Discord/Telegram bot and receives a message like:

```
Gateway pairing required. Please contact the bot owner with this code: XXXX-XXXX
```

**What is happening:** OpenClaw's default security policy requires the bot owner to manually approve each new user before they can interact with the AI. The user got a pairing code, but you have not approved them yet.

**Fix:**

1. Ask the user to share the pairing code they received
2. Run:

```bash
openclaw pairing approve whatsapp XXXX-XXXX
```

Replace `whatsapp` with `discord` or `telegram` depending on which channel they are using.

3. The user can now chat with the bot

**Check for pending requests:**

```bash
openclaw pairing list
```

---

## Error: Telegram not connecting (Pakistan)

**Symptom:** The Telegram channel login command hangs or gives a connection error. You are in Pakistan.

**What is happening:** Telegram is blocked by the PTA at the ISP level.

**Fix:**

1. Connect a VPN on Windows before running any Telegram commands
2. WSL2 shares the Windows network, so once the VPN is on in Windows, WSL will also route through it
3. Run the login command again after the VPN is connected

See [Telegram Setup](telegram.md) for recommended free VPNs.

---

## Discord Bot Not Responding

**Symptom:** You message in Discord but the bot does not reply.

**Possible causes and fixes:**

**1. Bot was not @mentioned**

Discord uses mention gating by default. Try:

```
@YourBotName hello
```

**2. Bot is in the channel but lacks permissions**

Go to your Discord server settings → Roles → check that your bot role has **Read Messages** and **Send Messages** in that channel.

**3. Gateway is not running**

```bash
openclaw status
```

If the gateway shows as stopped, restart it:

```bash
systemctl --user restart openclaw-gateway.service
```

**4. Token is wrong or expired**

Go to the Discord Developer Portal, regenerate the token, and reconnect:

```bash
openclaw channels logout --channel discord
openclaw channels login --channel discord --token NEW_TOKEN
```

---

## WhatsApp QR Code Expired

**Symptom:** The QR code appeared but you didn't scan it in time. It now shows an error or a blank screen.

**Fix:** Just run the login command again — it generates a fresh QR code each time:

```bash
openclaw channels login --channel whatsapp
```

---

## WhatsApp Shows "linked" But Bot Doesn't Reply

**Symptom:** `openclaw status` shows WhatsApp as linked, but messages don't get a response.

**Fix:**

1. Check if the gateway is actually running:

```bash
systemctl --user status openclaw-gateway.service
```

2. Check logs for errors:

```bash
journalctl --user -u openclaw-gateway.service -n 50
```

3. Check if your model is set correctly:

```bash
openclaw config get agents.defaults.model
```

It should return something like `claude-cli/claude-sonnet-4-6`. If it is empty, set it:

```bash
openclaw config set agents.defaults.model claude-cli/claude-sonnet-4-6
systemctl --user restart openclaw-gateway.service
```

---

## Gateway Service Not Starting After WSL Reboot

**Symptom:** After closing and reopening WSL, `openclaw status` shows the gateway as stopped.

**Fix:** The daemon should auto-start, but if it doesn't:

```bash
systemctl --user start openclaw-gateway.service
```

To ensure it always starts on login:

```bash
systemctl --user enable openclaw-gateway.service
```

---

## "openclaw: command not found"

**Symptom:** After installing, the terminal can't find the `openclaw` command.

**Fix:** Close the terminal and open a new one. The installer adds OpenClaw to your PATH, but the current session doesn't pick it up until you restart.

If it still doesn't work after restarting:

```bash
source ~/.bashrc
```

or

```bash
source ~/.zshrc
```

---

## General Debug Steps

When something is broken and you're not sure why:

```bash
# 1. Check overall status
openclaw status

# 2. Check daemon logs
journalctl --user -u openclaw-gateway.service -n 100

# 3. Restart everything
systemctl --user restart openclaw-gateway.service

# 4. Check config
openclaw config get agents.defaults.model
```

If you're still stuck, check the [OpenClaw GitHub Issues](https://github.com/openclaw-ai/openclaw) for similar problems.
