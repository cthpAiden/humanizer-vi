# humanizer-vi — Design Spec

- **Ngày:** 2026-07-24
- **Trạng thái:** Viết **hồi tố** — skill đã được implement và ship trước khi có spec này. Doc ghi lại yêu cầu + quyết định thiết kế đã theo, cho người đọc/đóng góp sau.
- **Quy trình:** Có brainstorming (hỏi–đáp, trình thiết kế, chủ dự án duyệt). **Bỏ qua** bước spec-doc + writing-plans của Superpowers vì chủ dự án yêu cầu build thẳng; dùng task list thay cho plan. Doc này lấp chỗ spec còn thiếu.

## 1. Tổng quan

`humanizer-vi` là một Agent Skill: nhận văn bản **tiếng Việt**, xóa dấu hiệu "văn AI", trả lại bản đọc như người thật viết. Đóng gói dạng thư mục skill (`SKILL.md`), publish public trên GitHub.

**Vấn đề:** công cụ humanize hiện có đều nhắm tiếng Anh. Dấu hiệu văn AI tiếng Việt khác hẳn — không dịch bộ luật tiếng Anh sang xài được. Phân tích tiếng Việt đang có chỉ liệt kê chung chung, không có cặp trước/sau, bỏ qua văn khẩu ngữ. → khoảng trống để chiếm.

## 2. Quyết định thiết kế (chốt ở brainstorming)

| Quyết định | Chọn | Vì sao |
|---|---|---|
| Cơ chế | **Rules-based** (bộ luật + ví dụ cho LLM) | Bền, đúng hướng, không cần train. KHÔNG làm kiểu né máy dò AI (trò mèo–chuột, dễ lỗi thời, dính gian lận). |
| Register | **Thích ứng theo input** | Tự nhận trang trọng/khẩu ngữ rồi humanize đúng tông. Sai tông lộ hơn cả để nguyên tell. |
| Output | **Chỉ text đã sửa** | Gọn, dân dụng. Không kèm báo cáo tell. |
| Catalog | **Research sâu, mẫu thật** | Catalog là moat. Ví dụ từ Voz/blog SEO/văn mẫu thật, không bịa. |
| Đóng gói | **Skill** (`SKILL.md`) | Chạy trong Claude Code, dễ cài. |
| Phân phối | **Repo GitHub riêng** | Publish như các humanizer khác; tách khỏi dự án Clawdometer. |

## 3. Kiến trúc

**Repo:**
```
humanizer-vi/
  SKILL.md              # bộ luật chính
  README.md
  LICENSE               # MIT
  docs/research-notes.md  # nguồn + ghi chú 5 vòng research
  docs/superpowers/specs/ # spec này
  tests/fixtures.md     # cặp trước/sau kiểm thử
```

**SKILL.md — các khối:**
1. **Nhiệm vụ** — nhận diện register → quét catalog → viết lại giữ nghĩa/độ dài/dialect → trả text sạch.
2. **Quy tắc vàng** — humanize đúng register: input trang trọng → văn người viết giỏi (không slang); input khẩu ngữ → giọng đời thường (tiểu từ/viết tắt).
3. **Nhận diện register** + **giữ chất địa phương** (bảng từ Trung/Nam).
4. **Catalog** — Nhóm A trang trọng (A1–A20), Nhóm B khẩu ngữ (B1–B9); mỗi tell: *lộ vì sao* + ❌ trước → ✅ sau + nhãn register. Có **Bảng tra nhanh** để audit.
5. **Kho văn-người** — tiểu từ, viết tắt, xưng hô, slang bền, lược chủ ngữ, chửi nhẹ, chèn tiếng Anh, biến âm (các nhóm dễ lỗi thời đều có cảnh báo).
6. **Chống vô hồn** — sạch tell nhưng đều đơ vẫn lộ (theo ViDetect): kiểm nhịp/quan điểm/chi tiết.
7. **Voice calibration** (tùy chọn) — nếu có mẫu văn của người dùng thì bắt chước giọng đó.
8. **Quy trình** draft → audit → rewrite → chống vô hồn → final.

## 4. Phạm vi đã làm

- **29 tell** (20 trang trọng + 9 khẩu ngữ), mỗi tell có cặp trước/sau tiếng Việt thật.
- Phủ: marketing/SEO, nghị luận học đường, email/công sở, văn dịch máy (trang trọng); forum Voz + Gen-Z social (khẩu ngữ); vùng miền Trung/Nam.
- **9 fixtures** trải cả hai register + case chống-over-humanize.
- Dựng qua **5 vòng gom mẫu thật**, mỗi vòng dogfood trên văn-AI thật (grep khách quan xác nhận tell biến mất). Nguồn ghi ở `docs/research-notes.md` (Vòng 1–5).

## 5. Non-goals (YAGNI)

- Không làm công cụ né máy dò AI (GPTZero/Turnitin).
- Không train model / ML.
- Chưa đóng gói thành plugin cài được (`plugin.json` + marketplace) — để sau.
- Không có UI/web/CLI riêng — chạy trong Claude Code là đủ cho v1.

## 6. Kiểm thử

- **Fixtures** (`tests/fixtures.md`): đưa phần ❌ cho skill, so kết quả với ✅ về *chất* (hết tell, giữ nghĩa, đúng register) — không cần khớp từng chữ.
- **Dogfood**: chạy skill trên đoạn văn-AI thật, `grep` các cụm tell trong output kỳ vọng = 0, đếm số câu giữ nguyên.

## 7. Ghi chú quy trình

Skill được build thẳng theo lệnh chủ dự án ("bắt đầu làm theo thiết kế"), bỏ qua bước spec-doc + writing-plans chuẩn của Superpowers — hợp lệ vì lệnh người dùng đè quy trình skill. Thiết kế trước đó nằm rải ở chat + README + research-notes + memory; spec này gom lại cho chuẩn hồ sơ.
