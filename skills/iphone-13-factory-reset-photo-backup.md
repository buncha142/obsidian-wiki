---
title: "iPhone 13 — Backup รูป → ล้างเครื่อง → เคลียร์ iCloud"
tags: [how-to, hardware, backup, it-equipment]
category: skills
created: 2026-08-24
updated: 2026-08-24
sources: [user-provided]
summary: "ขั้นตอนปลอดภัยสำหรับสำรองรูปจาก iPhone 13 ลง External SSD → ตรวจสอบความครบ → Erase All Content and Settings → ลบรูปออกจาก iCloud พร้อม Checklist แบบติ๊กได้"
---

# iPhone 13 — Backup รูป → ล้างเครื่อง → เคลียร์ iCloud

คู่มือนี้เขียนสำหรับชุดอุปกรณ์จริงที่มีอยู่: [[entities/iphone-13|iPhone 13 256GB]] + [[entities/macmini-m4-2024|Mac mini M4]] + [[entities/wd-black-sn7100-ssd|WD Black SN7100 2TB]] (ใน [[entities/ulanzi-qt03-docking-station|Ulanzi QT03]]) + [[entities/wd-blue-sn550-ssd|WD Blue SN550 1TB]] (ใน [[entities/orico-m2pv-c3-ssd-enclosure|ORICO M2PV-C3]])

---

## ⚠️ กับดัก 6 ข้อ — อ่านก่อนเริ่ม

| # | กับดัก | ผลที่เกิด |
|---|---|---|
| 1 | **Erase All Content and Settings ไม่ลบรูปใน iCloud** | ล้างเครื่องแล้วรูปยังอยู่ใน iCloud ครบ กินพื้นที่เท่าเดิม — ต้องลบแยกอีกขั้นตอน |
| 2 | **iCloud Photos = กระจกบานเดียวกัน** | ถ้าเปิด iCloud Photos อยู่ ลบรูปในเครื่อง = ลบทุกเครื่องที่ล็อกอิน Apple ID เดียวกัน → **[[entities/ipad-air-11-m2\|iPad Air M2]] จะหายด้วย** |
| 3 | **Optimize iPhone Storage** | ถ้าเปิดอยู่ ไฟล์ต้นฉบับความละเอียดเต็มอยู่บน iCloud ไม่ได้อยู่ในเครื่อง → import ผ่านสาย USB เฉย ๆ อาจได้ไฟล์ย่อหรือหลุดบางไฟล์ |
| 4 | **Recently Deleted เก็บ 30 วัน** | ลบแล้วยังกินพื้นที่ iCloud อยู่จนกว่าจะ Empty ซ้ำ |
| 5 | **2FA / Authenticator / eSIM** | ล้างเครื่องโดยไม่ย้ายก่อน = เข้าบัญชีที่ผูก Authenticator ไม่ได้อีก, eSIM ต้องขอออกใหม่จากค่าย (มีค่าธรรมเนียม) |
| 6 | **Photos Library วางบน exFAT ไม่ได้** | ถ้าจะเก็บ Photos Library บน SSD ตัวนั้นต้องฟอร์แมตเป็น APFS หรือ Mac OS Extended เท่านั้น (ไฟล์ export ธรรมดาวางบน exFAT ได้) |

---

## ลำดับที่ปลอดภัยที่สุด

```
1. เตรียมตัว (จดรหัส/ย้าย 2FA/เช็คพื้นที่)
        ↓
2. Backup รูปลง SSD  ←── ยังไม่ลบอะไรทั้งนั้น
        ↓
3. ✅ ตรวจสอบว่าครบจริง + ทำสำเนาที่ 2
        ↓
4. Backup ทั้งเครื่อง (encrypted) เผื่อต้องกู้
        ↓
5. Erase All Content and Settings
        ↓
6. ลบรูปออกจาก iCloud + Empty Recently Deleted  ←── ขั้นสุดท้ายเสมอ
```

