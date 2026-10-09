---
title: "Mac mini M4 (2024)"
tags: [it-equipment, hardware]
category: entities
created: 2026-06-19
updated: 2026-10-09
sources: [user-provided]
summary: "Mac mini รุ่น 2024 ชิป Apple M4 RAM 24GB SSD 500GB เครื่องหลักที่โต๊ะทำงาน office ห้องสติ ต่อจอคู่ BenQ RD280U + LG Full HD; มีบันทึกรายการเปิดอัตโนมัติ (Login Items/LaunchAgents/LaunchDaemons) ผลตรวจสมรรถภาพเครื่อง การตั้งค่าอัดหน้าจอพร้อมเสียงด้วย OBS Studio และปุ่มลัด Cmd+Option+1 สลับจอ BenQ ไป HDMI (PC-PTMC072) ด้วย m1ddc + skhd"
---

# Mac mini M4 (2024)

## ข้อมูลทั่วไป
- **ประเภท:** เดสก์ท็อป (Mac mini)
- **ยี่ห้อ/รุ่น:** Apple Mac mini, 2024
- **ปีที่ซื้อ:** 2024
- **ราคา/ที่มา (ถ้าจำได้):** (ยังไม่ระบุ)

## สเปกหลัก
- **ชิป/CPU:** Apple M4
- **RAM:** 24 GB
- **Storage:** SSD 500 GB (APPLE SSD AP0512Z)
- **OS / Firmware version:** macOS Tahoe 26.6.2 (build 25G83) — ตรวจสอบล่าสุด 2026-09-04
- **Model identifier:** Mac16,10
- **Serial number:** WGFQJ4M5WH
- **Limited Warranty:** หมดอายุ 7 ธันวาคม 2569 (พ.ศ.) — ครอบคลุม Hardware Service และ Chat/Phone Support
- **จอที่ต่อใช้งาน:**
  - [[entities/benq-rd280u-monitor|BenQ RD280U]] — 28.2 นิ้ว (3840 × 2560) ต่อทาง **USB-C** (ใช้จอร่วมกับ [[entities/pc-ptmc072-desktop|PC-PTMC072]] ที่ต่อทาง HDMI)
  - LG FULL HD — 24 นิ้ว (1080 × 1920)

## การใช้งานจริง
- **ใช้ทำอะไรเป็นหลัก:** dev โปรเจค Laravel/TALL Stack (admin.ptmc072), งานธุรการ/เอกสาร, ประชุมออนไลน์และสื่อสาร
- **ใช้คู่กับอุปกรณ์/ซอฟต์แวร์อะไร:** VS Code + [[entities/claude|Claude]] Code, Google Workspace (Docs/Sheets/Drive), โปรแกรมบัญชี/เอกสารราชการ; สำรองไฟด้วย [[entities/zircon-pi-ups-1000va|ZIRCON Pi UPS 1000VA]]; พิมพ์/สแกนผ่าน [[entities/brother-dcp-t430w-printer|Brother DCP-T430W]] ด้วย AirPrint (ไม่ลง driver ของผู้ผลิต)
- **ตั้งอยู่ที่ไหน:** โต๊ะทำงาน office "ห้องสติ"

## การเชื่อมต่อเครือข่าย (ตรวจ 2026-10-08)
เครื่องต่อ **2 วงเครือข่ายพร้อมกัน**:

| ช่อง | วงเครือข่าย | IP | ต่อผ่าน |
|---|---|---|---|
| en0 (สาย LAN) — ช่องหลัก | วง A · LAN หลัก `192.168.200.0/24` | `192.168.200.177` | สวิตช์ **TP-Link TL-SG1024D** (24 พอร์ต gigabit แบบ unmanaged ไม่มี IP) ในตู้ rack → เราเตอร์ **AIS Fibre** (ตัวเครื่อง Huawei) `192.168.200.75` |
| en1 (Wi-Fi) | วง B · Wi-Fi ของ Deco `192.168.68.0/24` | `192.168.68.109` | TP-Link Deco mesh ที่ตั้งเป็นโหมด Router ซ้อนอยู่หลังวง A (Double NAT) |

