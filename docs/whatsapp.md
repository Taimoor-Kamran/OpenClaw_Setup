# WhatsApp Setup

## Step 1 — Connect WhatsApp
```bash
openclaw channels login --channel whatsapp
```
A QR code will appear in the terminal.

## Step 2 — Scan QR Code
On your phone:
- Open WhatsApp
- Go to Settings → Linked Devices → Link a Device
- Scan the QR code

## Step 3 — Verify Connection
```bash
openclaw status
```
You should see:
WhatsApp │ ON │ OK │ linked

## Step 4 — Approve Other Users
When someone messages your bot they get a pairing code.
Approve them with:
```bash
openclaw pairing approve whatsapp <CODE>
```

## Notes
- Bot runs as a background systemd service
- Automatically restarts when WSL reopens
- Default DM policy is "pairing" for security
