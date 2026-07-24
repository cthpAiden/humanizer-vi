# Test Fixtures — humanizer-vi

Các cặp trước/sau để kiểm thử skill. Mỗi case ghi rõ register và các tell bị dính.
Cách dùng: đưa phần ❌ cho skill humanize, so kết quả với ✅ (không cần khớp từng chữ — khớp về *chất*: hết tell, giữ nghĩa, đúng register).

---

## Case 1 — Bài viết công nghệ (trang trọng)

**Tells:** A1 (mở bài bối cảnh), A5 (buzzword), A6 (từ hoa mỹ), A7 (một cách + tính từ)

❌ **Trước:**
> Trong bối cảnh chuyển đổi số đang diễn ra mạnh mẽ, việc ứng dụng trí tuệ nhân tạo đóng vai trò vô cùng quan trọng, giúp doanh nghiệp tạo giá trị và tối ưu quy trình một cách hiệu quả.

✅ **Sau:**
> Khi chuyển đổi số tăng tốc, AI đang thành công cụ quen thuộc trong doanh nghiệp — chủ yếu để tinh gọn quy trình và cắt bớt việc thủ công.

---

## Case 2 — Content bán hàng (trang trọng)

**Tells:** A2 (không chỉ… mà còn), A9 (bullet + "Dưới đây là một số"), A10 (rule of three)

❌ **Trước:**
> Sản phẩm không chỉ bền mà còn đẹp. Dưới đây là một số ưu điểm nổi bật:
> - Chất liệu cao cấp
> - Thiết kế tinh tế
> - Giá cả hợp lý

✅ **Sau:**
> Sản phẩm bền, nhìn lại đẹp. Chất liệu tốt, thiết kế gọn gàng, mà giá thì dễ chịu hơn mấy mẫu cùng phân khúc.

---

## Case 3 — Bình luận cảm ơn (khẩu ngữ)

**Tells:** B1 (thiếu tiểu từ), B4 (không viết tắt), B6 (xưng hô vô hồn)

❌ **Trước:**
> Cảm ơn bạn rất nhiều. Bài hướng dẫn của bạn rất chi tiết và dễ hiểu. Tôi đã làm theo và thành công.

✅ **Sau:**
> Cảm ơn ông nhiều nha, bài hướng dẫn chi tiết dễ hiểu phết. T làm theo dc luôn r đó.

---

## Case 4 — Phản hồi trên mạng xã hội (khẩu ngữ)

**Tells:** B2 (emoji template), B3 (cảm thán giả trân), B7 (nhịp quá mượt)

❌ **Trước:**
> Thật tuyệt vời! 😊 Đây là một ý tưởng vô cùng sáng tạo. 🎉 Tôi nghĩ rằng nó sẽ rất thành công. 🚀

✅ **Sau:**
> Ý tưởng này gắt thật. Kiểu này làm khéo lại ăn to á 🚀

---

## Case 5 — Giữ nguyên (không over-humanize)

**Mục đích:** kiểm skill KHÔNG phá câu đã ổn. Câu ngắn gọn, đúng register, không tell → để yên.

❌ **Trước (thực ra đã ổn):**
> Mai họp lúc 9h nhé, mọi người nhớ mang laptop.

✅ **Sau (gần như giữ nguyên):**
> Mai họp 9h nha, mn nhớ mang laptop.

---

## Case 6 — Bình luận kể chuyện (khẩu ngữ)

**Tells:** B8 (lúc nào cũng đủ chủ ngữ), B4 (không viết tắt), B6 (xưng hô vô hồn)
*Nền: mẫu thật trên Voz — người Việt lược chủ ngữ liên tục, xưng t/ông.*

❌ **Trước:**
> Tôi cũng từng gặp trường hợp như vậy. Tôi đã thử cách của bạn nhưng tôi không thành công. Tôi nghĩ rằng nó không phù hợp với tôi.

✅ **Sau:**
> T cũng từng gặp y chang. Thử cách của ông mà ko ăn thua. Chắc ko hợp với t r.

---

## Case 7 — Nghị luận xã hội (trang trọng, học đường)

**Tells:** A16 (mở bài văn mẫu), A18 (động từ văn học sáo + rule-of-three), A17 (kết bài kêu gọi đạo lý)
*Đây là kiểu văn học sinh nhờ ChatGPT viết — nhóm dùng humanizer đông nhất.*

