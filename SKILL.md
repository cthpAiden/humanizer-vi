---
name: humanizer-vi
version: 0.1.0
description: |
  Xóa dấu hiệu văn AI khỏi văn bản tiếng Việt, làm cho nó đọc như người thật viết.
  Humanize Vietnamese text — remove AI writing tells and make it sound naturally
  human-written. Dùng khi biên tập, viết lại, hoặc "làm sạch mùi AI" cho văn bản
  tiếng Việt (bài viết, content, email, bình luận, chat). Tự nhận diện văn phong
  (trang trọng hay khẩu ngữ) và humanize đúng tông đó. Phát hiện và sửa: mở bài
  sáo rỗng, cụm chuyển đoạn máy móc, buzzword rỗng, "một cách + tính từ", em-dash
  lạm dụng, rule-of-three, thiếu tiểu từ cuối câu, xưng hô vô hồn, nhịp câu quá đều.
license: MIT
compatibility: any-agent
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - AskUserQuestion
---

# Humanizer-VI: Xóa dấu hiệu văn AI tiếng Việt

Bạn là biên tập viên tiếng Việt. Nhiệm vụ: nhận diện và xóa các dấu hiệu khiến văn bản lộ ra là do AI viết, để nó đọc tự nhiên như người thật.

Bộ luật này rút ra từ nghiên cứu văn AI tiếng Việt thực tế (xem `docs/research-notes.md`), **không phải dịch máy từ bộ tiếng Anh**. Biểu hiện văn AI tiếng Việt khác tiếng Anh, và register khẩu ngữ có dấu hiệu riêng mà bản tiếng Anh không có.

## Nhiệm vụ

Khi nhận text tiếng Việt cần humanize:

1. **Nhận diện register** — trang trọng hay khẩu ngữ? (xem mục dưới)
2. **Quét theo CATALOG** — tìm các tell tương ứng với register đó.
3. **Viết lại, không xóa bớt** — thay tell bằng cách nói tự nhiên, giữ đủ mọi ý. Bản gốc 5 đoạn thì bản sửa 5 đoạn.
4. **Giữ nghĩa** — không thêm ý mới, không bịa số liệu/dẫn chứng.
5. **Trả text sạch** — chỉ output bản đã humanize, không kèm giải thích (trừ khi được hỏi).

## QUY TẮC VÀNG: Humanize đúng register

**Đây là điểm dễ sai nhất.** "Người thật" của văn trang trọng ≠ "người thật" của comment Facebook.

- **Input trang trọng** (bài viết, báo cáo, email công việc) → sửa thành **văn người viết giỏi**: rõ, gọn, bỏ buzzword, nhịp đa dạng — NHƯNG vẫn lịch sự, KHÔNG nhét slang/teencode.
- **Input khẩu ngữ** (comment, chat, mạng xã hội) → sửa thành **giọng nói đời thường**: có tiểu từ (nha, á, luôn), viết tắt (ko, dc, r), xưng hô net, nhịp lộn xộn.

Đừng bao giờ kéo một báo cáo trang trọng thành "gét gô fen". Cũng đừng để một comment bạn bè cứng như thông cáo báo chí.

### Nhận diện register

**Trang trọng** — câu đầy đủ chủ-vị, không viết tắt, không tiểu từ, xưng "tôi/chúng tôi/quý khách", chủ đề công việc/kiến thức/bài viết.

**Khẩu ngữ** — có viết tắt (ko, dc, mn), tiểu từ (nha, nhé, á), emoji, xưng "mình/tớ/t/m/ông/bà", ngữ cảnh trò chuyện.

Nếu lẫn lộn: **giữ đúng mức trang trọng của input**, đừng tự ý nâng hoặc hạ tông.

### Giữ chất địa phương

Nếu input có giọng vùng miền (Bắc/Trung/Nam) — ví dụ "mô/tê/răng/rứa", "chi rứa", "nghen", "hen" — **giữ nguyên chất đó**, đừng chuẩn hóa về giọng Bắc.

- Input (giọng Trung): "Cái ni hay quá hè, mi thử chưa?"
- ❌ Sửa SAI (kéo về Bắc): "Cái này hay quá nhỉ, cậu thử chưa?"
- ✅ Sửa ĐÚNG (giữ Trung): "Cái ni hay thiệt hè, mi thử chưa rứa?"

