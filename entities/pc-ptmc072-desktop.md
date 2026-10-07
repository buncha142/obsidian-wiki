---
title: "PC-PTMC072 (ASUS Z97-K / i7-4790)"
tags: [it-equipment, hardware, windows, maintenance-log]
category: entities
created: 2026-10-06
updated: 2026-10-06
sources: [user-provided]
summary: "Desktop ประกอบเอง เมนบอร์ด ASUS Z97-K + i7-4790 RAM 24 GB NVMe Kingston NV2 500 GB ลง Windows 11 Pro ใหม่ 2026-10-06 ตั้งใช้งานที่ห้องสติ; บันทึกการแก้ปัญหาบูต (ย้าย EFI จาก USB มา NV2) สุขภาพดิสก์ ไดรเวอร์ ค่า performance ตั้งต้น และงานค้าง"
---

# PC-PTMC072

## ที่ตั้ง/การใช้งาน
- **ตั้งใช้งานที่:** ห้องสติ (office เดียวกับ [[entities/macmini-m4-2024|Mac mini M4]])

Desktop ประกอบเอง บนเมนบอร์ด ASUS Z97-K ลง Windows 11 Pro ใหม่เมื่อ 2026-10-06 วันเดียวกันนั้นพบและแก้ปัญหาบูต ตรวจสุขภาพเครื่อง และเก็บค่า performance ตั้งต้นไว้

> [!summary] สถานะล่าสุด (2026-10-06)
> - ฮาร์ดแวร์แข็งแรง: ไม่มี error ของดิสก์ ไม่มี WHEA/BugCheck และ RAM ผ่านการทดสอบ
> - **แก้ปัญหาบูตแล้ว:** EFI bootloader เคยอยู่บนแฟลชไดรฟ์ ตอนนี้ย้ายมาอยู่บน NV2 แล้ว
> - คอขวดของเครื่อง: ช่อง M.2 เป็น PCIe 2.0 x2 และการ์ดจอเป็นแบบออนบอร์ด

## สเปกเครื่อง

| หมวด | รายละเอียด |
|---|---|
| Hostname | `PC-PTMC072` |
| เมนบอร์ด | ASUS Z97-K (chipset Intel Z97 / 9 Series), BIOS 2902, UEFI |
| CPU | Intel Core i7-4790 @ 3.60 GHz (Haswell, Gen 4), 4C/8T, L2 1 MB, L3 8 MB |
| RAM | 24 GB DDR3-1600 1.5 V: Kingston HyperX `KHX1600C10D3/8G` 8 GB × 3 ช่อง (A1, B1, B2) **ช่อง A2 ว่าง** บอร์ดรองรับสูงสุด 32 GB |
| การ์ดจอ | Intel HD Graphics 4600 (ออนบอร์ด) driver 20.19.15.4531 (2016-09-29) |
| จอ | 1920×1080 @ 60 Hz |
| SSD | Kingston NV2 `SNV2S500G` 500 GB NVMe, firmware `SBN00100`, S/N `0026_B778_5C65_D8B5` |
| ลิงก์ของ SSD | **PCIe Gen2 x2** (ตัวไดรฟ์รองรับ Gen4 x4) ต่อผ่าน chipset root port 1 (`8086:8C90`) |
| ไดรเวอร์ NVMe | Microsoft `stornvme` 10.0.26100.9278 |
| เครือข่าย | Realtek PCIe GbE 1 Gbps (ต่อสาย) |
| USB 3.0 | Intel xHCI และ Renesas USB 3.0 |
| PSU | Cougar STC750 750 W, +12V rail เดียว 60 A / 720 W, 80 PLUS (ระดับพื้นฐาน), TÜV Rheinland, มีสาย PCIe (6+2 pin) ว่างอยู่สองหัว ดูหัวข้อ "ผลตรวจ PSU" |
| OS | Windows 11 Pro 64-bit build 26300 (Retail, Licensed) ลงเมื่อ 2026-10-06 13:49 |
| BIOS | Secure Boot = Other OS, VT-x **ปิดอยู่** ใน NVRAM ยังมีรายการ legacy "Hard Drive" ซึ่งน่าจะแปลว่า CSM เปิดอยู่ (คาดการณ์) |

