---
title: Tutorial — เรียนรู้การใช้งาน Wiki
updated: 2026-04-27
---

# Tutorial — เรียนรู้การใช้งาน Wiki

> อ่านไฟล์นี้ครั้งเดียวตอนเริ่มต้น — หลังจากนั้นใช้ `GUIDE.md` เป็น reference ประจำวัน

---

## โครงสร้างที่สร้างไว้ให้แล้ว

```
obsidian-wiki/
│
├── GUIDE.md                          ← reference: skills ทั้งหมด, format, config
├── TUTORIAL.md                       ← ไฟล์นี้
│
├── concepts/
│   ├── llm-wiki-pattern.md           ← แนวคิดหลักของระบบ
│   └── delta-tracking.md             ← วิธีที่ระบบ track การเปลี่ยนแปลง
│
├── entities/
│   ├── andrej-karpathy.md            ← บุคคล
│   └── obsidian.md                   ← เครื่องมือ
│
├── skills/
│   └── wiki-ingest-workflow.md       ← ขั้นตอน ingest เอกสาร (3 เส้นทาง)
│
├── references/
│   └── karpathy-gist.md              ← source ต้นฉบับที่เป็นแรงบันดาลใจ
│
├── synthesis/
│   └── ai-knowledge-management.md   ← AI วิเคราะห์ข้ามหัวข้อ
│
├── journal/
│   └── 2026-04-27.md                ← บันทึกวันที่ setup vault
│
├── projects/
│   └── obsidian-wiki-setup.md       ← decision log การ setup
│
└── _raw/
    └── rough-note-example.md        ← โน้ตหยาบตัวอย่าง — รอ ingest
```

**ทุก page มี:**
- `frontmatter` — title, tags, summary, sources
- `[[wikilinks]]` — เชื่อม pages กัน
- `## Related` — บอก pages ที่เกี่ยวข้อง

---

## บทเรียนที่ 1 — ดูภาพรวมของ Wiki

เปิด `index.md` เพื่อดูสารบัญ หรือพิมพ์ prompt นี้ใน Claude:

```
อ่าน index.md ให้ฉันดูว่ามีอะไรบ้างใน wiki
```

**Prompt นี้ทำอะไร:** Claude อ่าน `index.md` แล้วสรุปภาพรวมของ wiki ทั้งหมดในการตอบเดียว

---

## บทเรียนที่ 2 — Query จาก Wiki (skill หลักที่ใช้ทุกวัน)

```
/wiki-query อธิบาย LLM Wiki Pattern ให้ฉันฟัง
```

**Prompt นี้ทำอะไร:** Claude จะ:
1. ค้นหา pages ที่เกี่ยวข้องกับ topic
2. อ่าน `summary:` ของแต่ละ page ก่อน (เร็ว, ประหยัด)
3. เปิด body เต็มเฉพาะ pages ที่จำเป็น
4. ตอบพร้อม citations บอกว่ามาจาก page ไหน

**ตัวอย่าง queries อื่น ๆ:**
```
/wiki-query Andrej Karpathy คือใคร?
/wiki-query delta tracking ทำงานอย่างไร?
/wiki-query quick: ความแตกต่างระหว่าง RAG กับ wiki pattern
```
> `quick:` = ค้นแค่ titles + summaries ไม่เปิด body — เร็วกว่า

---

## บทเรียนที่ 3 — ทดสอบ Staging Area

`_raw/rough-note-example.md` คือโน้ตหยาบเกี่ยวกับ Transformer architecture ที่รอ promote

ลองพิมพ์:
```
/wiki-ingest
```

**Prompt นี้ทำอะไร:** Claude จะ:
- อ่านทุกไฟล์ใน `_raw/` และ `~/Documents` (เฉพาะที่ยังไม่ ingest)
- สร้าง wiki pages ที่เหมาะสม เช่น `concepts/transformer-architecture.md`
- ลบไฟล์ออกจาก `_raw/` หลัง promote แล้ว
- อัปเดต `index.md`, `log.md`, `hot.md`

**การใช้งานจริง:** เมื่อมีโน้ตหยาบหรือไอเดียใหม่:
1. สร้างไฟล์ `.md` ใน `_raw/` (เนื้อหาอะไรก็ได้ ยังไม่ต้องจัดระเบียบ)
2. สั่ง `/wiki-ingest` — AI จัดการให้เอง

---

## บทเรียนที่ 4 — ดึง Knowledge จาก Claude Conversations

```
/claude-history-ingest
```

**Prompt นี้ทำอะไร:** Claude อ่าน `~/.claude/projects/*/` — conversations ทั้งหมดของคุณ แล้วดึง:
- Concepts ที่เคยเรียนรู้
- Decisions ที่เคยตัดสินใจ
- Patterns และเทคนิคที่ใช้บ่อย
- แล้วสร้าง/อัปเดต wiki pages พร้อม source attribution

> นี่คือ feature ที่ทรงพลังมาก — ขุดความรู้จากทุก conversation ที่เคยคุยกับ Claude

---

## บทเรียนที่ 5 — ตรวจสุขภาพ Wiki

หลังจาก ingest เนื้อหาแล้ว ลองพิมพ์:

```
/wiki-lint
```

**Prompt นี้ทำอะไร:** ตรวจหา:
- `[[wikilinks]]` ที่ชี้ไป page ที่ไม่มีจริง
- Pages ที่ไม่มีใคร link ถึง (orphans)
- Pages ที่ขาด frontmatter
- Claims ที่ขัดแย้งกันระหว่าง pages

ตามด้วย:
```
/cross-linker
```
AI จะสแกน vault แล้วเพิ่ม `[[wikilinks]]` อัตโนมัติในจุดที่ยังขาดอยู่

---

## สรุป Flow การใช้งานจริง

```
มีโน้ตหยาบ?        → โยนลง _raw/  แล้วสั่ง /wiki-ingest
มีเอกสารใหม่?       → /wiki-ingest
ทำงานกับ project?   → /wiki-update  (บันทึกสิ่งที่เรียนรู้)
อยากรู้บางอย่าง?     → /wiki-query [คำถาม]
ทำสัปดาห์ละครั้ง:    → /wiki-lint  แล้ว  /cross-linker
vault ใหญ่เกินไป?   → /wiki-rebuild  (archive + rebuild จากศูนย์)
```

---

## ขั้นตอนถัดไปที่แนะนำ

- [ ] เปิด vault ใน Obsidian → ดู Graph View (`Cmd+P` → "Open graph view")
- [ ] ทดลอง **บทเรียนที่ 2** — `/wiki-query` กับ demo pages ที่มีอยู่
- [ ] รัน `/claude-history-ingest` — ขุด conversations ของคุณ
- [ ] รัน `/wiki-ingest` — ingest `~/Documents`

---

*สำหรับ reference ทุก skills: ดู `GUIDE.md`*
