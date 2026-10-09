---
title: "PC-PTMC072 (ASUS Z97-K / i7-4790)"
tags: [it-equipment, hardware, windows, maintenance-log]
category: entities
created: 2026-10-06
updated: 2026-10-09
sources: [user-provided]
summary: "Desktop ประกอบเอง เมนบอร์ด ASUS Z97-K + i7-4790 RAM 32 GB การ์ดจอ ZOTAC GTX 1060 6GB NVMe Kingston NV2 500 GB + HDD WD 500 GB ลง Windows 11 Pro ใหม่ 2026-10-06 ตั้งใช้งานที่ห้องสติ ใช้ไลฟ์สด Facebook/TikTok ด้วย OBS (NVENC) ใช้คีย์บอร์ด เมาส์ และจอ BenQ ร่วมกับ Mac mini M4 (ปุ่มแบบ Mac ผ่าน PowerToys, สลับจอผ่าน DDC/CI) เปิด Wake-on-LAN แล้ว; บันทึกการแก้ปัญหาบูต การอัปเกรด RAM/การ์ดจอ การสำรองและปลด HDD WD 1 TB ที่เสีย สุขภาพดิสก์ ไดรเวอร์ ค่า performance และงานค้าง"
---

# PC-PTMC072

## ที่ตั้ง/การใช้งาน
- **ตั้งใช้งานที่:** ห้องสติ (office เดียวกับ [[entities/macmini-m4-2024|Mac mini M4]])
- **งานหลัก:** ไลฟ์สดผ่าน Facebook และ TikTok ด้วย OBS Studio (ใช้ตัวเข้ารหัส NVENC ของการ์ดจอ)

Desktop ประกอบเอง บนเมนบอร์ด ASUS Z97-K ลง Windows 11 Pro ใหม่เมื่อ 2026-10-06 วันเดียวกันนั้นพบและแก้ปัญหาบูต แล้ววันที่ 2026-10-08 อัปเกรด RAM เป็น 32 GB ใส่การ์ดจอ GTX 1060 ตั้งค่า OBS ต่อ HDD เดิม 2 ลูก สำรองข้อมูล และปลด HDD 1 TB ที่เสีย

