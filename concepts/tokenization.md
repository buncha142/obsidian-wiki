---
title: Tokenization และระบบ Token
tags: [concept, token, pricing, thai, tokenization, llm]
category: concepts
created: 2026-06-14
updated: 2026-06-14
sources: [claude-manual-stag-2026]
summary: "Token คือหน่วยพื้นฐานที่ LLM ใช้อ่านและสร้างข้อความ — ภาษาไทยใช้ token มากกว่าอังกฤษ 2–2.8 เท่า ส่งผลต่อราคาและ context window"
---

# Tokenization และระบบ Token

## Token คืออะไร

**Token** คือหน่วยพื้นฐานที่ LLM ใช้ในการประมวลผลข้อความ — ไม่ใช่คำ ไม่ใช่ตัวอักษร แต่เป็น **ชิ้นส่วนของข้อความ** ที่ tokenizer แบ่งไว้

```
"Hello, world!" → ["Hello", ",", " world", "!"] = 4 tokens

"สวัสดีครับ" → ["สวัส", "ดี", "ครับ"] ≈ 3-5 tokens
(แล้วแต่ tokenizer)
```

## ทำไมภาษาไทยถึงแพงกว่า

Claude ใช้ **BPE (Byte Pair Encoding)** ซึ่งถูก optimize สำหรับภาษาอังกฤษเป็นหลัก

| ภาษา | คำ 100 คำ ≈ กี่ token |
|------|----------------------|
| อังกฤษ | ~100–130 tokens |
| ไทย | ~200–360 tokens |
| อัตราส่วน | **ไทยแพงกว่า 2–2.8×** |

### ผลกระทบในทางปฏิบัติ

- **ค่าใช้จ่าย:** prompt ภาษาไทย 1,000 คำ อาจเสียเงินเท่ากับภาษาอังกฤษ 2,800 คำ
- **Context Window:** ถ้า context 200K tokens → จุได้ข้อความไทยน้อยกว่าอังกฤษ ~2×
- **Speed:** ภาษาไทยสร้าง output ช้ากว่าเล็กน้อย (tokens มากกว่า)

## การนับ Token

### กฎทั่วไป (ประมาณ)
```
1 token ≈ 4 ตัวอักษรอังกฤษ
1 token ≈ ¾ คำภาษาอังกฤษ
100 tokens ≈ 75 คำอังกฤษ

1 หน้า A4 (อังกฤษ) ≈ 500–750 tokens
1 หน้า A4 (ไทย) ≈ 1,000–1,500 tokens
```

### Context 200K tokens ≈ เท่าไหร่
| เนื้อหา | ประมาณ |
|---------|--------|
| หนังสืออังกฤษ | ~150,000 คำ (300 หน้า A4) |
| โค้ด Python | ~7,500 บรรทัด |
| ไฟล์ไทย | ~100,000 คำ |
| บทสนทนา | ~1,000 รอบ ถาม-ตอบ |

## Input vs Output Tokens

Claude คิดราคาแยก Input กับ Output:

```
Input Tokens  = ทุกอย่างที่ส่งให้ Claude (System Prompt + History + Message ปัจจุบัน)
Output Tokens = สิ่งที่ Claude ตอบกลับมา

ราคา Output มักแพงกว่า Input 3–5×
```

### ตัวอย่างราคา (Sonnet 4.6)
```
Input:  $3 / 1M tokens
Output: $15 / 1M tokens

สนทนา 10,000 tokens input + 2,000 tokens output:
= (10,000 × $3/1M) + (2,000 × $15/1M)
= $0.03 + $0.03 = $0.06 ต่อการสนทนา
```

## Cache Tokens (Prompt Caching)

Anthropic รองรับ **Prompt Caching** — เก็บ System Prompt ที่ซ้ำกันไว้ใน cache:

| | ราคาปกติ | Cache Write | Cache Read |
|--|---------|------------|------------|
| Sonnet | $3/MTok | $3.75/MTok | $0.30/MTok |

- Cache TTL: 5 นาที
- ประหยัดได้ถึง 90% สำหรับ System Prompt ขนาดใหญ่

## เทคนิคลดต้นทุน Token

1. **เขียน Prompt เป็นอังกฤษ** เมื่อเป็นไปได้ (ถูกกว่า 2×)
2. **ใช้ Prompt Caching** สำหรับ System Prompt ที่ซ้ำ
3. **Batch API** ลด 50% สำหรับงานที่ไม่ real-time
4. **เลือกโมเดลให้เหมาะ** — Haiku สำหรับงานง่าย
5. **จำกัด Output Length** ด้วย `max_tokens`

## Related
- [[concepts/claude-models-family]]
- [[concepts/context-window]]
- [[references/claude-api-cheatsheet]]
