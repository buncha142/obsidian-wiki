---
title: "Health Folder — Workflow & Prompts"
tags: [สุขภาพ, workflow, fitness, sleep, reference]
category: health-reference
created: 2026-06-13
updated: 2026-06-13
summary: "คู่มือการใช้งานโฟลเดอร์ health/ — ภาพรวมระบบ, daily/weekly workflow, และ prompts สำเร็จรูป"
---

# Health Folder — Workflow & Prompts

คู่มือนี้อธิบายวิธีใช้งานโฟลเดอร์ `health/` ทั้งหมด ตั้งแต่การสร้างบันทึกรายวัน ไปจนถึงการรีวิวรายสัปดาห์และเตรียมข้อมูลก่อนพบแพทย์

---

## ภาพรวมระบบ

```
แผน (อ่านครั้งเดียว)                 บันทึก (ทำทุกวัน)
─────────────────────────────         ────────────────────────────
health/sleep.md                       health/fitness/logs/YYYY-MM-DD.md
health/fitness/workout-plan.md                ↑
health/fitness/equipment.md           คัดลอกจาก daily-template.md
health/conditions/gastritis.md

อ้างอิง (เปิดเมื่อต้องการ)
─────────────────────────────
health/records/            ← ผลตรวจเลือด, CT scan
health/fitness/equipment.md ← HR zone, อุปกรณ์
```

### ไฟล์หลักและหน้าที่

| ไฟล์ | หน้าที่ | แก้ไขเมื่อ |
|------|---------|------------|
| [[health/sleep]] | แผนนอน 4 สัปดาห์ + weekly tracking table | รายสัปดาห์ |
| [[health/fitness/workout-plan]] | ตารางออกกำลังกาย 4 สัปดาห์ | เมื่อปรับแผน |
| [[health/fitness/equipment]] | HR zones, รายการอุปกรณ์ | ไม่บ่อย |
| [[health/conditions/gastritis]] | ยา, อาการ, คำถามหมอ | ก่อนนัดหมอ |
| [[health/fitness/logs/daily-template]] | Template บันทึกรายวัน | ไม่แก้ (ใช้คัดลอก) |
| [[health/fitness/logs/index]] | ตารางสรุปรายเดือน | ทุกวัน (เพิ่ม row) |

---

## Daily Workflow (~5 นาที/วัน)

### เช้า — หลังตื่น 04:30

```
1. เปิด Mi Fitness
   → Sleep tab: เข้านอน / ตื่น / รวม / หลับลึก / REM / ตื่นกลางดึก / HR / หายใจ
   → Activity tab: ก้าว / ระยะทาง / แคลอรี่ / SpO2

2. สร้างไฟล์ใหม่
   health/fitness/logs/YYYY-MM-DD.md
   (คัดลอกจาก daily-template.md)

3. กรอก 3 section แรก
   - การนอน       ← จาก Mi Fitness
   - Wind-down    ← จำจากเมื่อคืน
   - สภาพแวดล้อม ← จำจากเมื่อคืน
```

### เย็น — หลังออกกำลังกาย

```
4. กรอก section ออกกำลังกาย + กิจกรรม
   - ตรวจสอบ Focus ของวัน ใน workout-plan.md
   - บันทึก HR จาก POLAR H7 (Zone 2 = 109–127 bpm)

5. อัพเดต logs/index.md
   เพิ่ม row ใหม่ในตารางเดือนปัจจุบัน
```

---

## Weekly Workflow (~10 นาที/สัปดาห์)

```
1. เปิด health/fitness/logs/index.md
   → มองภาพรวม 7 วัน

2. ตรวจ 4 pattern หลัก
   □ หลับลึก < 1h45m กี่วัน?
   □ ก้าวเกิน 10,000 กี่วัน?
   □ Wind-down ทำครบ checklist กี่/7 วัน?
   □ ออกกำลังกายตรงแผนกี่วัน?

3. กรอก health/sleep.md
   → Weekly tracking table (Sleep Score, ตื่น 04:30 ✅/❌, ก้าว, หลับลึก, REM)

4. ระบุ 1 จุดปรับสัปดาห์หน้า
   → บันทึกใน health/sleep.md หรือ logs/index.md
```

---

## ไฟล์ที่แก้ไขบ่อยที่สุด