> [!summary] สถานะล่าสุด (2026-10-09)
> - **Wake-on-LAN ใช้งานได้** (ทดสอบแล้ว 14:25 แหล่งที่ปลุก = Realtek) เปลี่ยนไดรเวอร์แลนเป็น Realtek 10.10.714.2016 และเปิด BIOS Power On By PCI-E/PCI
> - **ใช้อุปกรณ์ร่วมกับ Mac mini M4:** Keychron K6 (บลูทูธ), MX Master 3 (Unifying), จอ BenQ RD280U (PC = HDMI, Mac = USB-C) สลับจอด้วย Cmd+Option+2
> - **ปุ่มคีย์บอร์ดแบบ Mac** ผ่าน PowerToys Keyboard Manager (Caps Lock สลับภาษา, Shift+Caps Lock = ตัวใหญ่ค้าง)
>
> **สถานะ 2026-10-08**
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
| จอ | **BenQ RD280U** (28" 3:2, ความละเอียดจริง 3840×2560, EDID `BNQ805B`) ต่อด้วย **HDMI** จึงได้ 3840×2560 @ **50 Hz** (ดูหัวข้อ "จอและสาย") ใช้ร่วมกับ Mac mini ผ่าน USB-C สั่งสลับช่องผ่าน DDC/CI ได้ |
| SSD | Kingston NV2 `SNV2S500G` 500 GB NVMe, firmware `SBN00100`, S/N `0026_B778_5C65_D8B5` |
| ลิงก์ของ SSD | **PCIe Gen2 x2** (ตัวไดรฟ์รองรับ Gen4 x4) ต่อผ่าน chipset root port 1 (`8086:8C90`) |
| ไดรเวอร์ NVMe | Microsoft `stornvme` 10.0.26100.9278 |
| HDD | **WD Blue 500 GB** `WD5000AZLX` = ไดรฟ์ `G:` "Data" (ดูหัวข้อ HDD) ส่วน WD Blue 1 TB `WD10EZEX` **เสียและถอดออกแล้ว** (2026-10-08) |
| ตำแหน่ง HDD | อยู่ในช่องใต้ฝาครอบ PSU (PSU shroud) ฝั่งหน้าเคส ต้องเปิดฝาข้างด้านหลังเมนบอร์ดจึงจะถอดได้ |
| Storage controller | Intel SATA โหมด **AHCI** (`storahci`) |
| เครือข่าย | Realtek RTL8168 PCIe GbE 1 Gbps (ต่อสาย) MAC `1C-87-2C-60-24-3C`, IP `192.168.200.108` (DHCP) ไดรเวอร์ Realtek 10.10.714.2016 **เปิด Wake-on-LAN แล้ว** (ดูหัวข้อ "Wake-on-LAN และรีโมต") |
| Wi-Fi | ไม่มีในตัว (Z97-K ไม่มี Wi-Fi และบลูทูธ) |
| บลูทูธ | USB dongle CSR `0A12:0001` **Bluetooth 4.0** ไดรเวอร์ Microsoft `bth.inf` น่าจะเป็นชิปเลียนแบบ CSR8510 (คาดการณ์) ใช้กับ Keychron K6 |
| อุปกรณ์ป้อนข้อมูล | Keychron K6 (บลูทูธ) และ Logitech MX Master 3 (ตัวรับ Unifying `046D:C52B`) ใช้ร่วมกับ Mac mini (ดูหัวข้อ "อุปกรณ์ร่วมกับ Mac mini") |
| เสียง | ออนบอร์ด (ใช้ไดรเวอร์ทั่วไปของ Microsoft "High Definition Audio Device" ยังไม่ใช่ไดรเวอร์ Realtek) และ NVIDIA HD Audio (ส่งเสียงไปลำโพงจอ BenQ) **ยังไม่มีไมค์ที่ใช้งานได้** |
| USB 3.0 | Intel xHCI ออนบอร์ด ส่วนการ์ด Renesas USB 3.0 แบบ PCIe **ถอดออกแล้ว** (2026-10-08) |
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

## อุปกรณ์ร่วมกับ Mac mini (2026-10-09)

ใช้คีย์บอร์ด เมาส์ และจอชุดเดียวกับ [[entities/macmini-m4-2024|Mac mini M4]] แล้วสลับเครื่องด้วยมือ

| สลับไป | จอ | Keychron K6 | MX Master 3 |
|---|---|---|---|
| **PC** | Cmd+Option+1 (ตั้งใน Display Pilot 2 บน Mac ยังไม่ได้ตั้ง) | Fn+1 (บลูทูธ ช่อง 1) | ปุ่ม 1 (Unifying) |
| **Mac** | **Cmd+Option+2** (PowerToys → MonitorInput.exe) | Fn+2 (บลูทูธ ช่อง 2) | ปุ่ม 2 (บลูทูธ) |

- **Keychron K6:** ต่อผ่าน dongle บลูทูธ CSR (MAC ของคีย์บอร์ด `DC:2C:26:FC:7B:D4`) แจ้งตัวเป็นรหัส Apple `05AC:024F` **สวิตช์ข้างคีย์บอร์ดค้างไว้ที่ Mac/iOS ตลอด** การแมปปุ่มด้านล่างออกแบบสำหรับโหมดนี้
- **MX Master 3:** ต่อผ่านตัวรับ Unifying ลง **Logi Options+ 2.9.984725** (winget `Logitech.OptionsPlus` ตัวติดตั้งมีลายเซ็น Logitech Inc) winget แจ้งรหัส 1008 แต่ติดตั้งครบ เพราะตัวติดตั้งไปโหลดเวอร์ชันที่ใหม่กว่ามาลงเอง
- ถอดตัวรับของคีย์บอร์ด AJAZZ AK820 MAX และตัวรับเมาส์ Logitech นาโน `046D:C52F` ออกแล้ว
- dongle บลูทูธเป็น BT 4.0 ใช้ไมค์บลูทูธได้แค่โหมดคุณภาพต่ำ (HFP) จึง**ไม่เหมาะกับไมค์ไลฟ์** Event BTHUSB 34/18 ตอนเสียบเป็นเรื่องปกติของชิปรุ่นเก่า

### ปุ่มคีย์บอร์ดแบบ Mac (PowerToys Keyboard Manager)

ติดตั้ง **PowerToys 0.101.2362** (winget `Microsoft.PowerToys` แบบ user scope) ไฟล์ตั้งค่าอยู่ที่ `%LOCALAPPDATA%\Microsoft\PowerToys\Keyboard Manager\default.json` เปิด editor ด้วย Ctrl+Shift+Q (ตำแหน่ง Mac) หรือปิดการแมปทั้งหมดได้ที่สวิตช์ Keyboard Manager ในแอป

| กดบน K6 (โหมด Mac) | Windows ทำ |
|---|---|
| Cmd (ซ้าย/ขวา) | Ctrl ทำให้ Cmd+C/V/X/Z/A/S/F/T/W ใช้ได้เหมือน Mac |
| Ctrl ตัวซ้ายสุด | Win |
| **Caps Lock** | สลับภาษาไทย ↔ อังกฤษ (Win+Space) |
| **Shift + Caps Lock** | เปิด/ปิด Caps Lock (ทดสอบแล้วใช้ได้) |
| Cmd+Space / Cmd+Q / Cmd+Tab | ค้นหา / Alt+F4 / Alt+Tab |
| Ctrl+Tab | สลับแท็บ |
| Cmd+←/→, Cmd+↑/↓ | ต้นหรือท้ายบรรทัด, ต้นหรือท้ายเอกสาร |
| Option+←/→, Option+Backspace | กระโดดทีละคำ, ลบทีละคำ |
| Cmd+Shift+Z / 3 / 4 | Redo / จับภาพเต็มจอ / Snipping Tool |
| Cmd+[ / ] (Chrome, Edge) | ย้อนกลับ / ไปหน้าถัดไป |

ข้อจำกัด: การแมปปุ่มไม่ทำงานในโปรแกรมที่รันแบบ Administrator ยกเว้นตั้ง PowerToys ให้รันแบบ admin ด้วย และใน Windows ภาษาไทย ปุ่ม `` ` `` ยังเป็นปุ่มสลับภาษาตามค่าเริ่มต้น

### สลับช่องจอ BenQ RD280U ผ่าน DDC/CI

- จอตอบคำสั่ง DDC/CI (MCCS 2.2) ช่องสัญญาณ VCP `0x60`: `0x0F` = DisplayPort, `0x11` = HDMI (PC), **`0x13` = USB-C (Mac)** ยืนยันด้วยการทดสอบจริงเมื่อ 2026-10-09
- **`C:\Users\ptmc0\Scripts\MonitorInput\MonitorInput.exe <รหัส>`** โปรแกรม 6 KB ที่คอมไพล์จาก `MonitorInput.cs` ในโฟลเดอร์เดียวกันด้วย csc ของ .NET Framework ไม่เปิดหน้าต่าง บันทึกผลลง `MonitorInput.log`
- PowerToys ผูก **Cmd+Option+2** (= Ctrl+Alt+2 หลังแมปปุ่ม) ให้รัน `MonitorInput.exe 0x13`
- ฝั่ง Mac ต้องใช้ **BenQ Display Pilot 2** (หรือ BetterDisplay / `m1ddc set input 17`) เพื่อสลับกลับมา HDMI ระหว่างนี้ใช้ปุ่มที่จอไปก่อน
- RD280U มี KVM ในตัว แต่ไม่ได้ใช้ เพราะคีย์บอร์ดและเมาส์เป็นแบบไร้สาย

## Wake-on-LAN และรีโมต (2026-10-09)

- เครื่องนี้ถูกรีโมตจาก Mac mini (192.168.200.177) ผ่าน **SSH** (`sshd` Automatic, พอร์ต 22) และ **RDP** (TermService, พอร์ต 3389)
- **WoL ใช้งานได้:** ทดสอบเมื่อ 14:23:45 สั่ง Sleep (S3) แล้วตื่นเมื่อ 14:25:05 Event Power-Troubleshooter และ `powercfg /lastwake` ระบุแหล่งที่ปลุก = **Realtek PCIe GBE Family Controller** firmware resume ประมาณ 0.7 วินาที
- คำสั่งปลุกจาก Mac: `wakeonlan -i 192.168.200.255 1C:87:2C:60:24:3C` (ติดตั้งด้วย `brew install wakeonlan`)

| รายการ | ก่อน | หลัง |
|---|---|---|
| ไดรเวอร์แลน | Microsoft 9.1.412.2015 (2015-03-31) WoL = Unsupported | **Realtek 10.10.714.2016** (2016-07-14) จาก Windows Update (UpdateID `c2e4a0cb-fb39-44f7-bcc8-100c3de59d24`) match `SUBSYS_859E1043&REV_11 ;ASUS` โดยตรง • .cat ลงนามโดย Microsoft Windows Hardware Compatibility Publisher • .sys ลงนามโดย Realtek Semiconductor Corp. |
| WakeOnMagicPacket / WakeOnPattern | Unsupported / Unsupported | **Enabled / Disabled** |
| S5 WoL / EEE / Green Ethernet | ไม่มีให้ตั้ง | Enabled / Disabled / Disabled |
| wake_armed | คีย์บอร์ดและเมาส์ | คีย์บอร์ด เมาส์ และ **Realtek** |
| BIOS (Advanced → APM) | Power On By PCI-E/PCI = Disabled | **Enabled** ส่วน Deep S4 = Disabled (BIOS นี้ไม่มีเมนู ErP Ready) ค่าอื่นไม่ได้แตะ |

- ไดรเวอร์ตัวเดิมสำรองไว้ที่ `C:\DriverBackup\2026-10-09\` (rt640x64.inf/.sys + `baseline-before.txt` + `install.log`) ย้อนกลับด้วย Device Manager → Roll Back Driver
- ไม่ได้สร้าง restore point ใหม่ เพราะ Windows จำกัดวันละ 1 จุด และมีจุดจาก Windows Update เวลา 07:52 อยู่แล้ว
- ⚠️ หลังรีบูต `Get-NetAdapterPowerManagement` แจ้ง error 31 **กับทุกการ์ด** ส่วนที่มีปัญหาน่าจะเป็นตัวที่ Windows ใช้อ่านข้อมูลการ์ดผ่าน CIM (คาดการณ์) ไม่กระทบ WoL ให้ตรวจค่าจาก registry (`Get-NetAdapterAdvancedProperty`) และ `powercfg /devicequery wake_armed` แทน
- ⚠️ Event Tcpip 4199: IPv6 address ชนกับอุปกรณ์อื่นในวง (`B8-E8-56-39-2A-CA` ซึ่ง B8-E8-56 เป็น prefix ของ Apple และ `8A-B5-61-22-CA-4B`) น่าจะเกิดจาก DHCPv6 ของเราเตอร์ (คาดการณ์) IPv4 ไม่มีปัญหา

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
| `ACPI\PNP0A0A` (`\_SB.MBDA`) | ยังไม่มีไดรเวอร์ (error code 28) น่าจะเป็นอุปกรณ์ ACPI เฉพาะของ ASUS (คาดการณ์) ปล่อยไว้ได้ Windows Update มีไดรเวอร์ ASUS 1.0.1.0 (2014-03-17) ให้เป็นตัวเลือก ยังไม่ได้ติดตั้ง |
| **Realtek LAN** | **10.10.714.2016** จาก Windows Update (2026-10-09) แทนไดรเวอร์ Microsoft 9.1.412.2015 เพื่อใช้ WoL |
| บลูทูธ (CSR dongle) | Microsoft `bth.inf` ที่มากับ Windows |
| Logi Options+ | 2.9.984725 + Logi Plugin Service 6.4.2.3414 มีบริการ `OptionsPlusUpdaterService` (Automatic) |
| PowerToys | 0.101.2362 (user scope) เปิดพร้อมเครื่องผ่าน scheduled task `\PowerToys\Autorun for ptmc0` |
| ไดรเวอร์ทางเลือกใน Windows Update ที่ยังไม่ได้ติดตั้ง | Intel 9 Series chipset (2016), Intel HD 4600 20.19.15.4624, ASUS ACPI 1.0.1.0, LG monitor extension (ไม่ต้องลง) |

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
- [x] (10-09) เสียบ dongle บลูทูธ CSR จับคู่ Keychron K6 และตัวรับ Unifying ของ MX Master 3 แล้วลง Logi Options+
- [x] (10-09) ลง PowerToys และตั้ง Keyboard Manager ให้ปุ่มเหมือน Mac รวมถึงปุ่มลัดสลับจอ Cmd+Option+2 ส่วนโมดูลอื่นของ PowerToys ยังเปิดอยู่ตามค่าเริ่มต้น
- [x] (10-09) สร้าง `MonitorInput.exe` สำหรับสลับช่องจอผ่าน DDC/CI
- [x] (10-09) เปลี่ยนไดรเวอร์แลนเป็น Realtek, ตั้งค่า WoL (ปิด EEE และ Green Ethernet) และเปิด BIOS Power On By PCI-E/PCI
- โปรแกรมที่เปิดพร้อมเครื่อง: OneDrive, SecurityHealth, Logitech Download Assistant ×2 (มากับ Logi Options+ ปิดได้), PowerToys (ผ่าน scheduled task)
- Sleep: 15 นาทีเมื่อเสียบปลั๊ก (เปิด hybrid sleep, Hibernate after = Never) ปิดชั่วคราวระหว่างงานยาวแล้วตั้งกลับแล้ว
- ค่าที่ไม่ได้เปลี่ยน: power plan เป็น Balanced, Transparency เปิดอยู่

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
- [ ] **🟡 ตั้ง Display Pilot 2 บน Mac:** Cmd+Option+1 สลับจอไป HDMI และจับคู่ K6 (Fn+2) กับ MX Master 3 (ช่อง 2) กับ Mac
- [ ] **⚠️ ปิด qBittorrent ให้หมดก่อนไลฟ์** (คลิกขวาที่ tray → Exit) ไม่อย่างนั้นอาจแย่ง upload
- [ ] (ไม่บังคับ) ลดโปรแกรมเบื้องหลัง ได้ RAM คืนประมาณ 1 GB: ปิดโมดูล PowerToys ที่ไม่ได้ใช้ (Shortcut Guide, Command Palette, Color Picker, Peek, FancyZones, Awake, Always On Top, Quick Access), ปิด Logi Download Assistant ใน startup, ปิด M365 Copilot และ Widgets
- [ ] (ไม่บังคับ) ถ้าเครื่องตื่นเองบ่อย ให้ปิดสิทธิ์ปลุกเครื่องของเมาส์ (ตอนทดสอบ WoL รอบแรก เครื่องตื่นเพราะ USB)
- [ ] (ไม่บังคับ) ถ้าปุ่ม `` ` `` สลับภาษาโดยไม่ตั้งใจ ให้ปิด hotkey นี้ใน Windows
- [ ] ดูต้นเหตุ IPv6 address ชนกัน (Tcpip 4199) ที่เราเตอร์

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

# Wake-on-LAN: ค่าในไดรเวอร์ อุปกรณ์ที่ปลุกเครื่องได้ และตัวที่ปลุกครั้งล่าสุด
Get-NetAdapterAdvancedProperty -Name 'อีเทอร์เน็ต' -RegistryKeyword '*WakeOnMagicPacket','*WakeOnPattern','S5WakeOnLan','EEE','EnableGreenEthernet'
powercfg /devicequery wake_armed
powercfg /lastwake

# สลับจอ BenQ ด้วยคำสั่ง (0x11 = HDMI/PC, 0x13 = USB-C/Mac)
& "$env:USERPROFILE\Scripts\MonitorInput\MonitorInput.exe" 0x13
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

### 2026-10-09

| เวลา | เหตุการณ์ |
|---|---|
| ~10:30 | ประเมินการ์ด TP-Link Archer T4E (Wi-Fi อย่างเดียว ไม่มีบลูทูธ) และการ์ด USB-C PCE3U1C-R31 จากรูป **ยังไม่ได้ใส่ทั้งคู่** |
| 10:48 | เสียบ dongle บลูทูธ CSR (BT 4.0) |
| 10:51 | เสียบตัวรับ Unifying ของ MX Master 3 |
| 10:56 | ลง Logi Options+ 2.9 |
| ~11:00 | จับคู่ Keychron K6 ผ่านบลูทูธ และถอดตัวรับ AJAZZ กับ Logitech C52F ออก |
| 11:12–11:24 | ลง PowerToys 0.101 แล้วตั้งปุ่มแบบ Mac และ Shift+Caps Lock |
| 12:27–12:32 | สร้าง MonitorInput.exe และผูกปุ่ม Cmd+Option+2 ทดสอบสลับจอไป USB-C ผ่าน 4 ครั้ง |
| ~12:40 | สำรวจโปรแกรมเบื้องหลัง: RAM ว่าง 24.4/31.9 GB พบ qBittorrent เปิดอยู่ และพบโปรแกรมที่ไม่จำเป็น (ยังไม่ได้ปิด) |
| ~13:50–14:05 | งาน WoL: สำรองไดรเวอร์เดิม ลงไดรเวอร์ Realtek จาก Windows Update (ติดตั้งเสร็จ 14:02 ไม่ต้องรีบูต) แล้วตั้งค่า WoL |
| 14:11–14:18 | ตั้ง BIOS Power On By PCI-E/PCI = Enabled แล้วรีบูต ตรวจหลังบูต: ค่าทั้งหมดอยู่ครบ sshd/RDP ปกติ |
| 14:23–14:25 | ทดสอบ WoL: สั่ง Sleep แล้วปลุกด้วย magic packet จาก Mac **ผ่าน** |

## Related
- [[entities/macmini-m4-2024]] — เครื่องหลักอีกเครื่องในห้องสติ
- [[entities/tplink-tl-sg1024d-switch]] — สวิตช์เครือข่ายที่ใช้ร่วมกันในห้อง (ยังไม่ยืนยันว่าเครื่องนี้ต่อผ่านสวิตช์ตัวนี้)
