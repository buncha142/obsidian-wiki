---
title: Delta Tracking
tags: [knowledge-management, ingest, efficiency, manifest]
category: concepts
created: 2026-04-27
updated: 2026-04-27
sources: [obsidian-wiki-readme]
summary: "วิธีที่ระบบ track ว่า source file ไหน ingest ไปแล้ว — ผ่าน .manifest.json — เพื่อให้ ingest ครั้งต่อไปประมวลผลแค่ส่วนที่เปลี่ยน ไม่ต้อง re-process ทั้งหมด"
---

# Delta Tracking

หนึ่งในความสามารถหลักของระบบ [[llm-wiki-pattern]] — แทนที่จะ re-ingest เอกสารทั้งหมดทุกครั้ง ระบบ track สิ่งที่ทำไปแล้วและ **process เฉพาะส่วนที่เปลี่ยน**

## กลไก

ไฟล์ `.manifest.json` ที่รากของ vault เก็บข้อมูล:
- **path** — absolute path ของ source file
- **last_ingested** — timestamp ที่ ingest ล่าสุด
- **hash** — content hash เพื่อ detect การเปลี่ยนแปลง
- **wiki_pages** — list ของ wiki pages ที่ผลิตออกมาจาก source นี้

## Flow เมื่อ /wiki-ingest รัน

```
1. อ่าน .manifest.json
2. Scan source directory
3. เปรียบเทียบ hash → แยก: new | changed | unchanged
4. Process เฉพาะ new + changed
5. อัปเดต .manifest.json
```

## ประโยชน์

- **ประหยัด token** — ไม่ re-process สิ่งที่ไม่เปลี่ยน
- **ปลอดภัย** — ไม่ overwrite wiki pages ที่ดีอยู่แล้วโดยไม่จำเป็น
- **Traceable** — รู้ว่า wiki page แต่ละหน้ามาจาก source ไหน

## Related
- [[llm-wiki-pattern]] — pattern ภาพรวมที่ delta tracking เป็นส่วนหนึ่ง
- [[wiki-ingest-workflow]] — ขั้นตอนที่ delta tracking ทำงานอยู่ใน
