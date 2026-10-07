---
title: Claude Code Agent Teams
tags: [claude, claude-code, multi-agent, agent, parallelism]
category: concepts
created: 2026-10-07
updated: 2026-10-07
sources: [kimi-agent-teams-guide-2026]
summary: "ฟีเจอร์ experimental ของ Claude Code ให้หลายเซสชันทำงานขนานเป็นทีม: lead + teammates, shared task list, mailbox, file lock — ต่างจาก subagents ที่เป็นการมอบหมายทางเดียว"
provenance:
  extracted: 0.80
  inferred: 0.12
  ambiguous: 0.08
---

# Claude Code Agent Teams

**Agent Teams = หลายเซสชันของ Claude Code ทำงานบน codebase เดียวกันแบบขนาน โดยมีชั้นประสานงาน (coordination layer) คอยคุม**

เป็นการต่อยอด pattern Orchestrator-Subagents / Peer-to-Peer ใน [[concepts/claude-agent-sdk]] มาเป็นฟีเจอร์สำเร็จรูปใน [[concepts/claude-products|Claude Code]] ^[inferred]

> ⚠️ แหล่งที่มาเป็นบทความของ Kimi ซึ่งเป็นคู่แข่งและปิดท้ายด้วยการโปรโมท [[entities/kimi-agent-swarm]] — ตัวเลขเวอร์ชัน/ค่า config ควรตรวจกับเอกสารทางการของ Anthropic ก่อนใช้ ^[ambiguous]

---

## องค์ประกอบ

| ส่วน | หน้าที่ |
|---|---|
| **Lead (หัวหน้าทีม)** | เซสชันหลักที่ผู้ใช้คุยด้วย — สร้างทีม, spawn teammates, แตกงาน, สังเคราะห์ผลลัพธ์ |
| **Teammates** | อินสแตนซ์ Claude Code แยก แต่ละตัวมี context window ของตัวเอง ไม่แชร์บริบทกับ lead หรือกันเอง |
| **Shared task list** | คิวงานสดที่ทุก agent อ่าน/เขียน — lead เติมตอนแตกงาน, teammate รับงาน → ทำ → mark done; dependency ถูกบังคับอัตโนมัติ งานที่ถูกบล็อกจะปลดเองเมื่องานก่อนหน้าเสร็จ |
| **Mailbox** | ระบบข้อความ agent-to-agent โดยตรง |

- ไฟล์ config ทีมและ task list อยู่ที่ `~/.claude/teams/` และ `~/.claude/tasks/` — **ห้ามแก้ด้วยมือ** เพราะจะถูกเขียนทับในการอัปเดตสถานะครั้งถัดไป

### 3 ความสามารถที่ "เปิดหลายเซสชันเอง" ไม่มี

1. **Peer-to-peer messaging** — เช่น security reviewer แจ้งข้อค้นพบให้ performance reviewer ระหว่างรันได้เลย
2. **File locking** — ไฟล์ที่ teammate กำลังเขียนถูกล็อก กันการเขียนทับกันเงียบๆ
3. **Dependency tracking** — lead ระบุ dependency ตอนแตกงาน ระบบบังคับให้เอง

---

## การตั้งค่า (ตามแหล่งที่มา)

ต้องใช้ Claude Code **v2.1.32+** (เช็คด้วย `claude --version`) — ฟีเจอร์ปิดเป็นค่าเริ่มต้น ต้อง opt-in ^[ambiguous]

1. **เปิด feature flag** `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1` — วิธีที่แนะนำคือใส่ใน `~/.claude/settings.json`:
   ```json
   { "env": { "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1" } }
   ```
   หรือ `export` ใน `~/.zshrc` / inline `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1 claude` — แก้ไฟล์แล้วต้อง restart Claude Code
