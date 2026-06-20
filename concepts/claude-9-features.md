---
title: 9 Features ของ Claude (Unit 3)
tags: [concept, claude, api, tool-use, mcp, vision, batch, caching, thinking, computer-use, stag]
category: concepts
created: 2026-06-14
updated: 2026-06-14
sources: [claude-manual-stag-2026]
summary: "9 Features ที่ทำให้ Claude ต่างจาก chatbot ธรรมดา — Tool Use, MCP, Files API, Vision, Citations, Batch API, Prompt Caching, Extended Thinking, Computer Use"
provenance:
  extracted: 0.95
  inferred: 0.05
  ambiguous: 0.0
---

# 9 Features ของ Claude (Unit 3)

> "90% ประหยัดได้ด้วย Caching · 50% ลดราคา Batch API · 40% แม่นขึ้นด้วย Thinking"

คนส่วนใหญ่รู้จักแค่ 1–2 features — แต่การรู้ทั้ง 9 คือ competitive advantage

## ภาพรวม 9 Features

| Feature | แก้ปัญหาอะไร | Complexity | Cost Impact |
|---------|-------------|-----------|------------|
| Tool Use | ให้ Claude เรียก function เองได้ | Medium | ตาม tool call |
| MCP | เชื่อม Claude กับ app/service มาตรฐาน | Medium-High | ตาม service |
| Files API | ส่งไฟล์ใหญ่โดยไม่ส่งซ้ำ | Low | เพิ่มเล็กน้อย |
| Vision | ให้ Claude วิเคราะห์รูปภาพ | Low | ~1,600 tokens/รูป |
| Citations | อ้างอิงแหล่งที่มาอัตโนมัติ | Low | ไม่เพิ่ม |
| Batch API | ประมวลผลพร้อมกันหลายพัน request | Low | ลด 50% |
| Prompt Caching | Cache system prompt ยาวๆ | Low | ลด 60–90% |
| Extended Thinking | ให้ Claude คิดลึกก่อนตอบ | Low | เพิ่ม 2–5x |
| Computer Use | Claude ควบคุม desktop ได้ | High | สูงมาก |

---

## Feature #1 — Tool Use (การเรียกใช้เครื่องมือ)

Tool Use เปลี่ยน Claude จาก text generator เป็น **agent ที่ทำงานได้จริง** — Claude ตัดสินใจเรียก function ไหน ด้วย parameter อะไร เพื่อให้ได้ข้อมูลที่ต้องการ

### Specifications
- รองรับ: parallel tool calls — เรียกหลาย function พร้อมกัน
- Max tools ต่อ request: 64 tools
- Tool definition: JSON Schema สำหรับ input validation
- Claude ตัดสินใจจะเรียก tool ไหน ตาม description ที่คุณให้

### 4-Step Tool Use Loop

| Step | ชื่อ | อธิบาย |
|------|------|---------|
| 1 | Define tools | ส่ง JSON schema บอก Claude ว่ามี tools อะไรให้ใช้ |
| 2 | Claude decides | Claude เลือก tool + parameters ที่เหมาะสม |
| 3 | You execute | คุณรัน function จริงและส่งผลกลับ |
| 4 | Claude responds | Claude ใช้ผลนั้นตอบ user |

```python
# Python — Tool Use: Define + Call
import anthropic, json
client = anthropic.Anthropic()
tools = [{'name': 'get_stock_price',
'description': 'Get current stock price for a ticker symbol',
'input_schema': {'type': 'object',
'properties': {'ticker': {'type': 'string'}},
'required': ['ticker']}}]
response = client.messages.create(
  model='claude-sonnet-4-6-20260101', max_tokens=1024,
  tools=tools,
  messages=[{'role':'user','content':'Apple stock price?'}])
if response.stop_reason == 'tool_use':
  tc = next(b for b in response.content if b.type=='tool_use')
  result = get_stock_price(tc.input['ticker'])  # your function
# Step 2: Return result to Claude
final = client.messages.create(
  model='claude-sonnet-4-6-20260101', max_tokens=1024, tools=tools,
  messages=[
    {'role':'user','content':'Apple stock price?'},
    {'role':'assistant','content':response.content},
    {'role':'user','content':[{
      'type':'tool_result', 'tool_use_id':tc.id,
      'content':json.dumps(result)}]}])
```

