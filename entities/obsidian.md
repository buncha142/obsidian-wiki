---
title: Obsidian
tags: [tool, note-taking, markdown, knowledge-management]
category: entities
created: 2026-04-27
updated: 2026-04-27
sources: [obsidian-wiki-readme]
summary: "Markdown note-taking app ที่เก็บ files ไว้ใน local machine — ทำหน้าที่เป็น viewer และ navigator ใน vault นี้ ขณะที่ AI เป็นคน maintain เนื้อหา"
---

# Obsidian

Markdown-based note-taking app ที่เก็บทุกอย่างเป็น `.md` files ใน local machine — ไม่มี vendor lock-in

## บทบาทใน vault นี้

Obsidian เป็น **viewer และ navigator** ไม่ใช่คนเขียนเนื้อหา:

| Obsidian ทำ | AI ทำ |
|---|---|
| แสดง wiki pages | สร้าง/อัปเดต wiki pages |
| Graph View — เห็น network | ตัดสินใจว่า page ไหนต้องมี |
| Navigate ด้วย [[wikilinks]] | merge, cross-link, flag contradictions |

## Features ที่ใช้ใน workflow นี้

- **Graph View** — เห็น network ความเชื่อมโยงระหว่าง concepts (`Cmd+P` → "Open graph view")
- **Wikilinks** `[[page-name]]` — navigate ระหว่าง pages
- **Frontmatter** — metadata ที่ AI อ่านและเขียน (title, tags, summary, sources)
- **Dataview plugin** — query pages เหมือน database (ติดตั้งไว้แล้ว)

## เปิด Vault

File → Open Vault → เลือก `/Users/miniboxmacmini/Obsidian/obsidian-wiki`

## Related
- [[llm-wiki-pattern]] — pattern ที่ใช้ Obsidian เป็น viewer
- [[ai-knowledge-management]] — บริบทที่กว้างขึ้น
