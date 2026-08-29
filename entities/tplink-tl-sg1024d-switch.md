---
title: "TP-Link TL-SG1024D 24-Port Gigabit Switch"
tags: [it-equipment, hardware, networking]
category: entities
created: 2026-07-12
updated: 2026-07-12
sources: [img-0358-front-panel-photo, user-provided]
summary: "สวิตช์เครือข่าย TP-Link TL-SG1024D 24-Port Gigabit แบบ unmanaged ที่ห้องสติ เชื่อมกับ Synology NAS พอร์ต LAN 1"
provenance:
  extracted: 0.55
  inferred: 0.4
  ambiguous: 0.05
---

# TP-Link TL-SG1024D 24-Port Gigabit Switch

## ข้อมูลทั่วไป
- **ประเภท:** เครือข่ายสวิตช์ (Ethernet Switch) — 24-Port Gigabit
- **ยี่ห้อ/รุ่น:** TP-Link TL-SG1024D
- **ปีที่ซื้อ:** (ยังไม่ระบุ)
- **ราคา/ที่มา (ถ้าจำได้):** (ยังไม่ระบุ)

## สเปกหลัก
- **จำนวนพอร์ต:** 24 พอร์ต RJ45, Gigabit (1000Mbps) ทุกพอร์ต ^[extracted]
- **ประเภทการจัดการ:** Unmanaged switch — รุ่น "D" ของ TP-Link ไม่มีหน้าเว็บตั้งค่า ไม่รองรับ VLAN, ไม่รองรับ Link Aggregation (802.3ad/LACP) ^[inferred]
- **สถานะขณะถ่ายภาพ:** ไฟ Power ติด, พอร์ตที่มีการเชื่อมต่อ (Link) และ active ตามภาพ: พอร์ต 1, 3, 5 (แถวบน) และ 2, 4, 6, 8, 14 (แถวล่าง) ^[extracted]

## การใช้งานจริง
- **ใช้ทำอะไรเป็นหลัก:** กระจายสัญญาณเครือข่าย LAN ให้อุปกรณ์ในบ้าน/ออฟฟิศ ^[inferred]
- **ใช้คู่กับอุปกรณ์/ซอฟต์แวร์อะไร:** เชื่อมต่อกับ [[entities/synology-ds920plus-nas|Synology DS920+ NAS]] ผ่านสาย LAN — ต่อจากพอร์ต LAN 1 ของ NAS เข้าสวิตช์ตัวนี้ ^[extracted]; คาดว่า [[entities/macmini-m4-2024|Mac mini M4]] อยู่ในวง LAN เดียวกันผ่านสวิตช์นี้เช่นกัน (ยังไม่ยืนยันพอร์ตที่ใช้) ^[inferred]
- **ตั้งอยู่ที่ไหน:** โต๊ะทำงาน office "ห้องสติ" ^[extracted]

## ปัญหา/ข้อจำกัดที่เจอ
- เป็น unmanaged switch จึง **ไม่รองรับ Link Aggregation (LACP)** — หากต้องการรวมพอร์ต LAN 2 ช่องของ [[entities/synology-ds920plus-nas|Synology DS920+]] เพื่อเพิ่ม throughput จะต้องเปลี่ยนไปใช้ managed switch รุ่นอื่นแทน ^[inferred]

## แผนในอนาคต
- (ยังไม่ระบุ)

## Related
- [[entities/macmini-m4-2024]]
- [[entities/synology-ds920plus-nas]]
