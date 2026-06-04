# eClaims Macro Generator v5
**by ohmmer** · Powered by Gemini 3.1 Flash Lite + ui.vision

เครื่องมือช่วยกรอก NTT eClaims อัตโนมัติ — อ่านใบเสร็จด้วย AI แล้ว generate script สำหรับ ui.vision RPA

---

## ความสามารถ

| Feature | รายละเอียด |
|---|---|
| 📸 OCR ใบเสร็จ | อัปโหลดรูป → Gemini อ่าน COL1–COL6 ให้อัตโนมัติ |
| ✏️ แก้ไขตาราง | แก้ไขข้อมูลได้ในหน้าเว็บก่อน export |
| ⬇️ Download Excel/CSV | export ข้อมูลครบ 10 คอลัมน์ |
| ⚡ Generate Macro | สร้าง ui.vision JSON script สำหรับกรอก eClaims อัตโนมัติ |
| ✨ Gemini Prompt | copy prompt สำหรับใช้กับ Gemini โดยตรง |

---

## วิธีใช้งาน

### Tab 1 — 📸 OCR ใบเสร็จ

1. ใส่ **Gemini API Key** → กด Save (เก็บใน browser ของเครื่องคุณเท่านั้น)
2. อัปโหลดรูปใบเสร็จ (JPG / PNG / หลายไฟล์ได้)
3. กด **"อ่านใบเสร็จทั้งหมด"**
4. ตรวจสอบและแก้ไขข้อมูลในตาราง
5. กรอก **COL7–COL10** (สีเหลือง) ที่ต้องกรอกเอง:
   - COL7: Company Name of Client
   - COL8: Name & Designation of Person(s)
   - COL9: Number of Person(s)
   - COL10: Description
6. เลือก **Download Excel** หรือ **Download CSV** — หรือกด **ส่งเข้า Macro Tab**

### Tab 2 — ⚡ ui.vision Macro

1. อัปโหลด Excel ที่มีข้อมูล eClaims (COL1–COL10) หรือรับข้อมูลจาก Tab OCR
2. ตั้งค่า Macro Name และ Row range
3. กด **Generate** → ได้ไฟล์ `.json`
4. เปิด eClaims → New Claim → เลือก Type → เปิด **ui.vision** → วาง JSON → กด Play
5. ห้ามสลับ tab ระหว่าง macro รัน

### Tab 3 — ✨ Gemini Prompt

- Copy prompt สำเร็จรูปสำหรับใช้กับ Gemini.google.com โดยตรง (ไม่ต้องใช้ API Key)

---

## โครงสร้างคอลัมน์ Excel

| คอลัมน์ | ชื่อฟิลด์ | แหล่งข้อมูล |
|---|---|---|
| COL1 | ชื่อร้าน / Vendor | 🤖 Gemini OCR |
| COL2 | วันที่ (DD-Mon-YYYY ปี ค.ศ.) | 🤖 Gemini OCR |
| COL3 | เลขที่ใบเสร็จ / Tax Invoice | 🤖 Gemini OCR |
| COL4 | ยอดรวม VAT (Grand Total) | 🤖 Gemini OCR |
| COL5 | ประเภทรายการ | 🤖 Gemini OCR |
| COL6 | เขต / อำเภอ | 🤖 Gemini OCR |
| COL7 | Company Name of Client | ✏️ กรอกเอง |
| COL8 | Name & Designation of Person(s) | ✏️ กรอกเอง |
| COL9 | Number of Person(s) | ✏️ กรอกเอง |
| COL10 | Description | ✏️ กรอกเอง |

---

## Gemini API Key

- ขอฟรีได้ที่ **[aistudio.google.com/apikey](https://aistudio.google.com/apikey)**
- เลือก **"Create API key in new project"** (อย่าเลือก project ที่มี Billing)
- Key เก็บใน `localStorage` ของ browser เท่านั้น ไม่ได้ส่งไปที่อื่น

### Quota (Free Tier)

| Model | RPD ฟรี |
|---|---|
| Gemini 3.1 Flash Lite *(ใช้อยู่)* | **500 req/day** |
| Gemini 2.5 Flash | 20 req/day |

- **1 ไฟล์ = 1 request** (ไม่ใช่ 1 หน้า)
- ถ้า quota เต็ม จะขึ้น error — รอรีเซ็ตเที่ยงคืน Pacific Time
- ฟรี 100% ตราบใดที่ไม่ได้เปิด Billing ใน project

---

## กฎ OCR สำคัญ

1. ใบเสร็จ 1 ใบ = 1 แถว
2. ถ้ามีทั้ง **Tax Invoice** และ **Itemized bill** ร้านเดียวกันวันเดียวกัน → นับเป็น 1 แถว ใช้ Tax Invoice เป็น primary
3. COL2 ต้องเป็น **ปี ค.ศ.** เสมอ (เช่น 22-May-2026 ไม่ใช่ 2569)
4. COL4 คือ **Grand Total รวม VAT** ไม่มี comma (เช่น 4360.00)

---

## Tech Stack

- **Frontend**: HTML + CSS + Vanilla JS (single file, no server)
- **OCR**: Google Gemini 3.1 Flash Lite API (vision)
- **Excel**: SheetJS (xlsx.js)
- **RPA**: ui.vision Chrome Extension
- **Hosting**: GitHub Pages / เปิดไฟล์ตรงๆ ก็ได้

---

## Changelog

| Version | การเปลี่ยนแปลง |
|---|---|
| v5 | เพิ่ม Tab OCR (Gemini API), Download Excel/CSV, แสดง COL5-COL6 |
| v4 | Gemini Prompt tab, ui.vision macro generator |
