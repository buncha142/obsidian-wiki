---
title: Claude API Cheatsheet
tags: [reference, api, python, typescript, sdk, pricing, model-id]
category: references
created: 2026-06-14
updated: 2026-06-14
sources: [claude-manual-stag-2026]
summary: "Claude API quick reference: Model IDs, ราคา, Python SDK patterns, TypeScript SDK patterns, Tool Use, Streaming, Extended Thinking"
---

# Claude API Cheatsheet

## Model IDs (2026)

```python
# Opus — ฉลาดที่สุด
"claude-opus-4-8"
"claude-opus-4-6"

# Sonnet — สมดุล (แนะนำสำหรับ production)
"claude-sonnet-4-6"

# Haiku — เร็วและถูก
"claude-haiku-4-5-20251001"
```

## ราคา ($/Million Tokens)

| Model | Input | Output | Cache Write | Cache Read |
|-------|-------|--------|-------------|------------|
| Opus 4.x | $15 | $75 | $18.75 | $1.50 |
| Sonnet 4.6 | $3 | $15 | $3.75 | $0.30 |
| Haiku 4.5 | $0.25 | $1.25 | $0.30 | $0.03 |

**Batch API:** ลด 50% จากราคาข้างต้น

---

## Python SDK

### ติดตั้ง
```bash
pip install anthropic
```

### Basic Message
```python
import anthropic

client = anthropic.Anthropic(api_key="YOUR_API_KEY")

message = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=1024,
    messages=[
        {"role": "user", "content": "Hello, Claude!"}
    ]
)

print(message.content[0].text)
```

### System Prompt
```python
message = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=1024,
    system="You are a helpful Thai language tutor.",
    messages=[
        {"role": "user", "content": "What is สวัสดี?"}
    ]
)
```

### Multi-turn Conversation
```python
messages = []

# เพิ่ม message ทีละรอบ
messages.append({"role": "user", "content": "ฉันชื่อมิน"})

response = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=512,
    messages=messages
)

# เพิ่ม response กลับเข้า history
messages.append({
    "role": "assistant",
    "content": response.content[0].text
})

# รอบต่อไป
messages.append({"role": "user", "content": "ฉันชื่ออะไร?"})
response2 = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=512,
    messages=messages
)
```

### Streaming
```python
with client.messages.stream(
    model="claude-sonnet-4-6",
    max_tokens=1024,
    messages=[{"role": "user", "content": "เขียนบทกวีสั้น"}]
) as stream:
    for text in stream.text_stream:
        print(text, end="", flush=True)
```

### Vision (Image Input)
```python
import base64

with open("image.jpg", "rb") as f:
    image_data = base64.standard_b64encode(f.read()).decode("utf-8")

message = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=1024,
    messages=[{
        "role": "user",
        "content": [
            {
                "type": "image",
                "source": {
                    "type": "base64",
                    "media_type": "image/jpeg",
                    "data": image_data,
                },
            },
            {"type": "text", "text": "อธิบายภาพนี้"}
        ],
    }]
)
```

### Tool Use (Function Calling)
```python
tools = [
    {
        "name": "get_weather",
        "description": "Get current weather for a city",
        "input_schema": {
            "type": "object",
            "properties": {
                "city": {"type": "string", "description": "City name"},
                "unit": {"type": "string", "enum": ["celsius", "fahrenheit"]}
            },
            "required": ["city"]
        }
    }
]

response = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=1024,
    tools=tools,
    messages=[{"role": "user", "content": "อากาศกรุงเทพเป็นยังไง?"}]
)

# ถ้า Claude อยากใช้ tool:
if response.stop_reason == "tool_use":
    tool_call = next(b for b in response.content if b.type == "tool_use")
    print(f"Tool: {tool_call.name}, Input: {tool_call.input}")
```

### Prompt Caching
```python
response = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=1024,
    system=[
        {
            "type": "text",
            "text": "คุณคือ assistant ที่ช่วยงานด้าน [domain]...",
            "cache_control": {"type": "ephemeral"}  # cache 5 นาที
        }
    ],
    messages=[{"role": "user", "content": "คำถาม..."}]
)
```