### Best Practices สำหรับ Tool Design
- **ชื่อ tool ต้องชัดเจน:** `get_weather` ดีกว่า `tool_1`
- **Description ละเอียด:** บอกว่า tool ทำอะไร รับ input อะไร return อะไร และเมื่อไหร่ควรใช้
- **Schema เข้มงวด:** ใช้ required fields, enum values, format hints เพื่อลด invalid calls
- **Error handling ใน tool:** ถ้า tool fail → return error message ชัดเจน Claude จะอธิบายให้ user ได้
- **Human-in-the-loop:** สำหรับ tools ที่มี side effects (write/delete/send) ให้ confirm ก่อน execute

> **Tool Use ≠ ปลอดภัยโดยอัตโนมัติ** — Claude ตัดสินใจเรียก tool ตาม prompt ถ้า tool มีสิทธิ์ลบข้อมูล Claude อาจทำโดยไม่ได้ตั้งใจ Validate inputs เสมอก่อน execute และใช้ human confirmation สำหรับ destructive actions

---

## Feature #2 — MCP (Model Context Protocol)

MCP คือ open protocol ที่ Anthropic พัฒนาเพื่อแก้ปัญหา integration — แทนที่แต่ละ developer จะต้อง build integration เอง MCP ให้มาตรฐานเดียวที่ service ต่างๆ ใช้ร่วมกันได้

### MCP Architecture

| Component | บทบาท | ตัวอย่าง |
|-----------|--------|---------|
| MCP Host | AI model ที่ใช้งาน tools | Claude |
| MCP Client | Connector ระหว่าง Host กับ Server | Claude Desktop, Claude Code |
| MCP Server | Service ที่ expose capabilities | GitHub, Slack, Google Drive, DB |
| Transport | วิธีการสื่อสาร | stdio (local), HTTP+SSE (remote) |

### Popular MCP Servers พร้อมใช้

| MCP Server | ทำอะไรได้ | Use Case ที่ดี |
|-----------|----------|--------------|
| GitHub | อ่าน/เขียน code, PR, issues | Code review อัตโนมัติ |
| Google Drive | อ่าน/เขียนไฟล์ใน Drive | วิเคราะห์เอกสาร internal |
| Slack | ส่งข้อความ อ่าน channel | สรุป conversation |
| PostgreSQL | Query database โดยตรง | วิเคราะห์ข้อมูล real-time |
| Filesystem | อ่าน/เขียนไฟล์ local | จัดการไฟล์ในเครื่อง |
| Brave Search | ค้นหาเว็บ | Research อัตโนมัติ |
| Puppeteer | ควบคุม browser | Web scraping, testing |

```python
# Python — สร้าง MCP Server ด้วย FastMCP
from mcp.server.fastmcp import FastMCP
mcp = FastMCP('Company CRM Tools')
@mcp.tool()
def get_customer_info(customer_id: str) -> dict:
    '''Get customer data from CRM by ID.'''
    return {'id': customer_id, 'name': 'John Doe',
            'tier': 'Premium', 'last_order': '2026-01-15'}
@mcp.tool()
def search_orders(customer_id: str, status: str = 'all') -> list:
    '''Search orders. Status: pending/shipped/delivered/all'''
    return [{'order_id': 'ORD-001', 'status': 'delivered', 'total': 1250.00}]
if __name__ == '__main__':
    mcp.run(transport='stdio')
```

> **MCP vs Tool Use — เลือกอันไหน?**
> - Tool Use: เหมาะสำหรับ custom logic เฉพาะ app ของคุณ ควบคุมได้เต็มที่
> - MCP: เหมาะสำหรับ standard integrations ที่มี server พร้อมแล้ว setup เร็วกว่ามาก
> - ทั้งคู่ใช้ร่วมกันได้ — MCP เป็น wrapper ของ Tool Use นั่นเอง

---

## Feature #3 — Files API (การจัดการไฟล์)

Files API ให้คุณ upload ไฟล์ไปเก็บบน Anthropic servers แล้ว reference ด้วย `file_id` แทนที่จะส่ง content ทุก request เหมาะมากสำหรับเอกสารที่ใช้ซ้ำบ่อยๆ

### Specifications
- ขนาดไฟล์สูงสุด: 32MB ต่อไฟล์
- Format ที่รองรับ: PDF, TXT, CSV, DOCX, images และอื่นๆ
- Storage duration: 30 วัน (ต่ออายุได้)
- ราคา: Storage ฟรี — คิดแค่ tokens ที่ Claude ใช้อ่าน
- Beta header required: `betas=['files-api-2025-04-14']`

