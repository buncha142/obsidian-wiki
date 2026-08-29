---
title: "Synology DS920+ NAS"
tags: [it-equipment, hardware]
category: entities
created: 2026-07-11
updated: 2026-07-12
sources: [img-0357-label-photo, img-0358-front-panel-photo]
summary: "Synology DS920+ 4-bay NAS ติดตั้งที่โต๊ะทำงาน office ห้องสติ สำรองไฟผ่าน ZIRCON Pi UPS 1000VA เชื่อมเครือข่ายผ่าน TP-Link switch แบบ unmanaged"
provenance:
  extracted: 0.55
  inferred: 0.4
  ambiguous: 0.05
---

# Synology DS920+ NAS

## ข้อมูลทั่วไป
- **ประเภท:** Network Attached Storage (NAS), 4-bay desktop
- **ยี่ห้อ/รุ่น:** Synology DS920+
- **ปีที่ซื้อ:** (ยังไม่ระบุ)
- **ราคา/ที่มา (ถ้าจำได้):** (ยังไม่ระบุ)
- **ผลิตที่:** Taiwan ^[extracted]

## สเปกหลัก
- **Serial Number:** 2190TERV3JXAH ^[extracted]
- **MAC Address:** 9009D004A7D5, 9009D004A7D6 (2 พอร์ต LAN) ^[extracted]
- **DC Input:** +12V, 8.33A ^[extracted]
- **มาตรฐาน/certification บนฉลาก:** KC, FCC, CE, VCI, RCM, EAC, RoHS (D33A87), IS 13252 Part 1:2010, BIS (R-41052124) ^[extracted]
- **หมายเหตุสเปก:** DS920+ เป็นรุ่น 4-bay ของ Synology (CPU Intel Celeron J4125, RAM 4GB ขยายได้ถึง 8GB, รองรับ M.2 NVMe cache) — ยังไม่ได้ตรวจสอบสเปกภายในเครื่องจริงจากฉลากนี้ ^[inferred]

## การใช้งานจริง
- **ใช้ทำอะไรเป็นหลัก:** (ยังไม่ระบุ — เพิ่งติดตั้ง)
- **ใช้คู่กับอุปกรณ์/ซอฟต์แวร์อะไร:** สำรองไฟด้วย [[entities/zircon-pi-ups-1000va|ZIRCON Pi UPS 1000VA]] ^[extracted]; เชื่อมเครือข่ายผ่านพอร์ต LAN 1 เข้ากับ [[entities/tplink-tl-sg1024d-switch|TP-Link TL-SG1024D switch]] ที่ห้องสติ ^[extracted]
- **ตั้งอยู่ที่ไหน:** โต๊ะทำงาน office "ห้องสติ" ^[extracted]

## ปัญหา/ข้อจำกัดที่เจอ
- [[entities/tplink-tl-sg1024d-switch|TP-Link TL-SG1024D]] ที่ต่ออยู่เป็น unmanaged switch — ไม่รองรับ Link Aggregation (802.3ad/LACP) จึงไม่สามารถรวมพอร์ต LAN 2 ช่องของ NAS เพื่อเพิ่ม throughput ได้ ปัจจุบันใช้แค่ LAN 1 เชื่อมกับสวิตช์ ส่วน LAN 2 ยังว่าง ^[extracted]

## แผนในอนาคต
- (ยังไม่ระบุ)

## Related
- [[entities/zircon-pi-ups-1000va]]
- [[entities/macmini-m4-2024]]
- [[entities/tplink-tl-sg1024d-switch]]
