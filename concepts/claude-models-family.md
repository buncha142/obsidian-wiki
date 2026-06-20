---
title: Claude Models Family
tags: [concept, claude, models, pricing, api, opus, sonnet, haiku]
category: concepts
created: 2026-06-14
updated: 2026-06-14
sources: [claude-manual-stag-2026]
summary: "ตระกูลโมเดล Claude ประกอบด้วย Opus (ฉลาดสุด), Sonnet (สมดุล), Haiku (เร็วและถูก) — ทุกรุ่น 200K context window"
---

# Claude Models Family

[[entities/anthropic]] จัดกลุ่มโมเดลเป็น 3 tier ตามระดับความสามารถและราคา

## ภาพรวมตระกูล

```
Opus 4.x    ← ฉลาดที่สุด / แพงที่สุด
Sonnet 4.x  ← สมดุลดี / recommended สำหรับ production
Haiku 4.5   ← เร็วที่สุด ถูกที่สุด / งานขนาดเล็ก
```

## ตารางเปรียบเทียบ (ข้อมูล ณ ต้นปี 2026)

| โมเดล | Model ID | Input ($/MTok) | Output ($/MTok) | Context | Vision |
|--------|----------|----------------|-----------------|---------|--------|
| Claude Opus 4.8 | `claude-opus-4-8` | $15 | $75 | 200K | ✅ |
| Claude Opus 4.6 | `claude-opus-4-6` | $15 | $75 | 200K | ✅ |
| Claude Sonnet 4.6 | `claude-sonnet-4-6` | $3 | $15 | 200K | ✅ |
| Claude Haiku 4.5 | `claude-haiku-4-5-20251001` | $0.25 | $1.25 | 200K | ✅ |

> **MTok** = Million Tokens (ล้าน token)

## แนวทางเลือกโมเดล

### Opus — เมื่อต้องการความฉลาดสูงสุด
- งานวิจัยเชิงลึก วิเคราะห์เอกสารซับซ้อน
- โค้ดขนาดใหญ่ที่ต้องการความแม่นยำ
- งานที่ต้องคิดหลายขั้นตอน (Multi-step Reasoning)
- ✅ ใช้เมื่อ: คุณภาพสำคัญกว่าต้นทุน

### Sonnet — จุดสมดุลที่ดีที่สุด
- API production ทั่วไป
- Chatbot, Customer service, Content generation
- งานที่ต้องการทั้งคุณภาพและความเร็ว
- ✅ ใช้เมื่อ: ไม่รู้จะเลือกอะไร — Sonnet มักเป็นคำตอบ

### Haiku — เมื่อต้องการความเร็วและต้นทุนต่ำ
- Classification, Routing, Summarization
- Real-time chat ที่ต้องการ latency ต่ำ
- งานขนาดเล็กที่ทำซ้ำจำนวนมาก
- ✅ ใช้เมื่อ: ประมวลผลจำนวนมาก (batch jobs)

## Context Window 200K

ทุกโมเดลรองรับ **200,000 tokens** (~150,000 คำภาษาอังกฤษ / ~300 หน้า A4)

ดูรายละเอียด: [[concepts/context-window]]

## Vision Capability

ทุกโมเดล Claude 4.x รองรับการอ่านภาพ:
- รูปภาพ JPG, PNG, GIF, WebP
- PDF (บางรุ่น)
- กราฟ ตาราง แผนภาพ
- UI Screenshot

## Rate Limits (ระดับ Free/Tier 1)

| | Free | Tier 1 |
|--|--|--|
| RPM (Requests/min) | 5 | 50 |
| TPM (Tokens/min) | 25K | 50K |
| TPD (Tokens/day) | 50K | 1M |

## Batch API

สำหรับงานที่ไม่ต้องการ real-time:
- ลดราคา 50% จากราคาปกติ
- ส่ง request เป็น batch และรับผลภายใน 24 ชั่วโมง
- เหมาะกับ: data processing, bulk analysis

## ประวัติ Model Versions

```
Claude 1 (2023) → Claude 2 (2023) → Claude 3 (2024)
→ Claude 3.5 (2024) → Claude 3.7 (2025) → Claude 4.x (2025–2026)
```

## Related
- [[entities/claude]]
- [[entities/anthropic]]
- [[concepts/context-window]]
- [[concepts/tokenization]]
- [[references/claude-api-cheatsheet]]