**เหตุผลที่ลบ iCloud เป็นขั้นสุดท้าย:** ระหว่างทาง iCloud ทำหน้าที่เป็นตาข่ายนิรภัย ถ้า backup พังหรือไฟล์หาย ยังดึงกลับได้ ตราบใดที่ยังไม่กดลบใน iCloud

---

## ขั้นที่ 1 — สำรวจก่อนว่ามีเท่าไหร่

บน iPhone:
- **Settings → General → iPhone Storage → Photos** → ดูขนาดที่ใช้จริง (GB)
- **Photos app → Library → เลื่อนลงสุด** → จะขึ้น "X Photos, Y Videos" — **จดเลข 2 ตัวนี้ไว้** ใช้เทียบตอนตรวจสอบ
- **Settings → [ชื่อคุณ] → iCloud → Photos** → ดูว่าเลือก *Optimize iPhone Storage* หรือ *Download and Keep Originals*

บน Mac ดูพื้นที่ SSD ว่าพอไหม:
```bash
df -h /Volumes/*
```

> **แนะนำ:** ใช้ WD Black SN7100 2TB เป็นสำเนาหลัก และ WD Blue SN550 1TB เป็นสำเนาที่ 2 (หลัก 3-2-1: 3 สำเนา, 2 สื่อ, 1 นอกสถานที่)

---

## ขั้นที่ 2 — Backup รูป (เลือก 1 วิธี)

### วิธี A — ผ่าน Photos บน Mac ⭐ แนะนำ

ได้ไฟล์ต้นฉบับความละเอียดเต็มครบทั้ง library รวมของที่อยู่แต่บน iCloud

1. บน Mac เปิด **Photos** → ล็อกอิน Apple ID เดียวกับ iPhone
2. **Photos → Settings → iCloud** → ติ๊ก **iCloud Photos** และเลือก **Download Originals to this Mac**
3. รอโหลดจนเสร็จ (ดูสถานะที่ล่างสุดของ Library — ต้องขึ้นว่า Updated / เสร็จสมบูรณ์ **ห้ามข้ามขั้นนี้**)
4. **Edit → Select All** (`⌘A`) → **File → Export → Export Unmodified Original for N items**
   - Subfolder Format: **Moment Name** (แยกโฟลเดอร์ตามวัน/เหตุการณ์)
   - ติ๊ก **Export IPTC as XMP** เพื่อเก็บ metadata
   - ปลายทาง: `/Volumes/WD_BLACK/iPhone13-Photos-2026-08-24/`
5. **สำคัญ:** โฟลเดอร์ที่ export ออกมานี้เป็นไฟล์ธรรมดา **ไม่ sync กับ iCloud อีกแล้ว** — ปลอดภัยจากขั้นตอนลบในภายหลัง

> ถ้าพื้นที่ในเครื่อง Mac ไม่พอ: ย้าย Photos Library ไปไว้บน SSD ก่อน (SSD ต้องเป็น **APFS**) แล้วค่อยเปิด Download Originals

### วิธี B — ต่อสาย USB (Image Capture)

เร็วกว่า แต่ได้เฉพาะสิ่งที่อยู่ในเครื่องจริง

1. ที่ iPhone: **Settings → Photos → Download and Keep Originals** → รอโหลดจนครบ (ต้องมีพื้นที่ว่างพอ)
2. ต่อสายเข้ากับ Mac → กด **Trust This Computer**
3. เปิดแอป **Image Capture** → เลือก iPhone → ตั้ง *Import To* เป็นโฟลเดอร์บน SSD → **Import All**
4. **อย่าติ๊ก** "Delete after import" ในรอบแรก

### วิธี C — ขอสำเนาจาก Apple โดยตรง

ช้า (หลายวัน) แต่ได้ไฟล์ต้นฉบับครบโดยไม่ต้องพึ่งการ sync

- ไปที่ **privacy.apple.com → Request a copy of your data → Photos** → Apple ส่งลิงก์ ZIP มาให้ดาวน์โหลด
- เหมาะใช้เป็น **สำเนาสำรองอีกชั้น** ควบคู่กับวิธี A

