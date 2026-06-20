---
title: Hot Cache
updated: 2026-06-20
---

# Hot Cache

*A ~500-word semantic snapshot of recent activity. Updated after every major write operation.*

## Recent Activity

- [2026-06-20] INGEST — IT Equipment batch ที่โต๊ะทำงาน office "ห้องสติ" (raw mode, 19 drafts promoted)
  - **ใหม่:** entities/bewell-ergonomic-desk (โต๊ะปรับระดับไฟฟ้า), entities/keychron-k6-hotswap + entities/ajazz-ak820-max-plus-keyboard (คีย์บอร์ดหลัก+สำรอง), entities/logitech-mx-master-3 (เมาส์หลัก), entities/audio-technica-atr2500x + entities/boya-cm40-microphone (ไมค์สำรอง+ไมค์ประชุม), entities/edifier-mr4-speakers (ลำโพงมอนิเตอร์), entities/ajazz-akp03-stream-dock (สตรีมเด็ค), entities/ugreen-80888-sd-card-reader (เครื่องอ่านการ์ด), entities/ulanzi-qt03-docking-station + entities/wd-black-sn7100-ssd (docking+SSD คู่กัน), entities/orico-m2pv-c3-ssd-enclosure + entities/wd-blue-sn550-ssd (กล่อง SSD+SSD คู่กัน), entities/baseus-rotation-countdown-timer-pro, entities/ipad-air-11-m2 + entities/apple-pencil-pro (คู่กัน), entities/iphone-13 + entities/apple-airpods-4 (คู่กัน), entities/xiaomi-smart-band-9
  - ทุกหน้ามาจากสกรีนช็อตคำสั่งซื้อ Shopee/Lazada เสริมด้วยสเปกเว็บ `^[inferred]`; เชื่อมโยงกับ entities/macmini-m4-2024 หรือกันเองตามการใช้งานจริง
