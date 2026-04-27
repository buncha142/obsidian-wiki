# โน้ตหยาบ — ตัวอย่าง staging

วันนี้อ่านเรื่อง Transformer architecture แล้วมีบางอย่างน่าสนใจ

attention mechanism คือการถ่วงน้ำหนัก tokens ว่าอันไหนสำคัญต่อกัน
- query, key, value คือ 3 projection ที่ใช้
- self-attention ดูความสัมพันธ์ภายใน sequence เดียวกัน
- multi-head ทำ attention หลาย ๆ "มุมมอง" พร้อมกัน

ยังสับสนเรื่อง positional encoding ว่าทำไมต้อง add ไม่ใช่ concat?

link ที่อ่าน: Attention is All You Need paper

---
*โน้ตนี้อยู่ใน _raw/ — พิมพ์ `/wiki-ingest` เพื่อให้ AI promote เป็น wiki pages ที่ concepts/transformer-architecture.md และ concepts/attention-mechanism.md*
