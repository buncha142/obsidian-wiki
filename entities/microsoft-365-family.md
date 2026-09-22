---
title: "Microsoft 365 Family"
tags: [software, subscription, productivity]
category: entities
created: 2026-09-15
updated: 2026-09-19
sources: [user-provided]
summary: "แพ็กเกจสมาชิก Microsoft 365 แบบครอบครัว ราคา 3,699 บาท/ปี ใช้ได้ 1-6 คน คนละสูงสุด 5 อุปกรณ์ พื้นที่คลาวด์รวม 6TB (1TB/คน) รวม Copilot, Word, Excel, PowerPoint, Outlook, OneDrive, Defender, Teams; บัญชี buncha142@gmail.com เป็นสมาชิกที่ถูกเชิญโดยศูนย์ปฏิบัติธรรมพัทลุง"
---

# Microsoft 365 Family

## ข้อมูลแพ็กเกจ
- **แผนที่ใช้:** Microsoft 365 Family
- **ราคา:** ฿3,699.00 / ปี
- **จำนวนผู้ใช้:** 1–6 คน (AI/Copilot ใช้ได้เฉพาะเจ้าของบัญชีที่สมัครสมาชิก)
- **จำนวนอุปกรณ์:** แต่ละคนใช้งานพร้อมกันได้สูงสุด 5 เครื่อง
- **พื้นที่เก็บข้อมูลคลาวด์:** สูงสุด 6TB รวม (1TB ต่อคน)
- **วันหมดอายุ:** 21 ธันวาคม 2569 (21/12/2026)
- **สถานะบัญชี buncha142@gmail.com:** เป็นสมาชิกที่ถูกเชิญเข้าแพ็กเกจ ไม่ใช่เจ้าของบัญชีหลัก — แพ็กเกจนี้ **"Shared and managed by ศูนย์ปฏิบัติธรรมพัทลุง จ.พัทลุง"** (ตรวจสอบผ่าน account.microsoft.com/subscriptions เมื่อ 2026-09-19)

## แอปที่รวมอยู่ในแพ็กเกจ
- Microsoft 365 Copilot
- Word
- Excel
- PowerPoint
- Outlook
- OneDrive
- Microsoft Defender
- Teams

> รวมทุกอย่างใน Microsoft 365 Personal พร้อมสิทธิ์แชร์ให้ครอบครัวสูงสุด 6 คน

## การใช้งานจริง
- ติดตั้งและใช้งานบน [[entities/macmini-m4-2024|Mac mini M4 (2024)]] — เดิมเปิด Microsoft 365 Copilot อัตโนมัติตอนเปิดเครื่อง (Login Items) ภายหลังปิดออกแล้วเมื่อ 2026-09-15 เพราะไม่จำเป็นต้องเปิดค้างตลอดเวลา
- OneDrive sync มีการรันเป็น background service อยู่แล้วผ่าน `com.microsoft.OneDriveStandaloneUpdater` และ daemon ที่เกี่ยวข้อง (ดูรายละเอียดใน [[entities/macmini-m4-2024]])

## ปัญหา/ข้อจำกัดที่เจอ
- **2026-09-19 — PowerPoint ขึ้นเตือน "Subscription Required to Edit and Save" ทั้งที่มี Family plan ใช้งานได้:** ตรวจที่ account.microsoft.com ยืนยันว่า subscription ยัง active และบัญชี buncha142@gmail.com อยู่ในแพ็กเกจจริง (เป็นสมาชิกที่ถูกเชิญ ไม่ใช่เจ้าของ) — สาเหตุคือแอป PowerPoint บนเครื่องยังไม่ได้ sign in/activate ด้วยบัญชีนี้ ไม่ใช่ปัญหาที่ตัว subscription **แก้แล้ว:** เปิด PowerPoint → sign in ด้วย buncha142@gmail.com → ผ่านหน้า privacy dialog "Getting better together" (เลือก "No, don't send optional data" ก็ได้ ไม่กระทบ activation) → กด Accept → เตือนหายไป

## Related
- [[entities/macmini-m4-2024]]
