---
title: คู่มือ Claude ฉบับสมบูรณ์ 2026 (STAG)
tags: [reference, claude, book, stag, thai]
category: references
created: 2026-06-14
updated: 2026-06-14
sources: [claude-manual-stag-2026]
summary: "หนังสือคู่มือ Claude ภาษาไทยฉบับสมบูรณ์โดย STAG ครอบคลุม 500 หน้า ตั้งแต่พื้นฐาน Constitutional AI จนถึง Advanced Agentic Workflows"
---

# คู่มือ Claude ฉบับสมบูรณ์ 2026 (STAG)

**ชื่อเต็ม:** คู่มือ Claude ฉบับสมบูรณ์  
**ผู้จัดทำ:** STAG  
**ปี:** 2026  
**ภาษา:** ไทย  
**จำนวนหน้า:** 500 หน้า  
**ไฟล์ต้นฉบับ:** `_raw/คู่มือ_Claude_ฉบับสมบูรณ์-STAG.pdf`

## โครงสร้างหนังสือ

| Unit | ชื่อ | หน้า | สถานะ ingest |
|------|------|------|---------------|
| Unit 0 | Claude คืออะไร | 1–15 | ✅ ingested |
| Unit 1 | Models & Tokens | 16–34 | ✅ ingested |
| Unit 2 | Prompt Engineering | 67–93 | ✅ ingested |
| Unit 3 | Advanced Techniques | ~100–150 | ⬜ pending |
| Unit 4 | Agentic Workflows | ~150–200 | ⬜ pending |
| Unit 5–9 | Advanced Topics | ~200–400 | ⬜ pending |
| Appendix | Glossary + API Cheatsheet | 475–500 | ✅ ingested |

## เนื้อหาหลักที่ ingest แล้ว (Focus Mode: Units 0–2 + Glossary)

### Unit 0 — Claude คืออะไร (หน้า 1–15)
- [[entities/anthropic]] — บริษัทผู้สร้าง Claude
- [[concepts/constitutional-ai]] — หลัก Helpful, Harmless, Honest
- [[entities/claude]] — Claude เป็น AI ไม่ใช่ Search Engine
- Principal Hierarchy: Anthropic → Operator → User
- 5-Layer Context Model

### Unit 1 — Models & Tokens (หน้า 16–34)
- [[concepts/claude-models-family]] — Opus / Sonnet / Haiku ราคาและการเลือกใช้
- [[concepts/tokenization]] — ระบบ token ภาษาไทยแพงกว่า 2–2.8×
- [[concepts/context-window]] — 200K tokens, Lost-in-the-Middle Effect
- Vision capability, Rate Limits, Batch API

### Unit 2 — Prompt Engineering (หน้า 67–93)
- [[concepts/prompt-engineering]] — 6-component anatomy + เทคนิค
- XML Tagging, Chain-of-Thought, Few-shot
- 5 Anti-patterns ที่ควรหลีกเลี่ยง
- PARE Framework สำหรับทดสอบ prompt

### Appendix — Glossary + API Cheatsheet (หน้า 475–500)
- [[references/claude-glossary]] — 110+ คำศัพท์ไทย-อังกฤษ
- [[references/claude-api-cheatsheet]] — Model IDs, ราคา, Python/TypeScript SDK

## Related
- [[entities/anthropic]]
- [[entities/claude]]
- [[concepts/claude-models-family]]
- [[concepts/prompt-engineering]]
- [[concepts/constitutional-ai]]
- [[references/claude-glossary]]
- [[references/claude-api-cheatsheet]]