> [!warning] ข้อจำกัด
> i7-4790 ไม่อยู่ในรายชื่อ CPU ที่ Windows 11 รองรับ ตอนติดตั้งจึงข้ามการตรวจ TPM/CPU/Secure Boot ด้วย `autounattend.xml` อัปเดตใหญ่ในอนาคตอาจมีปัญหา

## โครงสร้างดิสก์ (Disk 0: NV2, GPT)

| Partition | ประเภท | ขนาด | หมายเหตุ |
|---|---|---|---|
| P1 | MSR | 16 MB | |
| P2 | `C:` NTFS | 475,729 MB | ไดรฟ์ Windows |
| P3 | **EFI System** FAT32 (label `SYSTEM`) | 260 MB | สร้างเมื่อ 2026-10-06 |
| P4 | Recovery (WinRE) | 893 MB | |

แฟลชไดรฟ์ Kingston DataTraveler 3.0 32 GB (label `WIN10`) เป็นตัวติดตั้ง Windows ที่สร้างบน macOS **ตอนนี้ไม่จำเป็นต่อการบูตแล้ว**

## ประวัติปัญหาและการแก้ไข

### อาการก่อนแก้
1. ตอนแรก Windows Setup มองไม่เห็น NV2 หลังถอดเสียบใหม่จึงเห็น
2. เจอ `0xc000000e` ("A required device isn't connected") สองครั้ง รวมถึงหลังลง Windows ใหม่ทั้งเครื่อง
3. เคยค้างที่โลโก้ ASUS โดยไม่มีจุดหมุน
4. สมมติฐานตอนแรกคือ NV2 หลุดการเชื่อมต่อเป็นครั้งคราว

### สาเหตุที่พบ
- **ข้อเท็จจริง:** NV2 ไม่มี EFI System Partition เลย ESP มีอยู่ที่เดียวคือบนแฟลชไดรฟ์ ค่า `FirmwareBootDevice` ชี้ไปที่ partition บน USB และ NVRAM Boot0000 "Windows Boot Manager" ก็ชี้ไปที่ USB
- **คาดการณ์:** แฟลชไดรฟ์ถูกมองเป็นดิสก์แบบ Fixed และมี ESP ที่ macOS สร้างไว้อยู่แล้ว Windows Setup จึงนำ ESP นั้นมาใช้ซ้ำ อาการ `0xc000000e` เข้ากับสาเหตุนี้มากกว่าสมมติฐานว่า NV2 หลุด

### ขั้นตอนแก้ (2026-10-06)
1. ย่อ `C:` ลง 300 MB
2. ใช้ `diskpart` สร้าง partition efi 260 MB และฟอร์แมต FAT32
3. รัน `bcdboot C:\Windows /s S: /f UEFI` (คำสั่งนี้ไม่ได้อัปเดต NVRAM ให้)
4. ถอด USB แล้วบูตผ่าน F8 → เลือก Windows Boot Manager (KINGSTON) หนึ่งครั้ง bootmgr จึงเขียน NVRAM ใหม่ให้ชี้ไปที่ NV2 เอง
5. `reagentc /enable` ล้มเหลว (error 2) เพราะยังอ้าง BCD ID เก่าบน USB แก้ด้วย `bcdedit /deletevalue {current} recoverysequence` แล้วรัน `reagentc /enable` ใหม่จนสำเร็จ
6. ทดสอบแล้วว่าบูตได้เองโดยไม่ต้องเสียบ USB ทั้งตอน Shut down (Fast Startup) และตอน Restart

> [!note] Kernel-Power 41 ครั้งเดียว
> เกิดตอนบูตเวลา 20:31 หลังเปลี่ยนเส้นทางบูต ค่า BugcheckCode = 0, PowerButtonTimestamp = 0 และฝั่ง NV2 ไม่นับเป็น unsafe shutdown หลังจากนั้นปิดเครื่องอีก 2 รอบก็ปกติ จึง**น่าจะเกิดครั้งเดียวจากการเปลี่ยนเส้นทางบูต** (คาดการณ์)

## สุขภาพ NV2: ค่า SMART ตั้งต้น