- พิมพ์/สแกนกับ [[entities/brother-dcp-t430w-printer|Brother DCP-T430W]] ได้เพราะเครื่องพิมพ์อยู่วง B และ Mac mini ต่อ Wi-Fi วงนั้นอยู่ — **ถ้าปิด Wi-Fi จะใช้เครื่องพิมพ์นี้ไม่ได้**
- ในตู้ rack เดียวกันมีเครื่องบันทึกกล้องวงจรปิด (DVR) ต่อ LAN อยู่ด้วย
- แผนผังเต็ม + รายชื่ออุปกรณ์/IP + ผลตรวจความปลอดภัย: `PARA/02_Areas/ศูนย์ปฏิบัติธรรมพัทลุง/IT-Network/`

## ปัญหา/ข้อจำกัดที่เจอ
- **2026-09-17 — Microsoft Defender ทำเครื่องช้า:** หลังติดตั้ง Microsoft Defender (พบว่าลงเมื่อ 2026-09-15) ตรวจพบว่า `wdavdaemon_unprivileged` (real-time protection) กิน CPU 20–112% ต่อเนื่อง และ RAM ว่างลดจาก 87% เหลือ ~245 MB จาก 24 GB — สาเหตุหลักของอาการเครื่องช้าที่รู้สึกได้ **แก้แล้ว: ถอดถอน Defender ออกทั้งหมด** (ดูหัวข้อ "ถอดถอน Microsoft Defender" ด้านล่าง)

## การตั้งค่าระบบที่ทำไว้

### จัดการรายการเปิดอัตโนมัติ (2026-09-04)
- **uTorrent Web:** ปิดการเปิดอัตโนมัติตอน login — ลบออกจาก Login Items ผ่าน System Events ต้องเปิดเองเมื่อต้องการใช้งานเท่านั้น
- **ลบ LaunchDaemons ที่ซ้ำซ้อน** ใน `/Library/LaunchDaemons/` (ตรวจแล้วว่าไม่ได้ถูกโหลดใน launchd เลย ไม่กระทบการทำงาน):
  - `homebrew.mxcl.nginx.plist`, `homebrew.mxcl.php@8.3.plist`, `homebrew.mxcl.php@8.4.plist`, `homebrew.mxcl.dnsmasq.plist` — เศษเหลือจากตอนใช้ `brew services` ปัจจุบัน **Laravel Herd** (`de.beyondco.herd.helper`) จัดการ nginx/php/dnsmasq เองแล้ว
  - `jp.co.canon.MasterInstaller.plist` — ไม่ได้ต่อเครื่องพิมพ์ Canon แล้ว

### รายการที่ยังเปิดอัตโนมัติอยู่ (ตรวจล่าสุด 2026-09-15)
| ระดับ | รายการ |
|---|---|
| Login Items | Google Drive, **Herd** |
| User LaunchAgents | Google Updater (keystone ×3), MySQL, PostgreSQL@16 (Homebrew) |
| System LaunchAgents | Google keystone, Logitech Options+/RightSight, OneDrive updater, Microsoft AutoUpdate/SyncReporter, Zoom updater |
| System LaunchDaemons | Docker (socket/vmnetd), Google Updater, Logitech updater, OneDrive/Microsoft/Office helpers, **Laravel Herd helper**, **NetBird VPN**, Zoom daemon |

> เปลี่ยนแปลงจากครั้งก่อน (2026-09-04): Login Items มี **Herd** และ **Microsoft 365 Copilot** เพิ่มเข้ามา ส่วนระดับอื่นไม่เปลี่ยน

### ลดรายการ Login Items (2026-09-15)
- ลบออกจาก Login Items ผ่าน System Events: **Microsoft 365 Copilot**, **GeminiAppLauncher**, **FigmaAgent**, **Stream Dock AJAZZ** — ต้องเปิดเองเมื่อจะใช้งาน (Stream Dock ต้องเปิดแอปก่อน ปุ่มถึงจะทำงาน)
- เก็บไว้: **Google Drive** (ใช้ sync เอกสาร) และ **Herd** (ใช้ dev Laravel)
- ถ้าแอปใดกลับมาเปิดอัตโนมัติอีก ให้ปิดตัวเลือก "Launch at login" ในหน้าตั้งค่าของแอปนั้น