```python
# Python — Files API: Upload Once, Use Many Times
# Step 1: Upload once
with open('company_policy.pdf', 'rb') as f:
    file_obj = client.beta.files.upload(
        file=('company_policy.pdf', f, 'application/pdf'))
file_id = file_obj.id  # save this!
# Step 2: Reference by ID — no re-upload needed
def ask_about_policy(question: str):
    return client.beta.messages.create(
        model='claude-sonnet-4-6-20260101', max_tokens=1024,
        betas=['files-api-2025-04-14'],
        messages=[{'role':'user','content':[
            {'type':'document',
             'source':{'type':'file','file_id':file_id}},
            {'type':'text','text':question}]}])
# Same file_id works across multiple questions
r1 = ask_about_policy('How many vacation days per year?')
r2 = ask_about_policy('What is the remote work policy?')
```

### Use Cases ที่เหมาะกับ Files API
- **Knowledge base Q&A:** upload เอกสาร internal ทั้งหมดครั้งเดียว แล้วให้ user ถามได้ตลอด ไม่ต้องส่งซ้ำ
- **Document processing pipeline:** รับ PDF จาก user, upload, process หลายขั้นตอนโดยใช้ file_id เดิมตลอด ลด bandwidth
- **Batch processing:** ใช้คู่กับ Batch API เพื่อ process เอกสารหลายพันชิ้นโดย reference file_id เดียวกัน
- **Multi-turn analysis:** วิเคราะห์เอกสารเดิมใน conversation หลาย turns โดยไม่เพิ่ม token cost

---

## Feature #4 — Vision (การมองเห็น)

Vision รองรับทุก model ใน Claude 4 family — Claude อ่านความในรูป วิเคราะห์ chart และเข้าใจ diagram ได้ดี เหมาะสำหรับงาน business ที่ต้องการ visual analysis

### 3 วิธีส่งรูป

| วิธีส่งรูป | เหมาะกับ | ข้อดี | ข้อเสีย |
|-----------|---------|-------|---------|
| Base64 encode | รูปจาก local/memory | ไม่ต้อง host | payload ใหญ่ |
| URL reference | รูปบน internet | ส่งเร็ว payload เล็ก | Claude ต้อง fetch |
| Files API | รูปที่ใช้ซ้ำบ่อย | ส่งครั้งเดียว | ต้อง upload ก่อน |

```python
# Python — Vision: Analyze Dashboard Screenshot
import base64
with open('dashboard.png', 'rb') as f:
    img_b64 = base64.standard_b64encode(f.read()).decode()
response = client.messages.create(
    model='claude-sonnet-4-6-20260101', max_tokens=1500,
    messages=[{'role':'user','content':[
        {'type':'image',
         'source':{'type':'base64','media_type':'image/png','data':img_b64}},
        {'type':'text','text':'''Analyze this business dashboard.
Provide: 1) Key metrics and values 2) Notable trends
3) Any anomalies 4) Top 3 actionable insights.
Format as structured bullet points.'''}]}])
```

### Vision Use Cases

| Use Case | Input | Output | Model แนะนำ |
|---------|-------|--------|------------|
| อ่าน invoice/receipt | รูปถ่ายใบเสร็จ | JSON ข้อมูล | Haiku (เร็ว+ถูก) |
| วิเคราะห์ dashboard | Screenshot | Text + insights | Sonnet |
| ตรวจสอบ UI/UX | App screenshot | Feedback ละเอียด | Sonnet |
| OCR เอกสาร | รูปถ่ายสัญญา | Text ที่ extract ได้ | Sonnet |
| อ่าน whiteboard | รูปถ่ายกระดาน | Text + structure | Sonnet |

---

## Feature #5 — Citations (การอ้างอิง)

Citations บังคับให้ Claude อ้างอิงข้อมูลจากเอกสารที่ให้ไว้เท่านั้น ไม่สร้างข้อมูลขึ้นมาเอง ซึ่งช่วยลด hallucination ได้อย่างมาก และผู้ใช้สามารถ verify ข้อมูลได้ทันทีจาก source ที่ Claude cite