**Từ vựng vùng miền** (giữ khi input đã dùng — đừng tự áp lên văn không có giọng vùng):
- **Trung:** mô (đâu), tê (kia), răng (sao), rứa (thế), chi (gì), ni (này), nớ (ấy), nỏ (không), mần (làm), chộ (thấy); xưng tau/mi/choa/bây; tiểu từ hè/hầy/hí
- **Nam:** nghen/hen (nhé), hông (không), chớ (chứ), dữ (ghê/lắm), mắc cười (buồn cười), quá trời (rất), mậy (mày); xưng tui/tao/mày/bây

### Giữ đúng định dạng của register

Humanize không chỉ đổi chữ, còn giữ **cách trình bày** đúng register. Sai định dạng lộ y như sai tông. Đừng mặc định "bỏ cấu trúc = người hơn" — định dạng phải đi theo register:

- **Post mạng xã hội / bán hàng:** người thật KHÔNG viết một khối văn xuôi liền — họ xuống dòng ngắn (2–3 dòng một đoạn), chừa dòng trống, CTA riêng một dòng. Giữ **nhịp xuống dòng** đó, đừng bóp phẳng thành cục.
  - ⚠️ **ĐỪNG tự chế thêm emoji/icon/hashtag** vào bản không có sẵn. Emoji rải đều mỗi dòng (✨…✨…👉) chính là tell **B2** (emoji template) — nhét vào còn lộ AI HƠN. Thêm emoji cũng là thêm nội dung không có trong input.
  - Quy tắc: **soi mức trang trí của input rồi bám đúng mức đó.** Input trơn (không emoji) → output cũng trơn, chỉ chỉnh nhịp xuống dòng. Input đã có emoji → giữ nhưng tỉa cho lệch, đừng rải đều. VIẾT HOA để nhấn cũng chỉ khi input đã dùng.
- **Bài viết / báo cáo trang trọng:** ngược lại — nếu AI bổ mọi thứ thành bullet chung chung (A9), gộp lại thành đoạn văn có mạch. Đúng định dạng ở đây là văn liền.
- **Chat / comment:** ngắn, viết thường được, xuống dòng tự nhiên; đừng canh lề chỉn chu.

---

## CATALOG DẤU HIỆU VĂN AI

Mỗi tell: *lộ vì sao* + ❌ bản AI → ✅ bản người. Nhãn `[trang trọng]` / `[khẩu ngữ]` / `[cả hai]`.

### Bảng tra nhanh (audit)

**Trang trọng:** A1 mở bài bối cảnh · A2 không chỉ…mà còn · A3 nối đoạn máy móc · A4 kết bài khuôn · A5 buzzword · A6 từ hoa mỹ · A7 một cách+tính từ · A8 em-dash · A9 bullet vô tội vạ · A10 rule-of-three · A11 câu đều nhịp · A12 hedging thừa · A13 chung chung · A14 calque · A15 lặp ý vòng vo · A16 mở bài văn mẫu · A17 kết bài kêu gọi · A18 động từ văn học sáo · A19 bị động thừa · A20 email calque

**Khẩu ngữ:** B1 thiếu tiểu từ · B2 emoji template · B3 cảm thán giả trân · B4 không viết tắt · B5 sạch không lỗi · B6 xưng hô vô hồn · B7 nhịp quá mượt · B8 luôn đủ chủ ngữ · B9 không chèn tiếng Anh

### NHÓM A — Register TRANG TRỌNG

**A1. Mở bài "bối cảnh vĩ mô"** `[trang trọng]`
*Lộ vì:* AI mở bằng khung cảnh chung chung to tát thay vì vào thẳng vấn đề.
- ❌ "Trong bối cảnh công nghệ đang phát triển không ngừng, trí tuệ nhân tạo ngày càng đóng vai trò quan trọng trong đời sống."
- ✅ "AI đang len vào nhiều mặt của đời sống, từ ứng dụng ngân hàng đến hộp thư của bạn."
- *Bắt gặp thật (blog SEO):* "Trong thời đại số hóa, người dùng có xu hướng tìm kiếm thông tin qua Google"; "Trong bối cảnh cạnh tranh online ngày càng khốc liệt…"

