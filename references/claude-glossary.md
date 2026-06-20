---
title: Claude & AI Glossary (ไทย-อังกฤษ)
tags: [reference, glossary, thai, ai, claude, vocabulary]
category: references
created: 2026-06-14
updated: 2026-06-14
sources: [claude-manual-stag-2026]
summary: "คำศัพท์ AI และ Claude ภาษาไทย-อังกฤษ 110+ คำ จากหนังสือ คู่มือ Claude ฉบับสมบูรณ์ โดย STAG — ครอบคลุมตั้งแต่พื้นฐาน LLM จนถึง Agentic AI"
---

# Claude & AI Glossary (ไทย-อังกฤษ)

*จากหนังสือ คู่มือ Claude ฉบับสมบูรณ์ โดย STAG — หน้า 475–494*

## A

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Agentic AI** | AI ที่สามารถดำเนินการหลายขั้นตอนได้อัตโนมัติ วางแผนและใช้เครื่องมือได้เอง |
| **API (Application Programming Interface)** | ช่องทางเชื่อมต่อโปรแกรมกับ Claude แบบโปรแกรมเมอร์ |
| **Artifact** | ผลผลิตจาก Claude เช่น โค้ด เอกสาร รูปภาพ |
| **Attention Mechanism** | กลไก Transformer ที่ช่วยให้โมเดลเน้นส่วนสำคัญของข้อมูล |

## B

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Batch API** | API สำหรับส่ง request จำนวนมากพร้อมกัน ราคาถูกกว่า 50% |
| **BPE (Byte Pair Encoding)** | วิธี tokenization ที่ Claude ใช้ แบ่งข้อความเป็น subword units |
| **Budget Tokens** | จำนวน token ที่กำหนดให้ Extended Thinking ใช้ในการคิด |

## C

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Chain-of-Thought (CoT)** | เทคนิค prompt ให้โมเดลแสดงขั้นตอนการคิดก่อนตอบ |
| **Claude** | AI Assistant จาก Anthropic — ไม่ใช่ Search Engine แต่เป็น Reasoning Engine |
| **Constitutional AI** | วิธีฝึก AI ด้วยหลักการ (Constitution) แทน Human Feedback ล้วนๆ |
| **Context Window** | ขนาด "หน่วยความจำระยะสั้น" ของ LLM — Claude = 200K tokens |
| **Context Stuffing** | การยัด context ทั้งหมดเข้า prompt แทนการใช้ RAG |
| **CSAM** | Child Sexual Abuse Material — เนื้อหาที่ Claude ปฏิเสธสร้างเด็ดขาด |

## D

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Delta** | ส่วนต่างของข้อมูลที่เพิ่มขึ้น — ใน wiki-ingest หมายถึงข้อมูลใหม่ที่ยังไม่ได้ ingest |
| **Diffusion Model** | โมเดลสร้างภาพโดย denoise ทีละขั้น (DALL-E, Stable Diffusion) |

## E

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Embedding** | การแปลงข้อความเป็น vector ตัวเลข เพื่อใช้ในการค้นหาเชิงความหมาย |
| **Extended Thinking** | ฟีเจอร์ Claude ที่ให้โมเดลคิดภายในก่อนตอบ (Opus/Sonnet) |

## F

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Few-shot Prompting** | การให้ตัวอย่างใน prompt เพื่อสอนรูปแบบการตอบ |
| **Fine-tuning** | การฝึกโมเดลต่อบนข้อมูลเฉพาะทาง |
| **Function Calling / Tool Use** | ความสามารถของ Claude ในการเรียกใช้ function/tool ภายนอก |

## G

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Grounding** | การให้ข้อมูลจริงแก่โมเดลเพื่อลด hallucination |
| **Guardrails** | ขอบเขตและกฎที่กำหนดพฤติกรรม AI |

## H

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Hallucination** | การที่ LLM สร้างข้อมูลที่ไม่มีจริงหรือผิดพลาด แต่ฟังดูน่าเชื่อถือ |
| **Harmful Content** | เนื้อหาที่ก่อความเสียหาย — Claude ประเมินตาม context |
| **Haiku** | Claude tier เร็วที่สุดและถูกที่สุด เหมาะกับงาน classification |
| **HHH** | Helpful, Harmless, Honest — 3 ค่านิยมหลักของ Claude |
| **Human Turn** | ส่วนของการสนทนาที่ User พิมพ์ข้อความ |

## I

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Inference** | กระบวนการที่โมเดล generate output จาก input |
| **Input Tokens** | token ทั้งหมดที่ส่งให้ Claude (System Prompt + History + Message) |

## J

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **JSON Mode** | การบังคับให้ Claude ตอบเป็น JSON เท่านั้น |
| **Jailbreak** | การพยายาม bypass ข้อจำกัดความปลอดภัยของ AI |

