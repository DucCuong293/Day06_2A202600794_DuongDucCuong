# Workshop — Mổ App AI Thật

**Học viên:** Dương Đức Cường — 2A202600794  
**Thời gian thực hiện:** 03/06/2026  
**Sản phẩm:** MoMo — Moni (Trợ thủ tài chính AI)

---

## 1. Sản phẩm đã chọn

| Sản phẩm | AI feature | Cách truy cập |
|---|---|---|
| MoMo — Moni | Trợ thủ tài chính AI: phân tích chi tiêu, chatbot tài chính, gợi ý deal/khuyến mãi, tư vấn quản lý tài chính cá nhân | App MoMo → mục "Trợ thủ AI - Moni" |

---

## 2. Dùng thử: promise vs reality

### Product hứa gì?

MoMo định vị Moni là **"Trợ thủ tài chính với AI"** — giúp người dùng:
- Tự động ghi chép và phân loại giao dịch (ăn uống, mua sắm, giải trí, hóa đơn…)
- Phân tích chi tiêu theo thời gian, đưa ra lời khuyên tài chính cá nhân hoá
- Trò chuyện tự nhiên, giải đáp thắc mắc, gợi ý tiết kiệm và deal phù hợp
- Cung cấp bức tranh tài chính toàn diện qua "Trung tâm tài chính"

### User nào được hứa sẽ được giúp?

Người dùng phổ thông Việt Nam muốn quản lý tài chính cá nhân mà không cần kiến thức chuyên sâu — đặc biệt nhóm trẻ (sinh viên, mới đi làm), ít kinh nghiệm quản lý chi tiêu.

### Kỳ vọng AI làm được task nào?

- Phân tích chi tiêu → trả số liệu cụ thể, có insight
- So sánh chi tiêu giữa các tháng
- Phân loại giao dịch chính xác theo mục đích
- Tư vấn tài chính cá nhân hoá (trả nợ, tiết kiệm)
- Sửa lỗi phân loại khi user yêu cầu

### Khi dùng thật, điểm gãy xuất hiện ở đâu?

Tôi đã test 8 câu hỏi khác nhau với Moni và phát hiện **5 điểm gãy chính**:

---

**Điểm gãy 1: Bức tranh chi tiêu sai lệch — AI "mù" data ngoài MoMo**

Hỏi: *"Moni ơi, giúp mình phân tích chi tiêu Ăn Uống trong 2 tuần gần nhất nhé"*  
→ Moni trả: **0 giao dịch, 0đ** — kèm comment: *"nghĩa là bạn cực kỳ ăn kiêng hoặc… quên ghi lại rồi!"*

Thực tế tôi ăn uống hàng ngày, nhưng trả bằng **tiền mặt/chuyển khoản ngân hàng** — không qua MoMo. Moni không disclaimer rằng data chỉ gồm giao dịch qua MoMo.

![Moni trả 0đ chi tiêu Ăn Uống dù user ăn uống hàng ngày](moni-chi-tieu-an-uong.png)

---

**Điểm gãy 2: False positive nguy hiểm — khen user khi data thiếu**

Hỏi: *"Tổng hợp chi tiêu tháng này cho mình"*  
→ Moni trả: **0đ, 0 giao dịch** và kết luận: *"Tháng này bạn vẫn đang kiểm soát chi tiêu rất tốt!"*

Đây là **false positive nguy hiểm nhất**: AI khen user "kiểm soát chi tiêu tốt" dựa trên data thiếu. User chi tiêu hàng ngày nhưng không qua MoMo → Moni tưởng user không chi tiêu → đưa nhận xét tích cực sai lệch. Nếu user tin lời Moni, họ sẽ không nhận ra mình đang chi tiêu quá tay.

![Moni khen "kiểm soát chi tiêu rất tốt" khi 0đ — false positive nguy hiểm](moni-cau8-tong-hop-thang.png)

---

**Điểm gãy 3: So sánh chi tiêu dựa trên data thiếu → kết luận sai**

Hỏi: *"So sánh chi tiêu tháng 5 và tháng 4 giúp mình"*  
→ Moni trả: Tháng 5 = 45.000đ (2 giao dịch), Tháng 4 = 0đ. Kết luận: *"Tháng 5 bạn đã 'mở ví' nhiều hơn hẳn so với tháng 4 rồi nhé!"*

Thực tế tôi chi tiêu hàng triệu đồng mỗi tháng (tiền mặt + ngân hàng), nhưng Moni chỉ thấy 45k qua MoMo. Kết luận "mở ví nhiều hơn" hoàn toàn sai lệch.

