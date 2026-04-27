---
title: LLM Wiki Pattern
tags: [knowledge-management, llm, pattern, ai]
category: concepts
created: 2026-04-27
updated: 2026-04-27
sources: [karpathy-gist]
summary: "แนวทาง compile ความรู้เป็น interconnected markdown files ครั้งเดียว แทนที่จะถาม LLM ซ้ำหรือทำ RAG ทุกครั้ง — LLM เป็น maintainer, Obsidian เป็น viewer"
---

# LLM Wiki Pattern

แนวคิดที่เสนอโดย [[andrej-karpathy]] — แทนที่จะถาม LLM คำถามเดิมซ้ำ ๆ หรือทำ RAG ทุกครั้ง ให้ **compile ความรู้ครั้งเดียว** เป็น markdown files ที่เชื่อมโยงกัน แล้วให้ LLM เป็นคนดูแลและอัปเดต

## หลักการ

- **Compile once, query many times** — ลงทุนเวลาอ่านและสรุปครั้งเดียว ใช้ได้นานหลายเดือน
- **LLM เป็น maintainer** — ไม่ใช่ search engine — มันอ่าน, merge, ตัดสินใจว่า page ไหนต้อง update
- **Obsidian เป็น viewer** — ดู graph ความเชื่อมโยง, navigate ด้วย [[wikilinks]]
- **Schema emerges** — ไม่ต้องออกแบบ taxonomy ล่วงหน้า มันจะ emerge จากเนื้อหาเอง

## ทำไมดีกว่า RAG ธรรมดา

| RAG | LLM Wiki |
|---|---|
| index ทุก chunk เป็น vector | compile เป็น wiki pages ที่มีความหมาย |
| ตอบจาก raw text | ตอบจาก curated, cross-linked knowledge |
| ไม่รู้ว่า sources ขัดแย้งกันไหม | flag contradictions ชัดเจน |
| rebuild index ทุกครั้ง | [[delta-tracking]] — process แค่ส่วนที่เปลี่ยน |

## Implementation ใน vault นี้

ดูที่ [[wiki-ingest-workflow]] สำหรับขั้นตอนจริง

## Related
- [[delta-tracking]] — วิธี track ว่า ingest อะไรไปแล้ว
- [[wiki-ingest-workflow]] — ขั้นตอน ingest เอกสาร
- [[andrej-karpathy]] — ผู้เสนอ pattern นี้
- [[ai-knowledge-management]] — big picture view
