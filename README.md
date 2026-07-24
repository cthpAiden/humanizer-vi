# humanizer-vi

Một Agent Skill xóa dấu hiệu văn AI khỏi văn bản **tiếng Việt** — làm cho nó đọc như người thật viết, chứ không phải ChatGPT.

> A Claude / agent skill that strips AI writing tells from **Vietnamese** text and makes it read like a real person wrote it.

## Vì sao có cái này

Mấy công cụ "humanize" hiện tại đều nhắm tiếng Anh. Dấu hiệu văn AI tiếng Việt thì **khác hẳn** — không thể dịch bộ luật tiếng Anh sang rồi xài. Các bài phân tích tiếng Việt đang có chỉ liệt kê chung chung 6–10 dấu hiệu, không có cặp trước/sau, và bỏ qua hoàn toàn văn khẩu ngữ (comment, chat).

`humanizer-vi` là bộ luật đầu tiên:
- Rút từ văn AI tiếng Việt thực tế, **không dịch máy** từ bộ tiếng Anh.
- Có **cặp ❌ trước → ✅ sau** cho từng dấu hiệu.
- Xử được **cả hai register**: trang trọng (bài viết, báo cáo) và khẩu ngữ (comment, chat) — mỗi register có dấu hiệu riêng.

## Nó làm gì

- Tự nhận diện văn phong input (trang trọng hay khẩu ngữ) rồi humanize **đúng tông** đó.
- Quét hơn 30 dấu hiệu (35: 26 trang trọng + 9 khẩu ngữ — marketing, nghị luận học đường, email, văn dịch, comment): mở bài sáo rỗng, cụm chuyển đoạn máy móc ("Hơn nữa", "Bên cạnh đó"), buzzword rỗng ("đóng vai trò quan trọng"), "một cách + tính từ", em-dash lạm dụng, rule-of-three, calque tiếng Anh, thiếu tiểu từ cuối câu (nha/á/luôn), xưng hô vô hồn, nhịp câu quá đều...
- Giữ nguyên nghĩa và độ dài. Chỉ đổi *cách nói*, không đổi *nội dung*.
- Trả về text đã sạch, gọn.

## Cài đặt

Skill này là một thư mục. Đặt nó vào `~/.claude/skills/`:

**Clone thẳng vào skills:**

```bash
git clone https://github.com/cthpAiden/humanizer-vi.git ~/.claude/skills/humanizer-vi
```

**Windows (PowerShell):**

```powershell
git clone https://github.com/cthpAiden/humanizer-vi.git "$env:USERPROFILE\.claude\skills\humanizer-vi"
```

Hoặc copy tay cả thư mục vào `~/.claude/skills/humanizer-vi/`. Miễn là `SKILL.md` nằm trong đó.

## Cách dùng

Gọi skill rồi đưa text cần làm sạch.

**Văn trang trọng:**

> Humanize đoạn này: "Trong bối cảnh công nghệ đang phát triển không ngừng, sản phẩm của chúng tôi không chỉ hiệu quả mà còn đóng vai trò quan trọng trong việc tối ưu công việc một cách toàn diện."

→ *"Sản phẩm của chúng tôi giúp bạn làm việc nhanh và gọn hơn hẳn."*

**Văn khẩu ngữ:**

> Humanize: "Cảm ơn bạn. Thông tin này rất hữu ích. Tôi sẽ thử."

→ *"Cảm ơn nha, thông tin xịn đó. Để thử coi sao."*

**Theo giọng của bạn** (tùy chọn): đưa kèm một đoạn văn cũ của bạn, skill sẽ bắt chước giọng đó thay vì giọng mặc định.

## Cấu trúc

```
humanizer-vi/
  SKILL.md              # bộ luật chính (catalog + quy trình)
  README.md
  LICENSE               # MIT
  docs/research-notes.md  # nguồn + ghi chú nghiên cứu dấu hiệu văn AI tiếng Việt
  tests/fixtures.md     # các cặp trước/sau để kiểm thử
```

## Nguồn cảm hứng

- Ý tưởng "humanizer skill" và kiến trúc (Nhiệm vụ → Voice Calibration → catalog theo nhóm → Draft/Audit/Final → chế độ output) bám theo bộ [blader/humanizer](https://github.com/blader/humanizer), cùng trang **"Signs of AI writing"** của Wikipedia (WikiProject AI Cleanup). Phần register khẩu ngữ, dialect, và kho tiểu từ/viết tắt là bổ sung riêng cho tiếng Việt.
- Phần khung dấu hiệu văn AI tiếng Việt dựa trên nghiên cứu thực tế — chi tiết nguồn trong [`docs/research-notes.md`](docs/research-notes.md), gồm cả paper **ViDetect** (Vietnamese AI Generated Text Detection).

## License

[MIT](LICENSE)
