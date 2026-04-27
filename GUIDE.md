---
title: Wiki Guide — คู่มือการใช้งาน
updated: 2026-04-27
---

# Wiki Guide — คู่มือการใช้งาน

> **TL;DR** — บอก AI ว่าอยากเรียนรู้อะไร → AI อ่านเอกสาร → สร้าง wiki pages → คุณถามได้ตลอดเวลา

---

## โครงสร้างของ Vault นี้

```
obsidian-wiki/
│
├── concepts/          ← แนวคิด, คำศัพท์, patterns
├── entities/          ← คน, เครื่องมือ, บริษัท, โปรเจกต์
├── skills/            ← วิธีทำสิ่งต่าง ๆ, how-to, เทคนิค
├── references/        ← แหล่งอ้างอิง, เอกสารต้นฉบับ
├── synthesis/         ← การวิเคราะห์ข้ามหัวข้อ (AI สร้าง)
├── journal/           ← บันทึกตาม timeline
├── projects/          ← ความรู้เฉพาะโปรเจกต์
│
├── _raw/              ← โยนโน้ตหยาบไว้ก่อน → AI จัดการให้
├── _archives/         ← snapshot ก่อน rebuild
│
├── index.md           ← สารบัญ (AI อัปเดตให้เอง)
├── log.md             ← Audit log ทุก operation
├── hot.md             ← Snapshot กิจกรรมล่าสุด
├── .env               ← Config: vault path, sources
└── GUIDE.md           ← ไฟล์นี้
```

---

## หัวใจของระบบ — 4 ขั้นตอน

```
1. INGEST    → AI อ่านเอกสาร/conversations ของคุณ
2. EXTRACT   → ดึง concepts, entities, claims, relationships ออกมา
3. RESOLVE   → merge เข้า wiki ที่มีอยู่ (ไม่ duplicate)
4. SCHEMA    → จัดหมวด, สร้าง wikilinks, อัปเดต index
```

**ทุกครั้งที่ ingest ซ้ำ:** ระบบ track ว่าไฟล์ไหน ingest ไปแล้ว → ประมวลผลแค่ส่วนที่เปลี่ยน (delta only)

---

## Skills ทั้งหมด — เรียงตาม workflow

### Phase 1: Setup & Status

| Prompt ที่พิมพ์ | ทำอะไร |
|---|---|
| `/wiki-status` | ดูว่า ingest ไปแล้วอะไร อะไรยังรอ กี่ pages |
| `/wiki-setup` | initialize vault structure (ทำครั้งเดียวตอนเริ่ม) |

### Phase 2: Ingest Sources

| Prompt ที่พิมพ์ | ทำอะไร |
|---|---|
| `/wiki-ingest` | อ่านเอกสารใน `~/Documents` → สร้าง/อัปเดต wiki pages |
| `/claude-history-ingest` | ขุด Claude conversations (~/.claude) → wiki pages |
| `/data-ingest` | ingest text ใด ๆ — chat export, transcript, log |
| `/ingest-url [url]` | อ่านเว็บเพจแล้วสรุปเข้า wiki |
| `/wiki-research [topic]` | ค้นเว็บหลายรอบแล้วบันทึกผลลง wiki อัตโนมัติ |
| `/wiki-capture` | บันทึก conversation ปัจจุบันเป็น wiki note ทันที |

### Phase 3: Query & Read

| Prompt ที่พิมพ์ | ทำอะไร |
|---|---|
| `/wiki-query [คำถาม]` | ถามคำถาม — AI ค้น wiki แล้วตอบพร้อม citations |
| `/wiki-query quick: [คำถาม]` | ค้นแบบเร็ว — อ่านแค่ titles + summaries ไม่เปิด body |

### Phase 4: Maintain & Improve

| Prompt ที่พิมพ์ | ทำอะไร |
|---|---|
| `/wiki-lint` | หา broken links, orphan pages, contradictions |
| `/cross-linker` | เพิ่ม [[wikilinks]] อัตโนมัติระหว่าง pages |
| `/tag-taxonomy` | normalize tags ให้สอดคล้องทั่วทั้ง vault |
| `/wiki-synthesize` | AI หา gaps แล้วสร้าง synthesis pages ข้ามหัวข้อ |
| `/wiki-update` | sync ความรู้จาก project ปัจจุบันเข้า wiki |

### Phase 5: Export & Rebuild

| Prompt ที่พิมพ์ | ทำอะไร |
|---|---|
| `/wiki-export` | export graph เป็น JSON, GraphML, HTML interactive |
| `/wiki-rebuild` | archive ทั้งหมด แล้ว rebuild จากศูนย์ |
| `/wiki-dashboard` | สร้าง Obsidian Bases dashboard views |

---

## Format ของ Wiki Page

ทุก page มีโครงสร้างนี้:

```markdown
---
title: ชื่อ page
tags: [tag1, tag2]
category: concepts
created: 2026-04-27
updated: 2026-04-27
sources: [reference-slug]
summary: "1-2 ประโยค — ใช้ตอน wiki-query preview ก่อนเปิดเต็ม"
---

# ชื่อ page

เนื้อหา...

## Related
- [[wikilink-to-related-page]]
```

**`summary:`** สำคัญมาก — `/wiki-query` อ่าน summary ก่อนเสมอ เพื่อตัดสินว่าต้องเปิด page เต็มไหม

---

## Flow การใช้งาน Day-to-Day

```
เมื่อมีเอกสารใหม่:
  → โยนลง _raw/  (ถ้าเป็นโน้ตหยาบ)
  → หรือสั่ง /wiki-ingest  (ถ้าอยาก ingest เลย)

เมื่ออยากรู้บางอย่าง:
  → /wiki-query [คำถาม]

เมื่อทำงานกับ project:
  → /wiki-update  (บันทึกสิ่งที่เรียนรู้เข้า wiki)

เป็นประจำ (weekly):
  → /wiki-lint    (ตรวจสุขภาพ wiki)
  → /cross-linker (เพิ่ม wikilinks ที่หาย)
```

---

## _raw/ Staging Area — ใช้อย่างไร

1. มีโน้ตที่อยากบันทึก แต่ยังไม่พร้อมจัด
2. สร้างไฟล์ `.md` ใด ๆ ใน `_raw/`
3. สั่ง `/wiki-ingest` — AI จะ:
   - อ่านทุกไฟล์ใน `_raw/`
   - สร้าง/อัปเดต wiki pages ที่เหมาะสม
   - **ลบไฟล์ออกจาก `_raw/`** หลัง promote แล้ว

---

## Obsidian Graph View

เปิด graph ดูความเชื่อมโยงระหว่าง pages:
- **Mac:** `Cmd + P` → พิมพ์ "Open graph view"
- **Ribbon:** คลิกไอคอน network ด้านซ้าย

ถ้าอยากให้ nodes มีสีตามโฟลเดอร์/tag:
→ บอก AI ว่า **"color my graph"** → skill `graph-colorize` จะจัดการให้

---

## ตัวอย่าง Prompts ที่ใช้บ่อย

```
# ดู status ทั้งหมด
/wiki-status

# ingest Claude conversations
/claude-history-ingest

# ถามเรื่องที่ ingest ไปแล้ว
/wiki-query what do I know about [topic]?

# บันทึกโน้ตหยาบ
→ สร้างไฟล์ใน _raw/ แล้วสั่ง /wiki-ingest

# ดูแล wiki รายสัปดาห์
/wiki-lint
/cross-linker
```

---

*ไฟล์นี้ไม่ได้อัปเดตอัตโนมัติ — อ่านได้ตลอดเวลาเป็น reference*