```python
# Python — เปิดใช้งาน Citations
response = client.messages.create(
    model='claude-sonnet-4-6-20260101', max_tokens=2000,
    messages=[{'role':'user','content':[
        {'type':'document',
         'source':{'type':'text','media_type':'text/plain',
                   'data': annual_report_text},
         'title': 'Annual Report 2025',
         'citations': {'enabled': True}},   # <- enable here
        {'type':'text',
         'text':'What were the top 3 revenue drivers in 2025?'}]}])
for block in response.content:
    if hasattr(block, 'citations'):
        for cite in block.citations:
            print(f'Source: {cite.document_title}')
            print(f'Text: {cite.cited_text[:100]}')
```

### Use Cases ที่ Citations สำคัญที่สุด
- **Legal & Compliance:** ทุกข้อมูลต้องอ้างอิงได้ Claude ระบุว่าข้อมูลมาจากหน้าไหนของเอกสาร
- **Medical/Research:** ลด hallucination ที่อันตราย ถ้าไม่มีข้อมูลใน document Claude จะบอกแทนที่จะแต่งขึ้นมา
- **Customer Support:** ตอบจาก FAQ/Policy เท่านั้น ไม่ตอบนอกขอบเขต
- **Academic research:** สรุป paper พร้อม citation ที่ตรวจสอบได้

---

## Feature #6 — Batch API (การประมวลผลแบบ Batch)

Batch API เหมาะสำหรับงานที่ไม่ต้องการ real-time response แลกเวลา (ภายใน 24 ชั่วโมง) กับราคาที่ถูกลง 50% และ rate limit ที่สูงกว่า standard API มาก

### Specifications
- ราคา: 50% ถูกกว่า Standard API ทุก model
- Response time: ภายใน 24 ชั่วโมง (มักเร็วกว่า)
- Max requests per batch: 10,000
- Rate limit: ไม่มี (แต่ขนาด batch จำกัดที่ 256MB)

```python
# Python — Batch API: วิเคราะห์ Product Reviews
def create_review_batch(reviews: list[dict]) -> str:
    requests = []
    for review in reviews:
        requests.append({
            'custom_id': f"review-{review['id']}",
            'params': {
                'model': 'claude-haiku-4-5-20260101',
                'max_tokens': 100,
                'messages': [{'role':'user','content':
                    f'Analyze sentiment. Return JSON only: '
                    f'{{"sentiment":"positive/neutral/negative",'
                    f'"score":1-5}}\nReview: {review["text"]}'}]}})
    batch = client.messages.batches.create(requests=requests)
    return batch.id

def get_results(batch_id: str):
    batch = client.messages.batches.retrieve(batch_id)
    if batch.processing_status == 'ended':
        return {r.custom_id: json.loads(r.result.message.content[0].text)
                for r in client.messages.batches.results(batch_id)
                if r.result.type == 'succeeded'}
    return None  # still processing
```

### Batch API vs Standard API

| เหตุการณ์ | Batch API | Standard API |
|----------|----------|-------------|
| วิเคราะห์ review 10,000 ชิ้น | ประหยัด 50% ไม่มี rate limit | ติด rate limit |
| Chatbot ตอบ user real-time | รอถึง 24 ชั่วโมง | ตอบใน <1 วินาที |
| แปล catalog 5,000 รายการ | ส่งพร้อมกันทั้งหมด | ต้องจัดการ queue |
| Monthly data processing | ประหยัดไม่ต้องดูแล | ต้องจัดการเอง |

---

## Feature #7 — Prompt Caching (การ Cache Prompt)

Prompt Caching เป็น feature ที่ให้ ROI สูงที่สุดใน 9 features สำหรับ production app ที่มี system prompt ยาวหรือ knowledge base ที่ใช้ซ้ำ — ลงทุนแค่เพิ่ม `cache_control` สองบรรทัด ประหยัดได้ทันที

### Specifications
- Cache write: คิดราคาปกติ + 25% (ครั้งแรก)
- Cache read: คิดแค่ 10% ของราคาปกติ (ครั้งถัดไป)
- Cache TTL: 5 นาที — ต่ออายุทุกครั้งที่ใช้
- Min tokens to cache: 1,024 tokens
- Max cache breakpoints: 4 ต่อ request

### การคำนวณประหยัดจริง (RAG Chatbot ตัวอย่าง)
RAG Chatbot มี knowledge base 50,000 tokens — user ถามวันละ 1,000 คำถาม:

