---
title: "MacBook Air M2 (2022)"
tags: [it-equipment, hardware]
category: entities
created: 2026-09-14
updated: 2026-09-25
sources: [user-provided, macos-about-this-mac-screenshot]
summary: "MacBook Air ชิป Apple M2 (2022) RAM 8GB SSD ~256GB ชื่อเครื่อง \"MacBook Air M2 LP'Pan\" ใช้คู่กับ Mac mini M4 และเครื่องพิมพ์ Brother DCP-T430W ที่ห้องสติ"
provenance:
  extracted: 0.9
  inferred: 0.1
  ambiguous: 0.0
---

# MacBook Air M2 (2022)

## ข้อมูลทั่วไป
- **ประเภท:** โน้ตบุ๊ก (MacBook Air)
- **ยี่ห้อ/รุ่น:** Apple MacBook Air, ชิป M2 (2022)
- **ชื่อเครื่อง:** MacBook Air M2 LP'Pan
- **ปีที่ซื้อ:** 2022
- **ราคา/ที่มา:** (ยังไม่ระบุ)

## สเปกหลัก
- **ชิป/CPU:** Apple M2
- **RAM:** 8 GB
- **Storage:** Macintosh HD — 245.11 GB จากทั้งหมด (SSD ~256 GB) — เหลือว่าง 75.3 GB ณ 2026-09-25 (เดิม 39.17 GB ณ 2026-09-14)
- **OS / Firmware version:** macOS Tahoe เวอร์ชัน 26.2
- **จอ:** Built-in Liquid Retina Display 13.6 นิ้ว (2560 × 1664)
- **Serial number:** QFC4GPD6MY
- **Warranty:** Coverage Expired (หมดประกันแล้ว)

## การใช้งานจริง
- **ใช้ทำอะไรเป็นหลัก:** (ยังไม่ระบุ)
- **ใช้คู่กับอุปกรณ์/ซอฟต์แวร์อะไร:** พิมพ์/สแกนผ่าน [[entities/brother-dcp-t430w-printer|Brother DCP-T430W]] ด้วย AirPrint; ใช้ร่วมกับ [[entities/macmini-m4-2024|Mac mini M4]] ^[inferred]
- **ตั้งอยู่ที่ไหน:** โต๊ะทำงาน office "ห้องสติ" ^[inferred]

## ปัญหา/ข้อจำกัดที่เจอ
- ~~พื้นที่ว่างเหลือน้อย — 39.17 GB (~16%) ณ 2026-09-14~~ → แก้แล้ว: ว่าง 75.3 GB (~31%) หลังถอนแอป 2026-09-25
- RAM 8 GB ตึงเมื่อเปิด Chrome หลายแท็บ — Chrome กิน ~1.4–2.1 GB, compressor 2.5–3.2 GB (swap ยัง 0) ณ 2026-09-25

## Startup items (หลังทำความสะอาด 2026-09-25)
- **Login Items:** Google Drive, RunCat
- **เบื้องหลัง:** ไดรเวอร์ Epson (Event Manager, Scanner Monitor, Remote Print) + Canon MasterInstaller, Logi Options+ / LogiRightSight, Google Updater/Keystone, Microsoft AutoUpdate
- **เอาออกแล้ว:** Microsoft 365 Copilot + DBnginMenuHelper (Login Items); MySQL, PostgreSQL 17, nginx, php-fpm, dnsmasq (ไม่เปิดอัตโนมัติแล้ว — เปิดเองด้วย `brew services start <ชื่อ>`); ตัวค้างของ Logi Options รุ่นเก่า / Epson Software Updater / Steam
- **ถอนแอปแล้ว:** FileZilla Server, Zoom, Hik-Connect, HP, Outlook, OneNote, To Do, OneDrive, iMovie, CapCut, Goodnotes, GarageBand (+ ไฟล์เสียงประกอบ), SketchUp, Insomnia, GitHub Desktop, TradingView, Tapo, uTorrent Web, ข้อมูล Steam 7.7 GB — ย้ายไปถังขยะด้วยสคริปต์ `~/Desktop/mac-cleanup.sh`
- ผลด้านความปลอดภัย: ไม่มีพอร์ต MySQL (`*:3306`) / nginx / FTP เปิดรอรับการเชื่อมต่อแล้ว

## Performance check
| วันที่ | RAM | Swap | ดิสก์ว่าง | แบตเตอรี่ | หมายเหตุ |
|---|---|---|---|---|---|
| 2026-09-25 (ก่อน) | ใช้ 7.5 GB, compressor 3.2 GB | 0 | 43 GB (80%) | Cycle 168, 87%, Normal | Chrome 2.1 GB, load 14 |
| 2026-09-25 (หลัง restart) | ใช้ 7.4 GB, compressor 2.5 GB, free 50% | 0 | **75.3 GB (~31%)** หลัง Empty Trash (+~27 GB) | — | ไม่มีเซิร์ฟเวอร์รันเบื้องหลัง; ไม่มีคำเตือนความร้อน |

## แผนในอนาคต
- (ยังไม่ระบุ)

## Related
- [[entities/macmini-m4-2024]]
- [[entities/brother-dcp-t430w-printer]]