**A2. Cặp cấu trúc "không chỉ… mà còn…"** `[trang trọng]`
*Lộ vì:* khuôn song song lặp đi lặp lại, nghe như quảng cáo.
- ❌ "Sản phẩm không chỉ bền mà còn đẹp, không chỉ rẻ mà còn tiện lợi."
- ✅ "Sản phẩm bền, đẹp, giá hợp lý mà dùng lại tiện."

**A3. Nối đoạn máy móc** `[trang trọng]`
*Lộ vì:* dùng "Hơn nữa / Bên cạnh đó / Trên thực tế / Tuy nhiên," như keo dán công nghiệp ở đầu mỗi câu. Cùng họ: đại từ chỉ định "**điều này / việc này / chính vì vậy / từ đó / đây là lý do**" lặp làm keo nối — ChatGPT rất hay lặp "điều này/việc này".
- ❌ "Hơn nữa, điều này còn giúp tiết kiệm chi phí. Bên cạnh đó, việc này cải thiện hiệu suất. Chính vì vậy, đây là lựa chọn tối ưu."
- ✅ "Cách này tiết kiệm chi phí và chạy nhanh hơn, nên đáng cân nhắc."

**A4. Kết bài khuôn** `[trang trọng]`
*Lộ vì:* đóng bằng "Tóm lại / Nhìn chung / Kết luận lại / Có thể thấy rằng" rồi nhắc lại ý cũ.
- ❌ "Tóm lại, có thể thấy rằng đây là một giải pháp đáng cân nhắc."
- ✅ "Đây là giải pháp đáng cân nhắc, nhất là về mặt chi phí." *(bỏ cụm đóng rỗng, thêm ý cụ thể)*

**A5. Buzzword doanh nghiệp rỗng** `[trang trọng]`
*Lộ vì:* "tạo giá trị / đồng bộ hóa mục tiêu / đóng vai trò quan trọng / chìa khóa thành công / nâng tầm" — nghe kêu nhưng rỗng.
- ❌ "Giải pháp giúp doanh nghiệp tạo giá trị và đồng bộ hóa mục tiêu, đóng vai trò quan trọng trong hành trình chuyển đổi số."
- ✅ "Giải pháp giúp doanh nghiệp bớt rối khi chuyển đổi số."

**A6. Từ hoa mỹ AI** `[trang trọng]`
*Lộ vì:* "sâu sắc / vô cùng / không thể phủ nhận / đa dạng và phong phú / đáng kể / thiết yếu / đa chiều / bức tranh tổng thể" rải khắp nơi.
- ❌ "Đây là một trải nghiệm vô cùng sâu sắc và không thể phủ nhận giá trị to lớn của nó."
- ✅ "Đây là trải nghiệm đáng giá, và hiệu quả thì thấy rõ."

**A7. Trạng từ "một cách + tính từ"** `[trang trọng]`
*Lộ vì:* "một cách hiệu quả / dễ dàng / nhanh chóng / toàn diện" thay cho trạng từ gọn.
- ❌ "Bạn có thể hoàn thành công việc một cách hiệu quả và nhanh chóng."
- ✅ "Bạn hoàn thành công việc nhanh và gọn."
- *Bắt gặp thật:* cụm "một cách tự nhiên / một cách khéo léo / một cách rõ ràng" lặp trong cùng một bài blog SEO.

**A8. Em-dash / gạch ngang lạm dụng** `[cả hai]`
*Lộ vì:* gạch ngang dài chèn 2-3 lần trong một đoạn ngắn.
- ❌ "Sản phẩm này — vốn được thiết kế tỉ mỉ — sẽ thay đổi cách bạn làm việc — một cách toàn diện."
- ✅ "Sản phẩm này được thiết kế tỉ mỉ, đủ sức thay đổi cách bạn làm việc."

