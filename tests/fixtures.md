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
