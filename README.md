# พจนานุกรม ไทย–อังกฤษ (Offline PWA)

แอปพจนานุกรมไทย⇄อังกฤษ ใช้งานออฟไลน์ได้เต็มรูปแบบ ติดตั้งลงหน้าจอมือถือได้เหมือนแอปจริง
ข้อมูล 32,000+ คำ มาจาก Volubilis open dictionary

## ไฟล์ในโฟลเดอร์นี้

| ไฟล์ | หน้าที่ |
|------|---------|
| `index.html` | ตัวแอป (เล็ก ~24KB) |
| `dict.json` | ข้อมูลคำศัพท์ (~7.7MB) |
| `sw.js` | service worker — แคชไฟล์ให้ใช้ออฟไลน์ |
| `manifest.webmanifest` | ทำให้ติดตั้งเป็นแอปได้ |
| `icon-*.png` | ไอคอนแอป |

> ทั้งหมดต้องอยู่โฟลเดอร์เดียวกัน อย่าแยกย้าย

---

## วิธี deploy ขึ้น GitHub Pages

### วิธีที่ 1: ผ่านหน้าเว็บ GitHub (ไม่ต้องใช้ command line)

1. ไปที่ https://github.com แล้วกด **New repository** ตั้งชื่อเช่น `dict` ตั้งเป็น **Public** กด Create
2. ในหน้า repo กด **Add file → Upload files** แล้วลากไฟล์ทั้งหมดในโฟลเดอร์นี้เข้าไป (index.html, dict.json, sw.js, manifest.webmanifest, และไฟล์ icon ทุกอัน) กด **Commit changes**
3. ไปที่ **Settings → Pages**
4. ใต้ **Build and deployment → Source** เลือก **Deploy from a branch**
5. เลือก branch `main` โฟลเดอร์ `/ (root)` กด **Save**
6. รอ 1–2 นาที จะได้ลิงก์แบบ `https://<ชื่อผู้ใช้>.github.io/dict/`
7. เปิดลิงก์นั้นในมือถือได้เลย

### วิธีที่ 2: ผ่าน git command line

```bash
git init
git add .
git commit -m "Thai-English offline dictionary PWA"
git branch -M main
git remote add origin https://github.com/<ชื่อผู้ใช้>/dict.git
git push -u origin main
```
จากนั้นทำตามขั้นตอน 3–6 ของวิธีที่ 1

---

## วิธีติดตั้งเป็นแอปบนมือถือ

หลัง deploy แล้ว เปิดลิงก์ `github.io` ในมือถือ แล้ว:

**iPhone (Safari)**
แตะปุ่ม Share (กล่องลูกศรขึ้น) → **Add to Home Screen** → จะได้ไอคอนบนหน้าจอ เปิดเต็มจอเหมือนแอป ใช้ออฟไลน์ได้

**Android (Chrome)**
แตะเมนู ⋮ → **Add to Home screen** (หรือจะมีแถบ "Install" เด้งขึ้นมาเอง)

เปิดครั้งแรกต้องต่อเน็ตเพื่อโหลดข้อมูลครั้งเดียว หลังจากนั้นใช้ออฟไลน์ได้ตลอด

---

## เวลาแก้ไขแล้วอยากอัปเดต

ถ้าแก้ `index.html`, `dict.json` หรือ `sw.js` ให้เปิด `sw.js` แล้วเปลี่ยนเลขเวอร์ชัน:

```js
const CACHE_VERSION = 'dict-v1';   // เปลี่ยนเป็น 'dict-v2' ทุกครั้งที่แก้ไฟล์
```

แล้ว upload/push ขึ้นใหม่ เครื่องที่ติดตั้งไว้จะดึงไฟล์ใหม่อัตโนมัติเมื่อเปิดแอปครั้งถัดไป
(ถ้าไม่เปลี่ยนเวอร์ชัน เครื่องอาจยังใช้ไฟล์เก่าจากแคช)
