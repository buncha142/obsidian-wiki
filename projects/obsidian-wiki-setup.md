---
title: Obsidian Wiki Setup
tags: [project, setup, knowledge-management, active]
category: projects
created: 2026-04-27
updated: 2026-04-27
summary: "Project log การ setup personal wiki vault — decisions, config, และสิ่งที่เรียนรู้ระหว่าง initialize"
---

# Obsidian Wiki Setup

**Status:** Active — vault initialized, รอ ingest เนื้อหาจริง  
**Started:** 2026-04-27

---

## Config Decisions

| Decision | เลือก | เหตุผล |
|---|---|---|
| Vault path | `/Users/miniboxmacmini/Obsidian/obsidian-wiki` | เป็น repo เดียวกัน — git track ทุกอย่าง |
| Sources dir | `~/Documents` | default — เอกสารทั่วไปอยู่ที่นี่ |
| Claude history | auto-discover | `~/.claude` มีอยู่แล้ว |
| QMD | ปิด | ยังไม่ได้ install — ใช้ grep fallback ไปก่อน |

## Architecture ที่เลือก

Vault path = repo path — ข้อดี:
- git track ทุก change ใน wiki pages
- skills และ wiki pages อยู่ที่เดียวกัน

ข้อควรระวัง:
- `.gitignore` ควร ignore `.obsidian/workspace.json` (user-specific state)

## Skills ที่ install

ครบชุด obsidian-wiki skills ผ่าน `npx skills add`:
- `wiki-ingest`, `wiki-query`, `wiki-status`
- `claude-history-ingest`
- `cross-linker`, `wiki-lint`, `wiki-synthesize`
- และอื่น ๆ (ดู `GUIDE.md`)

## Open Questions

- [ ] QMD semantic search — ควร install ไหม เมื่อ vault ใหญ่ขึ้น?
- [ ] Plugin เพิ่มเติม: Dataview, Graph Analysis, Templater, Obsidian Git?

## Related
- [[journal/2026-04-27]] — บันทึกวันที่ setup
- [[llm-wiki-pattern]] — pattern ที่ vault นี้ implement
- [[obsidian]] — tool ที่ใช้