## K

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Knowledge Cutoff** | วันที่ข้อมูลใน training data หยุด — Claude ไม่รู้เรื่องหลังจากนั้น |

## L

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Latency** | เวลาที่ใช้ก่อนได้รับ response แรก (Time to First Token) |
| **LLM (Large Language Model)** | โมเดลภาษาขนาดใหญ่ ฝึกบนข้อมูลข้อความจำนวนมหาศาล |
| **Lost-in-the-Middle** | ปัญหาที่ LLM ลืมข้อมูลตรงกลาง context |

## M

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Max Tokens** | จำนวน token สูงสุดที่อนุญาตให้ Claude ตอบ |
| **Model Card** | เอกสารความโปร่งใสเกี่ยวกับความสามารถและข้อจำกัดของโมเดล |
| **Multi-modal** | โมเดลที่รับ input หลายประเภท (ข้อความ + ภาพ + เสียง) |
| **MTok** | Million Tokens — หน่วยที่ใช้คิดราคา API |

## N

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Neural Network** | โครงข่ายประสาทเทียม — พื้นฐานของ LLM |

## O

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Operator** | บริษัท/นักพัฒนาที่ใช้ Claude API เพื่อสร้างผลิตภัณฑ์ |
| **Opus** | Claude tier ฉลาดที่สุด เหมาะกับงานซับซ้อน |
| **Output Tokens** | token ที่ Claude สร้างในการตอบ (คิดราคาแยก แพงกว่า input 3–5×) |

## P

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **PARE Framework** | Prompt, Assess, Refine, Evaluate — กระบวนการทดสอบ prompt |
| **Persona** | บทบาทหรือตัวตนที่ Claude รับในการตอบสนอง |
| **Principal Hierarchy** | ลำดับชั้น Anthropic → Operator → User ที่ควบคุม Claude |
| **Prompt** | ข้อความที่ส่งให้ LLM เพื่อ generate output |
| **Prompt Caching** | การ cache System Prompt เพื่อลดต้นทุน (ประหยัดได้ถึง 90%) |
| **Prompt Engineering** | ศาสตร์การออกแบบ prompt เพื่อได้ผลลัพธ์ดีที่สุด |
| **Prompt Injection** | การฝังคำสั่งอันตรายใน input เพื่อ override System Prompt |

## R

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **RAG (Retrieval-Augmented Generation)** | เพิ่มข้อมูลภายนอกให้ LLM ผ่าน retrieval ก่อน generate |
| **Rate Limit** | ขีดจำกัด request/token ต่อนาทีของ API |
| **Reasoning Engine** | สิ่งที่ Claude เป็น — ประมวลผลและ generate ไม่ใช่แค่ search |
| **RLHF** | Reinforcement Learning from Human Feedback |
| **RPM** | Requests Per Minute — ขีดจำกัด API |

## S

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Sonnet** | Claude tier สมดุล — แนะนำสำหรับ production ทั่วไป |
| **Streaming** | การส่ง response ทีละ token แบบ real-time แทนรอทั้งหมด |
| **System Prompt** | ข้อความที่ Operator ส่งให้ Claude ก่อนการสนทนา ใช้กำหนด persona/rules |

## T

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Temperature** | ค่าความสุ่มของ output — 0 = deterministic, 1 = creative |
| **Token** | หน่วยพื้นฐานที่ LLM ใช้อ่านและสร้างข้อความ |
| **Tool Use** | ความสามารถ Claude ในการเรียกใช้ external function/API |
| **Top-p (Nucleus Sampling)** | พารามิเตอร์ควบคุม diversity ของ output |
| **TPM** | Tokens Per Minute — ขีดจำกัด API |
| **Transformer** | สถาปัตยกรรม neural network พื้นฐานของ LLM สมัยใหม่ |

## U

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **User** | ผู้ใช้ปลายทางที่สนทนากับ Claude — tier ต่ำสุดใน Principal Hierarchy |

## V

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Vector Database** | ฐานข้อมูลที่เก็บ embedding vectors สำหรับ semantic search |
| **Vision** | ความสามารถอ่านและวิเคราะห์ภาพของ Claude |

## W

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Weights** | พารามิเตอร์ที่เก็บความรู้ของโมเดล ได้จากการฝึก |

## X

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **XML Tags** | แท็ก `<tag>...</tag>` ที่ใช้ใน prompt เพื่อแบ่งส่วนชัดเจน — Claude เข้าใจดีมาก |

## Z

| คำอังกฤษ | คำไทย / ความหมาย |
|----------|------------------|
| **Zero-shot Prompting** | การ prompt โดยไม่ให้ตัวอย่าง — Claude ใช้ความรู้ที่ฝึกมา |

---

## Related
- [[concepts/prompt-engineering]]
- [[concepts/claude-models-family]]
- [[concepts/tokenization]]
- [[concepts/constitutional-ai]]
- [[references/claude-api-cheatsheet]]
- [[references/claude-complete-guide-2026]]
