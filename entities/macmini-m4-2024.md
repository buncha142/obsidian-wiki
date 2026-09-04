---
title: "Mac mini M4 (2024)"
tags: [it-equipment, hardware]
category: entities
created: 2026-06-19
updated: 2026-09-04
sources: [user-provided]
summary: "Mac mini รุ่น 2024 ชิป Apple M4 RAM 24GB SSD 500GB เครื่องหลักที่โต๊ะทำงาน office ห้องสติ ต่อจอคู่ BenQ RD280U + LG Full HD; มีบันทึกรายการเปิดอัตโนมัติ (Login Items/LaunchAgents/LaunchDaemons) และผลตรวจสมรรถภาพเครื่อง"
---

# Mac mini M4 (2024)

## ข้อมูลทั่วไป
- **ประเภท:** เดสก์ท็อป (Mac mini)
- **ยี่ห้อ/รุ่น:** Apple Mac mini, 2024
- **ปีที่ซื้อ:** 2024
- **ราคา/ที่มา (ถ้าจำได้):** (ยังไม่ระบุ)

## สเปกหลัก
- **ชิป/CPU:** Apple M4
- **RAM:** 24 GB
- **Storage:** SSD 500 GB (APPLE SSD AP0512Z)
- **OS / Firmware version:** macOS Tahoe 26.6.2 (build 25G83) — ตรวจสอบล่าสุด 2026-09-04
- **Model identifier:** Mac16,10
- **Serial number:** WGFQJ4M5WH
- **Limited Warranty:** หมดอายุ 7 ธันวาคม 2569 (พ.ศ.) — ครอบคลุม Hardware Service และ Chat/Phone Support
- **จอที่ต่อใช้งาน:**
  - [[entities/benq-rd280u-monitor|BenQ RD280U]] — 28.2 นิ้ว (3840 × 2560)
  - LG FULL HD — 24 นิ้ว (1080 × 1920)

## การใช้งานจริง
- **ใช้ทำอะไรเป็นหลัก:** dev โปรเจค Laravel/TALL Stack (admin.ptmc072), งานธุรการ/เอกสาร, ประชุมออนไลน์และสื่อสาร
- **ใช้คู่กับอุปกรณ์/ซอฟต์แวร์อะไร:** VS Code + [[entities/claude|Claude]] Code, Google Workspace (Docs/Sheets/Drive), โปรแกรมบัญชี/เอกสารราชการ; สำรองไฟด้วย [[entities/zircon-pi-ups-1000va|ZIRCON Pi UPS 1000VA]]
- **ตั้งอยู่ที่ไหน:** โต๊ะทำงาน office "ห้องสติ"

## ปัญหา/ข้อจำกัดที่เจอ
- (ยังไม่มีข้อมูล)

## การตั้งค่าระบบที่ทำไว้

### จัดการรายการเปิดอัตโนมัติ (2026-09-04)
- **uTorrent Web:** ปิดการเปิดอัตโนมัติตอน login — ลบออกจาก Login Items ผ่าน System Events ต้องเปิดเองเมื่อต้องการใช้งานเท่านั้น
- **ลบ LaunchDaemons ที่ซ้ำซ้อน** ใน `/Library/LaunchDaemons/` (ตรวจแล้วว่าไม่ได้ถูกโหลดใน launchd เลย ไม่กระทบการทำงาน):
  - `homebrew.mxcl.nginx.plist`, `homebrew.mxcl.php@8.3.plist`, `homebrew.mxcl.php@8.4.plist`, `homebrew.mxcl.dnsmasq.plist` — เศษเหลือจากตอนใช้ `brew services` ปัจจุบัน **Laravel Herd** (`de.beyondco.herd.helper`) จัดการ nginx/php/dnsmasq เองแล้ว
  - `jp.co.canon.MasterInstaller.plist` — ไม่ได้ต่อเครื่องพิมพ์ Canon แล้ว

### รายการที่ยังเปิดอัตโนมัติอยู่ (สถานะหลังทำความสะอาด)
| ระดับ | รายการ |
|---|---|
| Login Items | Google Drive, GeminiAppLauncher, FigmaAgent, Stream Dock AJAZZ |
| User LaunchAgents | Google Updater (keystone ×3), MySQL, PostgreSQL@16 (Homebrew) |
| System LaunchAgents | Google keystone, Logitech Options+/RightSight, OneDrive updater, Microsoft AutoUpdate/SyncReporter, Zoom updater |
| System LaunchDaemons | Docker (socket/vmnetd), Google Updater, Logitech updater, OneDrive/Microsoft/Office helpers, **Laravel Herd helper**, **NetBird VPN**, Zoom daemon |

> หมายเหตุ: MySQL + PostgreSQL@16 รันพื้นหลังตลอด ถ้าไม่ได้ dev ทุกวันสามารถหยุดด้วย `brew services stop mysql` / `brew services stop postgresql@16` แล้วสั่ง start เมื่อต้องใช้

## ผลตรวจสมรรถภาพ (2026-09-04)

ตรวจตอน uptime 18 นาที — **สุขภาพดีทุกด้าน ไม่มีคอขวด**

| ด้าน | ค่าที่วัดได้ | ประเมิน |
|---|---|---|
| CPU | Apple M4 10 cores (4P + 6E), load avg 1.62 / 2.59 / 4.45 | โหลดต่อ core ≈ 0.16 — ว่างมาก |
| Thermal | ไม่มีบันทึก thermal/performance warning | ไม่โดน throttle |
| RAM | free 87%, **swap ใช้ 0.00 MB** | RAM 24 GB เพียงพอเต็มที่ |
| Storage | ใช้ 154 GB เหลือ 285 GB (ใช้ 35%) | พื้นที่เหลือเยอะ |
| SSD health | SMART Status: **Verified** | ปกติดี |
| เสถียรภาพ | ไม่มี kernel panic log, 744 processes / 30,720 threads | ปกติสำหรับเครื่อง dev |

- **กิน CPU สูงสุด:** VS Code Renderer (6.4%), [[entities/claude|Claude]] Code extension (5.8%), WindowServer (4.9%)
- **กิน RAM สูงสุด:** VS Code, Google Chrome, LINE, Stream Dock AJAZZ — ไม่มีตัวใดเกิน 2% ต่อ process

## แผนในอนาคต
- (ยังไม่ระบุ)

## Related
- [[entities/benq-rd280u-monitor]]
- [[entities/benq-screenbar-light]]
- [[entities/zircon-pi-ups-1000va]]
- [[entities/claude]]