> หมายเหตุ: MySQL + PostgreSQL@16 รันพื้นหลังตลอด ถ้าไม่ได้ dev ทุกวันสามารถหยุดด้วย `brew services stop mysql` / `brew services stop postgresql@16` แล้วสั่ง start เมื่อต้องใช้

### ถอดถอน Microsoft Defender (2026-09-17)
- **สาเหตุ:** ติดตั้งเมื่อ 2026-09-15 แบบ manual (ไม่ได้ผ่าน MDM/enrollment ใดๆ — ตรวจแล้วว่า `profiles status -type enrollment` = No) เป็นชุด Defender for Endpoint เต็มรูปแบบ (รวม DLP component) ทำให้ real-time protection (`wdavdaemon_unprivileged`) กิน CPU 20–112% ต่อเนื่องและ RAM แทบเต็ม
- **วิธีถอด:** `sudo rm -rf "/Applications/Microsoft Defender.app"` → ไป trigger LaunchDaemon `com.microsoft.fresno.uninstall` ที่เฝ้า path นี้อยู่ ให้รัน official uninstall script อัตโนมัติ (ถอด daemon, DLP, auth rules, user data, settings directory ครบ — ดู log ที่ `/Library/Logs/Microsoft/mdatp/uninstall.log`)
- **ข้อควรระวัง:** system extension (`com.microsoft.wdav.epsext`) ไม่หลุดอัตโนมัติเพราะตอน script รันถึงขั้นตอนถอด extension ตัวแอปถูกลบไปก่อนแล้ว ต้องเคลียร์เพิ่มด้วย `sudo systemextensionsctl uninstall UBF8T346G9 com.microsoft.wdav.epsext` และ/หรือปิดผ่าน System Settings → General → Login Items & Extensions → Endpoint Security Extensions แล้ว restart เครื่อง

### ตั้งค่าอัดหน้าจอพร้อมเสียง — OBS Studio (2026-09-23)

- **ปัญหาเดิม:** เครื่องมือ built-in `⌘ + Shift + 5` อัดได้แค่ภาพหน้าจอ + เสียงไมค์ แต่**ไม่ได้เสียงระบบ** (system audio จาก YouTube/Zoom/วิดีโอในเครื่อง)
- **วิธีแก้:** ติดตั้ง **OBS Studio 32.2.2** ผ่าน `brew install --cask obs` — ตั้งแต่ macOS 13 เป็นต้นมา OBS ดึงเสียงระบบได้ตรงผ่าน **ScreenCaptureKit** จึง**ไม่ต้องลง BlackHole/Loopback** เป็น virtual audio driver อีกต่อไป

**การตั้งค่าที่ใช้ (ทำครั้งเดียว):**

| ส่วน | ค่าที่ตั้ง | ได้อะไร |
|---|---|---|
| Sources → `macOS Screen Capture` | เลือกจอ + ติ๊ก **Capture Audio** | ภาพหน้าจอ + **เสียงระบบ** |
| Sources → `Audio Input Capture` | เลือก **BOYA CM40** (ไมค์ USB) | เสียงพูดบรรยาย |
| Settings → Output → Recording Format | **MP4** | ไฟล์เปิดได้ทุกที่ |
| Settings → Output → Encoder | **Apple VT H264 Hardware** | ใช้ hardware encoder ของ M4 ไม่กิน CPU |

**ข้อควรระวัง:**
- รันครั้งแรกต้องอนุญาต Screen Recording + Microphone ที่ System Settings → Privacy & Security แล้ว **ปิด-เปิด OBS ใหม่** สิทธิ์ถึงจะมีผล
- อัดพร้อมเสียงระบบ **ต้องใส่หูฟัง** ไม่งั้นไมค์จะจับเสียงลำโพงซ้ำเป็น echo
- จอ [[entities/benq-rd280u-monitor|BenQ RD280U]] ความละเอียด 3840 × 2560 อัด 4K กินพื้นที่ ~1–2 GB ต่อนาที — ควรอัดเฉพาะบางส่วนของจอ หรือย้ายไฟล์ออกหลังอัดเสร็จ

