---
title: "PC-PTMC072 (ASUS Z97-K / i7-4790)"
tags: [it-equipment, hardware, windows, maintenance-log]
category: entities
created: 2026-10-06
updated: 2026-10-09
sources: [user-provided]
summary: "Desktop ประกอบเอง เมนบอร์ด ASUS Z97-K + i7-4790 RAM 32 GB การ์ดจอ ZOTAC GTX 1060 6GB NVMe Kingston NV2 500 GB + HDD WD 500 GB ลง Windows 11 Pro ใหม่ 2026-10-06 ตั้งใช้งานที่ห้องสติ ใช้ไลฟ์สด Facebook/TikTok ด้วย OBS (NVENC); บันทึกการแก้ปัญหาบูต การอัปเกรด RAM/การ์ดจอ การสำรองและปลด HDD WD 1 TB ที่เสีย สุขภาพดิสก์ ไดรเวอร์ ค่า performance การ์ด PCIe ที่ถอดเก็บสำรอง (Wi-Fi TP-Link Archer T4E, USB 3.0 Renesas) และงานค้าง"
---

# PC-PTMC072

## ที่ตั้ง/การใช้งาน
- **ตั้งใช้งานที่:** ห้องสติ (office เดียวกับ [[entities/macmini-m4-2024|Mac mini M4]])
- **งานหลัก:** ไลฟ์สดผ่าน Facebook และ TikTok ด้วย OBS Studio (ใช้ตัวเข้ารหัส NVENC ของการ์ดจอ)

Desktop ประกอบเอง บนเมนบอร์ด ASUS Z97-K ลง Windows 11 Pro ใหม่เมื่อ 2026-10-06 วันเดียวกันนั้นพบและแก้ปัญหาบูต แล้ววันที่ 2026-10-08 อัปเกรด RAM เป็น 32 GB ใส่การ์ดจอ GTX 1060 ตั้งค่า OBS ต่อ HDD เดิม 2 ลูก สำรองข้อมูล และปลด HDD 1 TB ที่เสีย

> [!summary] สถานะล่าสุด (2026-10-08)
> - ฮาร์ดแวร์หลักแข็งแรง: RAM 32 GB ผ่าน Memory Diagnostic, NV2 ไม่มี error (Unsafe คงที่ 22), การ์ดจอทำงานที่ PCIe 3.0 x16
> - **แก้ปัญหาบูตแล้ว:** EFI bootloader ย้ายจากแฟลชไดรฟ์มาไว้บน NV2 ตั้งแต่ 2026-10-06
> - **อัปเกรด 2026-10-08:** RAM 24 → 32 GB, ZOTAC GTX 1060 6GB (ไดรเวอร์ 582.78), OBS 32.2.2 + โปรไฟล์ NVENC, ปิด Fast Startup
> - **HDD WD 1 TB เสีย และถอดออกแล้ว** (2026-10-08 ~23:10) สำรองข้อมูลไปไว้ที่ WD 500 GB แล้ว
> - ⚠️ **จอฟ้า 1 ครั้ง** (BugCheck `0x3B`, 2026-10-08 ~22:5x) หลังถอด WD 1 TB ยังไม่เกิดซ้ำ (เช็กเมื่อ 23:25) แต่ยังต้องเฝ้าดูอีกสักระยะ
> - ถอน NVIDIA App แล้ว เหลือแค่ไดรเวอร์
> - คอขวดที่เหลือ: ช่อง M.2 เป็น PCIe 2.0 x2, ต่อจอด้วย HDMI ทำให้ได้แค่ 50 Hz

## สเปกเครื่อง

