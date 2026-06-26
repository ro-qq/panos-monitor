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

### Features

| Tab | What you get |
|-----|-------------|
| **Overview** | MP CPU, DP CPU, memory, sessions, throughput (kbps/cps/pps) cards + trend charts |
| **Interfaces** | Physical & logical interface rates, packet counters, errors, drops; hardware-level port statistics (25+ counters with tooltips) |
| **Session Details** | Session counts by state (active/closed/closing/discard/initial/opening), SSL decryption stats, ingress backlogs, per-vsys session distribution |
| **Resources** | MP CPU breakdown gauges (us/sy/id/wa/hi/si/ni/st); DP CPU trends at 5 time granularities (second/minute/hour/day/week); disk space usage |
| **Counter Details** | Full `show counter global` output; change highlighting; value & rate trend charts per counter |
| **GlobalProtect** | GP version info; live user list (username, computer, client IP, VPN IP, login time) |

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
Open your firewall's management URL in Chrome, log in with username/password. The extension automatically detects the login, extracts the API key, and adds the device.

**Method 2 — Manual:**
Click **Add Firewall** in the dashboard sidebar, enter the HTTPS URL and your API Key.

> **Self-signed certificates:** Before adding, open the firewall URL in Chrome and accept the certificate warning ("Advanced → Proceed"). This is required only once per device.

---

## Screenshots

> <img width="2838" height="1770" alt="image" src="https://github.com/user-attachments/assets/0ace37b5-c419-490e-8b4a-0d6f9692bfdb" />


---

## Disclaimer

This project is an independent open-source tool and is not affiliated with, endorsed by, or officially supported by Palo Alto Networks.

> 本项目为独立开源工具，与 Palo Alto Networks 官方无关。

---

## License

MIT License — see [LICENSE](LICENSE) for details.
