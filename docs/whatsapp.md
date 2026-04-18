# WhatsApp Setup

This guide covers two methods for connecting WhatsApp to OpenClaw: using the CLI directly, or using the web dashboard.

---

## Method 1 — CLI (Recommended)

### Step 1 — Start the WhatsApp Login

```bash
openclaw channels login --channel whatsapp
```

A QR code will appear in your terminal.

### Step 2 — Scan the QR Code

On your phone:

1. Open **WhatsApp**
2. Go to **Settings** → **Linked Devices** → **Link a Device**
3. Point your camera at the QR code in the terminal

WhatsApp will pair within a few seconds.

### Step 3 — Verify the Connection

```bash
openclaw status
```

You should see:

```
WhatsApp  │ ON  │ OK  │ linked
```

---

## Method 2 — Dashboard

1. Open your browser and go to `http://localhost:4000` (or whatever port your dashboard runs on)
2. Click **Channels** in the left sidebar
3. Click **Add Channel** → **WhatsApp**
4. A QR code will appear on screen
5. Scan it with WhatsApp on your phone (same steps as above)
6. The status will update to **linked** automatically

---

## Approving Users (Pairing Code)

By default, when someone messages your WhatsApp bot for the first time, they receive a **pairing code**. They need to share that code with you, and you approve them manually.

To approve a user:

```bash
openclaw pairing approve whatsapp <CODE>
```

Replace `<CODE>` with the actual code they received.

> **Why does this exist?** This is a security feature so random people cannot just start chatting with your bot. See [Troubleshooting](troubleshooting.md) for the "gateway pairing required" error.

---

## Notes

- The bot runs as a background systemd service and restarts automatically when you open WSL
- Only one WhatsApp account can be linked at a time
- If the QR code expires, just run the login command again

---

## Related

- [Commands Reference](commands.md)
- [Troubleshooting](troubleshooting.md)
