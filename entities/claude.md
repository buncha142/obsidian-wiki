---
title: Claude
tags: [entity, ai, assistant, claude, anthropic]
category: entities
created: 2026-06-14
updated: 2026-06-14
sources: [claude-manual-stag-2026]
summary: "AI Assistant จาก Anthropic — ไม่ใช่ Search Engine แต่เป็น Reasoning Engine ที่ฝึกด้วย Constitutional AI เน้น Helpful, Harmless, Honest"
---

# Claude

**ผู้สร้าง:** [[entities/anthropic]]  
**เปิดตัว:** 2023 (Claude 1), 2024 (Claude 2/3), 2025 (Claude 3.5/4)  
**ประเภท:** Large Language Model (LLM) — AI Assistant  
**ภาษาหลัก:** อังกฤษ (รองรับหลายภาษารวมถึงไทย)

## Claude ≠ Search Engine

ความเข้าใจผิดที่พบบ่อยที่สุด:

| | Search Engine | Claude |
|--|--|--|
| ทำงานอย่างไร | Index + Retrieve | Reasoning + Generate |
| ข้อมูล | Real-time web | Training data (มี cutoff) |
| ตอบคำถาม | Link + Snippet | ประมวลผลและสรุป |
| ความแม่นยำ | มักแม่น (link ต้นทาง) | อาจ hallucinate ได้ |
| เหมาะกับ | หาข้อเท็จจริงล่าสุด | วิเคราะห์ เขียน code |

> Claude คือ **Reasoning Engine** — รับ input ประมวลผลด้วย neural network แล้ว generate output ที่น่าจะเป็นไปได้มากที่สุด

## ตระกูลโมเดล

ดูรายละเอียดฉบับเต็มที่ [[concepts/claude-models-family]]

| โมเดล | จุดเด่น | ใช้เมื่อ |
|--------|----------|----------|
| **Opus 4.x** | ฉลาดที่สุด | งานซับซ้อน, วิเคราะห์เชิงลึก |
| **Sonnet 4.x** | สมดุล | งานทั่วไป, production |
| **Haiku 4.5** | เร็วและถูก | chatbot, classification |

## ความสามารถหลัก

- **Text:** เขียน สรุป แปล วิเคราะห์ ทุกภาษา
- **Code:** เขียน debug อธิบาย refactor โค้ด
- **Vision:** อ่านภาพ กราฟ เอกสาร (Opus/Sonnet)
- **Reasoning:** Chain-of-Thought, Math, Logic
- **Long Context:** อ่านเอกสาร 200K tokens (~150K คำอังกฤษ)

## หลักการทำงาน — Constitutional AI

Claude ฝึกด้วย [[concepts/constitutional-ai]] ซึ่งกำหนดค่านิยม 3 ข้อ:

1. **Helpful** — ช่วยเหลือผู้ใช้อย่างแท้จริง ไม่แค่ตอบสั้นๆ
2. **Harmless** — ไม่ทำร้ายผู้ใช้ บุคคลที่สาม หรือสังคม
3. **Honest** — ไม่โกหก ยอมรับความไม่แน่ใจ

## ข้อจำกัดที่ควรรู้

- **Knowledge Cutoff:** ข้อมูลหยุดที่วันที่ฝึกโมเดล — ไม่รู้เรื่องล่าสุด
- **Hallucination:** อาจสร้างข้อมูลที่ไม่มีจริง โดยเฉพาะเรื่องเฉพาะทาง
- **Context Window:** จำได้แค่ใน session ปัจจุบัน ไม่มีหน่วยความจำข้ามการสนทนา
- **ภาษาไทย:** ใช้ token มากกว่าอังกฤษ 2–2.8 เท่า (ดู [[concepts/tokenization]])

## การเข้าถึง Claude

| ช่องทาง | URL / วิธี |
|----------|------------|
| Web Chat | claude.ai |
| API | api.anthropic.com |
| Claude Code CLI | terminal — `claude` |
| Mobile | iOS/Android app |

## Related
- [[entities/anthropic]]
- [[concepts/constitutional-ai]]
- [[concepts/claude-models-family]]
- [[concepts/context-window]]
- [[concepts/tokenization]]
- [[references/claude-api-cheatsheet]]
- [[entities/macmini-m4-2024]] — เครื่องที่ใช้รัน Claude Code ประจำวัน