---

## ขั้นที่ 3 — ตรวจสอบว่าครบจริง (ห้ามข้าม)

```bash
DEST="/Volumes/WD_BLACK/iPhone13-Photos-2026-08-24"

# นับไฟล์ทั้งหมด
find "$DEST" -type f ! -name '.*' | wc -l

# นับแยกตามชนิด
find "$DEST" -type f \( -iname '*.heic' -o -iname '*.jpg' -o -iname '*.jpeg' -o -iname '*.png' -o -iname '*.dng' \) | wc -l
find "$DEST" -type f \( -iname '*.mov' -o -iname '*.mp4' \) | wc -l

# ขนาดรวม
du -sh "$DEST"
```

**เทียบกับเลขที่จดไว้จาก Photos app:**
- จำนวนรูป+วิดีโอ ควรใกล้เคียงกัน
- **Live Photos จะออกมาเป็น 2 ไฟล์** (`.HEIC` + `.MOV`) ทำให้ยอด `.mov` สูงกว่าจำนวนวิดีโอจริงมาก — เรื่องปกติ ไม่ใช่ความผิดพลาด
- ขนาดรวม (GB) ควรใกล้เคียงกับที่เห็นใน iPhone Storage → Photos

**เปิดไฟล์สุ่มตรวจ 10–20 ไฟล์** — ทั้งรูปเก่าสุด ใหม่สุด และวิดีโอยาว ๆ ว่าเปิดได้จริงและไม่ใช่ไฟล์ย่อ

### ทำสำเนาที่ 2 + ตรวจด้วย checksum

```bash
SRC="/Volumes/WD_BLACK/iPhone13-Photos-2026-08-24"
DST="/Volumes/WD_BLUE/iPhone13-Photos-2026-08-24"

rsync -avh --progress "$SRC/" "$DST/"

# ตรวจซ้ำด้วย checksum — ถ้าไม่พิมพ์ชื่อไฟล์ใดออกมาเลย = เหมือนกันทุกไฟล์
rsync -rcn --delete "$SRC/" "$DST/"
```

---

## ขั้นที่ 4 — ก่อนล้างเครื่อง: ย้ายสิ่งที่กู้ไม่ได้

สิ่งเหล่านี้ **ไม่ได้อยู่ในแอป Photos** และหายถาวรถ้าลืม:

- **Authenticator apps** (Google/Microsoft Authenticator) → export หรือย้ายไปเครื่องอื่นก่อน
- **eSIM** → ถ้าใช้ eSIM ต้องติดต่อค่าย (AIS/True) เพื่อย้ายหรือขอ QR ใหม่ ก่อน Erase; ถ้าเป็นซิมกายภาพ ให้ถอดซิมออก
- **LINE** → Settings → Chats → Back up chat history ลง iCloud Drive + ยืนยันว่าจำ email/password ของบัญชี LINE ได้
- **แอปธนาคาร** (K PLUS / SCB Easy / Krungthai NEXT) → เตรียมบัตร/สมุดบัญชี + เบอร์รับ OTP ไว้สมัครใหม่
- **Apple Wallet** → ลบบัตรออกก่อน
- **Voice Memos / Notes attachments / Files** → ตรวจว่ามีอะไรค้างที่ยังไม่ได้ backup
- **สื่อในแชท** (LINE / WhatsApp / Messages) → รูปในแชทไม่ได้อยู่ใน Photos ถ้าไม่ได้กด Save
- **Health data** → อยู่ใน backup แบบ **encrypted เท่านั้น**
- **ยืนยัน trusted phone number** ที่ appleid.apple.com ว่าเบอร์ยังใช้ได้ (เผื่อ iPhone เป็นอุปกรณ์ trusted เครื่องเดียว)

### Backup ทั้งเครื่องเผื่อกู้

ต่อ iPhone กับ Mac → เปิด **Finder** → เลือก iPhone ในแถบข้าง → ติ๊ก **Encrypt local backup** (ตั้งรหัสและจดไว้) → **Back Up Now**