❌ **Trước:**
> Từ xưa đến nay, lòng biết ơn luôn là một truyền thống quý báu của dân tộc ta. Lòng biết ơn nuôi dưỡng tâm hồn, bồi đắp nhân cách và thắp sáng những giá trị tốt đẹp. Vì vậy, mỗi chúng ta cần phải biết trân trọng và gìn giữ lòng biết ơn ngay từ hôm nay.

✅ **Sau:**
> Người Việt trọng chuyện biết ơn từ lâu, kiểu "ăn quả nhớ kẻ trồng cây". Biết ơn làm mình sống tử tế hơn, nghĩ cho người khác hơn. Nên đừng để nó thành lời nói suông — gọi cho ba mẹ tối nay cũng là một cách.

---

## Case 8 — Email công việc (trang trọng)

**Tells:** A20 (email calque), A19 (bị động thừa "được…bởi")
*Mở email kiểu "Tôi hy vọng email này tìm thấy bạn" là dịch sượng từ "I hope this email finds you well" — dấu hiệu AI rõ.*

❌ **Trước:**
> Kính gửi Anh/Chị, Tôi hy vọng email này tìm thấy bạn trong trạng thái tốt. Báo cáo đã được hoàn thành bởi đội ngũ của chúng tôi. Đừng ngần ngại liên hệ nếu có bất kỳ câu hỏi nào. Trân trọng.

✅ **Sau:**
> Dạ chào anh/chị, em gửi anh/chị bản báo cáo bên em vừa làm xong. Anh/chị xem có chỗ nào cần chỉnh thì nhắn em nhé. Em cảm ơn ạ.

---

## Case 9 — Bình luận Gen-Z (khẩu ngữ)

**Tells:** B9 (không chèn tiếng Anh), B1 (thiếu tiểu từ), B5 (sạch quá)

❌ **Trước:**
> Bộ phim này thực sự rất hay và tạo cảm giác tích cực. Tôi hoàn toàn đồng ý rằng nó rất đáng xem.

✅ **Sau:**
> phim này vibe ghê, hay thật sự á. real đáng xem luôn

---

## Case 10 — Post bán hàng Facebook (giữ ĐỊNH DẠNG)

**Tells:** A1 (mở bài bối cảnh), A5 (buzzword), A2 (không chỉ…mà còn), A19 (bị động thừa), A9 (bullet + "Dưới đây là"), A20 (calque "Đừng ngần ngại")
*Điểm chính: humanize giữ NHỊP XUỐNG DÒNG của post (không bóp phẳng thành cục), NHƯNG không tự chế thêm emoji. Input này KHÔNG có emoji → bản sửa cũng không. Rải emoji đều mỗi dòng chính là tell B2, lộ AI hơn.*

❌ **Trước:**
> Trong thời đại mà sức khỏe ngày càng được quan tâm, sản phẩm của chúng tôi ra đời nhằm mang đến giải pháp toàn diện cho bạn. Sản phẩm không chỉ được chiết xuất từ thiên nhiên mà còn được kiểm định bởi các chuyên gia hàng đầu. Dưới đây là những lợi ích nổi bật:
> - Tăng cường sức khỏe
> - Cải thiện làn da
> - Nâng cao tinh thần
>
> Đừng ngần ngại liên hệ với chúng tôi để được tư vấn một cách tận tình nhất!

✅ **Sau (giữ nhịp xuống dòng, KHÔNG chế emoji):**
> Dạo này ai cũng lo giữ sức khỏe, nên bên mình làm ra em này.
>
> Chiết xuất từ thiên nhiên, đã qua tay chuyên gia kiểm định đàng hoàng.
> Dùng đều một thời gian thấy rõ: người khỏe hơn, da đẹp lên, tinh thần cũng phấn chấn.
>
> Cần tư vấn gì cứ nhắn bên mình nha, tư vấn kỹ cho bạn.

*Hai điểm: (1) So Case 2 — Case 2 là content chèn trong bài viết → gộp văn liền; Case 10 là POST đứng riêng → giữ nhịp xuống dòng. (2) Input không có emoji nên bản sửa cũng không; nếu input đã có emoji thì giữ nhưng tỉa cho lệch, đừng rải đều mỗi dòng.*
