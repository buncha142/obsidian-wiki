---
title: Prompt Engineering
tags: [concept, prompt, engineering, technique, cot, few-shot, xml, pare]
category: concepts
created: 2026-06-14
updated: 2026-06-14
sources: [claude-manual-stag-2026]
summary: "ศาสตร์การเขียน Prompt ให้ได้ผลลัพธ์ดีจาก LLM — ครอบคลุม 6-component anatomy, XML tagging, Chain-of-Thought, Few-shot, 5 anti-patterns, และ PARE framework"
---

# Prompt Engineering

**Prompt Engineering** คือการออกแบบข้อความที่ส่งให้ LLM เพื่อให้ได้ผลลัพธ์ที่ต้องการ อย่างสม่ำเสมอและมีคุณภาพสูง

## 6-Component Anatomy of a Prompt

Prompt ที่ดีประกอบด้วย 6 ส่วน (ไม่จำเป็นต้องครบทุกส่วน):

```
┌─────────────────────────────────────────┐
│  1. ROLE     — "คุณคือ..."             │
│  2. TASK     — "ให้ทำ..."              │
│  3. CONTEXT  — "พื้นหลัง/สถานการณ์"   │
│  4. DATA     — <ข้อมูลที่ต้องใช้>      │
│  5. FORMAT   — "ตอบในรูปแบบ..."        │
│  6. CONSTRAINT — "ห้าม/ต้อง..."        │
└─────────────────────────────────────────┘
```

### ตัวอย่างการใช้ครบ 6 องค์ประกอบ

```xml
<role>คุณคือนักแปลเอกสารทางกฎหมายมืออาชีพ</role>

<task>แปลสัญญาต่อไปนี้จากภาษาอังกฤษเป็นภาษาไทย</task>

<context>ผู้อ่านเป็นลูกค้าทั่วไปที่ไม่มีพื้นฐานกฎหมาย
ต้องการภาษาที่เข้าใจง่าย</context>

<data>
[เนื้อหาสัญญา]
</data>

<format>
- แปลทีละย่อหน้า
- ใส่หมายเหตุสำหรับคำศัพท์กฎหมายสำคัญ
</format>

<constraint>
- ห้ามละเว้นเนื้อหาใดๆ
- ห้ามตีความหรือให้คำแนะนำทางกฎหมาย
</constraint>
```

## XML Tagging — เทคนิคสำคัญสำหรับ Claude

Claude ถูกฝึกมาให้เข้าใจ XML tags ได้ดีมาก ใช้แท็กเพื่อ:

### 1. แยกส่วน prompt ชัดเจน
```xml
<instructions>...</instructions>
<document>...</document>
<examples>...</examples>
```

### 2. ป้องกัน Prompt Injection
```xml
<user_input>
  [เนื้อหาจากผู้ใช้ที่ไม่ไว้ใจ — อยู่ในกล่อง ไม่สามารถ override instructions ได้]
</user_input>
```

### 3. ระบุรูปแบบ output
```xml
<output_format>
  <summary>สรุปภายใน 3 ประโยค</summary>
  <key_points>รายการ bullet points 5 ข้อ</key_points>
</output_format>
```

## Role Prompting

การกำหนด persona ให้ Claude ช่วยปรับโทนและความเชี่ยวชาญ:

```
"คุณคือ Senior Python Developer ที่เชี่ยวชาญ FastAPI และ PostgreSQL"
"คุณคือนักโภชนาการที่เน้น evidence-based nutrition"
"คุณคือครูสอนภาษาอังกฤษสำหรับเด็กประถม"
```

**ข้อควรระวัง:** Role เปลี่ยนโทนและ focus แต่ไม่ได้เพิ่มความรู้จริง — Claude ยังมีข้อจำกัดเดิม

## Chain-of-Thought (CoT)

บังคับให้ Claude "คิดก่อนตอบ" — เพิ่มความแม่นยำสำหรับงานที่ต้องการ reasoning:

### Zero-shot CoT
```
"แก้สมการต่อไปนี้ แสดงขั้นตอนการคิดทีละขั้น"
"คิดทีละขั้นตอน (think step by step)"
```

### Extended Thinking
สำหรับ Claude Opus/Sonnet — เปิด internal thinking:
```python
response = client.messages.create(
    model="claude-opus-4-8",
    thinking={"type": "enabled", "budget_tokens": 10000},
    ...
)
```

