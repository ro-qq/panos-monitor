# PAN-OS Monitor

---

**A Chrome Extension for Palo Alto Networks NGFW Monitoring**

[![Version](https://img.shields.io/badge/version-0.6.89-FFCB06?style=flat-square)](https://github.com/)
[![Manifest](https://img.shields.io/badge/Manifest-V3-blue?style=flat-square)](https://developer.chrome.com/docs/extensions/mv3/)
[![PAN-OS](https://img.shields.io/badge/PAN--OS-11.x%20%2F%2012.x-orange?style=flat-square)](https://docs.paloaltonetworks.com/)
[![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)](LICENSE)

---

## Downloads
Download the latest release from [release page](https://github.com/ro-qq/panos-monitor/releases).

---

**Read this in other languages: [简体中文](README.zhcn.md),[English](README.en.md)**

---

### Overview

PAN-OS Monitor is a Chrome MV3 browser extension that connects directly to Palo Alto Networks firewalls via the PAN-OS XML API and visualizes real-time health and performance data — **no server, no database, no middleware required**.

---

## 界面

> <img width="1513" height="855" alt="image" src="https://github.com/user-attachments/assets/9a1727aa-ac9b-42fe-ab09-903668652d9d" />
> <img width="1238" height="858" alt="image" src="https://github.com/user-attachments/assets/e90431cf-69b6-42ac-83c9-65d68625449e" />


---

### Features

| Tab | What you get |
|-----|-------------|
| **Overview** | Memory, active sessions, throughput (kbps/cps/pps) cards + trend charts; auto-refreshes every 5 min |
| **Interfaces** | Physical & logical interface rate trends; hardware-level port statistics (25+ counters with diagnostic tooltips) |
| **Session Details** | Session counts by state (active/closed/closing/discard/initial/opening), CPS trend, policy block rate, per-vsys distribution |
| **Resources** | CPU performance gauges (us/sy/id/wa/hi/si/ni/st); DP CPU trends at 5 time granularities (second/minute/hour/day/week); core service process performance chart; disk space |
| **Counter Details** | Full `show counter global` output; change highlighting; value & rate trend charts per counter |
| **GlobalProtect** | GP version info; live user list (username, computer, client IP, VPN IP, login time) |

### Key Technical Details

- **Chrome MV3 Service Worker** — no persistent background page; polling driven by Chrome Alarms API (every 5 minutes)
- **Tiered polling** — system info refreshes every 30 min; performance data every 5 min; GP skipped automatically if not configured
- **Per-tab partial refresh** — each tab's refresh button only fetches data relevant to that view
- **Content Script Proxy** — bypasses Private Network Access (PNA) restrictions for self-signed certificate devices
- **Auto-detect** — open your firewall's management page and log in; the extension automatically captures the API key and adds the device
- **Update notifications** — checks GitHub weekly for new releases; notifies via desktop notification and sidebar banner
- **Dual theme** — light and dark mode; Chinese/English UI
- **Zero dependencies** — pure vanilla JS, no npm, no build step

### Supported Devices

- Any PAN-OS 10.x / 11.x / 12.x device with management API access

### Installation (Developer Mode)

1. Download and unzip this repository
2. Open Chrome → `chrome://extensions`
3. Enable **Developer mode** (top right toggle)
4. Click **Load unpacked** → select the `panos-monitor` folder
5. Click the PAN-OS Monitor icon in the Chrome toolbar

### Adding a Firewall

**Method 1 — Auto-detect (recommended):**
Open your firewall's management URL in Chrome and log in. The extension automatically detects the login, extracts the API key, and adds the device.

**Method 2 — Manual:**
Click **Add Firewall** in the dashboard sidebar, enter the HTTPS URL and API Key.

> **Self-signed certificates:** Open the firewall URL in Chrome first and accept the certificate warning. Required only once per device.

### Data Collection

| Data | Frequency |
|------|-----------|
| Performance (CPU, sessions, interfaces, counters, GP) | Every 5 minutes (auto) |
| System info | Every 30 minutes (auto) |
| Disk space | Manual refresh only |
| Hardware port statistics | On demand (click interface row) |
| GitHub update check | Weekly |

All data is processed locally. No data is uploaded to any external server.