อ่านจาก NVMe SMART log (page 02h) เมื่อ 2026-10-06 ประมาณ 21:45

| ค่า | ผล |
|---|---|
| Critical Warning | 0x00 |
| Available Spare / Percentage Used | 100% / 0% |
| Media/Integrity Errors | 0 |
| Error Log Entries | 0 |
| Power Cycles | 46 |
| **Unsafe Shutdowns** | **22** |
| Power On Hours | 32 (อ่านเมื่อ 19:xx) |
| Data Written | 301 GB (อ่านเมื่อ 19:xx) |
| อุณหภูมิ | 31–36 °C, Warning/Critical temp time = 0 นาที |

> [!tip] วิธีเฝ้าดู
> ถ้าปิดเครื่องตามปกติแล้ว **Unsafe Shutdowns เพิ่มจาก 22** หรือ Error Log Entries ไม่เป็น 0 หรือ Event Log มี `stornvme` ID 11/129 หรือ `disk` ID 153 แสดงว่า NV2 อาจไม่เสถียรจริง
> ตัวเลข unsafe 22 ครั้งที่มีอยู่แล้ว น่าจะมาจากการกดปิดเครื่องตอนค้างหรือบูตไม่ผ่านก่อนการแก้ไข (คาดการณ์)

## ไดรเวอร์

| รายการ | สถานะ |
|---|---|
| Intel 9 Series chipset INF | ติดตั้งจากแพ็กเกจของ ASUS Z97-K (`Intel_Chipset_Win7-8-81-10_V100160_10117.zip`, Win10 SetupChipset 10.1.1.7) โดยใช้ `pnputil` ติดตั้งเฉพาะ `lynxpoint-hrefreshSystem.inf` (ใน driver store คือ `oem6.inf`) |
| อุปกรณ์ที่ได้ชื่อใหม่ | SMBus `8CA2` (เดิม error code 28) และ PCIe Root Port 1/3/8 (`8C90` ต่อ NV2, `8C94` ต่อแลน, `8C9E` ต่อ USB 3.0 Renesas) |
| Intel Chipset INF รุ่นล่าสุด 10.1.20658.8883 | ⚠️ บนเครื่องนี้รันไม่ได้ (exit `0xE0000001`) ให้ใช้แพ็กเกจของ ASUS แทน |
| `ACPI\PNP0A0A` (`\_SB.MBDA`) | ยังไม่มีไดรเวอร์ น่าจะเป็นอุปกรณ์ ACPI เฉพาะของ ASUS (คาดการณ์) ปล่อยไว้ได้ |

หน้าซัพพอร์ตของ ASUS Z97-K ค้นหาจากเว็บ ASUS ไม่เจอ ต้องเข้าลิงก์ตรง: https://www.asus.com/supportonly/z97-k/helpdesk_download/

## ค่า performance ตั้งต้น (2026-10-06 หลังแก้ระบบ)

| หมวด | ค่า |
|---|---|
| CPU ขณะใช้งานเบา | 4.6% (สูงสุด 8.5%), ความเร็ว 3,601/3,601 MHz ไม่มี throttling |
| RAM | commit 5.8 จาก 24 GB, pagefile ใช้ 0 MB |
| `winsat` disk seq read (C:) | **797 MB/s** ซึ่งเป็นเพดานของ PCIe 2.0 x2 |
| `winsat mem` | **21,144 MB/s** แปลว่า dual channel ทำงาน |
| `winsat` CPU AES-256 / LZW | 3,784 / 471 MB/s |
| พื้นที่ว่าง C: | 418.8 / 464.6 GB |

### เวลาบูต (Diagnostics-Performance Event 100)

| เวลาบูต | รวม | Main path | Post-boot | หมายเหตุ |
|---|---|---|---|---|
| 13:50 | 106.7 s | 28.3 s | 78.4 s | บูตแรกหลังติดตั้ง |
| 19:07 | 20.4 s | 5.1 s | 15.3 s | |
| 20:32 | 52.6 s | 14.6 s | 38.0 s | บูตแรกจาก NV2 |
| 21:42 | 39.1 s | 8.5 s | 30.6 s | Edge +18.6 s, Defender +8.0 s (Event 101) |