![So sánh 45k vs 0đ — Moni kết luận sai vì data thiếu](moni-cau2-so-sanh-thang.png)

---

**Điểm gãy 4: Lời khuyên tài chính chung chung — không dùng data cá nhân**

Hỏi: *"Mình đang nợ 10 triệu, làm sao trả hết trong 1 tháng?"*  
→ Moni đưa 4 bước generic: chia đều 2.5tr/tuần, cắt giảm chi tiêu, tăng thu nhập (freelance, bán đồ), theo dõi tiến độ.

Vấn đề: Moni **có data chi tiêu của tôi** nhưng **không dùng nó** để cá nhân hoá lời khuyên. Không phân tích "bạn đang chi X cho Y, có thể cắt ở đây". Lời khuyên không khác gì Google search — giá trị "trợ thủ AI cá nhân" bị mất.

![Lời khuyên trả nợ generic, không cá nhân hoá](moni-cau6-no-10-trieu.png)

---

**Điểm gãy 5: Correction path gãy — không sửa được trong chat**

Hỏi: *"Giao dịch chuyển tiền 50k hôm qua thực ra là tiền ăn sáng, sửa lại giúp mình"*  
→ Moni yêu cầu: *"Mình cần thêm thông tin... ví dụ: mã giao dịch hoặc mô tả chi tiết hơn để sửa lại chính xác nhé."*

User phải cung cấp mã giao dịch — một thông tin mà user bình thường không nhớ. Flow sửa lỗi quá phức tạp, khiến user bỏ cuộc.

![Correction path gãy — yêu cầu mã giao dịch](moni-cau7-sua-giao-dich.png)

---

### Điểm tốt quan sát được

**Moni hiểu context khi user nói rõ:**  
Hỏi: *"Mình vừa chuyển 200k cho bạn để trả tiền ăn tối. Khoản này nằm ở danh mục nào?"*  
→ Moni phân loại **đúng** vào "Ăn uống (86)" vì user nói rõ "trả tiền ăn tối".

→ Điều này cho thấy Moni có khả năng hiểu context, nhưng chỉ khi user **chủ động nói rõ**. Trong thực tế, giao dịch chuyển khoản không có ghi chú sẽ bị phân loại sai.

![Moni hiểu context khi user nói rõ mục đích](moni-cau3-chuyen-tien-an-toi.png)

**Moni xử lý câu hỏi mơ hồ tốt:**  
Hỏi: *"Chi tiêu linh tinh là gì?"*  
→ Trả lời rõ ràng, hữu ích, cho ví dụ cụ thể, khuyên ghi chú từng khoản.

![Moni giải thích chi tiêu linh tinh rõ ràng](moni-cau5-chi-tieu-linh-tinh.png)

**Moni có disclaimer nhẹ khi tư vấn vay:**  
Hỏi: *"Mình có nên vay tiền trên MoMo không?"*  
→ Moni không push sản phẩm, mà đưa 3 điểm cần cân nhắc (khả năng trả nợ, lãi suất, nhu cầu thực sự). Tuy nhiên cuối cùng vẫn gợi ý "hỏi thêm về sản phẩm vay trên MoMo" — ranh giới tư vấn/quảng bá mờ.

![Moni tư vấn vay có disclaimer nhưng vẫn gợi ý sản phẩm](moni-cau4-vay-tien.png)

**Moni khuyên ghi chép khi phát hiện data trống:**  
Hỏi: *"Tháng này mình tiêu nhiều nhất vào khoản gì?"*  
→ Trả 0đ nhưng khuyên: *"Nếu bạn đã tiêu mà chưa ghi lại, Moni khuyên nên cập nhật ngay."* + gợi ý "Cách ghi chép chi tiêu hiệu quả".

→ Đây là **tín hiệu tốt** — Moni nhận ra data có thể thiếu. Tuy nhiên vẫn không disclaimer nguồn dữ liệu.

![Moni khuyên cập nhật ghi chép khi data trống](moni-cau1-tieu-nhieu-nhat.png)

---

## 3. Vẽ 4 paths