> ต้องติ๊ก Encrypt เท่านั้น ถึงจะได้ Health data, Keychain (รหัสผ่าน/WiFi) ติดไปด้วย

---

## ขั้นที่ 5 — ล้างเครื่อง

**Settings → General → Transfer or Reset iPhone → Erase All Content and Settings**

- ระบบจะถามรหัส Apple ID → ใส่ให้ถูกต้อง (ขั้นนี้ปิด **Find My / Activation Lock** ให้อัตโนมัติ)
- ชาร์จแบตให้เกิน 50% หรือเสียบสายไว้
- ใช้เวลาไม่กี่นาที เครื่องจะกลับมาที่หน้า "Hello"

**ถ้าจะขาย/ยกให้คนอื่น:** หลัง Erase เสร็จ เข้า appleid.apple.com → **Devices** → เลือก iPhone 13 → **Remove from account**

---

## ขั้นที่ 6 — ลบรูปออกจาก iCloud

> 🛑 **จุดที่ย้อนกลับไม่ได้** — ทำเมื่อขั้นที่ 3 ผ่านแล้วเท่านั้น และรับทราบว่ารูปจะหายจาก iPad Air M2 ด้วย

**วิธีที่ 1 — ผ่านเว็บ (สะอาดที่สุด):**
1. เข้า **icloud.com/photos** → ล็อกอิน
2. เลือกรูปแรก → เลื่อนลงล่างสุด → **Shift + คลิก** รูปสุดท้าย (หรือ `⌘A`)
3. กด **Delete**
4. ไปที่ **Recently Deleted** → **Delete All** ← ขั้นนี้ต่างหากที่คืนพื้นที่จริง

**วิธีที่ 2 — ผ่าน Photos บน Mac:** `⌘A` → `⌘⌫` → เมนู Recently Deleted → Delete All

**อย่าลืมตรวจส่วนที่แยกออกมา:**
- **Shared Albums** — ต้องลบ/ออกจากอัลบั้มแยกต่างหาก
- **iCloud Shared Photo Library** (ถ้าเปิดใช้) — ต้องจัดการแยก

**ยืนยันผล:** Settings → [ชื่อคุณ] → iCloud → **Manage Account Storage** → บรรทัด Photos ควรเหลือใกล้ 0 (อาจใช้เวลาสักพักกว่าตัวเลขจะอัปเดต)

---

## ✅ Checklist

### ระยะที่ 1 — เตรียมตัว
- [ ] จดจำนวน Photos / Videos จาก Photos app (`____ รูป / ____ วิดีโอ`)
- [ ] จดขนาด Photos จาก Settings → General → iPhone Storage (`____ GB`)
- [ ] ตรวจว่าเปิด Optimize Storage หรือ Download and Keep Originals
- [ ] ตรวจพื้นที่ว่างบน WD Black SN7100 (`df -h`)
- [ ] ตรวจพื้นที่ว่างบน WD Blue SN550 สำหรับสำเนาที่ 2
- [ ] ยืนยันว่าจำ **รหัส Apple ID** และ **passcode เครื่อง** ได้ (ลองล็อกอินจริง)
- [ ] ตรวจ trusted phone number ที่ appleid.apple.com ว่ายังใช้ได้

### ระยะที่ 2 — Backup รูป
- [ ] เลือกวิธี: ☐ A (Photos+iCloud) ☐ B (USB) ☐ C (privacy.apple.com)
- [ ] เปิด iCloud Photos บน Mac + Download Originals to this Mac
- [ ] รอ sync จนสถานะขึ้นว่าเสร็จสมบูรณ์ (ห้ามรีบ)
- [ ] Export Unmodified Originals → `/Volumes/WD_BLACK/iPhone13-Photos-2026-08-24/`
- [ ] ติ๊ก Export IPTC as XMP + Subfolder = Moment Name