## การตั้งค่าที่เปลี่ยนไปแล้ว

- [x] ย้าย ESP และ bootloader มาไว้บน NV2 แล้วลงทะเบียน WinRE ใหม่
- [x] ตรวจ RAM ด้วย Windows Memory Diagnostic: **ไม่พบ error** (Event 1101/1201)
- [x] ติดตั้ง Intel 9 Series chipset INF
- [x] ปิด Edge AutoLaunch (StartupApproved = Disabled) ซึ่งทำให้ Edge ลบรายการ Run ของตัวเองออกไปด้วย
- [x] ปิด Edge Startup boost และการรันเบื้องหลังหลังปิด Edge
- [x] Defender Quick Scan ครั้งแรก: ไม่พบภัยคุกคาม (สแกน 231 s)
- โปรแกรมที่ยังเปิดพร้อมเครื่อง: OneDrive, SecurityHealth
- ค่าที่ไม่ได้เปลี่ยน: Fast Startup เปิดอยู่, power plan เป็น Balanced, Transparency เปิดอยู่

## ผลตรวจ PSU: Cougar STC750 ✅ ผ่าน (ตรวจจากฉลาก)

| จากฉลาก | ค่า | เทียบกับที่ต้องใช้ |
|---|---|---|
| กำลังรวม | 750 W | ทั้งระบบหลังใส่การ์ดจอแยกน่าจะกินไฟสูงสุดประมาณ 250 W คิดเป็นภาระแค่ประมาณ 1 ใน 3 ของ PSU (คาดการณ์) |
| +12V | 60 A / 720 W (rail เดียว) | GTX 1650 Super ใช้ประมาณ 100 W ส่วน i7-4790 ใช้ประมาณ 84 W |
| มาตรฐาน | 80 PLUS (ระดับพื้นฐาน), TÜV Rheinland | |
| หัว PCIe | สายติดป้าย "PCI-E" สองหัว (6+2 pin) ที่มุมขวาล่างในรูป ยังไม่ได้ใช้ | ใช้ได้ทันที |

สรุป: PSU รองรับการ์ดจอแยกได้โดยไม่ต้องเปลี่ยน ปลดข้อกังวลเรื่องเช็ก PSU ในงานค้างข้อซื้อการ์ดจอ

## งานค้างและคำแนะนำ

- [ ] วัดเวลาบูตหลังปิด Edge Startup boost เทียบกับ post-boot 30.6 s เดิม (คาดว่าจะลดลงประมาณ 15–20 s)
- [ ] เช็ก HDD WD 2 ลูก ซึ่งตอนตรวจระบบมองไม่เห็นเลย (ถอดออกอยู่ หรือมีปัญหาสาย SATA/BIOS?)
- [ ] (ถ้าดูวิดีโอ 4K หรือเล่นเกม) ซื้อการ์ดจอแยก เช่น GTX 1650 หรือ RX 6400 มือสอง ~฿2,500–4,500 (PSU ผ่านแล้ว ดูหัวข้อ "ผลตรวจ PSU") เหตุผลคือ HD 4600 ถอดรหัส VP9/AV1 ด้วยฮาร์ดแวร์ไม่ได้
  - 2026-10-07: มี GTX 1060 6GB **ใช้ได้** (~120 W ใช้ไฟ 6-pin หรือ 8-pin หนึ่งหัว PSU มีให้) ใส่ช่อง PCIe 3.0 x16 ช่องบน ถอดรหัส VP9 ได้แต่ AV1 ไม่ได้ ไดรเวอร์ Pascal ไม่มี Game Ready รุ่นใหม่แล้ว เหลือแค่ security update ⚠️ จะชนกับแผนการ์ดแปลง M.2 เพราะช่อง x16 ช่องที่สองน่าจะเป็น PCIe 2.0 x2 (คาดการณ์ ต้องเช็กคู่มือ)
  - 2026-10-07: ตัวที่มีคนเสนอขายคือ ZOTAC GTX 1060 6GB AMP! Edition มือสอง กล่องครบ ราคา ฿2,500 ประเมินว่าราคาค่อนข้างสูง ควรต่อลงเหลือ ~฿1,800–2,200 (คาดการณ์จากราคาตลาดมือสอง) และต้องทดสอบก่อนจ่ายเงิน
  - 2026-10-07: **มีเหตุผลที่ควรซื้อแล้ว** เพราะจะใช้เครื่องนี้ไลฟ์สดผ่าน Facebook และ TikTok ด้วย OBS ใช้ตัวเข้ารหัส NVENC ของ 1060 แทน CPU ได้ ถ้าไลฟ์สองแพลตฟอร์มพร้อมกัน ต้องมีเน็ตอัปโหลดอย่างน้อย ~15–20 Mbps และต่อสายแลน
  - 2026-10-07: ผู้ขายเสนอขายแรม `HX316C10FR/8` คู่กับการ์ด GTX 1060 ในราคารวม **฿2,900** ประเมินว่าราคาตลาดรวมอยู่ที่ ~฿2,100–2,800 จึง**รับได้ แพงกว่าตลาดเล็กน้อย** ควรต่อเหลือ ~฿2,500–2,600 แต่ถ้าทดสอบผ่าน ราคา 2,900 ก็ยังสมเหตุสมผล
