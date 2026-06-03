# Template — Thin SPEC Cuối Day 05

**Học viên:** Dương Đức Cường — 2A202600794  
**Ngày:** 03/06/2026

---

## 1. Track, product/app và user

**Track:** Fintech / Quản lý tài chính cá nhân  
**Product/app thật:** MoMo — Moni (Trợ thủ tài chính AI)  
**User cụ thể:** Người dùng MoMo trẻ (18-25 tuổi), sinh viên hoặc mới đi làm, chi tiêu đa kênh: MoMo chỉ chiếm phần nhỏ, phần lớn chi tiêu bằng tiền mặt và chuyển khoản ngân hàng. Muốn quản lý tài chính nhưng chưa chuyển hết giao dịch sang MoMo.  
**Nhóm có phải user thật không?** Có. Bản thân là sinh viên, dùng MoMo nhưng chủ yếu chi tiêu tiền mặt và chuyển khoản ngân hàng. Trải nghiệm self-use (8 bài test) phản ánh đúng pain thật — Moni khen "kiểm soát chi tiêu rất tốt" khi thực tế chi tiêu hàng ngày bằng tiền mặt.

---

## 2. Evidence summary

| Evidence | Nguồn | User/pain nói lên điều gì? | SPEC phải đổi gì? |
|---|---|---|---|
| Moni khen "kiểm soát chi tiêu rất tốt" khi 0đ, 0 giao dịch tháng 6. User thực tế chi tiêu hàng ngày bằng tiền mặt. | Self-use test #9, screenshot | **False positive nguy hiểm**: AI đưa nhận xét tích cực dựa trên data thiếu → user có thể tin và đưa quyết định tài chính sai. | Thêm safety rule: KHÔNG nhận xét đánh giá khi data thiếu. Thêm disclaimer + low-confidence path. |
| So sánh tháng 5 (45k) vs tháng 4 (0đ), kết luận "mở ví nhiều hơn". Thực tế user chi hàng triệu/tháng ngoài MoMo. | Self-use test #3, screenshot | AI so sánh và kết luận dựa trên data thiếu mà không cảnh báo. | Thêm disclaimer nguồn data ở mọi kết quả phân tích + so sánh. |
| Tư vấn trả nợ 10 triệu bằng 4 bước generic, không dùng data chi tiêu cá nhân. | Self-use test #7, screenshot | AI hứa cá nhân hoá nhưng lời khuyên không khác Google search. | Chưa trong scope Day 06 — ghi vào backlog. |
| Yêu cầu mã giao dịch khi user muốn sửa phân loại → correction path gãy. | Self-use test #8, screenshot | User bỏ cuộc sửa lỗi → data phân loại sai vĩnh viễn. | Chưa trong scope Day 06 — ghi vào backlog. |
| Hành vi không nhất quán: cùng data 0đ nhưng test #2 khuyên ghi chép (tốt), test #9 khen (nguy hiểm). | Self-use test #2 + #9, screenshot | Thiếu rule thống nhất khi xử lý data thiếu. | Thêm rule nhất quán: data 0đ/bất thường → LUÔN disclaimer + hỏi, KHÔNG khen. |
| Review public: "phân loại khó khăn ngoài hệ sinh thái MoMo", "giao dịch chuyển tiền thiếu context". | momo.vn support, Google Play reviews | Pain phổ biến, không chỉ cá nhân — validate build slice có giá trị thực. | Xác nhận scope đúng hướng. |

---

## 3. Pain statement

```text
User trẻ (sinh viên, mới đi làm) chi tiêu đa kênh đang gặp khó ở bước phân tích chi tiêu với Moni,
vì phần lớn chi tiêu hàng ngày diễn ra ngoài MoMo (tiền mặt, chuyển khoản ngân hàng),
nhưng Moni không biết data thiếu VÀ còn đưa nhận xét đánh giá sai lệch:
  "kiểm soát chi tiêu rất tốt!" khi thực tế 0đ chỉ vì data thiếu,
dẫn tới user có thể tin nhận xét sai → đưa quyết định tài chính sai
(nghĩ mình chi tiêu ít → chi tiêu thêm → nợ),
hoặc nhận ra AI sai → mất niềm tin → bỏ tính năng.
Bằng chứng chính: 9 screenshot từ 8 bài test thực tế với Moni
+ review công khai ghi nhận AI phân loại khó khăn ngoài hệ sinh thái MoMo.
```

---

## 4. Build slice

```text
Cho người dùng MoMo trẻ chi tiêu đa kênh đang hỏi Moni phân tích chi tiêu,
prototype sẽ dùng AI để augment quá trình phân tích:
  - Phát hiện khoảng trống dữ liệu bất thường
    (ví dụ: 0đ ăn uống 2 tuần, tổng 0đ cả tháng),
  - Disclaimer nguồn dữ liệu ở mọi kết quả: "Số liệu chỉ gồm giao dịch qua MoMo",
  - Proactive hỏi user: "Bạn có chi tiêu ngoài MoMo không? Nhập thêm để phân tích chính xác hơn",
  - KHÔNG đưa nhận xét đánh giá ("tốt"/"xấu") khi data không đủ cơ sở,
tạo ra kết quả phân tích đáng tin cậy hơn,
và xử lý failure mode "AI nhầm khoảng trống hợp lệ với khoảng trống do thiếu data"
bằng cách luôn hỏi xác nhận user trước khi kết luận,
và cho user tắt nhắc nhở nếu xác nhận data đúng.
```