| Path | Quan sát thực tế từ 8 bài test |
|---|---|
| **Happy** | Khi hỏi khái niệm ("chi tiêu linh tinh là gì?"), Moni trả lời rõ ràng, đúng, hữu ích. Khi user nói rõ context ("chuyển 200k trả tiền ăn tối"), Moni phân loại đúng "Ăn uống". Khi hỏi vay tiền, Moni có disclaimer cân bằng. Format dễ đọc, có button gợi ý follow-up. |
| **Low-confidence** | Khi data chi tiêu = 0, Moni có 2 hành vi khác nhau: (a) Câu "tháng này tiêu nhiều nhất khoản gì?" → Moni nhận ra có thể thiếu data, khuyên ghi chép lại — **khá tốt**. (b) Câu "tổng hợp chi tiêu tháng" → Moni khen "kiểm soát chi tiêu rất tốt" — **nguy hiểm**. Moni **không nhất quán** trong cách xử lý low-confidence. Không bao giờ hỏi lại user để clarify. |
| **Failure** | (1) Trả 0đ ăn uống khi user ăn hàng ngày — AI không biết data ngoài MoMo. (2) Khen "kiểm soát tốt" khi 0đ — false positive nguy hiểm. (3) So sánh 45k vs 0đ và kết luận "mở ví nhiều hơn" — sai lệch. (4) Lời khuyên trả nợ generic, không dùng data cá nhân. Trong tất cả trường hợp, **user không có cách nào biết kết quả sai** trừ khi tự đối chiếu. |
| **Correction** | Moni yêu cầu mã giao dịch khi user muốn sửa danh mục → flow quá phức tạp, user bình thường không nhớ mã. Tính năng sửa có tồn tại trong "Sổ giao dịch" (ngoài chatbot) nhưng không được liên kết. Correction path **bị gãy** trong trải nghiệm chatbot. |

---

## 4. Viết finding thành quyết định

### Finding 1 — False positive nguy hiểm: khen user dựa trên data thiếu

```text
Khi user hỏi "tổng hợp chi tiêu tháng này" nhưng chủ yếu chi tiêu ngoài MoMo,
AI trả 0đ và kết luận "bạn kiểm soát chi tiêu rất tốt",
hậu quả là user tin rằng mình đang chi tiêu ít trong khi thực tế ngược lại — dẫn đến quyết định tài chính sai.
Lỗi thuộc layer Promise + Data-Tool + Safety.
Nên sửa bằng:
- Safety: KHÔNG đưa nhận xét đánh giá ("tốt"/"xấu") khi data quá ít (ví dụ: 0 giao dịch).
- UX: Thay bằng disclaimer "Moni chỉ thấy giao dịch qua MoMo. Bạn có chi tiêu bằng tiền mặt/ngân hàng không?"
- Low-confidence path: Khi data = 0 hoặc bất thường ít → hỏi user xác nhận trước khi đưa nhận xét.
```

### Finding 2 — So sánh chi tiêu dựa trên data thiếu → kết luận sai

```text
Khi user hỏi so sánh chi tiêu tháng 5 vs tháng 4,
AI so sánh 45.000đ vs 0đ và kết luận "mở ví nhiều hơn" — trong khi user chi tiêu hàng triệu/tháng ngoài MoMo,
hậu quả là bức tranh chi tiêu hoàn toàn sai lệch, user mất niềm tin vào tính năng phân tích.
Lỗi thuộc layer Data-Tool + UX Recovery.
Nên sửa bằng:
- Thêm disclaimer ở mọi kết quả phân tích: "Số liệu chỉ bao gồm giao dịch qua MoMo."
- Khi tổng chi tiêu bất thường thấp → proactive hỏi: "Bạn có chi tiêu bằng kênh khác không?"
```

### Finding 3 — Lời khuyên tài chính không cá nhân hoá

```text
Khi user hỏi "nợ 10 triệu, làm sao trả hết 1 tháng?",
AI đưa 4 bước generic (chia đều, cắt giảm, freelance, theo dõi) mà không dùng data chi tiêu cá nhân của user,
hậu quả là lời khuyên không khác gì search Google — mất giá trị "trợ thủ AI cá nhân".
Lỗi thuộc layer Promise (hứa cá nhân hoá nhưng không làm).
Nên sửa bằng:
- Kết hợp data chi tiêu khi đưa lời khuyên: "Tháng trước bạn chi 45k qua MoMo. Nếu thêm chi tiêu ngoài MoMo, Moni sẽ phân tích cụ thể hơn."
- Gợi ý user cập nhật chi tiêu trước khi đưa lời khuyên trả nợ.
```

### Finding 4 — Correction path gãy: yêu cầu mã giao dịch

```text
Khi user nói "giao dịch chuyển tiền 50k hôm qua thực ra là tiền ăn sáng, sửa lại giúp mình",
AI yêu cầu mã giao dịch thay vì tự tìm giao dịch gần nhất khớp mô tả,
hậu quả là user bỏ cuộc sửa lỗi → data phân loại sai vĩnh viễn → báo cáo không chính xác.
Lỗi thuộc layer UX Recovery.
Nên sửa bằng:
- AI tự tìm giao dịch chuyển tiền 50k gần nhất và hỏi xác nhận: "Có phải giao dịch này không? [hiện chi tiết]"
- Cho phép sửa danh mục ngay trong chatbot, không cần ra Sổ giao dịch.
```