**ทางเลือกสำรอง (ไม่ต้องเปิด OBS):**
- งานสั้นที่ไม่ต้องใช้เสียงระบบ → `⌘ + Shift + 5` → Options → Microphone: BOYA CM40
- รีบมากและไม่เน้นคุณภาพ → Zoom (New Meeting คนเดียว → Share Screen → ติ๊ก **Share Sound** → Record)

### ปุ่มลัดสลับจอ BenQ ไป PC — m1ddc + skhd (2026-10-09) ✅ ทดสอบผ่าน

จอ [[entities/benq-rd280u-monitor|BenQ RD280U]] ใช้ร่วม 2 เครื่อง: Mac mini ต่อ **USB-C** · [[entities/pc-ptmc072-desktop|PC-PTMC072]] ต่อ **HDMI**

| ส่วน | ค่าที่ตั้ง |
|---|---|
| ปุ่มลัด | **Cmd + Option + 1** → สลับจอไป HDMI (PC) |
| เครื่องมือสั่งจอ | `m1ddc` (`brew install m1ddc`) สั่งผ่าน DDC ทางสาย USB-C |
| สคริปต์ | `~/bin/benq-input.sh hdmi\|usbc\|dp` (รหัส HDMI 1 = 17, USB-C = 27, DP = 15) — หาเลขจอจากชื่อรุ่น ไม่พังถ้าลำดับจอเปลี่ยน |
| ตัวรับปุ่มลัด | `skhd` (`brew install koekeishiya/formulae/skhd`) config `~/.config/skhd/skhdrc` รันเป็น service เปิดเองตอน login |
| สิทธิ์ | System Settings → Privacy & Security → **Accessibility** → เพิ่ม `/opt/homebrew/Cellar/skhd/0.3.9/bin/skhd` |

**ข้อควรรู้:**
- **สลับกลับมา Mac ต้องทำจากฝั่ง PC หรือปุ่มบนจอ** (Input → USB-C) เพราะเมื่อจออยู่ช่อง HDMI แล้ว Mac สั่งผ่าน DDC ไม่ได้
- `m1ddc` **อ่านค่าช่องปัจจุบันไม่ได้** (ค่า `get input` ที่ได้มั่ว 0/17/19) — ใช้สั่ง `set` อย่างเดียว
- ไม่ต้องใช้ Display Pilot 2 หรือ BetterDisplay สำหรับงานนี้
- ถ้าอัปเกรด skhd ผ่าน `brew upgrade` path ใน Cellar จะเปลี่ยน → ต้องให้สิทธิ์ Accessibility ใหม่ แล้วรัน `skhd --restart-service`
- เพิ่มปุ่มอื่นได้ที่ `skhdrc` เช่น `cmd + alt - 2 : ~/bin/benq-input.sh usbc` (ใช้ได้เฉพาะตอนจอยังแสดง Mac อยู่)

### ควบคุม PC-PTMC072 จาก Mac (2026-10-09) ✅ ทดสอบผ่าน

| ช่องทาง | วิธีใช้บน Mac |
|---|---|
| **SSH** | `ssh pc` → เข้า PowerShell ของ PC ทันทีโดยไม่ต้องใส่รหัสผ่าน (ใช้กุญแจ `~/.ssh/id_ed25519`) |
| **Remote Desktop** | แอป **Windows App** → เพิ่ม PC `PC-PTMC072.local` ผู้ใช้ `ptmc0` + รหัสผ่าน Windows |

- alias `pc` อยู่ใน `~/.ssh/config` (สำรองไฟล์เดิมไว้ที่ `~/.ssh/config.bak-2026-10-09`)
- Claude Code บน Mac สั่งคำสั่งบน PC ได้ตรงๆ เช่น `ssh pc 'Get-Service sshd'`
- รายละเอียดฝั่ง PC และข้อควรระวัง (Sleep, ห้ามใช้ RDP ระหว่างไลฟ์): ดู [[entities/pc-ptmc072-desktop]]
## ผลตรวจสมรรถภาพ (2026-09-04)

