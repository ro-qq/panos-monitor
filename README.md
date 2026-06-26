# PAN-OS Monitor

---

> 一款用于监控 Palo Alto Networks 下一代防火墙的 Chrome 扩展程序

[![Version](https://img.shields.io/badge/version-0.6.89-FFCB06?style=flat-square)](https://github.com/)
[![Manifest](https://img.shields.io/badge/Manifest-V3-blue?style=flat-square)](https://developer.chrome.com/docs/extensions/mv3/)
[![PAN-OS](https://img.shields.io/badge/PAN--OS-11.x%20%2F%2012.x-orange?style=flat-square)](https://docs.paloaltonetworks.com/)
[![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)](LICENSE)

---

## Downloads
Download the latest release from [release page](https://github.com/ro-qq/panos-monitor/releases).

---

**其他语言版本:  [English](README.en.md), [简体中文](README.zhcn.md)**

### 项目简介

PAN-OS Monitor 是一款基于 Chrome MV3 架构的浏览器扩展程序，通过 PAN-OS XML API 直接连接 Palo Alto Networks 防火墙，实时采集并可视化设备的健康状态与性能数据。**无需服务器、无需数据库、无需任何中间件**，安装扩展即可使用。

### 功能概览

| 菜单 | 内容 |
|------|------|
| **概览** | 内存、活跃会话、吞吐量（kbps/cps/pps）实时卡片 + 趋势图；每 5 分钟自动更新 |
| **接口详情** | 物理/逻辑接口速率趋势图；物理接口底层硬件统计（25+ 指标，含诊断说明） |
| **会话详情** | 按状态分类会话数（active/closed/closing 等）、CPS 趋势、策略拦截率、VSYS 会话分布 |
| **资源详情** | CPU 各分量仪表盘（us/sy/id/wa/hi/si/ni/st）；DP CPU 按 5 个时间粒度历史趋势图；管理平面核心服务进程性能图；磁盘空间 |
| **计数器详情** | 全量 `show counter global` 数据；变化高亮；每条计数器的值与速率趋势图 |
| **GlobalProtect** | GP 版本信息；实时在线用户列表（用户名、主机名、Client IP、VPN IP、登录时间） |

### 技术特点

- **Chrome MV3 Service Worker** — 无持久后台页，轮询由 Chrome Alarms 驱动（默认每 5 分钟）
- **分级轮询** — 系统信息每 30 分钟刷新；性能数据每 5 分钟；GP 未配置时自动跳过
- **局部刷新** — 每个子菜单的刷新按钮只采集当前页面所需数据，不浪费 API 请求
- **Content Script 代理** — 解决 Private Network Access (PNA) 限制，支持自签名证书设备
- **自动识别** — 在 Chrome 中打开防火墙管理页面并登录，扩展自动添加设备
- **版本更新提醒** — 每周检查 GitHub 新版本，有更新时发桌面通知 + 侧边栏提示
- **亮色/暗色主题** — 中英双语界面

### 数据采集频率

| 数据 | 频率 |
|------|------|
| 性能数据（CPU、会话、接口、计数器、GP） | 每 5 分钟自动采集 |
| 系统信息 | 每 30 分钟自动刷新 |
| 磁盘空间 | 手动刷新时采集 |
| 物理接口底层统计 | 按需（点击接口行时） |
| GitHub 版本检查 | 每 7 天一次 |

所有数据均在本地处理，不上传至任何外部服务器。

### 安装方式

1. 下载并解压本仓库
2. 打开 Chrome → `chrome://extensions` → 开启**开发者模式**
3. 点击**加载已解压的扩展程序** → 选择 `panos-monitor` 文件夹
4. 点击工具栏图标打开 Dashboard

### 添加防火墙

**自动识别（推荐）：** 在 Chrome 中打开防火墙管理页面并登录，扩展自动提取 API Key 并添加设备。

**手动添加：** 点击「Add Firewall」，输入防火墙 HTTPS 地址和 API Key。

> **自签名证书：** 首次添加前，先在 Chrome 中打开防火墙地址并手动接受证书警告，每台设备只需操作一次。

---

## Disclaimer

This project is an independent open-source tool and is not affiliated with or endorsed by Palo Alto Networks.

> 本项目为独立开源工具，与 Palo Alto Networks 官方无关。

---

## License

MIT License — see [LICENSE](LICENSE) for details.