- [2026-06-19] INGEST — IT Equipment ที่โต๊ะทำงาน office "ห้องสติ" (raw mode, 4 drafts promoted)
  - **ใหม่:** entities/macmini-m4-2024 (Mac mini M4, 24GB RAM, เครื่องหลัก dev Laravel/TALL Stack), entities/benq-rd280u-monitor (จอ Programming Monitor 28.2" 4K+ 3:2, ฿20,700 จาก Lazada), entities/benq-screenbar-light (โคมไฟ LED แขวนหน้าจอ, ฿4,990 ซื้อพร้อม RD280U), entities/zircon-pi-ups-1000va (UPS 1000VA/700W สำรองไฟให้ Mac mini+จอ, ฿3,910 จาก Shopee)
  - **อัปเดต:** entities/claude เพิ่ม backlink ไปยัง Mac mini ที่ใช้รัน Claude Code ประจำวัน
- [2026-06-15] INGEST — Appendix ก Prompt Cookbook ครบ 90 prompts (หน้า 441–474)
  - **อัปเดต:** references/claude-prompt-cookbook — ครบทุกหมวด: ก.1 Business #01-#15, ก.2 Content #16-#30, ก.3 Analysis #31-#45, ก.4 Coding #46-#60, ก.5 Writing #61-#75, ก.6 Productivity #76-#90
  - **Ingest ครบ 100%:** คู่มือ Claude ฉบับสมบูรณ์-STAG 500 หน้า ทุก Unit + Mini Workflow + Appendix เสร็จแล้ว

## Key Claude Knowledge Added

- **7.17 Hallucination 6 ประเภท:** Factual / Citation / Logical / Instruction / Entity / Temporal — แต่ละแบบมี Detection Strategy ต่างกัน Citation = check Google Scholar, Temporal = ใช้ web search
- **RAG ลด Hallucination 70–90%:** ดึงข้อมูลจาก DB ส่งเป็น context แทนให้ Claude 'รู้' เอง — ทำได้ง่ายด้วย Chain-of-Verification: ถาม 'Verify each fact you just stated' หลังได้คำตอบ
- **7.21 Thai Hallucination สูงกว่า EN:** Training data ไทยน้อยกว่า ให้ context มากขึ้น + verify Thai-specific knowledge เสมอ — Claude conservative กับหัวข้อ sensitive ไทย (ม.112) เป็นพฤติกรรมที่ถูกต้อง
- **7.22 Over-reliance 4 Stages:** Tool use (OK) → Primary source → Default answer → Deskilling (อันตราย) — แก้: คิดเองก่อน ค่อย verify + Disagree กับ Claude เป็นประจำ
- **7.23 Safety ROI Rule:** Safety budget = 10–20% ของ AI budget / ค่า 1 incident ≈ safety budget ทั้งปี / PDPA violation = ค่าปรับ 1–5 ล้านบาท + reputation damage
- **7.20 Production Checklist 16 items:** 4 sections — Safety Design (scope/HITL/escalation/adversarial test) / Privacy (anonymize/PDPA/consent/retention) / Security (injection/filtering/rate-limit/audit) / Monitoring (error tracking/anomaly/incident plan)
- **Hardcoded = ไม่มีทางเปลี่ยน 100%:** CBRN weapons / CSAM / undermine AI oversight / cyberweapons — ไม่มี roleplay/fiction/researcher framing ใดทำให้ผ่านได้
- **Principal Hierarchy L1→L2→L3:** Anthropic → Operator → User — แต่ละระดับขยายสิทธิ์ได้เฉพาะในขอบเขตที่ระดับบนอนุญาต
- **3 Hallucination Types:** Factual (HIGH, อ้างสิ่งไม่มีจริง) / Confident Fabrication (MEDIUM, ตอบมั่นใจในสิ่งไม่รู้) / Instruction Drift (LOW, ลืม system prompt ใน long conv)
- **5 Hallucination Signals:** ตัวเลข round เกิน / citation สมบูรณ์แบบ / ตอบเร็วเกินสำหรับคำถามยาก / detail มากผิดปกติ / ไม่ยอมรับว่าไม่รู้
- **Indirect Injection = อันตรายสูงสุด:** Claude อ่าน email/doc/web ที่มี malicious instruction → agent ถูก hijack — ป้องกัน: XML tags แยก data ออกจาก instructions
- **8 Pitfalls สรุปสั้น:** Over-reliance / Context Collapse (restart ทุก 50 msg) / False Precision (ขอ source เสมอ) / Voice Contamination (rewrite ในเสียงตัวเอง) / Automation Complacency (HITL irreversible) / Privacy Leak (anonymize ก่อน) / Sycophancy (ถาม weaknesses ตรงๆ) / Scope Creep (แยก prompt)
- **PDPA Data Rules:** Personal data (ชื่อ/ที่อยู่) = anonymize ก่อนส่ง / Sensitive data (สุขภาพ/การเงิน) = Enterprise plan + DPA required / Non-personal (aggregate/ไม่มีชื่อ) = ใช้ได้ปกติ

- **Agent vs Chatbot:** Agent วนลูป plan→action→evaluate เองจนเสร็จ, Chatbot รับ→ตอบครั้งเดียว — เลือก Agent เมื่อ task ต้องการ multiple steps หรือใช้ tools
- **Parallel Agent = 4× Faster:** asyncio.gather() รัน 5 research tasks พร้อมกัน sequential=50s vs parallel=~12s — pattern ที่ควรใช้ก่อนเสมอถ้า subtasks independent
- **HITL Required for Production:** Read-only=ไม่ต้อง, Write hard-to-reverse=จำเป็น, Financial/Access control=จำเป็นเสมอ — HumanCheckpoint class พร้อม auto_approve_low_risk flag
- **Minimal Footprint 4 Rules:** Request least privilege, Prefer reversible, Confirm before external effects, Explicit task scope
- **Prompt Injection ใน Agent อันตรายกว่า Chatbot:** Agent อ่าน web/files → malicious instructions ใน content → hijack agent behavior — ป้องกัน: XML tags แยก data ออกจาก instructions
- **Smart Model Routing:** Haiku classify (cheap) → route: analysis/research→Opus, code→Sonnet, else→Haiku — ลด cost มากโดยไม่เสีย quality
- **Token Budget Controller:** set max_tokens, warn_at 80% — ป้องกัน runaway agents เสีย bill ไม่รู้ตัว
- **Agent Memory 4 Types:** In-context (current task), External KV/Redis (session state), External Vector (RAG), Episodic (past actions) — Hybrid Memory ใช้ Redis summarize oldest messages ก่อน trim
- **Agent Error 6 Types:** Tool failure (retry 3x), Invalid call (validate first), Infinite loop (detect repeated), Context overflow (summarize+restart), Wrong direction (human correction), Resource exhaustion (graceful stop)
- **6.14 Debug: Verbose + Replay:** Print every step to see Claude's decisions; Record JSONL to replay with cached results แทน real API calls
- **W13 Chatbot KPIs:** Resolution Rate ≥75%, Escalation <20%, Accuracy ≥90% — วัดทุก week + Continuous Improvement Cycle 5 steps
- **W13 LINE Integration:** FastAPI webhook + per-user history 10 turns ด้วย dict[str, list] — deploy ง่ายที่สุดสำหรับ Thai market
- **MVP Rule #1 Build Less:** MVP = ทำแค่ที่จำเป็นเพื่อ validate 1 core assumption — scope creep = สาเหตุหลักที่ fail — เขียน 'Out of Scope' ออกมาก่อนเริ่ม build
- **MVP Pre-sale Trick:** ถ้า validate ด้วย pre-sale ได้ก็ยิ่งดี: landing page ขึ้นก่อน build — ถ้ามีคนจ่ายเงินแม้แต่ 1 คน = signal ที่ดีมาก
- **Tech Stack for MVP:** เลือก stack ที่ build ได้เร็วที่สุด ไม่ใช่ทันสมัยที่สุด — Streamlit = fastest (15 นาที setup), Railway = easiest for Python API
- **User Test Day 3 Not Day 5:** Share localhost via ngrok วันที่ 3 เลย — Feedback วันแรกมีค่าที่สุด ไม่ต้องรอ launch
- **Launch Day 10-item Checklist:** Production URL, No API keys in code, Error logging, Loading state, Copy function, Mobile responsive, Value prop in 5 sec, Contact, Privacy/Terms, Analytics
- **Impact vs Effort 4-Quadrant:** Quick Win (HIGH/LOW=ทำทันที), Big Bet (HIGH/HIGH=Sprint 2-3), Fill-in (LOW/LOW=ทำถ้ามีเวลา), Don't do (LOW/HIGH=Skip)
- **SKILL.md vs System Prompt:** SKILL.md = file บน disk, Git-trackable, scope เฉพาะ task / System Prompt = text ใน API call, ทุก conversation — เลือกตาม use case
- **Skill ROI Rule of Thumb:** 3+/week = สร้างทันที, 1-2/week = สร้างถ้าประหยัด 30+ นาที/ครั้ง, <1/week = ใช้ prompt template แทน
- **Skill Lifecycle 5 Stages:** Experimental → Active → Mature → Deprecated → Archived — archive ถ้าไม่ใช้ 6+ เดือน
- **Automation Integration 5 Patterns:** Zapier+Claude API, Scheduled Batch, Form→Analysis→Action, Document Upload→Intelligence, Multi-Agent Pipeline
- **Skill Testing 6 Types:** Happy path, Edge cases, Out-of-scope, Injection, Format compliance, Language handling — Python framework พร้อม code
- **Enterprise Skills:** Compliance Document Checker (PDPA/GDPR/SEC output), Board Report Synthesizer (RAG status 6 sections max 400 words)
- **Industry Skills:** Healthcare (4 skills, ห้าม medical diagnosis), E-commerce (4 skills), Real Estate (3 skills)
- **30-Day Skill Library Plan:** Week 1 Quick Wins → Week 2 Content → Week 3 Analysis → Week 4 Domain → Scale
- **Custom Skills 5 Layers:** Prompt Template → SKILL.md File → Projects Instruction → API System Prompt → MCP Server+Skill — เลือก layer ตาม use case
- **Skill Evaluation Rubric:** Accuracy ≥90%, Consistency ≤15% variance, Edge case ไม่ crash, Injection ไม่ follow, Format 100% match, Speed < threshold
- **W10 Digital Product Rule #1:** อย่าสร้าง template ก่อน validate — research 30 นาทีก่อน ดู Etsy Bestseller badge
- **W10 Pricing Sweet Spot:** $20–$39 = Best ROI (conversion 3–7%, revenue ดี) — อย่าตั้งราคาต่ำเกิน $9 เพราะ signal คุณภาพต่ำ
- **Gumroad vs Etsy:** Gumroad = audience ที่รู้จักคุณแล้ว (ต้อง drive traffic เอง), Etsy = organic search — แนะนำขายทั้งสองพร้อมกัน
- **Passive Income Flywheel:** Create → List → Promote → Review → Update → Bundle → Scale — 5 ขั้นตอนแรกทำครั้งเดียว
- **Principal Hierarchy:** Anthropic → Operator → User (ลำดับชั้นควบคุม Claude)
- **Model Selection:** Opus (ฉลาดสุด), Sonnet (สมดุล/แนะนำ), Haiku (เร็ว/ถูก) — ทุกรุ่น 200K context
- **Thai Token Cost:** ภาษาไทยแพงกว่าอังกฤษ 2–2.8× เพราะ BPE optimize ภาษาอังกฤษ
- **Lost-in-the-Middle:** LLM จำข้อมูลตรงกลาง context ได้แย่ที่สุด — วางสิ่งสำคัญต้น/ท้าย
- **6-Component Prompt:** ROLE, TASK, CONTEXT, DATA, FORMAT, CONSTRAINT
- **PARE Framework:** Prompt → Assess → Refine → Evaluate สำหรับ iterate prompt
- **API Production Patterns:** RAG (ดึงเฉพาะที่เกี่ยวข้อง), Structured Output (Pydantic+JSON), Parallel (asyncio 10x เร็วกว่า), Human-in-the-Loop (confirm ก่อน execute)
- **Prompt Injection:** ป้องกันด้วย XML tags แยก instruction ออกจาก `<user_text>` — ห้าม f-string ตรงๆ
- **ROI Rule:** Pro $20/เดือน (720 บาท) คุ้มถ้าประหยัดเวลาแค่ 1 ชม./เดือน
- **Claude Products Decision Guide:** claude.ai=แชท, Claude Code=เขียนโค้ด, Desktop=global hotkey+MCP, Mobile=เดินทาง, Office=Excel/Word/PPT, Projects=memory ถาวร, Cowork=no-code automation, API=build product
- **Evergreen Campaign 4 Stages:** AWARENESS (lead magnet) → NURTURE (welcome sequence) → CONVERT (genuine urgency) → ASCEND (upsell/referral)
- **Campaign KPIs ที่ถูก:** Revenue→ROAS, Lead Gen→CPL, Awareness→Brand recall — ห้ามโฟกัส likes/impressions
- **Budget Framework:** <5K บาท = Email 60%+Organic 40%, >100K = Full funnel with retargeting
- **Prompt Caching ROI:** RAG Chatbot 50K-token KB + 1,000 req/วัน = ประหยัด ~$3,990/เดือน ด้วย cache_control สองบรรทัด
- **Batch API:** 50% ถูกกว่า Standard, max 10,000 req/batch ไม่มี rate limit — ใช้สำหรับ bulk processing
- **Tool Use 4-Step Loop:** Define → Claude decides → You execute → Claude responds
- **MCP vs Tool Use:** MCP สำหรับ standard integrations (GitHub/Slack/DB พร้อมแล้ว), Tool Use สำหรับ custom logic

## Active Threads

- **IT Equipment Inventory** — บันทึกสเปก/ราคา/ที่ตั้งอุปกรณ์ office ห้องสติ ครบ 23 ชิ้น: Mac mini M4, จอ/โคมไฟ/UPS, โต๊ะปรับระดับ, คีย์บอร์ด/เมาส์/ไมค์/ลำโพง/สตรีมเด็ค, อุปกรณ์เก็บข้อมูล (docking+SSD x2 คู่), อุปกรณ์พกพา (iPad+Pencil, iPhone+AirPods, Smart Band) ([[entities/macmini-m4-2024]])
- **Phone Jail system** — ระบบ environment design ทดแทน willpower สำหรับการนอน ([[systems/phone-jail]])
- **Identity Statement** — "ฉันเดินทางมาไกลเกินกว่าจะถอยหลังแล้ว" — กำลัง integrate กับ behavior change ([[systems/identity-statement]])
- **Deanxit withdrawal** — documented และเพิ่ม warning ใน gastritis page — ต้องแจ้งแพทย์ก่อนปรับยา
- **Mi Fitness goals updated** — ก้าว hard cap 10,000, calories 700–800 kcal

## Key Takeaways

- **Deep sleep ≥ 1h45m** คือเกณฑ์จริงที่ทำให้ตื่น 04:30 ได้สดชื่น (จากข้อมูล 14 วัน)
- **Environment > Willpower** — ไม่มีมือถือ = ตื่น 04:30 ทุกวัน อัตโนมัติ
- **Step hard cap 10,000** — เดินเกินสะสม 5 วัน = เสียเวลาปฏิบัติ 5 วัน
- **Deanxit ห้ามหยุดเอง** — withdrawal ทำให้เสียเวลาปฏิบัติ 3+ วัน

## Flagged Contradictions

- Sleep Gummy **ห้ามใช้คู่กับ Deanxit** — ต้องตรวจสอบกับแพทย์ก่อนใช้ยาช่วยนอนใดๆ