ตรวจตอน uptime 18 นาที — **สุขภาพดีทุกด้าน ไม่มีคอขวด**

| ด้าน | ค่าที่วัดได้ | ประเมิน |
|---|---|---|
| CPU | Apple M4 10 cores (4P + 6E), load avg 1.62 / 2.59 / 4.45 | โหลดต่อ core ≈ 0.16 — ว่างมาก |
| Thermal | ไม่มีบันทึก thermal/performance warning | ไม่โดน throttle |
| RAM | free 87%, **swap ใช้ 0.00 MB** | RAM 24 GB เพียงพอเต็มที่ |
| Storage | ใช้ 154 GB เหลือ 285 GB (ใช้ 35%) | พื้นที่เหลือเยอะ |
| SSD health | SMART Status: **Verified** | ปกติดี |
| เสถียรภาพ | ไม่มี kernel panic log, 744 processes / 30,720 threads | ปกติสำหรับเครื่อง dev |

- **กิน CPU สูงสุด:** VS Code Renderer (6.4%), [[entities/claude|Claude]] Code extension (5.8%), WindowServer (4.9%)
- **กิน RAM สูงสุด:** VS Code, Google Chrome, LINE, Stream Dock AJAZZ — ไม่มีตัวใดเกิน 2% ต่อ process

## ผลตรวจสมรรถภาพ (2026-09-25)

ตรวจตอน uptime 2 วัน 14 ชม. — **โดยรวมดี แต่เจอ Defender extension ค้างรันอยู่**

| ด้าน | ค่าที่วัดได้ | ประเมิน |
|---|---|---|
| CPU | load avg 1.61 / 1.54 / 1.57 (10 cores) | ว่าง |
| Thermal | ไม่มี thermal/performance warning | ปกติ |
| RAM | free 78%, swap 0 MB (pageouts 71,061) | เพียงพอ |
| Storage | Data volume ใช้ 173 GB เหลือ 266 GB (40%); `~/Library/Caches` 9 GB | ดี |
| SSD health | SMART **Verified** | ปกติ |
| Processes | 893 | ปกติสำหรับเครื่อง dev |

- **ปัญหาที่พบ:** system extension `com.microsoft.wdav.epsext` (Microsoft Defender Endpoint Security Extension) ยังสถานะ `[activated enabled]` และรันตลอด (PID 541 ตั้งแต่ boot) กิน CPU เฉลี่ยสูงสุดในเครื่อง ~25% — การถอด Defender เมื่อ 2026-09-17 **ยังไม่ครบ** ตามที่เตือนไว้ในหัวข้อ "ข้อควรระวัง" ด้านบน; plist `com.microsoft.fresno.uninstall` ก็ยังค้างใน `/Library/LaunchDaemons/`
- **กิน RAM สูงสุด:** LINE (~1.1 GB), VS Code (หลาย process รวมหลาย GB), Google Chrome, Microsoft Word

