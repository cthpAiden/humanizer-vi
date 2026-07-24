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

---

## Case 11 — Giới thiệu bản thân trong CV (trang trọng)

**Tells:** A27 (tự khen không bằng chứng), A11 (câu đều nhịp), A13 (chung chung)
*Điểm chính: input không có sẵn số liệu/thành tích thật → bản sửa KHÔNG được bịa thêm số ("tăng doanh số 20%" chẳng hạn) để nghe thuyết phục hơn. Chỉ đổi tính từ liệt kê thành mô tả hành vi, vẫn giữ mức chung chung vốn có của bản gốc — không tự nâng cấp nội dung.*

❌ **Trước:**
> Tôi là một người năng động, hòa đồng và có tinh thần trách nhiệm cao trong công việc. Tôi luôn chủ động học hỏi những kiến thức mới và có khả năng làm việc nhóm tốt. Ngoài ra, tôi cũng có khả năng chịu được áp lực công việc cao và luôn hoàn thành tốt các nhiệm vụ được giao.

✅ **Sau:**
> Tôi thích làm việc nhóm và chủ động hỏi ngay khi chưa rõ việc. Việc gấp tôi vẫn cố làm cho xong đúng hạn, và sẵn sàng học thêm cái mới khi công việc cần.

---

## Case 12 — Nhắn tin phàn nàn shop (khẩu ngữ, cảm xúc bực)

**Tells:** B8 (đủ chủ ngữ), B1 (thiếu tiểu từ), B7 (nhịp quá mượt) + nhấn cảm xúc mạnh (mới, xem KHO)
*Điểm chính: AI viết than phiền mà vẫn lịch sự đều đều, mất chất "đang bực thật". Người thật khi giận hay lặp từ, dồn dấu câu, viết hoa vài chữ để nhấn — khác hẳn kiểu kéo dài dễ thương (Gen-Z vui) đã có sẵn trong KHO.*

❌ **Trước:**
> Trời ơi hôm nay mình gặp chuyện bực mình ghê. Mình đặt hàng mà giao trễ tận 3 ngày so với dự kiến. Mình đã nhắn shop hỏi nhưng đợi mãi mới thấy trả lời. Mình thấy khá thất vọng về dịch vụ lần này.

✅ **Sau:**
> Trời ơi bực ghê, đặt hàng mà trễ những 3 ngày lận. Nhắn shop hỏi thì đợi hoài đợi hoài mới thấy rep. THẤT VỌNG thiệt sự luôn á.

---

## Case 13 — Caption du lịch mạng xã hội (register lẫn: câu đầy đủ + "mình" + emoji thưa)

**Tells:** A14 (khuôn "không...mà là" lặp 2 lần), A15 (một ý nhắc lại 3 lần)
*Điểm chính: đây là ca thật do người dùng đưa vào test, không phải tự tạo. Bắt được lỗi tự-kiểm thật: bản nháp đầu tay sửa được câu A14 thứ nhất nhưng QUÊN câu thứ hai dùng chung khuôn — đúng thứ mục self-check mới thêm ở QUY TRÌNH bước 5 nhắm tới. Register lẫn (câu đầy đủ, không tiểu từ, nhưng có "mình" + 2 emoji thưa) → giữ nguyên mức đó, không kéo hẳn về trang trọng hay khẩu ngữ.*

❌ **Trước:**
> 🌿 Ngắm một nơi đẹp, tự nhiên thấy lòng nhẹ hơn.
>
> Có những khung cảnh không cần quá nổi tiếng, cũng chẳng cần phải chỉnh màu thật nhiều. Chỉ cần bầu trời trong, vài tia nắng xuyên qua tán cây, mặt nước lặng và một cơn gió vừa đủ cũng đủ khiến mọi thứ chậm lại.
>
> Đôi khi, điều khiến một nơi trở nên đáng nhớ không nằm ở việc nó đẹp đến mức nào, mà là cảm giác bình yên nó mang lại. Đứng giữa thiên nhiên, hít một hơi thật sâu và tạm quên những bộn bề thường ngày, mình mới nhận ra có những khoảnh khắc đơn giản lại đáng giá hơn rất nhiều.
>
> Nếu có dịp, hãy dành thời gian đi đến một nơi bạn chưa từng ghé qua. Biết đâu, điều bạn mang về không phải là vài bức ảnh đẹp, mà là một tâm trạng tốt hơn.
>
> 📍 Mỗi chuyến đi đều có một câu chuyện. Còn bạn, nơi nào khiến bạn muốn quay lại nhiều lần nhất?