| รายการ | ไม่ใช้ Cache | ใช้ Caching |
|--------|------------|------------|
| Input tokens/วัน | 50,000 × 1,000 = 50M | 5M (cache hit 90%) |
| ราคา Input (Sonnet) | $150/วัน | ~$17/วัน |
| **ประหยัด/เดือน** | – | **≈ $3,990** |

```python
# Python — เปิด Prompt Caching ด้วย cache_control
response = client.messages.create(
    model='claude-sonnet-4-6-20260101', max_tokens=1024,
    system=[
        {'type':'text', 'text': base_instructions},
        {'type':'text', 'text': knowledge_base_50k,
         'cache_control': {'type':'ephemeral'}}  # <- add this
    ],
    messages=[{'role':'user','content':user_question}])
# Monitor cache hits
usage = response.usage
print(f'Cache created: {usage.cache_creation_input_tokens}')
print(f'Cache read: {usage.cache_read_input_tokens}')  # 90% cheaper
```

### Cache Strategy ที่ดีที่สุด
- **Static content ก่อนเสมอ:** system instructions, knowledge base, examples ควรอยู่ต้น prompt — cache ได้ยาวที่สุด
- **Dynamic content อยู่ท้าย:** user message, current date, session-specific info ควรอยู่ท้าย prompt — เปลี่ยนทุก request
- **Monitor `cache_read_input_tokens`:** ถ้าต่ำแสดงว่า TTL หมดก่อนมี request ถัดมา

---

## Feature #8 — Extended Thinking (การคิดเชิงลึก)

Extended Thinking ให้ Claude มี 'scratch pad' สำหรับคิดออกเสียงก่อนตอบ คล้ายกับการที่มนุษย์ทำ draft ก่อนเขียนจริง งานวิจัยพบว่า Thinking ช่วยเพิ่มความแม่นยำในงาน reasoning ได้ 40–60%

### ประเภทโจทย์กับ Improvement

| ประเภทโจทย์ | Improvement | ตัวอย่าง |
|------------|-----------|---------|
| Multi-step math/logic | 40–60% | Financial modeling, algorithm |
| Complex reasoning | 30–50% | Legal analysis, risk assessment |
| Code architecture | 25–40% | System design, refactoring |
| Strategic planning | 20–35% | Business strategy, competitive |
| Simple Q&A | ไม่มีผล | ตอบคำถามทั่วไป — เสียเงินเปล่า |

```python
# Python — Extended Thinking สำหรับ Market Analysis
response = client.messages.create(
    model='claude-opus-4-6-20260101',  # Opus best for Thinking
    max_tokens=16000,
    thinking={'type':'enabled', 'budget_tokens':8000},
    messages=[{'role':'user','content':'''
Analyze whether we should expand to Vietnam.
Consider: market size, competition, regulatory,
capital requirements, and current capabilities.
Provide Go/No-Go with clear rationale.'''}])
for block in response.content:
    if block.type == 'thinking':
        print('=== THINKING ===')
        print(block.thinking[:300], '...')
    elif block.type == 'text':
        print('=== FINAL ANSWER ===')
        print(block.text)
```

### Budget Token Guidelines

| Budget Tokens | เหมาะกับ | Cost Multiplier |
|-------------|---------|----------------|
| 1,000–2,000 | โจทย์ปานกลาง ทดสอบ | ~2x |
| 3,000–6,000 | Business analysis ทั่วไป | 3–4x |
| 8,000–12,000 | Complex strategy, legal | 5–7x |
| 16,000+ | Extremely hard problems | 8–10x+ |

> **Extended Thinking ≠ ช้าเสมอ** — Thinking tokens ไม่ถูก stream ผู้ใช้เห็นแค่ final answer ไม่เห็น thought process · Latency เพิ่มตาม budget_tokens — ทดสอบหาจุด sweet spot ก่อน · ใช้ Opus + Thinking เฉพาะงานสำคัญที่ justify cost เท่านั้น

---

## Feature #9 — Computer Use (การใช้คอมพิวเตอร์)

Computer Use เป็น feature ที่ทรงพลังที่สุดและเสี่ยงที่สุดใน 9 features — Claude สามารถดู screenshot ตัดสินใจ และสั่ง action บน computer ได้ เหมาะสำหรับ automation ที่ไม่มี API หรือต้องการ visual interaction

### Specifications
- Status: **Beta** — error rate สูงกว่า features อื่น
- รองรับ: Linux desktop, browser automation
- Actions: screenshot, mouse click, keyboard type, scroll
- ความเร็ว: ช้ากว่า scripting ปกติ — ต้องดู screenshot ทุก action
- แนะนำ: supervised workflows — ยังควร fully autonomous

