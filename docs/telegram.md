# Telegram Setup

> **Important for users in Pakistan:** Telegram is blocked by the Pakistan Telecommunication Authority (PTA). You must use a VPN to connect. See the VPN section below before proceeding.

---

## Pakistan VPN Requirement

Telegram's servers are blocked at the ISP level in Pakistan. This affects both:

- The Telegram app on your phone
- OpenClaw's ability to connect to Telegram's API from WSL

**You need a VPN on both your PC (WSL) and your phone** for this to work.

### Recommended Free VPNs

| VPN | Platform | Notes |
|---|---|---|
| Windscribe | Windows / Android | 10 GB/month free |
| ProtonVPN | Windows / Android | Unlimited free tier (slower) |
| 1.1.1.1 (WARP) | Windows / Android | Fast, but may not work for all ISPs |

### Enable VPN in WSL

Once your Windows VPN is connected, WSL2 inherits the network — you do not need to set up a separate VPN inside WSL. Just connect the VPN on Windows first, then proceed with the steps below.

---

## Prerequisites

You need a Telegram bot token from BotFather:

1. Open Telegram (with VPN on) and search for `@BotFather`
2. Send `/newbot`
3. Follow the prompts to name your bot
4. BotFather will give you a token like: `123456789:ABCDEFGhijklmnop`
5. Copy that token

---

## Method 1 — CLI

```bash
openclaw channels login --channel telegram --token YOUR_BOT_TOKEN
```

Replace `YOUR_BOT_TOKEN` with the token from BotFather.

Verify:

```bash
openclaw status
```

You should see:

```
Telegram  │ ON  │ OK  │ connected
```

---

## Method 2 — Dashboard

1. Open `http://localhost:4000` in your browser
2. Click **Channels** → **Add Channel** → **Telegram**
3. Paste your bot token
4. Click **Connect**
5. Status updates to **connected**

---

## Testing the Bot

1. Open Telegram and search for your bot by its username
2. Send `/start`
3. The bot should reply

If it does not reply, check that:
- Your VPN is still connected
- The gateway service is running (`openclaw status`)
- The token is correct

---

## Notes

- The bot token is tied to a specific Telegram bot — do not share it publicly
- If you stop your VPN mid-session, the Telegram channel will disconnect and you will need to restart the gateway
- Unlike WhatsApp, Telegram does not require QR code scanning — the token is enough

---

## Related

- [Commands Reference](commands.md)
- [Troubleshooting](troubleshooting.md)