2. **โหมดแสดงผล** (ไม่บังคับ) — `in-process` (ทุกตัวในเทอร์มินัลเดียว) หรือ split panes (ต้องมี tmux/iTerm2); ตั้ง `"teammateMode": "tmux"` ใน settings.json, ค่าเริ่มต้นคือ `"auto"`, บังคับรายเซสชันด้วย `claude --teammate-mode in-process`
3. **สั่งด้วยภาษาธรรมชาติ** — บอกงาน, deliverable, และบทบาทแต่ละคนใน prompt แล้ว Claude สร้างทีมให้
4. **Plan approval** (ไม่บังคับ) — ให้ teammates ทำงาน read-only เสนอแผนก่อน, lead อนุมัติแล้วค่อยลงมือ ใส่เกณฑ์อนุมัติใน prompt ได้ (เช่น "อนุมัติเฉพาะแผนที่วัด benchmark baseline ก่อน")
5. **แยกไฟล์ด้วย worktree** (แนะนำมาก) — ดู [[concepts/git-worktree-isolation]]
6. **ติดตามเป็นระยะ** — เช็คทุก 10–15 นาที; งานไม่ขยับ 20–30 นาที มักเกิดจาก permission prompt ค้าง, role ไม่ชัด หรือ dependency วนกลับ

### เรื่องโมเดล
Teammates **ไม่สืบทอดโมเดล** ของ lead — ระบุใน prompt ("Use Sonnet for every teammate"), ใน frontmatter ของไฟล์ role หรือตั้งค่าเริ่มต้นผ่าน `/config` ดูการเลือกรุ่นที่ [[concepts/claude-models-family]]

---

## Subagents vs Agent Teams

**Subagents = การมอบหมาย (delegation) · Agent Teams = การร่วมมือ (collaboration)**

| | Subagents | Agent Teams |
|---|---|---|
| การสื่อสาร | ทางเดียว: lead สั่ง → subagent รายงานกลับ | Peer-to-peer + lead ประสาน |
| สถานะร่วม | ไม่มี | Shared task list + dependency |
| Context window | ของตัวเอง ส่งผลกลับ lead | ของตัวเองต่อคน (แหล่งอ้าง "สูงสุด 1M tokens") ^[ambiguous] |
| กันไฟล์ชน | ไม่มีในตัว | File locking ในตัว |
| ค่า token | ต่ำกว่า | สูงกว่า (ทุกคนคืออินสแตนซ์เต็ม) |
| Resume เซสชัน | รองรับ | `/resume` และ `/rewind` **ไม่กู้** in-process teammates |
| Agent ซ้อน | รองรับ | ไม่รองรับ — มีแต่ lead ที่ spawn ได้ |
| เหมาะกับ | งานเฉพาะจุด, workflow ทำซ้ำ | งานหลายโดเมนที่ขนานได้และต้องคุยกัน |

**กฎตัดสินใจ:** ถ้านึก workstream ขนานที่อิสระจริงได้ **ไม่ถึง 3 สาย** → ใช้เซสชันเดียวหรือ subagents ถูกและดีกว่า

**เลือก Agent Teams เมื่อ:** teammates ต้องคุยกันเอง · ต้องมี task list พร้อม dependency ข้ามสาย · งานใหญ่เกินเซสชันเดียว
**เลือก Subagents เมื่อ:** ต้องการแค่สรุปสุดท้าย · งานจบในตัว · อยากจำกัด tools หรือใช้โมเดลถูกกว่า · research หลายเส้นทางที่ไม่พึ่งกัน

> Role ที่นิยามเป็น subagent type (scope project / user / plugin / CLI) ใช้ซ้ำเป็น teammate ได้ — นิยามครั้งเดียว ใช้ได้ทั้งสองแบบ

---

## 5 Use Cases ที่ทีมชนะเซสชันเดียว