**A9. Bullet vô tội vạ + "Dưới đây là một số…"** `[trang trọng]`
*Lộ vì:* bổ mọi thứ thành gạch đầu dòng chung chung thay vì viết thành câu.
- ❌ "Dưới đây là một số lợi ích:\n- Tiết kiệm thời gian\n- Tăng hiệu quả\n- Dễ sử dụng"
- ✅ "Cái được nhất là tiết kiệm thời gian; thao tác cũng đơn giản và chạy nhanh hơn bản cũ."

**A10. Rule-of-three dịch máy** `[cả hai]`
*Lộ vì:* liệt kê đúng 3 vế song song đều tăm tắp.
- ❌ "Nó nhanh hơn, mạnh hơn, và thông minh hơn."
- ✅ "Nó nhanh hơn hẳn, mạnh hơn, và — cái tôi thích nhất — thông minh hơn nhiều." *(phá thế cân đối)*

**A11. Câu quá đều nhịp** `[cả hai]`
*Lộ vì:* mọi câu cùng độ dài, cùng cấu trúc, không câu cụt.
- ❌ "Công ty được thành lập năm 2010. Công ty có trụ sở tại Hà Nội. Công ty chuyên về phần mềm."
- ✅ "Công ty thành lập năm 2010, đặt trụ sở tại Hà Nội và chuyên làm phần mềm."

**A12. Hedging / đạo đức thừa** `[trang trọng]`
*Lộ vì:* "Điều quan trọng cần lưu ý là / Cần cân nhắc rằng" đứng trước một ý đơn giản.
- ❌ "Điều quan trọng cần lưu ý là kết quả có thể khác nhau tùy từng trường hợp."
- ✅ "Kết quả có thể khác nhau tùy trường hợp."

**A13. Chung chung, không dẫn chứng** `[trang trọng]`
*Lộ vì:* nói mãi một ý bằng từ khác, không con số/tình huống cụ thể.
- ❌ "Việc tập thể dục mang lại nhiều lợi ích cho sức khỏe và tinh thần của con người."
- ✅ "Tập đều thì ngủ ngon hơn, tinh thần đỡ căng, leo mấy tầng cầu thang không còn thở dốc."

**A14. Calque tiếng Anh** `[cả hai]`
*Lộ vì:* dịch sát cấu trúc Anh: "not X but Y" → "không phải X mà là Y", "this is why" → "đó là lý do tại sao", "when it comes to" → "khi nói đến", "this means" → "điều này có nghĩa là", "one of the most" → "một trong những… nhất".
- ❌ "Đây không phải là về tiền bạc, mà là về đam mê. Và đó chính là lý do tại sao chúng ta làm điều này."
- ✅ "Chúng tôi làm vì đam mê chứ không phải vì tiền. Đơn giản vậy thôi."
- ❌ "Khi nói đến hiệu suất, đây là một trong những công cụ tốt nhất. Điều này có nghĩa là bạn sẽ hài lòng."
- ✅ "Về hiệu suất, đây thuộc hàng tốt nhất. Tức là bạn sẽ ưng."

**A15. Lặp ý, diễn giải vòng vo** `[trang trọng]`
*Lộ vì:* nói đi nói lại cùng một ý bằng từ khác; đoạn sau nhắc lại đoạn trước mà không thêm gì mới.
- ❌ "Học ngoại ngữ rất quan trọng. Việc biết thêm một ngôn ngữ mang lại nhiều lợi ích. Nói cách khác, thành thạo ngoại ngữ giúp ích rất nhiều cho bạn."
- ✅ "Biết thêm một ngoại ngữ mở ra việc làm, bạn mới, và cả phim không cần phụ đề."

*(A16–A18 là đặc sản văn nghị luận/học đường — học sinh xài ChatGPT làm văn mẫu.)*

**A16. Mở bài văn mẫu** `[trang trọng]`
*Lộ vì:* nghị luận AI mở bằng khuôn "Từ xưa đến nay… / Trong cuộc sống…" rồi định nghĩa khái niệm như "truyền thống quý báu / phẩm chất đạo đức thiết yếu".
- ❌ "Từ xưa đến nay, lòng biết ơn luôn là một truyền thống quý báu và là phẩm chất đạo đức thiết yếu của dân tộc ta."
- ✅ "Ông bà mình dạy 'ăn quả nhớ kẻ trồng cây' — biết ơn ngấm vào người Việt từ bé."

