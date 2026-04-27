---
title: Karpathy LLM Wiki Gist
tags: [reference, llm, knowledge-management, karpathy]
category: references
created: 2026-04-27
updated: 2026-04-27
summary: "Gist โดย Andrej Karpathy อธิบาย pattern การใช้ LLM ดูแล personal knowledge base — เป็นแรงบันดาลใจหลักของ vault และ framework นี้ทั้งหมด"
---

# Karpathy LLM Wiki Gist

**Source:** gist.github.com/karpathy/442a6bf555914893e9891c11519de94f  
**Author:** [[andrej-karpathy]]  
**Type:** Personal essay / pattern description

## แนวคิดหลักจาก gist

> แทนที่จะถาม LLM ซ้ำ ๆ หรือทำ RAG ทุกครั้ง ให้ compile ความรู้ครั้งเดียว เป็น interconnected markdown files ที่ LLM เป็นคน maintain

ประเด็นสำคัญ:
1. LLM เป็น **maintainer** ไม่ใช่ search engine
2. Knowledge ถูก compile ไว้แล้ว ไม่ต้อง re-process ทุกครั้งที่ถาม
3. Markdown + wikilinks เป็น format ที่ทั้งคนและ LLM อ่านได้ดี
4. Schema ไม่ต้องออกแบบล่วงหน้า — emerge จากเนื้อหาเอง

## สิ่งที่ framework นี้เพิ่มเติม

เทียบกับ gist ต้นฉบับ:
- **[[delta-tracking]]** — manifest tracks ว่า ingest อะไรไปแล้ว
- Multi-agent ingest — Claude history, Codex, documents, URLs
- Provenance tracking — บอกได้ว่า claim แต่ละอันมาจากไหน
- Cross-linking อัตโนมัติ
- Archive & rebuild

## Related
- [[llm-wiki-pattern]] — concept page ที่สรุป pattern นี้
- [[andrej-karpathy]] — ผู้เขียน
- [[ai-knowledge-management]] — synthesis ที่กว้างขึ้น