| ความถี่ | ไฟล์ | สิ่งที่ทำ |
|---------|------|----------|
| ทุกวัน | `logs/YYYY-MM-DD.md` (สร้างใหม่) | กรอกข้อมูลจาก Mi Fitness |
| ทุกวัน | `logs/index.md` | เพิ่ม row ในตารางเดือน |
| รายสัปดาห์ | `health/sleep.md` | กรอก weekly tracking table |
| ก่อนพบแพทย์ | `health/conditions/gastritis.md` | อัพเดตคำถาม/ยา |
| รายเดือน | `health/fitness/workout-plan.md` | ปรับแผนตาม progress |

---

## Prompts สำเร็จรูป

### เริ่มบันทึกวันใหม่

```
สร้างบันทึกสุขภาพวันนี้ (YYYY-MM-DD) จาก template
ข้อมูลจาก Mi Fitness:
- เข้านอน HH:MM, ตื่น 04:30
- นอนรวม XhXXm, หลับลึก XhXXm, REM XhXXm, ตื่นกลางดึก N ครั้ง
- HR นอน XX BPM, หายใจ XX ครั้ง/นาที
- ก้าว X,XXX, แคลอรี่ XXX, SpO2 XX%
Wind-down เมื่อคืน: [ทำครบ / ขาด: ...]
ห้อง: XX°C, [มืด/สว่าง], [เงียบ/มีเสียง], โทรศัพท์ [อีกห้อง/ข้างเตียง]
```

---

### สำรวจแผนออกกำลังกายวันนี้

```
วันนี้คือ [วันจันทร์] Week [1] ของ health/fitness/workout-plan.md
ช่วยบอกว่าวันนี้ควรทำอะไร?
- Focus ของวัน
- ระยะเวลา / HR target (POLAR H7)
- รายการ exercises ที่ต้องทำ
- สิ่งที่ต้องระวัง (ก้าว hard cap ฯลฯ)
```

---

### รีวิวสัปดาห์

```
จากบันทึก health/fitness/logs/ สัปดาห์นี้ (YYYY-MM-DD ถึง YYYY-MM-DD)
สรุป:
1. Sleep score แต่ละวัน — หลับลึก vs เป้า 1h45m
2. Wind-down compliance: กี่/7 วัน
3. ก้าวเกิน hard cap: กี่วัน
4. ออกกำลังกายตรงแผน: กี่วัน
5. แนะนำ 1 จุดปรับสำหรับสัปดาห์หน้า
```

---

### ก่อนพบแพทย์

```
เตรียมข้อมูลสำหรับนัดหมอ นพ. นิธิ มงคล (02-831-1512):
1. สรุปอาการกระเพาะ 1 เดือนที่ผ่านมา (จาก health/conditions/gastritis.md)
2. คำถามที่เตรียมไว้ทั้งหมด (section อาหารเสริม Pure 99 Sleep Well)
3. ข้อมูลการนอนที่เกี่ยวข้องกับ Deanxit (จาก health/sleep.md)
```

---

### อัพเดต index หลังบันทึกครบสัปดาห์

```
อัพเดต health/fitness/logs/index.md
เพิ่มข้อมูล 7 วันล่าสุด ในตารางเดือน [มิถุนายน 2569]:
วัน | ก้าว | นอนรวม | หลับลึก | HR นอน | แคล | link

[วางข้อมูล 7 แถว]
```

---

### วิเคราะห์คุณภาพการนอน

```
อ่าน health/fitness/logs/ 7 วันล่าสุด
วิเคราะห์:
- วันไหนหลับลึก ≥ 1h45m → ตื่น 04:30 ได้สดชื่น?
- วันไหนหลับลึกต่ำ → เกิดจากอะไร? (ก้าวเยอะ? Wind-down ไม่ครบ? ห้องร้อน?)
- pattern ที่เห็น vs เป้าหมายใน health/sleep.md
```

---

## ลำดับการอ่านสำหรับคนใหม่

1. [[health/index]] — ภาพรวมทั้งหมด
2. [[health/sleep]] — เป้าหมายและแผนนอน
3. [[health/fitness/workout-plan]] — แผนออกกำลังกาย
4. [[health/fitness/logs/daily-template]] — template บันทึกรายวัน
5. [[health/fitness/logs/index]] — ดูตัวอย่างการบันทึก
6. [[health/conditions/gastritis]] — ยาและข้อควรระวัง

---

## Related

- [[health/sleep]]
- [[health/fitness/workout-plan]]
- [[health/fitness/logs/daily-template]]
- [[health/fitness/logs/index]]
- [[health/conditions/gastritis]]