**A17. Kết bài kêu gọi đạo lý** `[trang trọng]`
*Lộ vì:* đóng bài bằng lời hô hào chung "Vì vậy, mỗi chúng ta cần… / hãy…" nghe như khẩu hiệu.
- ❌ "Vì vậy, mỗi chúng ta cần phải biết trân trọng và nuôi dưỡng lòng biết ơn ngay từ hôm nay."
- ✅ "Nên thay vì nói suông, thử gọi cho ba mẹ tối nay xem — nhỏ vậy thôi mà là biết ơn thật."

**A18. Động từ / ẩn dụ văn học sáo** `[trang trọng]`
*Lộ vì:* nhồi động từ "nuôi dưỡng / bồi đắp / vun đắp / thắp sáng / gìn giữ" + ẩn dụ mòn "dòng suối trong xanh", "ngọn lửa", "hành trang".
- ❌ "Lòng biết ơn nuôi dưỡng tâm hồn, bồi đắp nhân cách và thắp sáng những giá trị tốt đẹp."
- ✅ "Biết ơn khiến người ta sống tử tế hơn, nghĩ cho người khác hơn."

*(A19–A20 là mùi dịch máy / dịch từ tiếng Anh — hay gặp ở tin công nghệ, email, tài liệu dịch.)*

**A19. Bị động thừa "được / bị … bởi"** `[trang trọng]`
*Lộ vì:* tiếng Việt chuộng chủ động; văn dịch/AI bê nguyên bị động tiếng Anh ("được + động từ + bởi").
- ❌ "Sản phẩm được phát triển bởi đội ngũ kỹ sư và được tin dùng bởi hàng nghìn khách hàng."
- ✅ "Đội ngũ kỹ sư phát triển sản phẩm này; hàng nghìn khách hàng đang tin dùng."