## Few-shot Prompting

ให้ตัวอย่าง (examples) ก่อน prompt หลัก:

```
ตัวอย่างการจำแนกอารมณ์:
Input: "วันนี้อากาศดีมาก ใจฟู!" → Positive
Input: "รถติดตลอด เหนื่อยใจ" → Negative
Input: "ขอบคุณที่แจ้ง" → Neutral

ตอนนี้จำแนก: "อาหารอร่อยแต่รอนานมาก"
```

**จำนวนตัวอย่างที่แนะนำ:** 3–5 ตัวอย่าง (มากเกินไปเปลืองtoken)

## Output Format Control

### JSON Output
```
ตอบเป็น JSON เท่านั้น โดยมี format:
{"sentiment": "positive|negative|neutral", "confidence": 0.0-1.0, "reason": "..."}
```

### Markdown Structure
```
ตอบเป็น Markdown ประกอบด้วย:
# หัวข้อหลัก
## หัวข้อย่อย
- bullet points
```

### ความยาว
```
"สรุปในไม่เกิน 3 ประโยค"
"อธิบายแบบละเอียด ไม่ต้องจำกัดความยาว"
"ตอบด้วยคำว่า YES หรือ NO เท่านั้น"
```

## 5 Anti-patterns ที่ควรหลีกเลี่ยง

### ❌ 1. Prompt Bloat — prompt ยาวเกินไป
```
# แย่:
"กรุณาช่วยฉันในการ analyze ข้อมูลชุดนี้อย่างละเอียดและครบถ้วน
โดยให้พิจารณาทุกมิติของปัญหา รวมถึง..."

# ดี:
"วิเคราะห์ข้อมูล: [data] — เน้น trend และ outliers"
```

### ❌ 2. Ambiguous Instructions — คำสั่งคลุมเครือ
```
# แย่: "สรุปข้อความนี้ให้ดี"
# ดี:  "สรุปใน 3 bullet points แต่ละข้อไม่เกิน 20 คำ"
```

### ❌ 3. Negative-only Constraints — บอกแต่สิ่งที่ห้าม
```
# แย่: "อย่าพูดเรื่องการเมือง อย่าตอบเรื่องศาสนา อย่า..."
# ดี:  "เน้นตอบเรื่อง [topic] เท่านั้น"
```

### ❌ 4. Missing Context — ขาด context สำคัญ
```
# แย่: "แก้ bug ในโค้ดนี้"
# ดี:  "แก้ bug ในโค้ด Python นี้ที่ทำให้ได้ error: [error message]"
```

### ❌ 5. Assuming Knowledge — สมมติว่า Claude รู้สิ่งที่ไม่ได้บอก
```
# แย่: "อธิบาย project ของเรา"
# ดี:  "อธิบาย project: [ชื่อ] ซึ่งทำ [สิ่ง] สำหรับ [กลุ่มเป้าหมาย]"
```

## PARE Framework — ทดสอบ Prompt อย่างเป็นระบบ

ใช้สำหรับ iterate และปรับปรุง prompt:

```
P — Prompt    : เขียน prompt เบื้องต้น
A — Assess    : ทดสอบกับ input หลากหลาย
R — Refine    : ปรับปรุงจุดที่ล้มเหลว
E — Evaluate  : วัดผลกับ benchmark
```

### ตัวอย่าง Test Cases ที่ควรมี
- **Happy Path** — input ปกติที่คาดหวัง
- **Edge Cases** — input ขอบเขต (ว่าง, ยาวมาก, ภาษาอื่น)
- **Adversarial** — input ที่ตั้งใจทดสอบขีดจำกัด

## System Prompt vs User Prompt

| | System Prompt | User Prompt |
|--|--|--|
| ส่งโดย | Operator | User |
| ปรากฏที่ | ต้น context | Human turn |
| ใช้สำหรับ | กำหนด persona, rules | คำถาม/งาน |
| ผู้ใช้เห็น? | ปกติไม่เห็น | เห็น |

## Related
- [[concepts/context-window]]
- [[concepts/constitutional-ai]]
- [[concepts/claude-models-family]]
- [[references/claude-api-cheatsheet]]