✅ **Sau:**
> 🌿 Ngắm một nơi đẹp, tự nhiên thấy lòng nhẹ hơn.
>
> Cảnh cũng không cần nổi tiếng hay chỉnh màu gì nhiều. Chỉ cần bầu trời trong, vài tia nắng xuyên qua tán cây, mặt nước lặng, thêm cơn gió vừa đủ, vậy là đủ khiến mọi thứ chậm lại.
>
> Đứng giữa thiên nhiên, hít một hơi thật sâu, tạm quên hết bộn bề thường ngày, mình mới nhận ra cái đáng nhớ ở một nơi không nằm ở chuyện nó đẹp cỡ nào, mà là cảm giác bình yên nó mang lại.
>
> Có dịp thì cứ thử đến một nơi chưa từng ghé. Biết đâu cái mang về hóa ra lại là một tâm trạng nhẹ nhõm hơn, chứ không phải vài tấm ảnh đẹp.
>
> 📍 Mỗi chuyến đi đều có một câu chuyện riêng. Còn bạn, nơi nào khiến bạn muốn quay lại nhiều lần nhất?

*Lưu ý thêm: câu hỏi đóng ("Còn bạn... quay lại nhiều lần nhất?") KHÔNG phải tell — CTA mời tương tác là kỹ thuật content thật, người viết content thật cũng làm vậy. Để nguyên gần như y hệt.*

---

## Case 14 — Nhắn tin nhờ giúp đỡ, ĐÚNG mức thân (khẩu ngữ vừa phải)

**Tells:** B4 (không viết tắt), B6 (xưng hô cứng), B1 (thiếu tiểu từ)
*Điểm chính: đây là bản SỬA LẠI sau feedback người dùng — bản đầu dùng "tớ/cậu" + viết tắt "dc" bị chê sến/quá tay cho ngữ cảnh nhờ vả người không rõ độ thân. Casual không phải nhị phân: nhờ vả thì khẩu ngữ vừa phải (mình/bạn, tiểu từ thưa, KHÔNG cần viết tắt) mới tự nhiên, không phải cứ khẩu ngữ là kéo hết cỡ.*

❌ **Trước:**
> Chào bạn, tôi muốn nhờ bạn một việc. Tôi đang cần gấp một số tài liệu về marketing để hoàn thành báo cáo, không biết bạn có thể chia sẻ giúp tôi được không? Nếu bạn không có thời gian thì cũng không sao, tôi sẽ tìm cách khác. Cảm ơn bạn rất nhiều.

✅ **Sau:**
> Chào bạn, mình có việc này muốn nhờ chút. Mình đang cần gấp vài tài liệu marketing để làm báo cáo, bạn chia sẻ giúp mình được không? Không tiện thì thôi cũng được, mình tìm cách khác. Cảm ơn bạn nhiều nha.

*So với bản sửa sai trước đó: xưng "mình/bạn" thay "tớ/cậu" (đỡ sến), viết đủ chữ "được" thay "dc" (viết tắt là tùy chọn, không bắt buộc) — vẫn casual nhờ tiểu từ (chút, nha) và nhịp buông tự nhiên ("Không tiện thì thôi cũng được"), không cần abbreviation mới casual được.*

---

## Case 15 — Bài suy ngẫm về thiên nhiên/du lịch (trang trọng, DÀY tell)