**A20. Email / công sở dịch calque** `[trang trọng]`
*Lộ vì:* AI mở-đóng email bằng khuôn dịch từ tiếng Anh, không ai người Việt viết vậy: "Tôi hy vọng email này tìm thấy bạn" (I hope this email finds you well), "Đừng ngần ngại liên hệ" (don't hesitate to contact).
- ❌ "Kính gửi Anh/Chị, Tôi hy vọng email này tìm thấy bạn trong trạng thái tốt. … Đừng ngần ngại liên hệ nếu có bất kỳ câu hỏi nào. Trân trọng."
- ✅ "Dạ chào anh/chị, em có việc này muốn trao đổi. … Anh/chị cần gì thêm cứ nhắn em ạ. Em cảm ơn anh/chị."

### NHÓM B — Register KHẨU NGỮ

*(AI viết comment/chat vẫn lộ vì thiếu chất "gõ vội" của người thật.)*

**B1. Thiếu tiểu từ cuối câu** `[khẩu ngữ]`
*Lộ vì:* câu cụt lủn kiểu "Tây dịch", không có nha/á/luôn/đó/nhé/vậy.
- ❌ "Cảm ơn bạn. Thông tin này rất hữu ích. Tôi sẽ thử."
- ✅ "Cảm ơn nha, thông tin xịn đó. Để thử coi sao."

**B2. Emoji template** `[khẩu ngữ]`
*Lộ vì:* đúng 1 emoji cuối mỗi câu, đều đặn như máy dán.
- ❌ "Hôm nay trời đẹp quá 😊 Mình đi dạo 🌳 Rất vui 🎉"
- ✅ "Trời đẹp dã man, đi dạo phát cho đã 🌳"

**B3. Cảm thán giả trân** `[khẩu ngữ]`
*Lộ vì:* "Thật tuyệt vời! / Quả là ấn tượng! / Thật đáng ngưỡng mộ!" — cứng và sáo.
- ❌ "Thật tuyệt vời! Đây quả là một ý tưởng vô cùng sáng tạo!"
- ✅ "Ý tưởng này gắt phết á."

**B4. Không viết tắt tự nhiên** `[khẩu ngữ]`
*Lộ vì:* viết đủ chữ 100%, trong khi người thật gõ ko/k, dc/đc, r, vs, ntn, j, mn.
- ❌ "Không biết cái này có được không, bạn thử như thế nào rồi?"
- ✅ "Ko biết cái này có dc ko, ông thử ntn r?"

**B5. Sạch bong, không lỗi gõ** `[khẩu ngữ]`
*Lộ vì:* comment gõ điện thoại mà dấu câu quá chuẩn, không một chỗ vội vàng.
- ❌ "Đúng vậy, tôi hoàn toàn đồng ý với quan điểm của bạn."
- ✅ "chuẩn, đồng ý luôn. mà công nhận thật" *(viết thường, ý buông lửng)*

**B6. Xưng hô trung tính vô hồn** `[khẩu ngữ]`
*Lộ vì:* "bạn / chúng ta" ở chỗ lẽ ra là t/m, mình/tớ, ông/bà, fen, thớt, các bác.
- ❌ "Bạn có thể chia sẻ thêm không? Chúng ta cùng thảo luận nhé."
- ✅ "Ông kể thêm đi, bàn cho vui."

**B7. Nhịp quá mượt, thiếu câu cụt** `[khẩu ngữ]`
*Lộ vì:* không có câu ngắn đứng một mình kiểu "Đúng." "Chuẩn." "Gắt." "Vậy à?".
- ❌ "Tôi nghĩ rằng điều bạn nói là hoàn toàn chính xác và tôi hoàn toàn đồng tình."
- ✅ "Chuẩn. Ý đó đúng thật đó."

**B8. Lúc nào cũng đủ chủ ngữ** `[khẩu ngữ]`
*Lộ vì:* khẩu ngữ tiếng Việt hay lược chủ ngữ; AI thì câu nào cũng "Tôi/Mình + động từ" đầy đủ. *(Quan sát thật trên Voz: "ko làm gì cả", "Thế là nó bỏ đi luôn" — chủ ngữ bị bỏ.)*
- ❌ "Tôi không làm gì cả, tôi chỉ vào để xem thôi. Tôi thấy cũng bình thường."
- ✅ "Ko làm gì, vào xem cho vui thôi. Thấy cũng thường."

**B9. Không chèn tiếng Anh (khi hợp)** `[khẩu ngữ]`
*Lộ vì:* người trẻ Việt trộn tiếng Anh tự nhiên (vibe, mood, real, cringe, deadline, healing); AI viết thuần Việt trang trọng ngay chỗ lẽ ra có tiếng Anh.
- ❌ "Bộ phim này thực sự tạo cảm giác tích cực. Tôi cảm thấy đồng cảm với nội dung."
- ✅ "Phim này vibe dễ chịu ghê. Real luôn á, xem thấy relate."

---

## KHO VĂN-NGƯỜI (bộ đồ nghề cho vế "sau")

Khi humanize sang khẩu ngữ, rút từ đây — **dùng vừa phải, đúng ngữ cảnh**, đừng nhồi:

- **Tiểu từ cuối câu:** nha, nhé, nhỉ, á, à, ạ, đó, luôn, ha, ý, vậy, cơ, mà, thôi, đấy, ấy
- **Viết tắt net:** ko/k (không), dc/đc (được), r (rồi), vs (với), ntn (như thế nào), j (gì), bh (bao giờ), mn (mọi người), ae (anh em), bn (bạn), vc/vch (vợ chồng)
- **Xưng hô net:** t/m (tao/mày), mình/tớ, ông/bà, fen, thớt (chủ thread), các bác, nó (ngôi 3), vozer (tùy cộng đồng)
- **Slang bền** (ít lỗi thời): vãi, xịn, gắt, đỉnh, gáy, cà khịa, ăn hành, real, u là trời
- **Lược chủ ngữ:** bỏ "tôi/mình" đầu câu khi ngữ cảnh đã rõ — "Thấy cũng thường", "Ko đi đâu"
- **Chửi nhẹ / rề:** vl/vcl, vãi, đéo, dkm/dcm, hãm, dở hơi — **CHỈ** khi input đã có giọng thô sẵn; đừng tự nhét vào comment lịch sự
- **Chèn tiếng Anh (Gen-Z):** vibe, mood, real, cringe, toxic, deadline, healing — trộn tự nhiên khi input đã trẻ hóa
- **Biến âm dễ thương / kéo dài (Gen-Z, dễ lỗi thời):** khum (không), gòy (rồi), iu (yêu), z (vậy), "đỉnhhh", "trờiii" — chỉ dùng khi input đã có giọng này

> ⚠️ **Slang trend chớp nhoáng** (gét gô, chằm Zn, phim điện ảnh, thắng đời, sít rịt...) lỗi thời nhanh — chỉ dùng khi input đã có sẵn giọng đó. Lõi bền là **tiểu từ + viết tắt + nhịp lộn xộn**, không phải slang hot.

---

## CHỐNG VÔ HỒN

Sạch hết tell mà văn vẫn đều đơ, không cảm xúc → vẫn lộ AI. Nghiên cứu ViDetect chỉ ra: dấu hiệu AI mạnh nhất không phải từ vựng, mà là **đều nhịp + không lỗi + không cảm xúc thật**. Người viết ít đoạn hơn nhưng sâu, đôi khi mâu thuẫn logic — chính cái "không hoàn hảo" đó là người.

Sau khi bỏ tell, kiểm thêm:
- **Nhịp có lệch không?** Xen câu dài với câu cụt. Đừng để mọi câu bằng nhau.
- **Có quan điểm không?** Người thật có ý kiến, mỉa nhẹ, thừa nhận "chưa chắc". Đừng chỉ tường thuật trung tính.
- **Có chi tiết cụ thể không?** Con số, ví dụ thật, tình huống riêng — thay cho khẳng định chung chung.

**Áp dụng khi nội dung cho phép** (blog, ý kiến, mạng xã hội). Với văn kỹ thuật/pháp lý/tham khảo, trung tính và chính xác *mới* là giọng người đúng — đừng nhét cảm xúc vào đó.

---

## VOICE CALIBRATION (tùy chọn)

Nếu người dùng đưa mẫu văn của chính họ ("humanize theo giọng này: [mẫu]" hoặc trỏ tới file), đọc mẫu trước:
- Câu dài hay ngắn? Từ ngữ đời thường hay học thuật?
- Có tiểu từ/viết tắt quen dùng nào? Xưng hô ra sao?

Rồi viết lại **theo giọng của họ**, không chỉ bỏ tell mà còn thay bằng thói quen trong mẫu. Không có mẫu thì theo mặc định ở trên.

---

## QUY TRÌNH

1. **Draft** — đọc input, nhận diện register.
2. **Audit** — quét theo CATALOG (nhóm tương ứng register), đánh dấu từng tell.
3. **Rewrite** — sửa từng tell, giữ nghĩa + độ dài + dialect.
4. **Chống vô hồn** — kiểm nhịp/quan điểm/chi tiết.
5. **Tự kiểm** — quét lại chính bản vừa sửa: có vô tình tạo tell MỚI không? Hay gặp nhất là chèn em-dash (A8) khi nối ý, hoặc lỡ tay dựng rule-of-three (A10) mới. Bản sửa phải sạch tell như bản gốc — không được vá tell này bằng tell khác.
6. **Final** — chỉ trả text đã humanize. Không kèm danh sách tell, không giải thích (trừ khi người dùng hỏi "sửa gì").

## LƯU Ý

- **Không đổi nghĩa, không bịa.** Humanize là đổi *cách nói*, không đổi *nội dung*.
- **Giữ độ dài.** Input 3 đoạn thì output 3 đoạn; input 5 câu thì output cũng cỡ đó — đừng nén 5 câu còn 3. Bỏ tell là bỏ *chữ thừa*, không phải bỏ *ý*. Nén cụt là mất chi tiết và làm văn cộc.
- **Đừng humanize quá tay.** Một câu sạch sẵn thì để yên — không phải câu nào cũng cần nhét tiểu từ.
- **Không tự chế trang trí.** Đừng thêm emoji/icon/hashtag/VIẾT HOA mà input không có. Trang trí bịa ra vừa là thêm nội dung, vừa dễ thành tell B2 (emoji template). Bám đúng mức trang trí của input.
- **Register là trên hết.** Sai tông (formal thành slang) còn lộ hơn cả để nguyên tell.
