---
title: Anthropic
tags: [entity, company, ai, safety]
category: entities
created: 2026-06-14
updated: 2026-06-14
sources: [claude-manual-stag-2026]
summary: "บริษัท AI Safety ก่อตั้งปี 2021 โดยทีม OpenAI เดิม ผู้สร้าง Claude และผู้บุกเบิก Constitutional AI"
---

# Anthropic

**ประเภท:** บริษัท AI Safety  
**ก่อตั้ง:** 2021  
**ผู้ก่อตั้ง:** Dario Amodei, Daniela Amodei และทีมจาก OpenAI เดิม  
**สำนักงานใหญ่:** San Francisco, CA  
**เว็บไซต์:** anthropic.com

## พันธกิจ

> "AI safety company — สร้าง AI ที่ปลอดภัย เชื่อถือได้ และเป็นประโยชน์ต่อมนุษยชาติในระยะยาว"

Anthropic เชื่อว่า AI ทรงพลังกำลังจะมาถึง และบริษัทที่อยู่ในแนวหน้าของการพัฒนา AI ควรให้ความสำคัญกับ Safety เป็นอันดับแรก

## ผลงานสำคัญ

| ผลงาน | รายละเอียด |
|--------|------------|
| **[[entities/claude]]** | AI Assistant ตระกูลหลัก (Opus / Sonnet / Haiku) |
| **[[concepts/constitutional-ai]]** | วิธีฝึก AI ด้วยหลักการแทน RLHF บริสุทธิ์ |
| **Model Card** | เอกสารความโปร่งใสด้านความสามารถและข้อจำกัดของโมเดล |
| **Responsible Scaling Policy** | นโยบายพัฒนา AI อย่างรับผิดชอบ |

## Principal Hierarchy

Anthropic กำหนด hierarchy ผู้มีอำนาจสั่ง Claude:

```
Anthropic (สูงสุด — ฝังใน System Prompt ระดับ Training)
    ↓
Operator (บริษัทที่ใช้ API — ตั้ง System Prompt)
    ↓
User (ผู้ใช้ปลายทาง — พูดคุยใน Human Turn)
```

- **Anthropic** กำหนดค่านิยมและขอบเขตผ่าน Constitutional AI
- **Operator** สามารถขยายหรือจำกัดความสามารถของ Claude ได้
- **User** ทำงานภายในกรอบที่ Operator กำหนด

## ความแตกต่างจากคู่แข่ง

| | Anthropic / Claude | OpenAI / GPT | Google / Gemini |
|--|--|--|--|
| จุดเน้น | Safety-first | Capability-first | Integration |
| Training | Constitutional AI | RLHF | RLHF + Instruction |
| Context | 200K tokens | 128K tokens | 1M tokens |

## Related
- [[entities/claude]]
- [[concepts/constitutional-ai]]
- [[concepts/claude-models-family]]
- [[references/claude-complete-guide-2026]]
