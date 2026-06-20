---
title: Context Window
tags: [concept, context, memory, llm, lost-in-the-middle, rag]
category: concepts
created: 2026-06-14
updated: 2026-06-14
sources: [claude-manual-stag-2026]
summary: "Context Window คือ 'หน่วยความจำระยะสั้น' ของ LLM — Claude รองรับ 200K tokens แต่ต้องระวัง Lost-in-the-Middle Effect ที่ทำให้โมเดลลืมข้อมูลตรงกลาง"
---

# Context Window

## Context Window คืออะไร

**Context Window** คือขนาดสูงสุดของข้อความ (input + output รวมกัน) ที่โมเดลสามารถ "จำ" และประมวลผลได้ในการสนทนาครั้งหนึ่ง

```
┌─────────────────────────────────────┐
│         Context Window (200K)        │
│                                     │
│  System Prompt + Conversation History│
│  + Current Message + Response       │
│                                     │
└─────────────────────────────────────┘
```

เมื่อเกิน context window → โมเดลจะ "ลืม" ข้อความเก่า (ถูก truncate)

## Claude Context Window = 200,000 Tokens

ทุกโมเดล Claude 4.x รองรับ **200,000 tokens**

| เนื้อหา | ความจุ |
|---------|--------|
| หนังสืออังกฤษ | ~300 หน้า A4 |
| โค้ด Python | ~7,500 บรรทัด |
| ข้อความไทย | ~100,000–130,000 คำ |
| บทสนทนา | ~1,000 รอบ ถาม-ตอบ |

## Lost-in-the-Middle Effect

งานวิจัย (Liu et al., 2023) พบว่า LLM มีปัญหา **ลืมข้อมูลที่อยู่ตรงกลาง** context:

```
┌──────────┬──────────────────────┬──────────┐
│ จำดีมาก  │    จำได้น้อยที่สุด    │ จำดีมาก  │
│(ต้น)     │      (กลาง)          │ (ปลาย)   │
└──────────┴──────────────────────┴──────────┘
```

### วิธีแก้ Lost-in-the-Middle

1. **วางข้อมูลสำคัญต้นและท้าย** — ไม่ฝังไว้กลาง context
2. **ย่อข้อมูล** ก่อนส่ง — summarize เอกสารยาวก่อน
3. **ใช้ RAG** แทน context stuffing ขนาดใหญ่
4. **แบ่งงาน** — อย่าส่งเอกสาร 300 หน้าพร้อมกัน

## Context vs Memory

| | Context Window | Long-term Memory |
|--|--|--|
| ระยะเวลา | แค่ใน session นี้ | ข้ามการสนทนา |
| วิธีจัดเก็บ | อัตโนมัติ | ต้อง implement เอง |
| Claude รองรับ? | ✅ built-in | ❌ ต้อง RAG หรือ external DB |

## 5-Layer Context Model

[[entities/claude]] ไม่ได้รับแค่ message — มีบริบท 5 ชั้น:

```
Layer 1: Training Data (ฝังใน weights — ความรู้พื้นฐาน)
Layer 2: System Prompt (Operator กำหนด)
Layer 3: Conversation History (บทสนทนาที่ผ่านมา)
Layer 4: Current Message (ข้อความปัจจุบัน)
Layer 5: Retrieved Context (ถ้าใช้ RAG)
```

## RAG Pattern — แก้ปัญหา Context Limitation

**RAG (Retrieval-Augmented Generation)** = แทนที่จะยัดทุกอย่างใน context ให้ดึงเฉพาะส่วนที่เกี่ยวข้องมา

```
User Query
    ↓
Retriever (Vector DB / BM25)
    ↓ ดึงเฉพาะ k passages ที่เกี่ยวข้อง
Claude (200K context)
    ↓
Answer with citations
```

### เมื่อไหร่ควรใช้ RAG vs Context Stuffing

| สถานการณ์ | แนะนำ |
|-----------|--------|
| เอกสาร < 50K tokens | Context Stuffing (ง่ายกว่า) |
| เอกสาร > 100K tokens | RAG |
| ต้องการ real-time data | RAG + Search |
| อ่านครั้งเดียวทั้งไฟล์ | Context Stuffing |
| ถาม-ตอบซ้ำในฐานข้อมูล | RAG |

## เทคนิคจัดการ Context

### Context Compression
- สรุปประวัติการสนทนาเก่าก่อนส่งต่อ
- ลบ message ที่ไม่เกี่ยวข้องออก

### Sliding Window
- เก็บแค่ N message ล่าสุด
- เหมาะกับ chatbot ที่สนทนายาว

### Summary Buffer
- สรุป history ที่เกินขนาด แล้วแนบไปด้านหน้า

## Related
- [[concepts/tokenization]]
- [[concepts/claude-models-family]]
- [[concepts/prompt-engineering]]
