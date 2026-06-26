# PAN-OS Monitor

---

> 一款用于监控 Palo Alto Networks 下一代防火墙的 Chrome 扩展程序

[![Version](https://img.shields.io/badge/version-0.6.89-FFCB06?style=flat-square)](https://github.com/)
[![Manifest](https://img.shields.io/badge/Manifest-V3-blue?style=flat-square)](https://developer.chrome.com/docs/extensions/mv3/)
[![PAN-OS](https://img.shields.io/badge/PAN--OS-11.x%20%2F%2012.x-orange?style=flat-square)](https://docs.paloaltonetworks.com/)
[![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)](LICENSE)

---

## Downloads
Download the latest release from [release page](https://github.com/ro-qq/panos-monitor/releases/tag/v0.6.90).

---

**其他语言版本:  [English](README.en.md), [简体中文](README.zhcn.md)**

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

### 支持的设备

- 任何具有管理API访问权限的PAN-OS 10.x / 11.x / 12.x设备

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

## Screenshots

> <img width="2838" height="1770" alt="image" src="https://github.com/user-attachments/assets/0ace37b5-c419-490e-8b4a-0d6f9692bfdb" />


---

## Disclaimer

This project is an independent open-source tool and is not affiliated with, endorsed by, or officially supported by Palo Alto Networks.

> 本项目为独立开源工具，与 Palo Alto Networks 官方无关。

---

## License

MIT License — see [LICENSE](LICENSE) for details.
