# Toolkit — Từ Evidence Đến Build Slice

**Học viên:** Dương Đức Cường — 2A202600794  
**Ngày:** 03/06/2026

---

## 1. Gom evidence thành cụm

Gom theo **workflow/pain**, không gom theo tên feature.

| Cụm | Evidence thuộc về |
|---|---|
| **"AI đưa nhận xét sai khi data thiếu" (False Positive)** | Test #9: khen "kiểm soát tốt" khi 0đ; Test #3: kết luận "mở ví nhiều hơn" khi so sánh 45k vs 0đ. |
| **"Moni mù data ngoài MoMo, không disclaimer"** | Test #1: 0đ ăn uống; Test #2: 0đ tháng này; Test #9: 0đ tổng hợp. Tất cả không disclaimer nguồn data. |
| **"Hành vi không nhất quán khi data thiếu"** | Test #2 (khuyên ghi chép — tốt) mâu thuẫn với Test #9 (khen kiểm soát tốt — nguy hiểm). Cùng input 0đ nhưng output khác nhau. |
| **"Lời khuyên generic, không cá nhân hoá"** | Test #7: tư vấn trả nợ bằng 4 bước generic, không dùng data chi tiêu cá nhân. |
| **"Correction path gãy"** | Test #8: yêu cầu mã giao dịch khi user muốn sửa — quá phức tạp. |
| **"Moni hiểu context khi user nói rõ (điểm tốt)"** | Test #4: phân loại đúng "Ăn uống" khi user nói "trả tiền ăn tối"; Test #6: giải thích "chi tiêu linh tinh" rõ ràng. |

---

## 2. Viết insight

```text
User trẻ Việt Nam chi tiêu đa kênh (MoMo + tiền mặt + ngân hàng)
không chỉ cần một AI phân tích chi tiêu nhanh.
Họ thật ra cần một trợ thủ tài chính TRUNG THỰC VỀ GIỚI HẠN DỮ LIỆU,
vì evidence từ 8 bài test cho thấy:
  - AI đưa nhận xét tích cực sai lệch ("kiểm soát tốt") khi data = 0,
  - AI so sánh, kết luận dựa trên data thiếu mà không cảnh báo,
  - Hành vi không nhất quán: cùng data 0đ, lúc khuyên ghi chép lúc khen,
  - Lời khuyên tài chính generic dù đã có data cá nhân,
  - User không sửa được lỗi phân loại dễ dàng.
Vấn đề cốt lõi: AI "mù" data ngoài MoMo VÀ không trung thực về sự mù đó.
```

---

## 3. Viết opportunity

```text
Cơ hội là dùng AI để augment quá trình phân tích chi tiêu:
  - Phát hiện khoảng trống dữ liệu bất thường
    (ví dụ: 0đ ăn uống 14 ngày, tổng chi tiêu 0đ cả tháng),
  - Disclaimer nguồn dữ liệu ở MỌI kết quả phân tích,
  - Proactive hỏi user bổ sung chi tiêu ngoài MoMo,
  - KHÔNG đưa nhận xét đánh giá khi data không đủ cơ sở (ngăn false positive),
giúp user có bức tranh tài chính đáng tin cậy hơn,
trong khi vẫn kiểm soát rủi ro user đưa quyết định tài chính
dựa trên thông tin sai lệch từ AI.
```

---

## 4. Chọn build slice

Build slice đã qua 5 câu hỏi kiểm tra:

| Câu hỏi | Đánh giá |
|---|---|
| **User cụ thể chưa?** | ✅ Người dùng MoMo trẻ (18-25), sinh viên/mới đi làm, chi tiêu đa kênh (MoMo chỉ là phần nhỏ, chủ yếu tiền mặt + chuyển khoản ngân hàng). |
| **Task đủ hẹp chưa?** | ✅ Một task: hỏi Moni phân tích chi tiêu → AI kiểm tra data → trả kết quả có disclaimer + prompt bổ sung nếu phát hiện khoảng trống + KHÔNG nhận xét đánh giá khi data thiếu. Demo 3-5 phút. |
| **AI decision rõ chưa?** | ✅ AI quyết định: (1) data đủ hay thiếu? (2) nên disclaimer + hỏi bổ sung hay trả kết quả bình thường? (3) có đủ cơ sở để đưa nhận xét đánh giá không? → Augmentation: AI gợi ý, user quyết. |
| **Failure path rõ chưa?** | ✅ Case 1: AI nhầm khoảng trống hợp lệ (user thật sự không chi tiêu) → hỏi liên tục → phiền. Case 2: AI không phát hiện khoảng trống (data ít nhưng có vẻ đủ). |
| **Có evidence không?** | ✅ 9 screenshot self-use + review public + MoMo support page + 3 competitor analogs. |

---

## 5. Quyết định: giữ, giảm scope, hay đổi hướng?

| Tình huống | Quyết định |
|---|---|
| Evidence yếu? | Không — có 9 screenshot evidence từ self-use + public review + support page. |
| Ý tưởng quá rộng? | Không — đã cắt xuống một flow duy nhất: phân tích chi tiêu + phát hiện khoảng trống + ngăn false positive. |
| AI không cần thiết? | Cần — phát hiện khoảng trống cần AI phân tích pattern chi tiêu. Quyết định "đủ data hay thiếu?" cần intelligence. |
| Rủi ro cao? | Trung bình — chọn augmentation (AI hỏi, user quyết). Rủi ro chính: false positive nếu không ngăn được. |
| Demo được trong 1 ngày? | ✅ Có — prototype chatbot flow đơn giản thể hiện 4 paths. |

**Quyết định: GIỮ build slice, không cần giảm scope.**

---

## 6. Câu chốt cuối

```text
Dựa trên evidence từ 8 bài test thực tế với Moni
(đặc biệt: Moni khen "kiểm soát chi tiêu rất tốt" khi user 0đ chi tiêu qua MoMo
nhưng thực tế chi tiêu hàng ngày bằng tiền mặt — false positive nguy hiểm),
nhóm sẽ build prototype cải thiện flow phân tích chi tiêu,
cho người dùng MoMo trẻ chi tiêu đa kênh (chủ yếu ngoài MoMo),
để giải quyết pain "AI đưa nhận xét đánh giá sai lệch khi data không đủ",
bằng cách AI phát hiện khoảng trống dữ liệu,
disclaimer nguồn data, proactive hỏi user bổ sung,
và KHÔNG đưa nhận xét đánh giá khi chưa đủ cơ sở,
và sẽ test failure path: AI nhầm khoảng trống hợp lệ (user thật sự không chi tiêu)
với khoảng trống do thiếu data → hỏi user liên tục gây phiền.
```

---

## 7. Backlog

Những thứ **không build trong Day 06**:

- Tích hợp API ngân hàng để tự động lấy giao dịch ngoài MoMo (cần đối tác, không khả thi 1 ngày).
- Cá nhân hoá lời khuyên tài chính dựa trên data chi tiêu thực (ví dụ: tư vấn trả nợ kết hợp phân tích chi tiêu) — cần model phức tạp hơn.
- Sửa correction path trong chatbot: AI tự tìm giao dịch khớp mô tả → user xác nhận → sửa danh mục inline.
- Điều chỉnh tone giọng Moni theo context tài chính (vui vẻ khi user ổn, nghiêm túc khi user khó khăn).