---

## 5. Auto/Aug decision

Chọn một:

- [x] **Augmentation:** AI gợi ý/draft/phân loại, user quyết cuối.
- [ ] **Conditional automation:** AI tự làm trong case hẹp; case mơ hồ/rủi ro chuyển người.
- [ ] **Automation:** AI tự quyết và tự hành động.

**Lý do chọn:** Khi phát hiện khoảng trống dữ liệu, AI không nên tự suy luận (ví dụ: tự đoán user chi bao nhiêu) vì dễ sai. AI gợi ý + hỏi user xác nhận, user quyết định có nhập bổ sung hay không. Đặc biệt, AI KHÔNG tự đưa nhận xét đánh giá ("kiểm soát tốt") khi chưa được user xác nhận data đủ — vì false positive nguy hiểm hơn "không nhận xét gì".

**Human role:** Decider — user xác nhận data có thiếu hay không, nhập bổ sung nếu muốn, và quyết định tắt nhắc nhở nếu data đúng.

---

## 6. Four paths

| Path | Prototype phải thể hiện gì? |
|---|---|
| **Happy** | User hỏi phân tích chi tiêu → data MoMo đủ (nhiều giao dịch, pattern bình thường) → AI trả kết quả + disclaimer "Số liệu gồm giao dịch qua MoMo" + nhận xét có cơ sở + gợi ý bổ sung chi tiêu ngoài MoMo để chính xác hơn. |
| **Low-confidence** | AI phát hiện khoảng trống (0đ ăn uống 2 tuần, tổng 0đ cả tháng) → KHÔNG nhận xét đánh giá → hỏi user: "Moni chỉ thấy [X]đ qua MoMo. Bạn có chi tiêu bằng tiền mặt/ngân hàng không?" → User chọn nhập bổ sung hoặc xác nhận "không chi tiêu" → kết quả cập nhật. |
| **Failure** | User thật sự không chi tiêu (ăn ở nhà, cha mẹ nấu) → AI vẫn hỏi "bạn có chi ngoài MoMo không?" → User nói "Không" → AI ghi nhận, KHÔNG hỏi lại liên tục. Cho user tắt nhắc nhở cho danh mục cụ thể. |
| **Correction** | User đã nhập chi tiêu bổ sung → AI cập nhật phân tích → user thấy số liệu mới. Nếu user muốn sửa danh mục → prototype chỉ dẫn ra tính năng sửa (Sổ giao dịch). Trong scope Day 06, correction path đơn giản — inline edit là backlog. |

---

## 7. Failure mode nguy hiểm nhất

```text
Nếu user thật sự không chi tiêu ở một danh mục
(ví dụ: ăn ở nhà, cha mẹ nấu → 0đ ăn uống là đúng),
AI có thể nhầm rằng data thiếu và hỏi liên tục
"Bạn có chi tiêu ngoài MoMo không?",
hậu quả là user cảm thấy bị làm phiền, mất trải nghiệm, bỏ tính năng.

Prototype sẽ xử lý bằng:
  - Cho user chọn "Không, tôi thật sự không chi tiêu mục này"
    → ghi nhận preference.
  - Không hỏi lại cùng câu hỏi trong 30 ngày sau khi user confirm.
  - Thêm option "Tắt nhắc nhở bổ sung chi tiêu cho danh mục [X]".
  - Khi user đã confirm → kết quả 0đ hiển thị kèm ghi chú
    "Đã xác nhận bởi user" thay vì đưa nhận xét đánh giá.

Owner kiểm thử path này là Dương Đức Cường.
```

---

## 8. Owner plan cho sáng Day 06

| Thành viên | Việc phụ trách | Bằng chứng cần có trong repo |
|---|---|---|
| Dương Đức Cường | Research / evidence | Evidence pack hoàn chỉnh + 9 screenshot self-use + review public + 3 competitor analogs |
| Dương Đức Cường | SPEC | Thin SPEC + synthesis-decide toolkit + app-teardown (5 findings, 4 paths, as-is/to-be) |
| Dương Đức Cường | Prototype | Chatbot flow prototype thể hiện 4 paths: Happy / Low-confidence / Failure / Correction |
| Dương Đức Cường | Test / failure path | Test case: (1) false positive khi data thiếu, (2) khoảng trống hợp lệ vs thiếu data, (3) so sánh data thiếu, (4) disclaimer hiển thị |
| Dương Đức Cường | Demo script / repo | Script demo 3-5 phút: trình bày pain (screenshot Moni khen 0đ) → prototype giải quyết → test failure path |