- [ ] (ถ้าคัดลอกไฟล์ใหญ่บ่อย) ย้าย NV2 ไปการ์ดแปลง M.2 → PCIe x16 ~฿200–400 จะได้ PCIe 3.0 x4 ต้องทดสอบบูตใหม่หลังย้าย
- [ ] (ไม่เร่งด่วน) เพิ่ม RAM `KHX1600C10D3/8G` ที่ช่อง A2 ให้ครบ 32 GB ~฿250–500
  - 2026-10-07: มีแรม HyperX FURY `HX316C10FR/8` (DDR3-1600 CL10 1.5V 8 GB) **ใช้ได้** สเปกตรงกับแรมเดิม ใส่ที่ช่อง A2 แล้วให้ตรวจว่าเห็น 32 GB, `winsat mem` ยังได้ ~21 GB/s และรัน Memory Diagnostic อีกรอบ
- [ ] (ถ้าจะใช้ WSL2, Docker หรือ VM) เปิด VT-x ใน BIOS

## คำสั่งที่ใช้บ่อย

ทุกคำสั่งในส่วนนี้ต้องรันใน PowerShell แบบ Administrator

```powershell
# เช็กว่าบูตจากดิสก์ไหน
(Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control').FirmwareBootDevice
Get-Disk | Select Number, FriendlyName, BootFromDisk, IsSystem, IsBoot

# BCD และลำดับบูตของ firmware
bcdedit /enum firmware
reagentc /info

# Event ของดิสก์ ไฟดับ และฮาร์ดแวร์ error ย้อนหลัง 7 วัน
Get-WinEvent -FilterHashtable @{LogName='System'; StartTime=(Get-Date).AddDays(-7);
  ProviderName='stornvme','disk','Microsoft-Windows-Kernel-Power','Microsoft-Windows-WHEA-Logger'} |
  ? { $_.Level -le 3 } | Select TimeCreated, ProviderName, Id, Message

# ตั้งเวลาตรวจ RAM ตอนบูตครั้งหน้า
bcdedit /bootsequence '{memdiag}'
```

> [!example]- สคริปต์อ่าน NVMe SMART log (ไม่ต้องลงโปรแกรม)
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
> $l = [Nvme]::SmartLog(0)
> "Power Cycles=$([BitConverter]::ToUInt64($l,112)) Unsafe=$([BitConverter]::ToUInt64($l,144)) MediaErr=$([BitConverter]::ToUInt64($l,160)) ErrLog=$([BitConverter]::ToUInt64($l,176)) Temp=$([BitConverter]::ToUInt16($l,1)-273)C"
> ```

## Timeline 2026-10-06

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

## Related
- [[entities/macmini-m4-2024]] — เครื่องหลักอีกเครื่องในห้องสติ
- [[entities/tplink-tl-sg1024d-switch]] — สวิตช์เครือข่ายที่ใช้ร่วมกันในห้อง (ยังไม่ยืนยันว่าเครื่องนี้ต่อผ่านสวิตช์ตัวนี้)