### Extended Thinking (Opus/Sonnet)
```python
response = client.messages.create(
    model="claude-opus-4-8",
    max_tokens=16000,
    thinking={
        "type": "enabled",
        "budget_tokens": 10000  # จำนวน token ที่อนุญาตให้คิด
    },
    messages=[{"role": "user", "content": "แก้ปัญหาคณิตศาสตร์ยากๆ..."}]
)

# แยก thinking กับ response
for block in response.content:
    if block.type == "thinking":
        print("Thinking:", block.thinking)
    elif block.type == "text":
        print("Answer:", block.text)
```

### Batch API
```python
import anthropic

client = anthropic.Anthropic()

# สร้าง batch
batch = client.messages.batches.create(
    requests=[
        {
            "custom_id": "req-1",
            "params": {
                "model": "claude-haiku-4-5-20251001",
                "max_tokens": 100,
                "messages": [{"role": "user", "content": "Hello"}]
            }
        },
        # ... requests อื่นๆ
    ]
)

print(f"Batch ID: {batch.id}")

# ตรวจสถานะ
batch_status = client.messages.batches.retrieve(batch.id)
print(f"Status: {batch_status.processing_status}")

# ดึงผลลัพธ์ (เมื่อ ended)
for result in client.messages.batches.results(batch.id):
    print(f"{result.custom_id}: {result.result.message.content[0].text}")
```

---

## TypeScript SDK

### ติดตั้ง
```bash
npm install @anthropic-ai/sdk
```

### Basic Message
```typescript
import Anthropic from "@anthropic-ai/sdk";

const client = new Anthropic({ apiKey: process.env.ANTHROPIC_API_KEY });

const message = await client.messages.create({
  model: "claude-sonnet-4-6",
  max_tokens: 1024,
  messages: [{ role: "user", content: "Hello, Claude!" }],
});

console.log(message.content[0].text);
```

### Streaming
```typescript
const stream = await client.messages.stream({
  model: "claude-sonnet-4-6",
  max_tokens: 1024,
  messages: [{ role: "user", content: "เขียนบทกวีสั้น" }],
});

for await (const chunk of stream) {
  if (
    chunk.type === "content_block_delta" &&
    chunk.delta.type === "text_delta"
  ) {
    process.stdout.write(chunk.delta.text);
  }
}
```

### Tool Use
```typescript
const tools: Anthropic.Tool[] = [
  {
    name: "get_weather",
    description: "Get weather for a city",
    input_schema: {
      type: "object",
      properties: {
        city: { type: "string" },
      },
      required: ["city"],
    },
  },
];

const response = await client.messages.create({
  model: "claude-sonnet-4-6",
  max_tokens: 1024,
  tools,
  messages: [{ role: "user", content: "อากาศกรุงเทพเป็นยังไง?" }],
});
```

---

## Environment Variables

```bash
# .env
ANTHROPIC_API_KEY=sk-ant-...

# Python อ่านอัตโนมัติถ้าตั้ง ANTHROPIC_API_KEY
client = anthropic.Anthropic()  # ไม่ต้องใส่ api_key

# TypeScript
const client = new Anthropic();  # อ่านจาก process.env.ANTHROPIC_API_KEY
```

## Response Object Structure

```python
response = client.messages.create(...)

response.id           # "msg_01..."
response.model        # "claude-sonnet-4-6"
response.role         # "assistant"
response.content      # list of content blocks
response.stop_reason  # "end_turn" | "max_tokens" | "tool_use" | "stop_sequence"
response.usage.input_tokens   # จำนวน input tokens ที่ใช้
response.usage.output_tokens  # จำนวน output tokens ที่ใช้
```

## Related
- [[concepts/claude-models-family]]
- [[concepts/tokenization]]
- [[concepts/prompt-engineering]]
- [[references/claude-glossary]]