### แอปที่ไม่ได้ใช้/ไม่จำเป็น (ประเมิน 2026-09-25)
| แอป | ขนาด | ใช้ล่าสุด | หมายเหตุ |
|---|---|---|---|
| iMovie | 3.7 GB | ไม่เคย | ลบได้ ติดตั้งใหม่จาก App Store ได้ |
| GarageBand | 1.1 GB | ไม่เคย | ลบได้ |
| Keynote | 543 MB | ไม่เคย | ใช้ PowerPoint แทน |
| Display Pilot 2 | 804 MB | 2025-12-21 | ซอฟต์แวร์ BenQ — เก็บไว้ถ้ายังปรับจอ RD280U ผ่านแอป |
| Microsoft Outlook / OneNote / Excel | 2.6 / 1.3 / 2.5 GB | ไม่เคย | ใช้ Gmail/Google Sheets อยู่ — Excel ควรเก็บไว้เปิดไฟล์ราชการ |
| Microsoft Teams | 1.1 GB | 2026-09-08 | เก็บถ้ายังมีประชุม Teams |
| Microsoft 365 Copilot + Copilot | 1.0 GB + 151 MB | 2026-09-15/18 | ซ้ำกันสองตัว |
| OneDrive | 1.2 GB | ไม่เคย | มี LaunchAgent/Daemon updater 3 ตัวรันพื้นหลัง |
| Gemini (+ Google Gemini ใน ~/Applications) | 352 MB | ไม่เคย | ซ้ำกันสองตัว |
| Docker | 2.4 GB | 2026-08-31 | Herd ครอบคลุม dev Laravel แล้ว มี daemon 2 ตัว |
| uTorrent Web | 37 MB | 2026-09-04 | ความเสี่ยงด้านความปลอดภัย |
| Figma, Toggl Track, NetBird, FreeFileSync/RealTimeSync, Mi Fitness | — | 2026-01 ถึง 06 | ไม่ได้ใช้หลายเดือน — พิจารณาตามความจำเป็น |
| brew: `postgresql@17`, `nut` | — | — | ติดตั้งค้างแต่ไม่ได้รัน (ใช้ postgresql@16) |

### ผลการล้างเครื่อง (2026-09-25)
- รัน `~/mac-cleanup.sh --run` แล้ว: ลบแอป 17 ตัวตามตารางด้านบน (ยกเว้น Display Pilot 2, Excel, Teams, Microsoft 365 Copilot) + launchd plist ของ OneDrive/Docker/NetBird + `com.microsoft.fresno.uninstall` + brew `postgresql@17`, `nut`
- **Defender extension ยังถอดไม่ได้:** `systemextensionsctl uninstall` ใช้ไม่ได้เมื่อเปิด SIP ("this tool cannot be used if System Integrity Protection is enabled") หลัง restart `epsext` ยัง `[activated enabled]` และใช้ CPU ~25%
- **แก้แล้ว (2026-09-25):** ผู้ใช้ปิด extension ด้วยตนเอง (SIP ยังเปิดอยู่) → สถานะเปลี่ยนเป็น `[terminated waiting to uninstall on reboot]` process `epsext` หยุดแล้ว ไม่มีไฟล์ Defender/launchd ค้าง — restart อีกครั้งเพื่อให้ถอดออกจากรายการถาวร
- **หลังล้าง:** RAM ว่าง 88%, swap 0, Data volume ใช้ 157 GB เหลือ 282 GB (ได้คืน ~16 GB), ไม่มี process ใดกิน CPU เกิน 4%

## ตรวจอาการเครื่องร้อน (2026-10-05)

ตรวจตอน 19:02 uptime 11 ชม. — **ขณะตรวจเครื่องว่าง ไม่ throttle** สาเหตุความร้อนมาจากโหลดช่วงก่อนหน้า

| ด้าน | ค่าที่วัดได้ | ประเมิน |
|---|---|---|
| Thermal | `pmset -g therm` ไม่มี thermal/performance warning, log 12 ชม. ไม่มีเหตุการณ์ thermal | ร้อนแต่ยังไม่ถึงขั้นลดความเร็ว |
| CPU ขณะตรวจ | load avg 2.10 / 1.60 / 1.88, ไม่มี process เกิน 6% | ว่าง |
| RAM | free 68%, swap 0 | ปกติ — แต่เกิด JetsamEvent 10:28 (process ใหญ่สุด = LINE) |