| หมวด | รายละเอียด |
|---|---|
| Hostname | `PC-PTMC072` |
| เมนบอร์ด | ASUS Z97-K rev 2.01 (chipset Intel Z97 / 9 Series), BIOS 2902, UEFI |
| CPU | Intel Core i7-4790 @ 3.60 GHz (Haswell, Gen 4), 4C/8T, L2 1 MB, L3 8 MB ฮีตซิงก์ Intel ที่แถมมากับ CPU |
| RAM | **32 GB** DDR3-1600 1.5 V, 8 GB × 4 ช่อง (A1, A2, B1, B2) dual channel สมมาตร (ดูหมายเหตุ RAM) |
| การ์ดจอ | **ZOTAC GeForce GTX 1060 6GB AMP! Edition** (Pascal, `10DE:1C03`, subsystem `19DA:1438`), VBIOS 86.06.45.00.3c, power limit 120 W, ช่อง PCIe 3.0 x16 ช่องบน ลิงก์ Gen3 x16 |
| การ์ดจอออนบอร์ด | Intel HD Graphics 4600 ซึ่ง BIOS ปิดให้อัตโนมัติเมื่อมีการ์ดจอแยก |
| จอ | **BenQ RD280U** (28" 3:2, ความละเอียดจริง 3840×2560, EDID `BNQ805B`) ต่อด้วย **HDMI** จึงได้ 3840×2560 @ **50 Hz** (ดูหัวข้อ "จอและสาย") |
| SSD | Kingston NV2 `SNV2S500G` 500 GB NVMe, firmware `SBN00100`, S/N `0026_B778_5C65_D8B5` |
| ลิงก์ของ SSD | **PCIe Gen2 x2** (ตัวไดรฟ์รองรับ Gen4 x4) ต่อผ่าน chipset root port 1 (`8086:8C90`) |
| ไดรเวอร์ NVMe | Microsoft `stornvme` 10.0.26100.9278 |
| HDD | **WD Blue 500 GB** `WD5000AZLX` = ไดรฟ์ `G:` "Data" (ดูหัวข้อ HDD) ส่วน WD Blue 1 TB `WD10EZEX` **เสียและถอดออกแล้ว** (2026-10-08) |
| ตำแหน่ง HDD | อยู่ในช่องใต้ฝาครอบ PSU (PSU shroud) ฝั่งหน้าเคส ต้องเปิดฝาข้างด้านหลังเมนบอร์ดจึงจะถอดได้ |
| Storage controller | Intel SATA โหมด **AHCI** (`storahci`) |
| เครือข่าย | Realtek PCIe GbE 1 Gbps (ต่อสาย) |
| เสียง | ออนบอร์ด (ใช้ไดรเวอร์ทั่วไปของ Microsoft "High Definition Audio Device" ยังไม่ใช่ไดรเวอร์ Realtek) และ NVIDIA HD Audio (ส่งเสียงไปลำโพงจอ BenQ) **ยังไม่มีไมค์ที่ใช้งานได้** |
| USB 3.0 | Intel xHCI ออนบอร์ด ส่วนการ์ด Renesas USB 3.0 แบบ PCIe **ถอดออกแล้ว** (2026-10-08, ดูหัวข้อ "การ์ดที่ถอดเก็บสำรอง") |
| Wi-Fi | ไม่มี การ์ด TP-Link Archer T4E **ถอดเก็บสำรองแล้ว** (ดูหัวข้อ "การ์ดที่ถอดเก็บสำรอง") |
| PSU | Cougar STC750 750 W, +12V rail เดียว 60 A / 720 W, 80 PLUS (ระดับพื้นฐาน), TÜV Rheinland, หัว PCIe 6+2 pin สองหัว (ดูหัวข้อ "ผลตรวจ PSU") |
| พัดลมเคส | หน้า DeepCool CF120C × 3 และหลัง × 1 |
| OS | Windows 11 Pro 64-bit build 26300 (Retail, Licensed) ลงเมื่อ 2026-10-06 13:49 |
| BIOS | Secure Boot = Other OS, VT-x **ปิดอยู่** ใน NVRAM ยังมีรายการ legacy "Hard Drive" ซึ่งน่าจะแปลว่า CSM เปิดอยู่ (คาดการณ์) |

> [!warning] ข้อจำกัด
> i7-4790 ไม่อยู่ในรายชื่อ CPU ที่ Windows 11 รองรับ ตอนติดตั้งจึงข้ามการตรวจ TPM/CPU/Secure Boot ด้วย `autounattend.xml` อัปเดตใหญ่ในอนาคตอาจมีปัญหา
> Z97 ไม่รองรับ Resizable BAR จึงไม่ควรใช้การ์ด Intel Arc และมีช่อง PCIe 3.0 ความเร็วเต็มอยู่ช่องเดียว (การ์ดจอใช้อยู่)

> [!note] หมายเหตุ RAM
> แรมที่ซื้อเพิ่มตามบันทึกคือ HyperX FURY `HX316C10FR/8` แต่ Windows (WMI) รายงานทั้ง 4 แถวเป็น `KHX1600C10D3/8G` ที่ 1600 MHz 1.5 V
> S/N ที่อ่านได้: A1 `72133D63`, A2 `75134E63`, B1 `22030000`, B2 `1E2EF555` ยังไม่ได้ตรวจว่าแถวไหนคือแถวที่ซื้อมาใหม่

## โครงสร้างดิสก์

ลำดับเลขดิสก์ใน Windows **สลับได้หลังรีบูต** (2026-10-08 ช่วงหลัง NV2 เป็น Disk2) ให้ดูจากชื่อรุ่นเสมอ

### NV2 (GPT)

| Partition | ประเภท | ขนาด | หมายเหตุ |
|---|---|---|---|
| P1 | MSR | 16 MB | |
| P2 | `C:` NTFS | 475,729 MB | ไดรฟ์ Windows |
| P3 | **EFI System** FAT32 (label `SYSTEM`) | 260 MB | สร้างเมื่อ 2026-10-06 |
| P4 | Recovery (WinRE) | 893 MB | |

### WD 500 GB `WD5000AZLX` (MBR)

| Partition | ประเภท | ขนาด | หมายเหตุ |
|---|---|---|---|
| P1 | `G:` NTFS label **Data** | 465.8 GB | ฟอร์แมตใหม่เมื่อ 2026-10-08 (เดิมชื่อ "Program") ตอนนี้เก็บ `G:\Backup_WD1TB` |

แฟลชไดรฟ์ Kingston DataTraveler 3.0 32 GB (label `WIN10`) เป็นตัวติดตั้ง Windows ที่สร้างบน macOS **ไม่จำเป็นต่อการบูตแล้ว**

## ประวัติปัญหาและการแก้ไข

### 1. ปัญหาบูต (แก้แล้ว 2026-10-06)

**อาการก่อนแก้**
1. ตอนแรก Windows Setup มองไม่เห็น NV2 หลังถอดเสียบใหม่จึงเห็น
2. เจอ `0xc000000e` ("A required device isn't connected") สองครั้ง รวมถึงหลังลง Windows ใหม่ทั้งเครื่อง
3. เคยค้างที่โลโก้ ASUS โดยไม่มีจุดหมุน
4. สมมติฐานตอนแรกคือ NV2 หลุดการเชื่อมต่อเป็นครั้งคราว

**สาเหตุที่พบ**
- **ข้อเท็จจริง:** NV2 ไม่มี EFI System Partition เลย ESP มีอยู่ที่เดียวคือบนแฟลชไดรฟ์ ค่า `FirmwareBootDevice` ชี้ไปที่ partition บน USB และ NVRAM Boot0000 "Windows Boot Manager" ก็ชี้ไปที่ USB
- **คาดการณ์:** แฟลชไดรฟ์ถูกมองเป็นดิสก์แบบ Fixed และมี ESP ที่ macOS สร้างไว้อยู่แล้ว Windows Setup จึงนำ ESP นั้นมาใช้ซ้ำ อาการ `0xc000000e` เข้ากับสาเหตุนี้มากกว่าสมมติฐานว่า NV2 หลุด

**ขั้นตอนแก้**
1. ย่อ `C:` ลง 300 MB
2. ใช้ `diskpart` สร้าง partition efi 260 MB และฟอร์แมต FAT32
3. รัน `bcdboot C:\Windows /s S: /f UEFI` (คำสั่งนี้ไม่ได้อัปเดต NVRAM ให้)
4. ถอด USB แล้วบูตผ่าน F8 → เลือก Windows Boot Manager (KINGSTON) หนึ่งครั้ง bootmgr จึงเขียน NVRAM ใหม่ให้ชี้ไปที่ NV2 เอง
5. `reagentc /enable` ล้มเหลว (error 2) เพราะยังอ้าง BCD ID เก่าบน USB แก้ด้วย `bcdedit /deletevalue {current} recoverysequence` แล้วรัน `reagentc /enable` ใหม่จนสำเร็จ
6. ทดสอบแล้วว่าบูตได้เองโดยไม่ต้องเสียบ USB ทั้งตอน Shut down และตอน Restart

### 2. Kernel-Power 41 (ทั้งหมด 3 ครั้ง)

| ครั้ง | เวลา | หลักฐาน | สาเหตุ |
|---|---|---|---|
| 1 | 2026-10-06 20:31 | BugcheckCode 0, NV2 Unsafe ไม่เพิ่ม | น่าจะเกิดจากการเปลี่ยนเส้นทางบูตร่วมกับ Fast Startup (คาดการณ์) |
| 2 | 2026-10-08 17:34 | "last shutdown success = true", BootAppStatus `0xC00000D4`, NV2 Unsafe ยังเป็น 22 | Fast Startup กู้สถานะเดิมไม่ได้เพราะเปลี่ยน RAM และการ์ดจอ (คาดการณ์) **จึงปิด Fast Startup แล้ว** |
| 3 | 2026-10-08 22:58 | **BugcheckCode `0x3B`** (ดูหัวข้อถัดไป) | จอฟ้า |

กฎจากนี้: ก่อนเปลี่ยนหรือต่อฮาร์ดแวร์ ให้ **Shift + Shut down แล้วปิดสวิตช์ PSU** และห้ามต่อฮาร์ดแวร์ตอนเครื่อง Sleep (2026-10-08 พบว่า HDD ถูกต่อเข้ามาตอนเครื่อง Sleep)

### 3. จอฟ้า BugCheck 0x3B (2026-10-08, ยังไม่รู้สาเหตุ)
- เกิดในช่วงที่เปิดเครื่องหลังฟอร์แมต WD 1 TB ล้มเหลว (บูตตอน 22:50:55 แล้วล่มก่อน 22:58)
- `0x0000003b` (SYSTEM_SERVICE_EXCEPTION) พารามิเตอร์ `c0000005, fffff80577890b80, fffff58b6fe83780, 0`
- dump: `C:\Windows\Minidump\100826-6437-01.dmp` (volmgr 161 แจ้งว่าสร้าง dump แบบเต็มไม่สำเร็จ)
- ไม่มี error ของดิสก์บันทึกไว้ช่วงก่อนล่ม แต่ log อาจบันทึกไม่ทัน **ยังสรุปไม่ได้ว่าเกี่ยวกับ WD 1 TB หรือไม่** ถ้าเกิดซ้ำหลังถอด WD 1 TB ให้ติดตั้ง WinDbg แล้ววิเคราะห์ dump

### 4. HDD WD 1 TB เสีย (2026-10-08)
ดูหัวข้อ "HDD" ด้านล่าง

## สุขภาพ NV2: ค่า SMART

อ่านจาก NVMe SMART log (page 02h)

| ค่า | 2026-10-06 ~21:45 | 2026-10-08 ~19:20 |
|---|---|---|
| Critical Warning | 0x00 | 0x00 |
| Available Spare / Percentage Used | 100% / 0% | 100% / 0% |
| Media/Integrity Errors | 0 | 0 |
| Error Log Entries | 0 | 0 |
| Power Cycles | 46 | 55 |
| **Unsafe Shutdowns** | **22** | **22** |
| Power On Hours | 32 | 35 |
| Data Written | 301 GB | 324 GB |
| อุณหภูมิ | 31–36 °C | 33 °C |

> [!tip] วิธีเฝ้าดู
> ถ้าปิดเครื่องตามปกติแล้ว **Unsafe Shutdowns เพิ่มจาก 22** หรือ Error Log Entries ไม่เป็น 0 หรือ Event Log มี `stornvme` ID 11/129 หรือ `disk` ID 153 แสดงว่า NV2 อาจไม่เสถียรจริง
> ยังไม่ได้อ่านค่าหลังจอฟ้าเมื่อ 2026-10-08 22:5x ซึ่งอาจทำให้ Unsafe เพิ่มเป็น 23 ได้ตามปกติ

## HDD

### WD Blue 500 GB `WD5000AZLX` (S/N WD-WCC6Y5TXPXS6) ✅ ใช้งานต่อ

| ค่า (2026-10-08) | ผล |
|---|---|
| Health / PredictFailure | Healthy / False |
| Reallocated / Pending / Uncorrectable | 0 / 0 / 0 |
| **199 UDMA CRC Errors** | **8** (error จากสายหรือขั้วต่อในอดีต ถ้าเพิ่มให้เปลี่ยนสาย SATA) |
| Power-On Hours / Power Cycles | 7,519 / 2,954 |
| อุณหภูมิ | 34 °C |
| อ่านต่อเนื่อง (`winsat`) | 142 MB/s |

- 2026-10-08 ฟอร์แมตเป็น NTFS label **Data** (`G:`) ลบโฟลเดอร์ 11_Relax (ISO เกมจากปี 2019, 69.9 GB) และถังขยะออกตามที่ยืนยันแล้ว
- เก็บ **`G:\Backup_WD1TB`** ซึ่งเป็นสำเนาเดียวของข้อมูลจาก WD 1 TB:

| โฟลเดอร์ | ที่มา | ไฟล์ | ขนาด |
|---|---|---|---|
| `E_Photo&VOD` | E: Photo&VOD (รูปและวิดีโองาน: 01_งานบุญ, 02_งานก่อสร้าง, 03_งานหล่อหลอม, 04_งานส่งเสริมศีลธรรมจังหวัด, Other, ลพ แพน) | 60,545 | 297.22 GB |
| `F_PR` | F: Public Relation (PR) (ส่วนใหญ่ลบไปก่อนสำรอง) | 1 | 114 KB |
| `D_USER` | D: USER (ว่าง) | 0 | 0 |

- วิธีสำรอง: `robocopy /E /COPY:DAT /DCOPY:DAT /R:3 /W:5` ผล**ล้มเหลว 0 ไฟล์** ตรวจด้วยการเทียบชื่อและขนาดทุกไฟล์ ผลคือครบและตรงกันทั้งหมด ส่วนการตรวจ MD5 หยุดไว้ที่ประมาณ 14% ตามที่ผู้ใช้เลือก
- ⚠️ robocopy ทำให้โฟลเดอร์ปลายทางติดแอตทริบิวต์ Hidden + System จนมองไม่เห็นใน File Explorer แก้แล้วด้วย `attrib -h -s` ครั้งหน้าที่คัดลอกจาก root ของไดรฟ์ ให้ใส่ `/A-:SH`
- G: ว่างเหลือประมาณ 168 GB

### WD Blue 1 TB `WD10EZEX` (S/N WD-WCC3F6TV7DPU) ❌ เสีย ถอดออกแล้ว

| ค่า SMART | 2026-10-08 (ก่อนสำรอง) |
|---|---|
| 5 Reallocated Sectors | **54** |
| 196 Reallocation Events | 7 |
| 197 Current Pending | **1** |
| 198 Offline Uncorrectable | **1** |
| 200 Multi-Zone Error Rate | 5 |
| Power-On Hours | 12,434 |
| อ่านต่อเนื่อง | 165 MB/s |

- **2026-10-08 ~20:28–21:27:** สำรองข้อมูลทั้งหมดได้โดยไม่มี error การอ่านเลย
- **~22:14:** ลบพาร์ทิชันทั้ง 3 ตัว (D: USER, E: Photo&VOD, F: PR) แล้วทำเป็น GPT พาร์ทิชันเดียว 931.5 GB
- **22:15–22:18: ฟอร์แมตแบบเขียนศูนย์ล้มเหลวหลังเริ่มได้ประมาณ 3 นาที** มี `storahci` ID 129 (reset device) และ `disk` ID 51 จำนวน 16 ครั้ง
- หลังจากนั้น**อ่านค่า SMART ไม่ได้แล้ว** พาร์ทิชันยังเป็น RAW (ไม่มีระบบไฟล์)
- **สรุป:** ไม่ควรเอาไปใช้งานต่อ ข้อมูลเดิมส่วนใหญ่**ยังอยู่บนจาน** เพราะเขียนศูนย์ไปได้นิดเดียว ถ้าจะทิ้งให้ทำลายจานทางกายภาพ
- **~23:10 ถอดออกจากเครื่องแล้ว** หลังถอด ตรวจเมื่อ 23:25 พบว่าปิดเครื่องปกติ 2 รอบ ไม่มี error ของดิสก์ และไม่มีจอฟ้าซ้ำ

## จอและสาย

| ทดสอบเมื่อ 2026-10-08 | ผล |
|---|---|
| สายที่ใช้ | HDMI (การ์ดมีพอร์ต HDMI 2.0b) |
| 3840×2560 | ได้แค่ **50 Hz** (pixel clock 519 MHz เพราะ 60 Hz เกินขีดของ HDMI 2.0) |
| โหมด 60 Hz | ต้องลดเหลือ 1920×1200 หรือต่ำกว่า |
| แนะนำ | **สาย DisplayPort ↔ DisplayPort รุ่น DP 1.4** (VESA certified / HBR3) จะได้ 3840×2560 @ 60 Hz (คาดการณ์) ~฿200–500 อย่าใช้สาย USB-C ↔ DP |

สำหรับไลฟ์: จอเป็นสัดส่วน 3:2 แต่ OBS เป็น 16:9 ให้ใช้ "จับภาพเกม" หรือ "จับภาพหน้าต่าง" แทนจับภาพทั้งจอ ส่วนเกมควรตั้งความละเอียดในเกมเป็น 1920×1080

## OBS และการไลฟ์

- **OBS Studio 32.2.2** (ติดตั้งผ่าน winget `OBSProject.OBSStudio` ตรวจ hash และลายเซ็นแล้ว) UI เป็นภาษาไทย
- `obs-nvenc-test`: `nvenc_supported=true`, H.264 ได้ (B-frames 4, lookahead), HEVC ได้, **AV1 ไม่ได้**
- โปรไฟล์ **"NVENC Live 1080p30"** (`%APPDATA%\obs-studio\basic\profiles\NVENC_Live_1080p30`) ยืนยันจาก log แล้วว่าโหลดได้:

| ค่า | ตั้งไว้ |
|---|---|
| โหมดเอาต์พุต | ขั้นสูง |
| ตัวเข้ารหัสข้อมูลวิดีโอ | NVIDIA NVENC H.264 (`obs_nvenc_h264_tex`) |
| การควบคุมอัตราบิต / อัตราบิต | อัตราบิตคงที่ (CBR) / 6000 Kbps |
| ความถี่คีย์เฟรม | 2 วินาที |
| พรีเซ็ต / การปรับ | P5 / High Quality |
| ความละเอียด / FPS | 1920×1080 / 30 |
| เสียง | 48 kHz Stereo |

- ข้อจำกัดของ GTX 1060: ใช้ NVIDIA Broadcast ไม่ได้ (ต้องเป็น RTX) ให้ใช้ฟิลเตอร์ "การลดเสียงรบกวน" แบบ RNNoise ใน OBS แทน
- ถ้าไลฟ์ Facebook และ TikTok พร้อมกัน ต้องมีเน็ตอัปโหลดอย่างน้อยประมาณ 15–20 Mbps และต่อสายแลน
- ⚠️ **ไมค์:** ยังไม่มีอุปกรณ์อัดเสียงที่ใช้ได้ (OBS ขึ้น `GetDefaultAudioEndpoint 80070490`) ต้องเสียบไมค์ที่ช่องสีชมพูด้านหลัง หรือใช้ไมค์ USB ถ้าไม่ขึ้น ให้ลงไดรเวอร์เสียง Realtek จากหน้าซัพพอร์ต ASUS

## ไดรเวอร์

| รายการ | สถานะ |
|---|---|
| Intel 9 Series chipset INF | ติดตั้งจากแพ็กเกจของ ASUS Z97-K (`Intel_Chipset_Win7-8-81-10_V100160_10117.zip`, Win10 SetupChipset 10.1.1.7) โดยใช้ `pnputil` ติดตั้งเฉพาะ `lynxpoint-hrefreshSystem.inf` (ใน driver store คือ `oem6.inf`) |
| อุปกรณ์ที่ได้ชื่อใหม่ | SMBus `8CA2` (เดิม error code 28) และ PCIe Root Port 1/3/8 (`8C90` ต่อ NV2, `8C94` ต่อแลน, `8C9E` เคยต่อการ์ด USB Renesas ซึ่งถอดแล้ว) |
| Intel Chipset INF รุ่นล่าสุด 10.1.20658.8883 | ⚠️ บนเครื่องนี้รันไม่ได้ (exit `0xE0000001`) ให้ใช้แพ็กเกจของ ASUS แทน |
| **NVIDIA** | **582.78** "GeForce Security Update Driver" (2026-09-30, DCH, ลายเซ็น NVIDIA Corporation) อัปเดตจาก 560.94 เมื่อ 2026-10-08 Pascal ได้แค่อัปเดตความปลอดภัยแล้ว ไม่มี Game Ready รุ่นใหม่ |
| NVIDIA App 11.0.5 + ShadowPlay | **ถอนแล้ว** (2026-10-08 ~23:30 ด้วย `NVI2.DLL,UninstallPackage Display.NvApp -silent`) ส่วนประกอบ 12 รายการหายไปทั้งหมด เหลือไดรเวอร์จอ, HD Audio, PhysX, Install Application และ FrameView SDK (ไม่มีโปรแกรมใช้แล้ว ถอนได้ถ้าต้องการ) ข้อเสียคือไม่มีแจ้งเตือนไดรเวอร์ใหม่อัตโนมัติ ให้เช็กที่ nvidia.com เป็นระยะ |
| `ACPI\PNP0A0A` (`\_SB.MBDA`) | ยังไม่มีไดรเวอร์ น่าจะเป็นอุปกรณ์ ACPI เฉพาะของ ASUS (คาดการณ์) ปล่อยไว้ได้ |

หน้าซัพพอร์ตของ ASUS Z97-K ค้นหาจากเว็บ ASUS ไม่เจอ ต้องเข้าลิงก์ตรง: https://www.asus.com/supportonly/z97-k/helpdesk_download/

## ค่า performance

| หมวด | 2026-10-06 (24 GB, HD 4600) | 2026-10-08 (32 GB, GTX 1060) |
|---|---|---|
| CPU ขณะใช้งานเบา | 4.6% (สูงสุด 8.5%), 3,601/3,601 MHz ไม่มี throttling | — |
| RAM | commit 5.8 จาก 24 GB, pagefile ใช้ 0 MB | ว่าง 27.1 จาก 31.9 GB ตอนเพิ่งบูต |
| `winsat` disk seq read (C:) | **797 MB/s** ซึ่งเป็นเพดานของ PCIe 2.0 x2 | — |
| `winsat mem` | **21,144 MB/s** | **21,412 MB/s** |
| `winsat` CPU AES-256 / LZW | 3,784 / 471 MB/s | — |
| พื้นที่ว่าง C: | 418.8 / 464.6 GB | — |

### เวลาบูต (Diagnostics-Performance Event 100)

| เวลาบูต (2026-10-06) | รวม | Main path | Post-boot | หมายเหตุ |
|---|---|---|---|---|
| 13:50 | 106.7 s | 28.3 s | 78.4 s | บูตแรกหลังติดตั้ง |
| 19:07 | 20.4 s | 5.1 s | 15.3 s | |
| 20:32 | 52.6 s | 14.6 s | 38.0 s | บูตแรกจาก NV2 |
| 21:42 | 39.1 s | 8.5 s | 30.6 s | Edge +18.6 s, Defender +8.0 s (Event 101) |

## การตั้งค่าที่เปลี่ยนไปแล้ว

- [x] (10-06) ย้าย ESP และ bootloader มาไว้บน NV2 แล้วลงทะเบียน WinRE ใหม่
- [x] (10-06) ตรวจ RAM 24 GB ด้วย Windows Memory Diagnostic: **ไม่พบ error**
- [x] (10-06) ติดตั้ง Intel 9 Series chipset INF
- [x] (10-06) ปิด Edge AutoLaunch และ Startup boost รวมถึงการรันเบื้องหลังหลังปิด Edge
- [x] (10-06) Defender Quick Scan ครั้งแรก: ไม่พบภัยคุกคาม (สแกน 231 s)
- [x] (10-08) ใส่ RAM แถวที่ 4 (A2) ได้ 32 GB และตรวจด้วย Memory Diagnostic: **ไม่พบ error** (Event 1101/1201 เวลา 18:37)
- [x] (10-08) ใส่ ZOTAC GTX 1060 6GB และอัปเดตไดรเวอร์เป็น 582.78
- [x] (10-08) ถอดการ์ด USB 3.0 Renesas ออก
- [x] (10-08) **ปิด Fast Startup** (`HiberbootEnabled = 0`) แต่ยังเปิด Hibernate ไว้
- [x] (10-08) ติดตั้ง OBS 32.2.2 และสร้างโปรไฟล์ NVENC
- [x] (10-08) ฟอร์แมต WD 500 GB เป็น `G:` Data แล้วสำรองข้อมูลจาก WD 1 TB ไปไว้
- [x] (10-08) ลบพาร์ทิชัน WD 1 TB (ฟอร์แมตไม่ผ่าน) แล้วถอดดิสก์ออกจากเครื่อง
- [x] (10-08) ถอน NVIDIA App ออก
- โปรแกรมที่เปิดพร้อมเครื่อง: OneDrive, SecurityHealth
- Sleep: 15 นาทีเมื่อเสียบปลั๊ก (เปิด hybrid sleep, Hibernate after = Never) ปิดชั่วคราวระหว่างงานยาวแล้วตั้งกลับแล้ว
- ค่าที่ไม่ได้เปลี่ยน: power plan เป็น Balanced, Transparency เปิดอยู่

## การ์ดที่ถอดเก็บสำรอง

บันทึกเมื่อ 2026-10-09 จากภาพถ่ายการ์ดจริง ทั้งสองใบเป็น PCIe x1 ใส่กลับได้ที่ช่อง PCIe x1 ของ Z97-K (ช่อง PCIe 3.0 x16 ช่องบนใช้กับการ์ดจออยู่)

### 1. TP-Link Archer T4E — การ์ด Wi-Fi

| รายการ | ค่า |
|---|---|
| รุ่น | **Archer T4E(US) Ver 1.0** — AC1200 Wireless Dual Band PCI Express Adapter |
| S/N | `2223IQ4005260` (อ่านจากสติกเกอร์ ตัว `I`/`1` อาจสลับกัน) |
| FCC ID / IC | `TE7T4E` / `8853A-T4E` |
| อินเทอร์เฟซ | PCIe x1 |
| ความเร็ว | 802.11ac 2×2 dual band: 5 GHz สูงสุด 867 Mbps + 2.4 GHz สูงสุด 300 Mbps |
| เสาอากาศ | 2 ต้น แบบถอดได้ (ขั้ว RP-SMA) ติดมากับการ์ด |
| Bracket | ตอนนี้ติด bracket ความสูงเต็ม (full-height) ตัวการ์ดเป็นแบบ low-profile |
| ชิป | Realtek RTL8812AE ^[inferred] (ตามสเปก v1 ที่เผยแพร่ ยังไม่ได้ตรวจบนเครื่อง) |

- ถอดเมื่อ: ไม่ได้บันทึกวันที่ไว้ ตอนนี้เครื่องใช้สายแลน Realtek GbE ซึ่งเสถียรกว่าสำหรับการไลฟ์ ^[inferred]
- ใส่กลับเมื่อ: ต้องย้ายเครื่องไปจุดที่ไม่มีสายแลน หรือสายแลนเสีย
- ไดรเวอร์: Windows 11 มักลงให้เองผ่าน Windows Update ถ้าไม่ขึ้น ให้โหลดจากหน้าซัพพอร์ต TP-Link ของ Archer T4E **V1** ^[inferred]

### 2. PCE3U1C-R31 VER 005 — การ์ด USB 3.0 (Renesas)

| รายการ | ค่า |
|---|---|
| รุ่นบนแผงวงจร | `PCE3U1C-R31` VER 005 (การ์ดจีนไม่มียี่ห้อ มีตรา CE/FCC) |
| ชิป controller | **Renesas µPD720201** (USB 3.0 / 5 Gbps) ตรงกับที่ Windows เคยเห็นเป็น "Renesas USB 3.0" ก่อนถอด แม้ชื่อรุ่นจะมี "R31" ก็ไม่ใช่ USB 3.1 Gen 2 |
| พอร์ตด้านหลัง | USB-C × 1 + USB-A × 1 |
| ไฟเลี้ยง | **ต้องเสียบหัว SATA power จาก PSU** (ขั้วต่อ J5 ที่ขอบการ์ด) ไม่งั้นพอร์ตจ่ายไฟให้อุปกรณ์ไม่พอ |
| อินเทอร์เฟซ | PCIe x1 |
| Bracket | ความสูงเต็ม (full-height) |
| ตำแหน่งเดิม | PCIe Root Port 8 (`8C9E`) |
| ถอดเมื่อ | 2026-10-08 ~17:30 พร้อมตอนใส่การ์ดจอ |

- ใส่กลับเมื่อ: ต้องการพอร์ต USB-C หรือพอร์ต USB 3.0 เพิ่มด้านหลัง (เช่น กล้อง/การ์ดจับภาพสำหรับไลฟ์)
- ข้อควรระวัง: ทำตามกฎ **Shift + Shut down แล้วปิดสวิตช์ PSU** ก่อนใส่ และอย่าลืมเสียบสาย SATA power
- ไดรเวอร์: Windows 10/11 มีไดรเวอร์ xHCI ของ Microsoft ในตัว ไม่ต้องลงเพิ่ม

## ผลตรวจ PSU: Cougar STC750 ✅ ผ่าน (ตรวจจากฉลาก)

| จากฉลาก | ค่า | เทียบกับที่ต้องใช้ |
|---|---|---|
| กำลังรวม | 750 W | ทั้งระบบหลังใส่การ์ดจอแยกน่าจะกินไฟสูงสุดประมาณ 250 W คิดเป็นภาระแค่ประมาณ 1 ใน 3 ของ PSU (คาดการณ์) |
| +12V | 60 A / 720 W (rail เดียว) | GTX 1060 ใช้ประมาณ 120 W ส่วน i7-4790 ใช้ประมาณ 84 W |
| มาตรฐาน | 80 PLUS (ระดับพื้นฐาน), TÜV Rheinland | |
| หัว PCIe | สายติดป้าย "PCI-E" สองหัว (6+2 pin) | ใช้กับการ์ดจอแล้วหนึ่งหัว |

สรุป: PSU รองรับการ์ดจอได้โดยไม่ต้องเปลี่ยน ถ้าจะอัปเกรดการ์ดในอนาคต แนะนำให้ใช้การ์ดที่กินไฟไม่เกินประมาณ 220 W เพราะ PSU เป็นรุ่นประหยัด

## งานค้างและคำแนะนำ

- [x] ~~ถอด WD 1 TB ออกจากเครื่อง~~ ถอดแล้ว 2026-10-08 (ถ้าจะทิ้ง ให้ทำลายจาน เพราะข้อมูลเดิมยังอยู่)
- [ ] **🔴 เฝ้าดูจอฟ้าต่ออีกสักไม่กี่วัน** ถ้ายังเกิดอีก ให้ติดตั้ง WinDbg แล้ววิเคราะห์ `C:\Windows\Minidump\100826-6437-01.dmp`
- [ ] **🟡 สำรองข้อมูลชุดที่สอง** ของ `G:\Backup_WD1TB\E_Photo&VOD` (297 GB) ไว้ที่อื่น เช่น ดิสก์ใหม่ 1–2 TB (~฿1,800–2,500) หรือ cloud เพราะตอนนี้มีอยู่ชุดเดียว
- [ ] **🟡 ไมค์:** เสียบไมค์แล้วเช็กใน Windows และ OBS ถ้าไม่ขึ้น ให้ลงไดรเวอร์เสียง Realtek
- [ ] **🟡 เปลี่ยนสายจอเป็น DisplayPort 1.4** เพื่อให้ได้ 3840×2560 @ 60 Hz
- [x] ~~ถอน NVIDIA App~~ ถอนแล้ว 2026-10-08
- [ ] เช็กพอร์ต USB 3.0 หน้าเคสหลังถอดการ์ด Renesas ถ้าไม่ทำงาน ให้ย้ายสายไปหัว `USB3_12` บนเมนบอร์ด
- [ ] อ่าน NV2 SMART อีกครั้งหลังจอฟ้า (เช็ก Unsafe และ Error Log)
- [ ] เฝ้าดู UDMA CRC (8) ของ WD 500 GB ถ้าเพิ่มให้เปลี่ยนสาย SATA
- [ ] วัดเวลาบูตหลังปิด Edge Startup boost เทียบกับ post-boot 30.6 s เดิม
- [ ] (ถ้าจะใช้ WSL2, Docker หรือ VM) เปิด VT-x ใน BIOS
- [x] ~~เช็ก HDD WD 2 ลูก~~ ต่อแล้วและตรวจแล้วเมื่อ 2026-10-08
- [x] ~~ซื้อการ์ดจอแยก~~ ซื้อ ZOTAC GTX 1060 6GB AMP! มือสองพร้อมแรม `HX316C10FR/8` ในราคารวมที่เสนอ ฿2,900 (2026-10-07)
- [x] ~~เพิ่ม RAM ให้ครบ 32 GB~~ ทำแล้ว 2026-10-08
- [ ] ~~ย้าย NV2 ไปการ์ดแปลง M.2 → PCIe x16~~ **ทำไม่ได้แล้ว** เพราะการ์ดจอใช้ช่อง PCIe 3.0 ตัวเดียวที่มี

## คำสั่งที่ใช้บ่อย

ทุกคำสั่งในส่วนนี้ต้องรันใน PowerShell แบบ Administrator

```powershell
# เช็กว่าบูตจากดิสก์ไหน (เลข Disk สลับได้หลังรีบูต ให้ดูจากชื่อรุ่น)
(Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control').FirmwareBootDevice
Get-Disk | Select Number, FriendlyName, BootFromDisk, IsSystem, IsBoot

# BCD และลำดับบูตของ firmware
bcdedit /enum firmware
reagentc /info

# Event ของดิสก์ ไฟดับ และฮาร์ดแวร์ error ย้อนหลัง 7 วัน
Get-WinEvent -FilterHashtable @{LogName='System'; StartTime=(Get-Date).AddDays(-7);
  ProviderName='stornvme','disk','storahci','Microsoft-Windows-Kernel-Power','Microsoft-Windows-WHEA-Logger'} |
  ? { $_.Level -le 3 } | Select TimeCreated, ProviderName, Id, Message

# ตั้งเวลาตรวจ RAM ตอนบูตครั้งหน้า
bcdedit /bootsequence '{memdiag}'

# ปิด/เปิด Sleep ชั่วคราว (เสียบปลั๊ก)
powercfg /change standby-timeout-ac 0    # ไม่ Sleep
powercfg /change standby-timeout-ac 15   # Sleep หลัง 15 นาที

# สถานะการ์ดจอ
nvidia-smi --query-gpu=name,driver_version,pcie.link.gen.max,pcie.link.width.max,temperature.gpu,power.draw --format=csv
```

> [!example]- สคริปต์อ่าน NVMe SMART log (ไม่ต้องลงโปรแกรม)
> เลข PhysicalDrive ต้องตรงกับเลข Disk ของ NV2 ใน `Get-Disk` ณ ตอนนั้น
> ```powershell
> Add-Type -TypeDefinition @'
> using System; using System.Runtime.InteropServices; using Microsoft.Win32.SafeHandles;
> public static class Nvme {
>   [DllImport("kernel32.dll", SetLastError=true, CharSet=CharSet.Unicode)] static extern SafeFileHandle CreateFile(string n, uint a, uint s, IntPtr sa, uint c, uint f, IntPtr t);
>   [DllImport("kernel32.dll", SetLastError=true)] static extern bool DeviceIoControl(SafeFileHandle h, uint code, byte[] inb, int ins, byte[] outb, int outs, out int ret, IntPtr ov);
>   public static byte[] SmartLog(int drive) {
>     using (var h = CreateFile(@"\\.\PhysicalDrive" + drive, 0x80000000, 3, IntPtr.Zero, 3, 0, IntPtr.Zero)) {
>       byte[] buf = new byte[560];
>       BitConverter.GetBytes(50).CopyTo(buf, 0); BitConverter.GetBytes(3).CopyTo(buf, 8); BitConverter.GetBytes(2).CopyTo(buf, 12);
>       BitConverter.GetBytes(2).CopyTo(buf, 16); BitConverter.GetBytes(40).CopyTo(buf, 24); BitConverter.GetBytes(512).CopyTo(buf, 28);
>       int ret; DeviceIoControl(h, 0x002D1400, buf, buf.Length, buf, buf.Length, out ret, IntPtr.Zero);
>       byte[] log = new byte[512]; Array.Copy(buf, 48, log, 0, 512); return log; } } }
> '@
> $n = (Get-Disk | ? FriendlyName -match 'SNV2S500G').Number
> $l = [Nvme]::SmartLog($n)
> "Power Cycles=$([BitConverter]::ToUInt64($l,112)) Unsafe=$([BitConverter]::ToUInt64($l,144)) MediaErr=$([BitConverter]::ToUInt64($l,160)) ErrLog=$([BitConverter]::ToUInt64($l,176)) Temp=$([BitConverter]::ToUInt16($l,1)-273)C"
> ```

> [!example]- อ่าน SMART ของ HDD SATA (WMI ไม่ต้องลงโปรแกรม)
> ```powershell
> Get-CimInstance -Namespace root\wmi -ClassName MSStorageDriver_FailurePredictData | % {
>   $v=$_.VendorSpecific; "== $($_.InstanceName)"
>   for ($i=2; $i -lt 362; $i+=12) { $id=$v[$i]; if ($id -in 5,9,196,197,198,199) { "  ID $id value=$($v[$i+3]) raw=$([BitConverter]::ToUInt32($v,$i+5))" } } }
> ```

## Timeline

### 2026-10-06

| เวลา | เหตุการณ์ |
|---|---|
| 13:46 | ลง Windows 11 ใหม่ (บูตแรก) |
| 19:xx | สำรวจสเปก และตรวจสุขภาพแบบอ่านอย่างเดียว พบว่า ESP อยู่บน USB |
| 20:19 | ย่อ C:, สร้าง ESP บน NV2 และรัน `bcdboot` |
| 20:31 | บูตจาก NV2 สำเร็จครั้งแรก (มี Kernel-Power 41 หนึ่งครั้ง) แก้ WinRE |
| 20:40 | ทดสอบ Shut down แล้วเปิดเครื่อง (Fast Startup): ผ่าน |
| 20:56–21:30 | Windows Memory Diagnostic: ไม่พบ error |
| 21:40 | ติดตั้ง chipset INF แล้วรีสตาร์ท อุปกรณ์ทุกตัวทำงานปกติ |
| 22:10–22:16 | วัด performance ตั้งต้น, Defender Quick Scan, ปิด Edge Startup boost และ AutoLaunch |

### 2026-10-07
- ประเมินการ์ดจอและแรมที่มีคนเสนอขาย (ZOTAC GTX 1060 6GB AMP! + `HX316C10FR/8` รวม ฿2,900) และตรวจ PSU จากฉลาก ผลคือผ่าน

### 2026-10-08

| เวลา | เหตุการณ์ |
|---|---|
| ~17:30 | ใส่ RAM ที่ช่อง A2 และ GTX 1060 ที่ PCIe 3.0 x16 แล้วถอดการ์ด USB Renesas |
| 17:34 | บูตแรกหลังเปลี่ยนฮาร์ดแวร์ มี Kernel-Power 41 จาก Fast Startup |
| ~17:45 | SMART NV2: Unsafe 22 (ไม่เพิ่ม), `winsat mem` ได้ 21,412 MB/s |
| ~17:50 | อัปเดตไดรเวอร์ NVIDIA 582.78, ปิด Fast Startup, ตั้งเวลาตรวจ RAM |
| 17:55–18:37 | Restart แล้วตรวจ RAM 32 GB: ไม่พบ error |
| 18:52–19:15 | เครื่อง Sleep เองหลังไม่ได้ใช้ 15 นาที แล้วตื่นด้วยการกู้จากไฟล์ hibernate ระหว่างนั้นมีการต่อ HDD WD 2 ลูกเข้ามา |
| ~19:20–19:40 | ติดตั้ง OBS 32.2.2 และโปรไฟล์ NVENC ตรวจจอ (HDMI ได้ 50 Hz) และพบว่าไม่มีไมค์ |
| ~19:45 | ตรวจ HDD: WD 500 GB สภาพดี ส่วน WD 1 TB เริ่มเสื่อม |
| ~20:00 | ฟอร์แมต WD 500 GB เป็น G: Data |
| 20:28–21:27 | robocopy จาก WD 1 TB ไป `G:\Backup_WD1TB` ล้มเหลว 0 ไฟล์ (เครื่อง Sleep ไป 11 นาทีช่วง 20:57) |
| 21:27–21:47 | เริ่มตรวจ MD5 แล้วหยุดที่ประมาณ 14% เปลี่ยนเป็นเทียบชื่อและขนาดไฟล์ ผลคือครบทั้ง 60,545 ไฟล์ แก้แอตทริบิวต์ Hidden/System ของโฟลเดอร์สำรอง |
| 22:14–22:18 | ลบพาร์ทิชัน WD 1 TB แล้วฟอร์แมตแบบเขียนศูนย์ **ล้มเหลว** (storahci 129, disk 51 × 16) |
| 22:19 | ปิดเครื่องอัตโนมัติตามที่ตั้งไว้ (ปิดปกติ) |
| 22:51–22:58 | เปิดเครื่องแล้ว**จอฟ้า 0x3B** รีสตาร์ทเอง |
| 22:58 | บูตใหม่สำเร็จ และ WD 1 TB อ่านค่า SMART ไม่ได้แล้ว |
| 23:04–23:15 | ปิดเครื่องปกติ 2 รอบ แล้ว**ถอด WD 1 TB ออก** |
| 23:25 | ตรวจหลังถอด: เหลือ NV2 + WD 500 GB, บูตจาก NV2, ไม่มี error หรือจอฟ้าใหม่, สำเนาข้อมูลครบ 60,545 ไฟล์, GTX 1060 ปกติ |
| ~23:30 | ถอน NVIDIA App (ไดรเวอร์ 582.78 ยังทำงานปกติ) |

## Related
- [[entities/macmini-m4-2024]] — เครื่องหลักอีกเครื่องในห้องสติ
- [[entities/tplink-tl-sg1024d-switch]] — สวิตช์เครือข่ายที่ใช้ร่วมกันในห้อง (ยังไม่ยืนยันว่าเครื่องนี้ต่อผ่านสวิตช์ตัวนี้)