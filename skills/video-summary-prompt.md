---
title: Video Summary Prompt Template
tags: [skill, prompt, template, video, youtube, summarization]
category: skills
created: 2026-06-21
updated: 2026-06-21
sources: [video-summary-prompt-draft]
summary: "Prompt template ภาษาไทยสำหรับสรุปวิดีโอ (เช่น YouTube) แบบละเอียด แบ่ง 6 หัวข้อคงที่ ใช้ก่อนนำผลสรุปเข้า /wiki-ingest"
provenance:
  extracted: 0.9
  inferred: 0.1
  ambiguous: 0.0
---

# Video Summary Prompt Template

Prompt สำเร็จรูปสำหรับสั่งให้ Claude สรุปเนื้อหาวิดีโอ (เช่น YouTube ที่ดึง transcript มาแล้ว) แบบละเอียดและมีโครงสร้างคงที่ ใช้เป็นขั้นตอนก่อนหน้า — สรุปวิดีโอก่อน แล้วนำผลสรุปไปเก็บใน wiki ด้วย [[wiki-ingest-workflow]]

## Prompt เต็ม

```
สรุปเนื้อหาวิดีโอนี้แบบละเอียด โดยจัดเป็นหัวข้อต่อไปนี้:

1. ประเด็นหลัก (Main Thesis) — สรุป 2-3 ประโยค
2. แนวคิด/หลักการสำคัญ — list เป็น bullet พร้อมคำอธิบายสั้นๆ แต่ละข้อ
3. ตัวอย่าง/case study ที่พูดถึง (ถ้ามี)
4. ขั้นตอนหรือวิธีทำ (ถ้าเป็นเนื้อหาเชิง how-to) — list เป็นลำดับขั้น
5. คำพูด/quote ที่สำคัญ (ถ้ามี) — พร้อมระบุช่วงเวลาในวิดีโอ
6. ข้อควรระวัง/ข้อจำกัดที่พูดถึง

ตอบเป็นภาษาไทย ใช้ภาษากระชับ ไม่ต้องสรุปซ้ำในแต่ละหัวข้อ
```

## โครงสร้างตาม 6-Component Anatomy

| Component | ใช้จริงในนี้ |
|---|---|
| TASK | "สรุปเนื้อหาวิดีโอนี้แบบละเอียด" |
| FORMAT | 6 หัวข้อคงที่ (thesis/concepts/examples/steps/quotes/caveats) |
| CONSTRAINT | "ภาษาไทย กระชับ ไม่สรุปซ้ำ" |
| DATA | เนื้อหาวิดีโอ/transcript ที่แนบมาพร้อม prompt (ไม่ได้รวมอยู่ใน template) |

ไม่มี ROLE หรือ CONTEXT explicit — เหมาะกับงานสรุปทั่วไปที่ไม่ต้องการ persona เฉพาะทาง ดู [[concepts/prompt-engineering]] สำหรับ anatomy เต็ม

## เงื่อนไขแบบมีเงื่อนไข (Conditional Sections)

หัวข้อ 3, 4, 5, 6 มีวงเล็บ "(ถ้ามี)" — เป็นเทคนิคป้องกันไม่ให้ Claude "เติมเอง" เมื่อวิดีโอไม่มีเนื้อหาประเภทนั้น (เช่น วิดีโอบทสัมภาษณ์ที่ไม่มี how-to steps) ^[inferred]

## การใช้งาน

1. ดึง transcript หรือเนื้อหาวิดีโอ (เช่นจาก YouTube)
2. แนบ transcript ต่อจาก prompt นี้ในข้อความเดียว หรือใส่ใน `<data>` tag ตาม [[concepts/prompt-engineering]]
3. นำผลสรุปที่ได้ไปวางใน `_raw/` เพื่อให้ [[wiki-ingest-workflow]] ประมวลผลต่อเป็นหน้า wiki

## Related
- [[concepts/prompt-engineering]]
- [[wiki-ingest-workflow]]
- [[skills/claude-mini-workflows]]