**ผู้ต้องสงสัยหลัก (CPU สะสมตั้งแต่ boot):**
1. **LINE — ตัวการหลัก:** `LineCall` (โทร/วิดีโอคอล) เริ่ม ~15:30 ใช้ CPU สะสม **39 นาที** ใน 3.5 ชม. + ตัวแอป LINE อีก 25 นาที; ระบบออกรายงาน disk writes เกินเกณฑ์ (11:36); `LINE.AudioService` ค้าง assertion `PreventUserIdleSystemSleep` **19 ตัว** → เครื่องไม่ได้ sleep เลยแม้ไม่ได้ใช้
2. **WindowServer** 75 นาที — วาดจอคู่ (BenQ 3840×2560 + LG) ปกติแต่เพิ่มความร้อนพื้นฐาน
3. **Spotlight (`mds_stores`)** 10 นาที + **`apfsd`** CPU 77% ช่วง 09:15 — น่าจะ index/จัดการไดรฟ์ภายนอก `Buncha_Backup` (APFS 2 TB) และ `P.Buncha` (exFAT 1 TB ผ่าน FSKit → `fskitd`/`UVFSService` ทำงานเพิ่ม)
4. **Chrome** — disk writes เกินเกณฑ์ (11:46)

**คำแนะนำ:**
- หลังวางสาย LINE ให้ **Quit LINE (⌘Q)** แล้วเปิดใหม่ — เคลียร์ `LineCall` และ assertion กัน sleep; ถ้าคอลวิดีโอนานๆ ใช้ LINE บนมือถือแทน
- ปิด Spotlight index ไดรฟ์ภายนอก: System Settings → Spotlight → Search Privacy → เพิ่ม `Buncha_Backup`, `P.Buncha`; eject ไดรฟ์ที่ไม่ได้ใช้
- ตรวจการวางเครื่อง: ช่องระบายอากาศอยู่**ใต้เครื่อง** — อย่าวางบนผ้า/กระดาษ เว้นรอบเครื่อง ~10 ซม. อย่าวางของทับ
- ดูอุณหภูมิจริงได้ด้วย `sudo powermetrics --samplers smc,thermal -n 1` หรือแอป **Stats** — ติดตั้งแล้ว 2026-10-05 (v3.0.20 ผ่าน `brew install --cask stats`) แสดงอุณหภูมิ/พัดลม/CPU บน menu bar

## brew upgrade + ย้าย MySQL ไปรุ่น LTS 9.7 (2026-10-05)

- `brew upgrade` อัปเดต 57 formula — Herd ใช้ PHP ของตัวเอง และ Node มาจาก nvm (v23.11.1) จึงไม่กระทบ
- **ปัญหา:** `mysql` (สาย Innovation) กระโดดจาก 9.5 → **26.7** และเปิดฐานข้อมูลเดิมไม่ได้: `Cannot upgrade from 90500 to 260700` — รุ่น 26.7 รับการอัปเกรดจากรุ่น LTS ก่อนหน้า (9.7) เท่านั้น ข้อมูลไม่เสียหายเพราะหยุดก่อนเริ่มแปลง
- **วิธีแก้:** `brew uninstall mysql` → `brew install mysql@9.7` → `brew services start mysql@9.7` (อัปเกรดข้อมูล 9.5 → 9.7.2 อัตโนมัติ) → `brew link --force mysql@9.7` ให้ใช้คำสั่ง `mysql` ได้
- **ผล:** ตารางครบทุกฐาน และโปรเจกต์ dattajeewo-v2, monklife-admin, m-ptmc072-v2, takbat-ptmc เชื่อมต่อได้ปกติ
- **ไฟล์สำรอง:** `~/mysql-backup-2026-10-05.sql` (dump 11 MB) + `~/mysql-datadir-9.5-backup-2026-10-05/` (โฟลเดอร์ข้อมูล 9.5 ทั้งชุด)
- **บทเรียน:** ใช้ `mysql@<LTS>` แทน `mysql` เพื่อให้ `brew upgrade` อัปเดตเฉพาะรุ่นย่อยใน LTS เดียวกัน ส่วน LaunchAgent เปลี่ยนชื่อเป็น `sh.brew.mysql@9.7`

## แผนในอนาคต
- (ยังไม่ระบุ)

## Related
- [[entities/benq-rd280u-monitor]]
- [[entities/benq-screenbar-light]]
- [[entities/zircon-pi-ups-1000va]]
- [[entities/brother-dcp-t430w-printer]]
- [[entities/claude]]
- [[entities/pc-ptmc072-desktop]]
- [[entities/microsoft-365-family]]
