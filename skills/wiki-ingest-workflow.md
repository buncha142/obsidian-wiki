---
title: Wiki Ingest Workflow
tags: [workflow, ingest, how-to, wiki]
category: skills
created: 2026-04-27
updated: 2026-04-27
sources: [obsidian-wiki-readme]
summary: "ขั้นตอนการ ingest เอกสารเข้า wiki — ตั้งแต่ drop ไฟล์ลง _raw/ จนถึงการที่ AI สร้าง wiki pages พร้อม wikilinks และ update index"
---

# Wiki Ingest Workflow

วิธีนำเอกสารของคุณเข้าสู่ wiki ผ่าน 2 เส้นทาง

---

## เส้นทาง A — Direct Ingest (เอกสารพร้อมแล้ว)

**Prompt ที่พิมพ์:**
```
/wiki-ingest
```

AI จะ:
1. อ่าน `.manifest.json` — รู้ว่า ingest อะไรไปแล้ว
2. Scan `~/Documents` — หาไฟล์ใหม่หรือที่เปลี่ยน
3. อ่านเฉพาะ files ที่ยังไม่ ingest (ดู [[delta-tracking]])
4. Extract: concepts, entities, claims, relationships
5. Resolve: merge เข้า pages ที่มีอยู่ หรือสร้างใหม่
6. อัปเดต `index.md`, `log.md`, `hot.md`

**รองรับ format:** `.md`, `.pdf`, `.txt`, `.jsonl`, plain text, images

---

## เส้นทาง B — Staging via `_raw/`

เหมาะสำหรับโน้ตหยาบ, clipboard paste, ไอเดียเร็ว ๆ

**ขั้นตอน:**
1. สร้างไฟล์ `.md` ใน `_raw/` (เนื้อหาอะไรก็ได้)
2. พิมพ์ `/wiki-ingest` — AI จะ promote ไฟล์นั้นเป็น wiki pages แล้วลบออกจาก `_raw/`

---

## เส้นทาง C — Claude History

**Prompt ที่พิมพ์:**
```
/claude-history-ingest
```

AI จะ:
1. อ่าน `~/.claude/projects/*/` — conversations ทั้งหมด
2. ดึง: decisions, patterns, concepts, project knowledge ออกมา
3. สร้าง/อัปเดต wiki pages พร้อม source attribution

---

## Provenance Tags

ทุก claim ใน wiki pages มี tag บอกที่มา:
- *(ไม่มี tag)* — extracted จาก source โดยตรง
- `^[inferred]` — AI synthesize/สรุปเอง
- `^[ambiguous]` — sources ขัดแย้งกัน

---

## Related
- [[delta-tracking]] — วิธี track ว่า ingest อะไรไปแล้ว
- [[llm-wiki-pattern]] — ภาพรวมของ pattern นี้