```python
# Python — Computer Use: กรอกแบบฟอร์มบนเว็บ
import anthropic, base64
from PIL import ImageGrab
client = anthropic.Anthropic()
def take_screenshot() -> str:
    img = ImageGrab.grab()
    img.save('/tmp/screen.png')
    with open('/tmp/screen.png', 'rb') as f:
        return base64.standard_b64encode(f.read()).decode()
def computer_action(screenshot_b64: str, task: str):
    return client.messages.create(
        model='claude-opus-4-6-20260101',
        max_tokens=4096,
        betas=['computer-use-2025-01-24'],
        tools=[{'type':'computer_20250124','name':'computer',
                'display_width_px':1920,'display_height_px':1080}],
        messages=[{'role':'user','content':[
            {'type':'image','source':{'type':'base64',
             'media_type':'image/png','data':screenshot_b64}},
            {'type':'text','text':task}]}])
screen = take_screenshot()
result = computer_action(screen, "Fill in the name field: 'John Doe'")
```

### Use Cases ที่เหมาะกับ Computer Use
- **Legacy system automation:** ระบบเก่าที่ไม่มี API ต้องกรอกข้อมูลซ้ำๆ
- **Web scraping ที่ซับซ้อน:** เว็บที่ block bot แต่ Claude ทำเหมือน human
- **GUI testing:** ทดสอบ UI แบบ end-to-end โดยไม่ต้องเขียน test script
- **Research workflows:** ค้นหาข้อมูลจากหลายเว็บและรวบรวมอัตโนมัติ

> **ข้อควรระวัง Computer Use** — ต้องมี human oversight เสมอ Claude อาจ click ผิดหรือทำ action ที่ไม่ตั้งใจ · ไม่ควรให้ access กับ production systems โดยไม่มี confirmation step · ค่าใช้จ่ายสูง — ทุก screenshot = ~1,600 tokens และ loop ได้นาน · ทดสอบใน sandbox environment ก่อนเสมอ

---

## 3.10 Feature Combinations — ใช้ร่วมกันให้ทรงพลังที่สุด

Features เหล่านี้ทรงพลังที่สุดเมื่อใช้ร่วมกัน — นี่คือ production patterns ที่จริงจังและ ROI สูงที่สุด

| Pattern | Features | ROI |
|---------|---------|-----|
| **RAG Chatbot** | Files API + Prompt Caching + Citations | ลดต้นทุน 85%+ เทียบกับ naive implementation |
| **Bulk Data Processing** | Batch API + Tool Use | ลดต้นทุน 50% ไม่ติด rate limit |
| **Intelligent Automation** | Computer Use + Extended Thinking | แทน RPA ที่ brittle และต้องการ maintenance สูง |
| **Visual Analytics** | Vision + Tool Use | Automated report generation จาก screenshot |
| **Enterprise Integration** | MCP + Prompt Caching | One-time setup ใช้ได้กับ Claude ทุก interface |

### Quick Decision Guide — งานแบบไหนใช้ Feature ไหน

| ต้องการอะไร? | Feature ที่เหมาะ | เหตุผล |
|------------|---------------|-------|
| Claude ทำงานกับ real-time data | Tool Use | เรียก API/function เองได้ |
| เชื่อมกับ Slack/GitHub/DB | MCP | มี server พร้อมแล้ว |
| ส่ง PDF ใหญ่ซ้ำๆ | Files API | ไม่ต้องส่งซ้ำทุก request |
| วิเคราะห์รูปภาพ | Vision | อ่านรูป chart diagram ได้ |
| ต้องอ้างอิงแหล่งที่มา | Citations | ลด hallucination |
| Process ข้อมูลปริมาณมาก | Batch API | 50% ถูกกว่า ไม่มี rate limit |
| System prompt ยาว ใช้ซ้ำ | Prompt Caching | ประหยัดสูงสุด 90% |
| โจทย์ซับซ้อน high-stakes | Extended Thinking | แม่นขึ้น 40–60% |
| Automate GUI / no API | Computer Use | ทำงานแบบ human บน desktop |

---

## Related
- [[concepts/claude-models-family]]
- [[concepts/prompt-engineering]]
- [[references/claude-api-cheatsheet]]
- [[references/claude-complete-guide-2026]]
- [[concepts/tokenization]]