**Tells:** A2 (không chỉ…mà còn, lặp 2 lần), A25 (danh-từ-hóa việc/sự, nhiều chỗ), A10 (rule-of-three LẶP KHUÔN 3 lần liên tiếp — ca nặng nhất bắt được), A14 (false range "từ…cho đến"), A3 ("Bên cạnh việc"), A4 ("Có thể khẳng định rằng"), A18 ("nuôi dưỡng" sáo văn học), A15 (lặp "nâng cao chất lượng" / "mở rộng" giữa các đoạn), A11 (nhịp đều toàn bài)
*Điểm chính: đoạn dày tell nhất từng test — không chỉ nhiều LOẠI tell mà rule-of-three (A10) lặp lại ĐÚNG KHUÔN 3 lần ở 3 đoạn khác nhau (mở rộng góc nhìn/tái tạo/tìm cảm hứng — không gian/âm thanh/không khí — mở rộng hiểu biết/nuôi dưỡng/tạo động lực). Sửa: giữ NGUYÊN khuôn liệt kê ở đoạn 1, phá khuôn ở đoạn 2 (gộp thành câu văn xuôi) và đoạn 3 (đổi sang liệt kê kiểu khác, "X hơn một chút") — vừa cắt lặp khuôn vừa giữ đủ thông tin.*

❌ **Trước:**
> Thiên nhiên luôn mang đến những giá trị đặc biệt, không chỉ về mặt thẩm mỹ mà còn góp phần nâng cao chất lượng trải nghiệm và cân bằng cảm xúc trong cuộc sống hiện đại. Việc dành thời gian khám phá những cảnh quan đẹp là cơ hội để mỗi người mở rộng góc nhìn, tái tạo năng lượng và tìm kiếm nguồn cảm hứng mới sau những áp lực thường ngày.
>
> Mỗi địa điểm đều sở hữu những nét đặc trưng riêng, từ cảnh quan thiên nhiên, điều kiện khí hậu cho đến giá trị văn hóa bản địa. Chính sự đa dạng này tạo nên sức hấp dẫn của mỗi hành trình, đồng thời mang lại những trải nghiệm khác biệt cho từng cá nhân. Bên cạnh việc lưu giữ những khoảnh khắc đáng nhớ thông qua hình ảnh, việc trực tiếp cảm nhận không gian, âm thanh và bầu không khí của điểm đến sẽ giúp chuyến đi trở nên trọn vẹn hơn.
>
> Có thể khẳng định rằng, khám phá cảnh đẹp không chỉ đơn thuần là một hoạt động du lịch mà còn là một hình thức nâng cao chất lượng cuộc sống. Mỗi hành trình đều góp phần mở rộng hiểu biết, nuôi dưỡng cảm xúc tích cực và tạo động lực để tiếp tục khám phá những điểm đến mới trong tương lai.

✅ **Sau:**
> Thiên nhiên luôn mang lại giá trị đặc biệt, không chỉ đẹp mà còn giúp cuộc sống hiện đại bớt ngột ngạt, cảm xúc cũng cân bằng hơn. Dành thời gian khám phá cảnh đẹp là dịp để mở rộng góc nhìn, nạp lại năng lượng và tìm cảm hứng mới sau những ngày áp lực.
>
> Mỗi địa điểm đều có nét riêng: cảnh quan, khí hậu, văn hóa bản địa mỗi nơi mỗi khác. Khác biệt đó làm nên sức hút riêng của từng hành trình, và mỗi người cũng cảm nhận theo cách của mình. Ảnh chụp giữ lại được khoảnh khắc, nhưng đứng giữa không gian đó, nghe âm thanh và hít thở bầu không khí thật mới là thứ khiến chuyến đi trọn vẹn.
>
> Khám phá cảnh đẹp vì vậy không đơn thuần là đi du lịch, mà là một cách để sống chất lượng hơn. Mỗi chuyến đi đều để lại điều gì đó: hiểu biết rộng hơn một chút, cảm xúc tích cực hơn một chút, và động lực để lần sau lại tiếp tục lên đường.