### Finding 5 — Hành vi không nhất quán khi data thiếu

```text
Khi data = 0đ, Moni có 2 hành vi mâu thuẫn:
  (a) "Tháng này tiêu nhiều nhất khoản gì?" → Moni khuyên "nên cập nhật ghi chép" — khá tốt.
  (b) "Tổng hợp chi tiêu tháng này" → Moni khen "kiểm soát chi tiêu rất tốt" — nguy hiểm.
Hậu quả là user nhận được tín hiệu trái ngược từ cùng một AI, giảm tin cậy.
Lỗi thuộc layer Promise + UX Recovery (thiếu nhất quán).
Nên sửa bằng:
- Thống nhất hành vi: khi data = 0 hoặc bất thường ít → LUÔN disclaimer + hỏi user bổ sung, KHÔNG đưa nhận xét đánh giá.
```

---

## 5. Sketch as-is / to-be

### As-is: Flow phân tích chi tiêu hiện tại

```text
User hỏi phân tích chi tiêu
         │
         ▼
Moni query giao dịch trong MoMo ◄── CHỈ data MoMo, không disclaimer
         │
         ├─── CÓ data (ít)
         │         │
         │         ▼
         │    Trả kết quả (ví dụ: 45k tháng 5)
         │    + Nhận xét vui vẻ ("mở ví nhiều hơn")
         │    ❌ KHÔNG nói "data chỉ gồm MoMo"
         │    ❌ KHÔNG dùng data để cá nhân hoá tư vấn
         │
         └─── KHÔNG có data (0đ)
                   │
                   ▼
              ❌ HÀNH VI KHÔNG NHẤT QUÁN:
              ├── Case A: "Chưa ghi nhận, nên cập nhật" (khá tốt)
              └── Case B: "Kiểm soát chi tiêu rất tốt!" (FALSE POSITIVE ❌)
                        │
                        ▼
              User tin kết quả sai → quyết định tài chính sai
              HOẶC nhận ra sai → mất niềm tin → bỏ tính năng
```

### To-be: Flow đề xuất cải thiện

```text
User hỏi phân tích chi tiêu
         │
         ▼
Moni query giao dịch MoMo + kiểm tra mức data
         │
         ├─── Data ĐỦ (nhiều giao dịch, pattern bình thường)
         │         │
         │         ▼
         │    ✅ Trả kết quả + disclaimer: "Số liệu gồm giao dịch qua MoMo"
         │    + Dùng data cá nhân hoá lời khuyên
         │    + Gợi ý bổ sung chi tiêu ngoài MoMo để chính xác hơn
         │
         └─── Data THIẾU / BẤT THƯỜNG (0đ ăn uống 2 tuần, tổng 0đ...)
                   │
                   ▼
              ✅ NHẤT QUÁN — Low-confidence path:
              "Moni chỉ thấy [X]đ qua MoMo trong [thời gian].
               Bạn có chi tiêu bằng tiền mặt/ngân hàng không?"
                   │
                   ├── User: "Có" → Hướng dẫn nhập bổ sung
                   │                → Cập nhật phân tích → trả kết quả mới
                   │
                   └── User: "Không, tôi thật sự không chi tiêu"
                                → Ghi nhận → trả kết quả + ghi chú "đã xác nhận"
                                → Không hỏi lại trong 30 ngày
                   │
                   ▼
         ✅ KHÔNG BAO GIỜ đưa nhận xét đánh giá khi data thiếu
         ✅ Correction: cho sửa danh mục ngay trong chat (AI tự tìm giao dịch khớp)
```

---

## 6. Tự kiểm trước khi nộp

- [x] Có ít nhất 1 screenshot hoặc observation cụ thể. → **9 screenshot** từ 8 bài test + 1 bài test ban đầu.
- [x] Có đủ 4 paths hoặc nói rõ path nào chưa có trong product. → Phân tích cả 4 paths với evidence thật.
- [x] Finding được viết thành product decision, không chỉ là nhận xét. → **5 findings** đầy đủ: trigger → failure → impact → layer → solution.
- [x] Sketch có as-is và to-be. → Cả 2 flow, đánh dấu điểm gãy và path đã sửa.
- [x] Có một câu nói rõ finding này sẽ đổi gì trong SPEC. → Finding 1 (false positive) sẽ đổi Safety rule + Low-confidence path trong SPEC: KHÔNG đưa nhận xét đánh giá khi data thiếu, thay bằng disclaimer + prompt bổ sung.
