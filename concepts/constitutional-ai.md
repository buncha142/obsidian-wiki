---
title: Constitutional AI
tags: [concept, ai-safety, anthropic, training, hhi]
category: concepts
created: 2026-06-14
updated: 2026-06-14
sources: [claude-manual-stag-2026]
summary: "วิธีฝึก AI ของ Anthropic โดยใช้ชุดหลักการ (Constitution) แทนการพึ่ง Human Feedback ล้วนๆ — กำหนด 3 ค่านิยมหลัก: Helpful, Harmless, Honest"
---

# Constitutional AI

Constitutional AI (CAI) คือวิธีการฝึก AI ที่ [[entities/anthropic]] พัฒนาขึ้น แทนที่จะพึ่ง RLHF (Reinforcement Learning from Human Feedback) อย่างเดียว จะใช้ **ชุดหลักการที่กำหนดไว้ล่วงหน้า** เป็น "รัฐธรรมนูญ" ของโมเดล

## 3 ค่านิยมหลัก (HHH)

### 1. Helpful (เป็นประโยชน์)
- ช่วยเหลือผู้ใช้อย่างแท้จริง ไม่ใช่แค่ตอบสั้นๆ ให้ผ่านไป
- ให้ข้อมูลที่ครบถ้วน ตรงประเด็น
- ไม่ปฏิเสธโดยไม่มีเหตุผล

### 2. Harmless (ไม่ก่อความเสียหาย)
- ไม่ช่วยทำสิ่งที่เป็นอันตรายต่อผู้ใช้ บุคคลที่สาม หรือสังคม
- หลีกเลี่ยงเนื้อหาที่ผิดกฎหมาย ลามก หรือส่งเสริมความรุนแรง
- ประเมิน harm ตาม context ไม่ใช่แค่คำพูดที่เขียน

### 3. Honest (ซื่อสัตย์)
- ไม่โกหกหรือสร้างข้อมูลเท็จ
- ยอมรับความไม่แน่ใจ ("ฉันไม่แน่ใจ...")
- ไม่แสร้งทำเป็นว่ารู้สิ่งที่ไม่รู้

## วิธีทำงานของ Constitutional AI

```
ขั้น 1: Supervised Learning
    — ฝึกด้วยข้อมูลตัวอย่างที่มนุษย์เลือก

ขั้น 2: Red-team Generation
    — โมเดลสร้าง response ที่อาจเป็นอันตราย

ขั้น 3: Constitutional Critique
    — โมเดลอีกตัวตรวจสอบว่า response ละเมิด "รัฐธรรมนูญ" ไหม

ขั้น 4: Revision
    — แก้ไข response ตามหลักการ

ขั้น 5: RLHF จาก AI (RLAIF)
    — ใช้ AI ที่ trained ด้วยรัฐธรรมนูญ ให้ feedback แทนมนุษย์
```

## ความแตกต่างจาก RLHF ทั่วไป

| | RLHF บริสุทธิ์ | Constitutional AI |
|--|--|--|
| Feedback จาก | มนุษย์ annotator | มนุษย์ + AI + หลักการ |
| ขนาด | ต้องการ annotator มาก | ลด human labor |
| ความสม่ำเสมอ | แล้วแต่ annotator | สม่ำเสมอตาม constitution |
| ความโปร่งใส | เข้าใจยาก | หลักการ explicit |

## Principal Hierarchy และ Constitutional AI

Constitutional AI ไม่ได้กำหนดแค่ HHH — ยังกำหนด **ลำดับชั้นความน่าเชื่อถือ**:

```
Anthropic (ฝังใน Training — ระดับสูงสุด)
    ↓ ไม่สามารถ override ได้
Operator System Prompt
    ↓ ขยาย/จำกัดได้ภายในขอบ Anthropic
User Message
    ↓ ทำงานในกรอบที่ Operator กำหนด
Claude's Response
```

## ขอบเขตที่ Claude ปฏิเสธเสมอ (Hard Limits)

ไม่ว่า Operator หรือ User จะขอ:
- อาวุธชีวภาพ/เคมี/นิวเคลียร์
- เนื้อหา CSAM
- การโจมตี infrastructure สำคัญ
- การหลีกเลี่ยง oversight ของมนุษย์

## Related
- [[entities/anthropic]]
- [[entities/claude]]
- [[concepts/claude-models-family]]
