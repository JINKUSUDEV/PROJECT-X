<div align="center">

# PROJECT X

### NFC relay platform for operator teams

**Android field app · Web operator panel · Dedicated regional relay**

[![Version](https://img.shields.io/badge/Platform-v5.5.17-gold?style=for-the-badge)](platform/version.py)
[![Website](https://img.shields.io/badge/Website-projectx.zip-black?style=for-the-badge)](https://projectx.zip)

**Subscribe:** [projectx.zip/order](https://projectx.zip/order) · **Client login:** your panel URL (provided after onboarding)

**Created by [JINKUSU.DEV](https://jinkusu.dev)** · Support: [@jinkusu](https://t.me/jinkusu)

</div>

---

## What is PROJECT X?

PROJECT X is a subscription platform for **remote NFC relay operations**. Your team runs live card-present flows with two Android devices (or optional Jinkusu field hardware), a **dedicated relay node** in your chosen region, and a **private web panel** to monitor and control everything.

Each subscription is an **isolated workspace**: your relay sessions, devices, cards, payments, and logs are never shared with other clients.

> **Educational & lawful testing only.** See [Legal notice](#legal-notice) at the end of this document.

---

## What you get as a client

| Included | Description |
|----------|-------------|
| **Operator web panel** | Private login (username + password + TOTP). Full dashboard for your tenant only. |
| **Regional relay node** | Assigned when you subscribe (EU, US, APAC, MENA, etc.). Handles live APDU forwarding between phones. |
| **Android APK** | Download from your panel. Install on Reader and Tag devices. |
| **QR provisioning** | Scan once from the panel — host, ports, session, PIN, and TLS settings pushed to the app. |
| **Session scope** | Your tenant token + session number isolate traffic on the shared relay port. |
| **Exports & analytics** | CSV/JSON exports for payments, sessions, cards, and APDU recordings. |
| **Jinkusu support** | Optional custom field hardware integration (ordered separately via [jinkusu.dev](https://jinkusu.dev)). |

You do **not** get platform-wide administration, other clients’ data, or infrastructure outside your assigned workspace.

---

## How it works

```
┌──────────────┐      ┌─────────────────┐      ┌──────────────┐
│ READER phone │ ───► │ Your relay node │ ───► │  TAG phone   │
│ (card side)  │      │ (your region)   │      │ (terminal)   │
└──────────────┘      └────────┬────────┘      └──────────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │  Your web panel     │
                    │  live logs · control│
                    └─────────────────────┘
```

1. **Reader** — reads the NFC card (phone antenna or Jinkusu Device).
2. **Relay** — forwards every APDU command/response in real time through your regional node.
3. **Tag** — emulates the card at the POS or ATM using Host Card Emulation (HCE).
4. **Panel** — you start/stop the relay, watch sessions, review payments, and push config to phones.

Typical round-trip latency is often **under 50 ms** per APDU on a tuned setup (region + stable Wi‑Fi).

---

## Getting started (after subscribe)

1. **Subscribe** — choose monthly or annual plan and region at [projectx.zip/order](https://projectx.zip/order).
2. **Receive credentials** — panel URL, username, password, and TOTP secret (via your onboarding channel).
3. **Log in to the panel** — enable TOTP on first login. This is your private workspace.
4. **Download the APK** — panel → **Download App**.
5. **Provision phones** — panel → **QR Connect** → scan on both devices (Reader + Tag).
6. **Start relay** — panel sidebar → **START**, then run **Relay** mode on both phones with matching session numbers.

The built-in **Guide** in the panel walks through the full workflow step by step.

---

## Android application

The PROJECT X app is the field tool your operators use on Android devices.

### Main capabilities

| Feature | What it does |
|---------|--------------|
| **Relay** | Live NFC bridge — Reader and Tag roles, multi-session support. |
| **Capture / Replay** | Record NFC traffic on-device; replay for analysis (static flows). |
| **Clone** | Clone static NFC tags (access cards). Not for storing live payment cards. |
| **QR Connect** | Scan panel QR to apply host, relay port, session, PIN, TLS. |
| **Remote config** | Panel pushes updates — apps pick up new session/PIN without reinstall. |
| **Panel sync** | Device reports, card metadata, payment results, BLE telemetry upload. |
| **External reader** | USB CCID or Bluetooth Jinkusu / ACR readers as Reader path. |
| **BLE Range** | Live signal strength and proximity monitoring. |
| **Wallet overlays** | Tag screen can show wallet-style UI while HCE runs underneath. |
| **Latency dashboard** | Live APDU round-trip (RTT) on Tag and Reader (v5.5.17+). |

### Relay roles

| Role | Purpose |
|------|---------|
| **Reader** | Reads the physical card or external reader. |
| **Tag** | Presents emulated card to the terminal. |
| **Same session #** | Reader and Tag must use the same session number to pair. |

### Requirements

- NFC-capable Android device(s).
- For full EMV relay features: prepared device with HCE and the PROJECT X Xposed module (see panel **Guide** → rooting section).
- Stable network (Wi‑Fi recommended for field use).

---

## Your operator panel

After login you see **your** panel only. Menu order matches the sidebar:

### 01 · Overview

| Section | Your access |
|---------|-------------|
| **Guide** | Full operator manual — app, panel, workflow, troubleshooting. |
| **Dashboard** | Relay START/STOP/RESTART, connected phones, live log tail, session table, IP blacklist/whitelist, maintenance mode. |
| **Stats** | Bypass success rates and history charts from app-reported transactions. |
| **Live APDU** | Real-time APDU stream; session recorder with JSONL export. |
| **Payments** | POS/ATM payment analytics, filters, CSV export. |
| **Operations** | Alerts, relay health, device tags/teams, remote disconnect, app lock via config push. |
| **System Health** | Relay status, payment pipeline checks, log export, backup visibility. |

### 02 · Data & devices

| Section | Your access |
|---------|-------------|
| **Cards** | Scanned card vault — BIN, scheme, metadata, bypass method, export JSON. |
| **Devices** | Registered app installations — UUID, model, last seen, online status, block/unblock. |
| **BLE Range** | Live Bluetooth telemetry from field apps (RSSI, role, Jinkusu proximity). |

### 03 · Server

| Section | Your access |
|---------|-------------|
| **Config** | Relay/panel ports, public host, Telegram alerts, payment thresholds, viewer password, scheduler, webhooks. |
| **QR Connect** | QR code + remote config push (session, PIN, target device, message to app). |
| **Download App** | Download the published APK for your workspace. |

### Additional tools (from Operations / navigation)

- **Timeline** — chronological session and device events.
- **APDU Replay** — review recorded APDU sessions.
- **APDU Compare** — side-by-side comparison of two sessions.

### Sidebar controls (operator account)

- **START / STOP / RESTART** — control your relay process.
- **Maintenance ON/OFF** — block new connections during maintenance.
- **LOGOUT** — end panel session.

### Viewer role (optional)

If your admin creates a **viewer** password in Config, viewers can read dashboards and download the APK but **cannot** start/stop the relay, change config, or run destructive actions.

---

## Security in your workspace

| Control | Description |
|---------|-------------|
| **TOTP login** | Panel requires username, password, and 6-digit authenticator code. |
| **Tenant isolation** | Dedicated relay assignment and tenant token — no cross-account data. |
| **Session PIN** | Optional PIN for relay session pairing and encryption. |
| **IP blacklist / whitelist** | Restrict which IPs can connect to your relay. |
| **Device UUID block** | Block specific app installations by UUID. |
| **Maintenance mode** | Reject new sessions without dropping active ops mid-flight. |
| **Remote app lock** | Push lock message to field apps from Operations. |
| **E2E relay encryption** | Optional AES encryption derived from session PIN. |
| **TLS** | Encrypted transport to panel and relay when enabled in config. |

---

## Regional relay coverage

Choose a region at subscribe time. Standard options include:

| Region | Example nodes |
|--------|----------------|
| **Europe** | Frankfurt, London |
| **Americas** | Virginia, Oregon, São Paulo |
| **Asia-Pacific** | Singapore, Tokyo |
| **Middle East** | Dubai |

Your traffic stays on the node assigned to your subscription.

---

## Jinkusu Device (optional hardware)

The **Jinkusu Device** is a compact NFC field unit built to order — integrated with the same relay and panel stack:

- 5 cm NFC cap-radius for contactless read/write
- Bluetooth link to the Android app (no manual phone pairing)
- Motion and ambient sensors with live telemetry in **BLE Range**
- Rechargeable battery for extended field use

Configure footprint, colors, and LEDs via the device customizer on the marketing site, then order through [jinkusu.dev](https://jinkusu.dev).

---

## Subscription

| Plan | Price |
|------|-------|
| **Monthly** | $2,000 / month |
| **Annual** | $10,000 / year (save $14,000 vs 12× monthly) |

Both plans include the full client stack: Android app, operator panel, relay assignment, QR provisioning, analytics, and support onboarding.

Order at **[projectx.zip/order](https://projectx.zip/order)**.

---

## Support

| | |
|---|-----|
| **Website** | [projectx.zip](https://projectx.zip) |
| **Subscribe** | [projectx.zip/order](https://projectx.zip/order) |
| **Telegram** | [@jinkusu](https://t.me/jinkusu) |
| **Hardware** | [jinkusu.dev](https://jinkusu.dev) |
| **In-panel help** | **Guide** section after login |

---

## Legal notice

PROJECT X is provided for **educational, research, and lawful testing** purposes only.

By subscribing or using the platform (panel, relay, mobile app, or hardware integration), you acknowledge that:

- You are solely responsible for compliance with laws and regulations in your jurisdiction.
- You assume full liability for how you configure and operate the software.
- The PROJECT X team and JINKUSU.DEV are not responsible for damages or losses arising from unauthorized or negligent use.

If you do not agree, do not subscribe or deploy the platform.

---

<div align="center">

**PROJECT X** · Platform v5.5.17

*Operation project X*

</div>
