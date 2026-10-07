---
title: Kimi Agent Swarm
tags: [entity, ai, multi-agent, kimi, tool]
category: entities
created: 2026-10-07
updated: 2026-10-07
sources: [kimi-agent-teams-guide-2026]
summary: "ระบบ multi-agent แบบ no-code ของ Kimi (Moonshot AI) — แตกงานให้ sub-agents สูงสุด 300 ตัวทำขนาน เน้นงานวิจัย/เอกสาร/สไลด์ มากกว่างานโค้ดใน terminal"
provenance:
  extracted: 0.70
  inferred: 0.10
  ambiguous: 0.20
---

# Kimi Agent Swarm

**ผู้พัฒนา:** Kimi (Moonshot AI) ^[inferred]
**ประเภท:** Multi-agent orchestration บนเว็บ — ไม่ต้องตั้ง env flag หรือ git
**คู่เทียบ:** [[concepts/claude-code-agent-teams]] (developer-native, ทำงานใน terminal + Git)

> ข้อมูลทั้งหมดมาจากบทความการตลาดของ Kimi เอง — ตัวเลขความสามารถยังไม่ได้ตรวจสอบอิสระ ^[ambiguous]

## ความสามารถที่อ้าง

- Sub-agents ขนานได้ **สูงสุด 300 ตัว**, เรียก tools **4,000+ ครั้ง** ต่อการรัน ^[ambiguous]
- รวมหลายทักษะในรันเดียว: deep research, pptx, รายงาน, vibe-coding, เว็บไซต์, บทความวิชาการ
- ประมวลผลไฟล์ batch 20+ รูปแบบ (PDF, Word, Excel, PPT, รูปภาพ)
- Wide research: ค้นเว็บ → ดาวน์โหลด → จัดหมวด → สรุป ขนานกัน
- หลายมุมมองผู้เชี่ยวชาญต่อปัญหาเดียว · ผลลัพธ์ยาวมาก (รายงานหลายร้อยหน้า) · deliverables หลายรูปแบบในรันเดียว

## วิธีใช้ 3 ขั้น

1. เปิดหน้า Agent Swarm → ป้อน prompt พร้อมขอบเขต, deliverable, ข้อจำกัด (ช่วงเวลา, แหล่งข้อมูล, รูปแบบ)
2. ปล่อยให้ระบบแตกงานและ spawn sub-agents — ดูความคืบหน้า real-time ได้
3. ดูตัวอย่าง → ดาวน์โหลด/แชร์ผลลัพธ์

## Use cases ที่อ้าง

เอกสารประมูล/ข้อเสนอ · วิเคราะห์การเงิน · วิจัยธุรกิจ · ทดสอบความปลอดภัย · full-stack development

## มุมมองต่อผู้ใช้ wiki นี้

งานเอกสาร/วิจัยหลายแหล่ง (เช่น รายงานโครงการ) เป็นโจทย์ที่ swarm แบบนี้อ้างว่าทำได้ดี แต่ต้องระวังเรื่องข้อมูลส่วนบุคคลตามกฎ PDPA ใน [[concepts/claude-safety-pitfalls]] ก่อนอัปโหลดเอกสารองค์กร ^[inferred]

## ดูเพิ่ม

- [[concepts/claude-code-agent-teams]]
- [[concepts/claude-agent-sdk]] — Multi-Agent patterns
- [[references/kimi-agent-teams-guide-2026]]
