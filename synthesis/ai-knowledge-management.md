---
title: AI + Knowledge Management — Synthesis
tags: [synthesis, knowledge-management, ai, llm, pkm]
category: synthesis
created: 2026-04-27
updated: 2026-04-27
sources: [karpathy-gist, obsidian-wiki-readme]
summary: "Synthesis ข้ามหัวข้อ: ทำไม LLM จึงเหมาะกับการ maintain knowledge base มากกว่าแค่ตอบคำถาม — และ tradeoffs ระหว่าง RAG, wiki pattern, และ plain chat"
provenance: "extracted: 60%, inferred: 40%"
---

# AI + Knowledge Management — Synthesis

*หน้านี้สร้างโดย AI จากการอ่านหลาย sources — มาร์กส่วนที่ synthesize ด้วย `^[inferred]`*

---

## ปัญหาที่แก้

การพึ่ง LLM แบบ plain chat มีปัญหา:
- ถามคำถามเดิมซ้ำหลายครั้ง — เสีย token, ได้คำตอบต่างกัน
- RAG แก้บางส่วน แต่ index raw chunks ที่ไม่ได้ curate — signal ต่ำ
- ไม่มีที่เดียวที่รู้ว่า "ฉันรู้อะไรแล้ว"

## ทำไม Wiki Pattern แก้ได้

[[llm-wiki-pattern]] เปลี่ยน LLM จาก *ผู้ตอบ* เป็น *ผู้ดูแลความรู้*:

```
Plain Chat:    คุณถาม → LLM ตอบจาก training data
RAG:           คุณถาม → ค้น vector index → LLM สรุป raw chunks
Wiki Pattern:  LLM compile ครั้งเดียว → คุณถามจาก curated wiki
```

ความแตกต่างที่สำคัญ: ^[inferred]
- **Quality** — wiki pages ถูก curate และ cross-link แล้ว ไม่ใช่ raw text
- **Consistency** — ถามซ้ำ ได้คำตอบที่ consistent เพราะ source เดิม
- **Transparency** — รู้ว่าความรู้มาจากไหน (provenance tracking)

## Tradeoffs

| ข้อดี | ข้อเสีย |
|---|---|
| Query cost คงที่ไม่ขึ้นกับขนาด vault | ต้องลงทุน ingest ครั้งแรก |
| Knowledge ถาวรและ traceable | ต้อง maintain เมื่อ sources เปลี่ยน |
| เห็น contradictions ชัด | ไม่เหมาะกับข้อมูล real-time |

## Pattern ที่ emerge ^[inferred]

จากการ ingest หลาย sources พบว่า knowledge management ที่ดีต้องมี 3 ชั้น:
1. **Capture** — raw notes, conversations, documents (`_raw/`)
2. **Compile** — curated wiki pages ที่ AI maintain (`concepts/`, `entities/`, etc.)
3. **Query** — ถามจาก compiled layer ไม่ใช่ raw layer

## Related
- [[llm-wiki-pattern]] — pattern หลัก
- [[delta-tracking]] — implementation detail ที่ทำให้ maintain ได้จริง
- [[wiki-ingest-workflow]] — วิธีปฏิบัติ
- [[karpathy-gist]] — source หลัก
- [[andrej-karpathy]] — ผู้เสนอ
- [[obsidian]] — tool ที่ใช้เป็น viewer
