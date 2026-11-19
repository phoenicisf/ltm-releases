# ltm — Lightweight Terminal Manager

โปรแกรมเล็กๆ บน Windows สำหรับใช้ AI CLI อย่าง Claude Code หรือ Codex แทนการเปิด VS Code ทั้งตัว

- PowerShell สูงสุด 7 ช่องในหน้าต่างเดียว
- รายการไฟล์ของโฟลเดอร์ที่ทำงาน (explorer) อยู่ด้านซ้าย และโน้ตสำหรับร่างคำสั่งอยู่ด้านขวา
- พิมพ์และแสดงภาษาไทยได้ไม่เพี้ยน
- `ltm.exe` ไฟล์เดียว ราว 7 MB ไม่ต้องติดตั้ง และอัปเดตตัวเองได้

repo นี้เก็บเฉพาะไฟล์ที่แจก (releases) ไม่มีซอร์สโค้ด

## ดาวน์โหลด

**[ltm.exe เวอร์ชันล่าสุด](https://github.com/phoenicisf/ltm-releases/releases/latest/download/ltm.exe)** ·
[ทุกเวอร์ชันและ release notes](https://github.com/phoenicisf/ltm-releases/releases)

## ติดตั้ง

1. วาง `ltm.exe` ไว้ในโฟลเดอร์ที่ตัวเองมีสิทธิ์เขียน แนะนำ `%LOCALAPPDATA%\Programs\ltm\`
   - **อย่าวางใน `C:\Program Files`** เพราะ ltm อัปเดตตัวเองโดยเขียนทับไฟล์นี้ ซึ่งในโฟลเดอร์นั้นต้องเป็น admin
2. ดับเบิลคลิกเพื่อเปิด หรือสั่ง `ltm.exe "C:\path\to\project"` เพื่อเปิดโฟลเดอร์นั้นเลย
3. ครั้งแรกที่เปิด Windows อาจเตือน SmartScreen เพราะ exe ยังไม่ได้เซ็นรับรอง ให้กด **More info → Run anyway**
4. ปักหมุดไว้ที่ taskbar จะได้ใช้รายการ **Recent Folders** ตอนคลิกขวาที่ไอคอน

หรือติดตั้งด้วย PowerShell คำสั่งเดียว:

```powershell
$dir = "$env:LOCALAPPDATA\Programs\ltm"; New-Item -ItemType Directory $dir -Force | Out-Null
Invoke-WebRequest https://github.com/phoenicisf/ltm-releases/releases/latest/download/ltm.exe -OutFile "$dir\ltm.exe"
& "$dir\ltm.exe"
```

## อัปเดต

ไม่ต้องดาวน์โหลดเองอีก ltm เช็ก repo นี้เองตอนเปิดและทุก 6 ชั่วโมง เมื่อมีเวอร์ชันใหม่จะดาวน์โหลดไว้และตรวจ SHA-256 ให้

- ปิด ltm ตามปกติแล้วตัวใหม่จะเข้าไปแทน หรือกด **⬆ Restart** ที่มุมขวาล่างเพื่อเปลี่ยนเลย
- กด **What's new** เพื่ออ่านว่าเวอร์ชันใหม่มีอะไร และเปิดครั้งแรกหลังอัปเดตจะขึ้นหน้าต่าง What's new เอง
- ปิดการอัปเดตอัตโนมัติได้ด้วยตัวแปร `LTM_NO_UPDATE=1`

## เครื่องที่ใช้ได้

- Windows 10 หรือ 11 แบบ 64-bit
- Windows PowerShell 5.1 ซึ่งมากับ Windows หรือ PowerShell 7 (`pwsh`) ถ้าติดตั้งไว้
- การ์ดจอที่รองรับ OpenGL ซึ่งเครื่องทั่วไปมี

## ตรวจไฟล์

ทุก release มี `ltm.exe.sha256` แนบมา ตรวจไฟล์ที่ดาวน์โหลดเองได้ด้วย:

```powershell
(Get-FileHash ltm.exe -Algorithm SHA256).Hash.ToLower()
```

ค่าที่ได้ต้องตรงกับในไฟล์ `ltm.exe.sha256` ของ release นั้น

## ถอนการติดตั้ง

ลบ `ltm.exe` และโฟลเดอร์ `%LOCALAPPDATA%\ltm\` (ที่เก็บ state, โน้ต และไฟล์อัปเดต) ltm ไม่เขียนอะไรลงในโฟลเดอร์ที่ทำงาน
