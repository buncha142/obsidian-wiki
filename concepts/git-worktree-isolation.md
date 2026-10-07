---
title: Git Worktree Isolation สำหรับ Multi-Agent
tags: [git, worktree, claude-code, multi-agent, isolation]
category: concepts
created: 2026-10-07
updated: 2026-10-07
sources: [kimi-agent-teams-guide-2026]
summary: "ใช้ git worktree แยก working directory ต่อ agent เพื่อไม่ให้หลาย agent เขียนไฟล์ทับกัน — ใน Claude Code ตั้งด้วย isolation: worktree หรือ claude -w"
provenance:
  extracted: 0.75
  inferred: 0.25
  ambiguous: 0.0
---

# Git Worktree Isolation สำหรับ Multi-Agent

**Git worktree = working directory แยกอีกชุด อยู่บน branch ของตัวเอง แต่ใช้ประวัติ `.git` เดียวกับ checkout หลัก**

เมื่อหลาย agent เขียนไฟล์พร้อมกัน การให้แต่ละตัวมี worktree ของตัวเองทำให้การแก้ไขของตัวหนึ่งไม่ไปแตะงานค้างของอีกตัว — ปัญหา "2 agents แก้ไฟล์เดียวกัน" เป็นหนึ่งในสาเหตุที่ทำให้ผลลัพธ์เสียหายได้แทบแน่นอนที่สุดใน [[concepts/claude-code-agent-teams]]

## วิธีใช้ใน Claude Code

| บริบท | วิธี |
|---|---|
| ต่อ agent (subagent / teammate) | ใส่ `isolation: worktree` ใน YAML frontmatter ของไฟล์ agent — Claude Code สร้าง worktree ใหม่ต่อการเรียกแต่ละครั้ง และลบให้อัตโนมัติเมื่อเสร็จ |
| เซสชัน CLI | `claude --worktree` หรือ `claude -w` |
| Desktop app | สร้าง worktree ต่อเซสชันให้อัตโนมัติ |

## เทียบกับ git ล้วน

ถ้าทำเอง คำสั่งพื้นฐานคือ `git worktree add ../feature-x -b feature-x` แล้วลบด้วย `git worktree remove ../feature-x` ^[inferred]

## หลักการที่ใช้คู่กัน

- Worktree แยก **ไฟล์** แต่ไม่แยก **ความรับผิดชอบ** — ยังต้องกำหนด ownership (1 โมดูล = 1 agent) ใน `CLAUDE.md` เพื่อลด conflict ตอน merge ^[inferred]
- งานที่ต้องแตะ component เดียวกันควรทำตามลำดับ ไม่ใช่ขนาน แม้แยก worktree แล้ว
- Merge กลับเข้า branch หลักให้ lead เป็นคนคุมลำดับ ^[inferred]
- ใช้ได้เฉพาะโฟลเดอร์ที่เป็น git repo — vault ที่ไม่ใช่ git (เช่น `~/Documents`) ใช้ไม่ได้ ^[inferred]

## ดูเพิ่ม

- [[concepts/claude-code-agent-teams]]
- [[concepts/claude-products]] — Claude Code กับ Git workflow
- [[references/kimi-agent-teams-guide-2026]]
