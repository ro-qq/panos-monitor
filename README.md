# PAN-OS Monitor

## 语言/Language
-  [中文](#中文)
-  [English](#english)

---

**A Chrome Extension for Real-Time Palo Alto Networks NGFW Monitoring**

> 一款用于实时监控 Palo Alto Networks 下一代防火墙的 Chrome 扩展程序

[![Version](https://img.shields.io/badge/version-0.6.89-FFCB06?style=flat-square)](https://github.com/)
[![Manifest](https://img.shields.io/badge/Manifest-V3-blue?style=flat-square)](https://developer.chrome.com/docs/extensions/mv3/)
[![PAN-OS](https://img.shields.io/badge/PAN--OS-11.x%20%2F%2012.x-orange?style=flat-square)](https://docs.paloaltonetworks.com/)
[![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)](LICENSE)

---

## 中文介绍

### 项目简介

PAN-OS Monitor 是一款基于 Chrome MV3 架构的浏览器扩展程序，通过 PAN-OS XML API 直接连接 Palo Alto Networks 防火墙，实时采集并可视化设备的健康状态与性能数据。

**无需服务器、无需数据库、无需任何中间件**，安装扩展即可使用。

### 功能概览

| 菜单 | 内容 |
|------|------|
| **概览** | MP CPU、DP CPU、内存、会话数、吞吐量（kbps/cps/pps）实时卡片 + 趋势折线图 |
| **接口详情** | 物理/逻辑接口速率、包速、错误、丢包趋势；物理接口底层硬件统计（25+ 指标，含悬浮说明） |
| **会话详情** | 按状态分类会话数；SSL 解密统计；Ingress Backlog；VSYS 会话分布 |
| **资源详情** | MP CPU 各分量仪表盘；DP CPU 按 5 个时间粒度的历史趋势图；磁盘空间 |
| **计数器详情** | 全量 `show counter global` 数据；变化高亮；每条计数器的值与速率趋势图 |
| **GlobalProtect** | GP 版本信息；实时在线用户列表 |

### 安装方式

1. 下载并解压本仓库
2. 打开 Chrome → `chrome://extensions`
3. 开启右上角**开发者模式**
4. 点击**加载已解压的扩展程序** → 选择 `panos-monitor` 文件夹
5. 点击 Chrome 工具栏中的图标打开 Dashboard

### 添加防火墙

**方法一（推荐）：自动识别** — 在 Chrome 中打开防火墙管理页面并登录，扩展自动添加设备。

**方法二：手动添加** — 点击「Add Firewall」，输入防火墙 HTTPS 地址和 API Key。

> **自签名证书：** 首次添加前，先在 Chrome 中打开防火墙地址，手动接受证书警告。

---

## English

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

### Key Technical Details

- **Chrome MV3 Service Worker** — no persistent background page; polling driven by Chrome Alarms API (every 5 minutes)
- **Content Script Proxy** — bypasses Private Network Access (PNA) restrictions for self-signed certificate devices
- **Auto-detection** — open your firewall's management page, log in, and the extension automatically captures the API key and adds the device
- **Multi-device** — monitor multiple firewalls simultaneously
- **Dual theme** — light and dark mode; Chinese/English UI
- **Zero dependencies** — pure vanilla JS, no npm, no build step

### Supported Devices

- PA-220, PA-440, PA-820, PA-850
- PA-3220, PA-3250, PA-3260
- PA-5220, PA-5250, PA-5260, PA-5450
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

### Data Collection Commands

| Function | PAN-OS Command |
|----------|---------------|
| System info | `show system info` |
| MP CPU & Memory | `show system resources` |
| DP CPU & Resources | `show running resource-monitor` |
| Session stats | `show session info` |
| Sessions by state | `show session all filter state <state> count yes` |
| Interface data | `show interface all` |
| Interface counters | `show counter interface all` |
| Global counters | `show counter global` |
| Jobs | `show jobs all` |
| GlobalProtect | `show global-protect-gateway current-user` |
| SSL decrypt stats | `show system state filter sw.mprelay.s1.dp0.stats.session` |
| Port hardware stats | `show system state filter sys.s1.p{N}.detail` |
| Disk space | `show system disk-space` |
| Licenses | `request license info` |

### File Structure

```
panos-monitor/
├── manifest.json          # Extension config (MV3)
├── background.js          # Service Worker: polling, storage, message routing
├── contentscript.js       # Injected into firewall pages: API proxy + auto-login
├── dashboard.html/js      # Main UI: 6-tab monitoring dashboard
├── i18n.js                # Internationalization (EN/ZH) + theme management
├── options.html/js        # Extension options page
├── lib/
│   └── panosapi.js        # PAN-OS XML API client (all monitoring functions)
├── rules/
│   └── panos_api.json     # declarativeNetRequest rules for header modification
├── icons/                 # Extension icons (16/48/128px)
├── PROJECT_REFERENCE.html # Full technical documentation
├── LICENSE                # MIT License
└── README.md              # This file
```

---

## Screenshots

> *(Add screenshots here)*

---

## Disclaimer

This project is an independent open-source tool and is not affiliated with, endorsed by, or officially supported by Palo Alto Networks.

> 本项目为独立开源工具，与 Palo Alto Networks 官方无关。

---

## License

MIT License — see [LICENSE](LICENSE) for details.