### ระยะที่ 3 — ตรวจสอบ 🔍
- [ ] นับไฟล์ด้วย `find ... | wc -l` → เทียบกับเลขที่จดไว้
- [ ] ตรวจขนาดรวมด้วย `du -sh` → ใกล้เคียงกับ GB ที่จดไว้
- [ ] สุ่มเปิดไฟล์ 10–20 ไฟล์ (เก่าสุด / ใหม่สุด / วิดีโอยาว)
- [ ] ยืนยันว่าเป็นไฟล์ต้นฉบับ ไม่ใช่ไฟล์ย่อ (ดู resolution + ขนาดไฟล์)
- [ ] `rsync` สำเนาที่ 2 ลง WD Blue SN550
- [ ] `rsync -rcn` ตรวจ checksum → ไม่มี output = ผ่าน
- [ ] (ทางเลือก) อัปสำเนาที่ 3 ขึ้น cloud อื่นเป็น off-site

### ระยะที่ 4 — ย้ายสิ่งที่กู้ไม่ได้
- [ ] Authenticator apps ย้าย/export แล้ว
- [ ] eSIM จัดการแล้ว / ถอดซิมกายภาพออกแล้ว
- [ ] LINE backup chat history เรียบร้อย + จำ email/password ได้
- [ ] จดรายการแอปธนาคารที่ต้องสมัครใหม่
- [ ] ลบบัตรออกจาก Apple Wallet
- [ ] ตรวจ Voice Memos / Notes / Files ว่าไม่มีอะไรค้าง
- [ ] ตรวจสื่อในแชท LINE / WhatsApp / Messages
- [ ] ปลด pairing: [[entities/apple-airpods-4|AirPods 4]], [[entities/xiaomi-smart-band-9|Xiaomi Smart Band 9]], CarPlay
- [ ] Finder backup แบบ **Encrypt local backup** + จดรหัส backup ไว้

### ระยะที่ 5 — ล้างเครื่อง
- [ ] แบตเกิน 50% หรือเสียบสายไว้
- [ ] Settings → General → Transfer or Reset → Erase All Content and Settings
- [ ] ใส่รหัส Apple ID เพื่อปลด Activation Lock
- [ ] เครื่องกลับมาที่หน้า "Hello" เรียบร้อย
- [ ] (ถ้าจะขาย/ยกให้) ลบเครื่องออกจาก appleid.apple.com → Devices

### ระยะที่ 6 — เคลียร์ iCloud 🛑
- [ ] **ยืนยันอีกครั้งว่าระยะที่ 3 ผ่านครบทุกข้อ**
- [ ] รับทราบว่ารูปจะหายจาก iPad Air M2 ด้วย
- [ ] icloud.com/photos → เลือกทั้งหมด → Delete
- [ ] Recently Deleted → **Delete All**
- [ ] ตรวจ Shared Albums แยกต่างหาก
- [ ] ตรวจ iCloud Shared Photo Library (ถ้าเคยเปิด)
- [ ] ยืนยัน Manage Account Storage → Photos เหลือใกล้ 0

---

## หมายเหตุเพิ่มเติม

- ถ้ายังอยากมีสำเนาบน cloud แต่ไม่อยากใช้ iCloud — อัปโหลดโฟลเดอร์ที่ export ไป Google Photos / Google Drive **ก่อน** ทำระยะที่ 6
- ถ้าเก็บ iPhone ไว้ใช้ต่อ: หลังตั้งค่าใหม่ **อย่าเพิ่งเปิด iCloud Photos** จนกว่าจะเคลียร์ iCloud เสร็จ ไม่งั้นจะ sync กลับมาบางส่วน
- โฟลเดอร์บน SSD ควรตั้งชื่อพร้อมวันที่เสมอ (`iPhone13-Photos-2026-08-24`) เพื่อไม่ทับกับรอบถัดไป

## Related
- [[entities/iphone-13]]
- [[entities/macmini-m4-2024]]
- [[entities/wd-black-sn7100-ssd]]
- [[entities/wd-blue-sn550-ssd]]
- [[entities/orico-m2pv-c3-ssd-enclosure]]
- [[entities/ipad-air-11-m2]]
