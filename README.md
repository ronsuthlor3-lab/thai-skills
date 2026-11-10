# thai-skills: ชุดสกิล Claude ภาษาไทย แจกฟรี

ชุดสกิล (Claude Agent Skills) สำหรับงานภาษาไทย โดยเฉพาะงานราชการ ใช้ฟรีภายใต้สัญญาอนุญาต MIT หลักการร่วมของทุกสกิลในชุดนี้คือ **ทุกกฎต้องบอกได้ว่ามาจากระเบียบหรือกฎหมายข้อไหน พร้อมลิงก์ไปยังแหล่ง** และแยกให้ชัดระหว่าง "ข้อบังคับ" กับ "แนวปฏิบัติ"

> **ไม่ใช่คำปรึกษาทางกฎหมาย** ดูหัวข้อ "คำปฏิเสธความรับผิด" ด้านล่าง

## สกิลในชุด

| สกิล | ทำอะไร | อยู่ที่ |
|---|---|---|
| **thai-official-letter** | ร่างและตรวจหนังสือราชการไทย (หนังสือภายนอก บันทึกข้อความ หนังสือประทับตรา คำสั่ง ระเบียบ ข้อบังคับ ประกาศ แถลงการณ์ ข่าว หนังสือรับรอง รายงานการประชุม) ตามระเบียบสำนักนายกรัฐมนตรีว่าด้วยงานสารบรรณ พ.ศ. 2526 และที่แก้ไขเพิ่มเติมถึงฉบับที่ 4 พ.ศ. 2564 | [`skills/thai-official-letter`](skills/thai-official-letter) (repo นี้) |
| **tor-review** | ตรวจ TOR การจัดซื้อจัดจ้างภาครัฐไทยเบื้องต้น อ้างกฎหมายและระเบียบพัสดุรายข้อ | [ronsuthlor3-lab/tor-review](https://github.com/ronsuthlor3-lab/tor-review) (แยก repo) |

## thai-official-letter ทำอะไรได้

- **โหมดร่าง:** ถามเฉพาะข้อมูลที่ขาด → เลือกชนิดหนังสือตามข้อ 10 → เลือกคำขึ้นต้น/คำลงท้ายจากตารางภาคผนวก 2 → ร่างตามลำดับส่วนประกอบ (ข้อ 11–27) → ตรวจทาน
- **โหมดตรวจ:** รับร่างที่เขียนมาแล้ว รายงานเป็นตาราง `ตำแหน่ง | พบ | ควรเป็น | อ้างอิง` แยกข้อผิดตามระเบียบออกจากข้อสังเกตเชิงแนวปฏิบัติ
- มีตารางคำขึ้นต้น สรรพนาม คำลงท้าย (ภาคผนวก 2) และรายชื่อ 15 ตำแหน่งที่ใช้ "กราบเรียน" ตามหนังสือ นร 0106/ว 913 (2555)
- แยกชัดว่า ฟอนต์ TH Sarabun PSK 16 พอยท์ ค่าจัดหน้า และเลขไทย เป็น **แนวปฏิบัติ ไม่ใช่ข้อบังคับในระเบียบ**
- ไม่สร้างเลขที่หนังสือ ลายมือชื่อ หรือชื่อบุคคลที่ผู้ใช้ไม่ได้ให้ ใช้ `{ช่องว่าง}` แทน และไม่ช่วยทำหนังสือราชการปลอม
- ส่งออกเป็น .docx ได้ ถ้าในเซสชันมีสกิลหรือเครื่องมือสร้าง Word

## โครงสร้างไฟล์

```
thai-skills/
├── skills/
│   └── thai-official-letter/
│       ├── SKILL.md                      # คำสั่งหลักของสกิล
│       ├── references/
│       │   ├── sources.md                # บัญชีแหล่ง S-01..S-10 และรายการที่ยืนยันไม่ได้
│       │   └── salutations.md            # ตารางภาคผนวก 2 + รายชื่อ 15 ตำแหน่ง
│       └── examples/
│           ├── external-letter.md        # หนังสือภายนอก
│           ├── internal-memo.md          # บันทึกข้อความ
│           ├── order.md                  # คำสั่ง
│           └── review-mode-example.md    # ตัวอย่างโหมดตรวจ
├── README.md
└── LICENSE
```

## วิธีติดตั้ง

### Claude.ai (เว็บหรือแอป)
1. ดาวน์โหลด repo นี้ แล้วบีบอัดโฟลเดอร์ `skills/thai-official-letter` เป็นไฟล์ zip (ให้ `SKILL.md` อยู่ในโฟลเดอร์ `thai-official-letter` ภายใน zip)
2. เปิดการตั้งค่า (Settings) แล้วไปที่หน้า **Skills**
3. อัปโหลดไฟล์ zip และเปิดใช้งานสกิล

(ชื่อเมนูอาจเปลี่ยนตามเวอร์ชันของ Claude.ai)

### Claude Code
```bash
mkdir -p ~/.claude/skills
cp -r skills/thai-official-letter ~/.claude/skills/
```
ตรวจว่ามีไฟล์ `~/.claude/skills/thai-official-letter/SKILL.md` แล้วเริ่มเซสชันใหม่

### ลองใช้
- "ช่วยร่างหนังสือภายนอกจากสำนักงาน… ถึงผู้อำนวยการ… เรื่องขอความอนุเคราะห์…"
- "ตรวจบันทึกข้อความนี้ให้หน่อย" แล้ววางร่าง
- "หนังสือถึงประธานศาลฎีกาต้องขึ้นต้นและลงท้ายว่าอะไร"

## แหล่งอ้างอิงหลัก

- ระเบียบสำนักนายกรัฐมนตรีว่าด้วยงานสารบรรณ พ.ศ. 2526 ฉบับรวมแก้ไขถึงฉบับที่ 4 (สำนักงานคณะกรรมการกฤษฎีกา): [lawreform.go.th](https://lawreform.go.th/uploads/files/1678240071-b99vw-cbccp.pdf)
- ระเบียบว่าด้วยการรักษาความลับของทางราชการ พ.ศ. 2544: [infocenter.oic.go.th](https://infocenter.oic.go.th/FILEWEB/CABINFOCENTER1/DRAWER007/GENERAL/DATA0000/00000049.PDF)
- รายการเต็มพร้อมสถานะการยืนยัน: [`skills/thai-official-letter/references/sources.md`](skills/thai-official-letter/references/sources.md)

ตรวจแหล่งล่าสุดเมื่อ **10 พฤศจิกายน 2569 (2026-11-10)**

## คำปฏิเสธความรับผิด

- สกิลนี้ช่วยร่างและตรวจรูปแบบเบื้องต้นเท่านั้น **ไม่ใช่คำปรึกษาทางกฎหมาย** และไม่รับรองว่าหนังสือที่ได้ถูกต้องครบถ้วน ผู้ใช้ต้องตรวจทานและรับผิดชอบเนื้อหาเอง
- ระเบียบ ภาคผนวก และหนังสือเวียนอาจถูกแก้ไขหลังวันที่ตรวจแหล่ง (ระเบียบข้อ 8 ให้แก้ภาคผนวกได้ด้วยหนังสือของปลัดสำนักนายกรัฐมนตรี) ให้ตรวจฉบับล่าสุดก่อนใช้จริง
- ส่วนราชการแต่ละแห่งอาจมีแบบหรือแนวปฏิบัติของตนเอง ให้ยึดแบบของหน่วยงานเป็นหลัก
- แหล่งบางรายการเป็นสำเนาที่หน่วยงานรัฐหรือมหาวิทยาลัยรัฐเผยแพร่ ไม่ใช่เว็บราชกิจจานุเบกษาโดยตรง (ดูสถานะใน `sources.md`)
- ห้ามใช้สกิลนี้ทำหนังสือราชการปลอม หรือแอบอ้างหน่วยงานหรือบุคคลจริง การปลอมเอกสารราชการอาจมีความผิดตามกฎหมาย
- โครงการนี้ไม่มีส่วนเกี่ยวข้องกับสำนักนายกรัฐมนตรีหรือหน่วยงานรัฐใด ๆ

## สัญญาอนุญาต

MIT — ดู [LICENSE](LICENSE)

---

## English summary

**thai-skills** is a free collection of Claude Agent Skills for Thai-language work, focused on Thai government tasks. Every rule in a skill must cite the specific regulation clause and link to its source, and mandatory rules are kept separate from common practice.

| Skill | Purpose | Location |
|---|---|---|
| `thai-official-letter` | Draft and review Thai official correspondence (external letters, internal memos, stamped letters, orders, regulations, announcements, certificates, meeting minutes) under the PM Office Regulation on Correspondence B.E. 2526 (1983), as amended through No. 4 B.E. 2564 (2021). Includes the Appendix 2 salutation/closing table and a review mode that outputs a `location / found / should be / reference` table. | this repo, `skills/thai-official-letter` |
| `tor-review` | Preliminary review of Thai public procurement TORs with clause-level citations. | [ronsuthlor3-lab/tor-review](https://github.com/ronsuthlor3-lab/tor-review) |

**Install:** Claude.ai — zip the `skills/thai-official-letter` folder and upload it on the Skills page in Settings (menu names may change between versions). Claude Code — `cp -r skills/thai-official-letter ~/.claude/skills/`.

**Disclaimer:** Not legal advice. Sources were checked on 2026-11-10 and may have changed since. Agencies may use their own templates. Do not use this skill to forge official documents or impersonate real agencies or people. Not affiliated with any Thai government agency.

**License:** MIT.