1. **Parallel code review** — security + performance + test coverage reviewer พร้อมกัน, lead รวมเป็น action list ตามความสำคัญ (ใช้กับ architecture review / compliance ได้เหมือนกัน)
2. **Competing-hypothesis debugging** — 5 agents ถือคนละสมมติฐาน ตัวแรกที่ยืนยันได้เสนอวิธีแก้ ที่เหลือหยุด
3. **Cross-layer refactor** — backend ต้องเสร็จก่อน frontend; test agent เริ่มวางโครงทดสอบขนานไปได้ — ใช้ dependency ของ task list คุมลำดับ
4. **Research without context contamination** — แยกโดเมนไม่ทับกัน (DB engine / 3rd-party API / build tool) ให้แต่ละตัวสรุปแบบมีโครงสร้าง แล้ว lead รวมเป็นเอกสารเปรียบเทียบ
5. **Large codebase migration** — 1 agent ต่อ 1 โมดูลอิสระ, รัน test ของตัวเอง, รายงาน interface ที่เปลี่ยน; lead ตรวจ interface และคุมลำดับ merge

---

## Do's

- **Pre-approve permissions** — teammates รับ permission mode ของ lead ตอน spawn (ถ้า lead ใช้ `--dangerously-skip-permissions` ทุกคนได้ไปด้วย); ปรับรายคนได้หลัง spawn แต่ตั้งตอน spawn ไม่ได้ — เชื่อมกับหลัก Minimal Footprint ใน [[concepts/claude-agent-sdk]] และ [[concepts/claude-safety-pitfalls]] ^[inferred]
- **Role prompt ระบุ 4 อย่าง:** ทำอะไร · ไฟล์/โดเมนไหน · โฟกัส/ตัดอะไรออก · deliverable หน้าตาแบบไหน (ต่อยอดจาก 6-component ใน [[concepts/prompt-engineering]]) ^[inferred]
- **บังคับ isolation** สำหรับทุก agent ที่เขียนลงดิสก์
- **เขียน dependency ลง task list** ไม่ใช่ใส่เป็นคำสั่งใน role prompt — ระบบบังคับได้, prompt ถูกอ่านผิด/ละเลยได้
- **กำหนด ownership ใน CLAUDE.md** — 1 โมดูล/ไดเรกทอรี = 1 agent เจ้าของ
- **Cleanup ผ่าน lead เสมอ** — teammate ไม่มีบริบทครบพอจะเก็บกวาดอย่างปลอดภัย

## Don'ts

- อย่า spawn ทีมกับงานที่เซสชันเดียวทำได้ — **วาดกราฟงานก่อน**
- อย่าให้ 2 agents แตะไฟล์/component เดียวกัน — ถ้าจำเป็นให้ทำตามลำดับ
- อย่าข้ามการอนุมัติสิทธิ์ล่วงหน้า — permission prompt กลางทางทำลายประโยชน์ของการขนาน
- อย่าหวังว่าจะกู้ทีมกลับมาได้ — บันทึกผลลัพธ์ระหว่างทางก่อนงานยาว
- อย่าเกิน **5 คน** โดยไม่มีเหตุผล — ค่า token โตเชิงเส้น แต่ภาระประสานงานโตเร็วกว่า; 3 ตัวบทบาทชัด > 5 ตัวบทบาทคลุมเครือ

---

## ข้อสังเกต / คำถามค้าง

- แหล่งที่มาบอกว่า teammate ต้องระบุโมเดลเองใน frontmatter/`/config` แต่ก็ยกตัวอย่างสั่งผ่าน prompt ได้ — ยังไม่ชัดว่าลำดับความสำคัญเป็นอย่างไร ^[ambiguous]
- File locking ทำงานระดับไหน (ไฟล์เดียว/ทั้ง worktree) ไม่ได้อธิบาย ^[ambiguous]
- สำหรับงานเลขา/เอกสาร (ไม่ใช่โค้ด) แนวคิด "≥3 workstream อิสระ" ใช้เป็นเกณฑ์ตัดสินใจได้เหมือนกันก่อนแตกงานให้หลาย agent ^[inferred]

## ดูเพิ่ม

- [[concepts/claude-agent-sdk]] — Multi-Agent Architecture เชิงทฤษฎี + code
- [[concepts/git-worktree-isolation]]
- [[concepts/context-window]] — ทำไมการแยก context ช่วยคุณภาพ
- [[entities/kimi-agent-swarm]] — ทางเลือกแบบ no-code จากผู้เขียนบทความ
- [[references/kimi-agent-teams-guide-2026]] — แหล่งที่มา
