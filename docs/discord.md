# Discord Setup

This guide covers two methods for connecting Discord to OpenClaw: using the CLI, or using the web dashboard.

---

## Prerequisites

You need a Discord bot token. Here is how to get one:

1. Go to the [Discord Developer Portal](https://discord.com/developers/applications)
2. Click **New Application** and give it a name
3. Go to **Bot** → **Add Bot**
4. Under **Token**, click **Reset Token** and copy it
5. Under **Privileged Gateway Intents**, enable:
   - **Message Content Intent**
   - **Server Members Intent**
6. Go to **OAuth2** → **URL Generator**
   - Check **bot** under Scopes
   - Check **Send Messages** and **Read Message History** under Bot Permissions
7. Copy the generated URL and open it in a browser to invite the bot to your server

---

## Method 1 — CLI

```bash
openclaw channels login --channel discord --token YOUR_BOT_TOKEN
```

Replace `YOUR_BOT_TOKEN` with the token you copied from the Developer Portal.

Verify:

```bash
openclaw status
```

You should see:

```
Discord  │ ON  │ OK  │ connected
```

---

## Method 2 — Dashboard

1. Open `http://localhost:4000` in your browser
2. Click **Channels** → **Add Channel** → **Discord**
3. Paste your bot token into the token field
4. Click **Connect**
5. The status will update to **connected**

---

## How It Works (Mention Gating)

Discord uses **mention gating** by default. This means the bot only responds when someone **@mentions** it directly in a message.

Example:

```
@YourBotName what is the capital of France?
```

The bot will not respond to regular messages in the channel — only to direct @mentions.

### Why Mention Gating?

This prevents the bot from responding to every single message in a busy server. It is intentional behavior.

### Disable Mention Gating (Optional)

If you want the bot to respond to all messages in a specific channel, you can configure it:

```bash
openclaw config set channels.discord.mention_only false
```

Restart the gateway after changing this:

```bash
systemctl --user restart openclaw-gateway.service
```

> **Warning:** Disabling mention gating in a busy server means the bot will try to respond to every message, which can get expensive fast.

---

## Notes

- Keep your bot token secret — never share it or commit it to GitHub
- If you regenerate the token in the Discord portal, you need to reconnect the channel
- The bot must have permission to read and send messages in the channel you are using it in

---

## Related

- [Commands Reference](commands.md)
- [Troubleshooting](troubleshooting.md)
