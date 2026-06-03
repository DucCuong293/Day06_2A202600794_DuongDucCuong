# VinUni AI Product Development Labs

**Học viên:** Dương Đức Cường — 2A202600794  
**Nhánh đào tạo:** Batch 02 — Day 05 & Day 06 AI Products Labs

---

## 📂 Cấu trúc Repository

```text
├── 01-invidual-workshop/
│   └── 2A202600794-DuongDucCuong/
│       ├── app-teardown.md          ← Cá nhân: Bài mổ app Moni (MoMo)
│       └── *.png                    ← Cá nhân: 9 screenshot bằng chứng thực tế
│
└── 02-group-spec/
    ├── evidence-pack-template.md    ← Nhóm: Tài liệu thu thập bằng chứng (ShopeeFood)
    ├── synthesis-decide-toolkit.md   ← Nhóm: Tổng hợp insight & lựa chọn build slice
    └── thin-spec-template.md        ← Nhóm: Bản tả tính năng chi tiết & kế hoạch chạy thử
```

---

## 👤 Phần 1: Cá nhân (Individual Workshop)
* **Ứng dụng phân tích:** MoMo — Moni (Trợ thủ tài chính AI)
* **Track:** Fintech / Quản lý tài chính cá nhân
* **Chi tiết bài làm:** [01-invidual-workshop/2A202600794-DuongDucCuong/app-teardown.md](file:///E:/VinUni/Day06-2A202600794-DuongDucCuong/01-invidual-workshop/2A202600794-DuongDucCuong/app-teardown.md)

### Tóm tắt nội dung:
* **Pain point chính:** Moni đưa nhận xét đánh giá sai lệch (Ví dụ khen *"Kiểm soát chi tiêu rất tốt!"* khi hiển thị 0đ chi tiêu) do AI chỉ đọc dữ liệu phát sinh qua ví MoMo mà không nhận thức được khoảng trống dữ liệu do người dùng chi tiêu bằng tiền mặt hoặc chuyển khoản ngân hàng ngoài hệ sinh thái.
* **Giải pháp đề xuất (Build slice):** Prototype AI phát hiện khoảng trống dữ liệu bất thường → hiển thị cảnh báo nguồn dữ liệu chỉ bao gồm giao dịch MoMo → chủ động hỏi người dùng bổ sung giao dịch ngoài hệ thống → KHÔNG đánh giá tốt/xấu khi chưa đủ cơ sở dữ liệu.

---

## 👥 Phần 2: Nhóm (Group Specification)
* **Ứng dụng phân tích:** ShopeeFood (Đặt đồ ăn & giao hàng)
* **Track:** Track C — Food & Local Delivery
* **Dự án nhóm:** AI Food Agent gợi ý món ăn theo ngữ cảnh (Context-aware Food Agent)
* **Thành viên nhóm:** 
  1. Dương Đức Cường (2A202600794)
  2. Đinh Hoàng Nam (2A202600884)
  3. Bùi Hoàng Sơn (2A202600925)
  4. Ngô Minh Khánh (2A202600953)
  5. Bùi Như Kiệt (2A202600895)
* **Chi tiết bài làm:** Xem các tài liệu trong [02-group-spec/](file:///E:/VinUni/Day06-2A202600794-DuongDucCuong/02-group-spec)

### Tóm tắt nội dung:
* **Pain point chính:** ShopeeFood đề xuất món ăn bị thiên vị quảng cáo (paid promotion) và không quan tâm đến ngữ cảnh thực tế của người dùng, dẫn đến các đề xuất không hợp lý (ví dụ: gợi ý ăn lẩu buffet vào sáng sớm, gợi ý nước đá/salad lạnh vào ngày mưa lạnh, gợi ý các quán đã đóng cửa lúc đêm muộn).
* **Giải pháp đề xuất (Build slice):** AI Food Agent giúp gợi ý món ăn dựa trên ngữ cảnh tức thời:
  * Tự động nhận diện thời tiết (Weather API) và thời gian thực.
  * Nhận dạng tâm trạng người dùng qua chatbot hoặc click nhanh (mood: stress, vui vẻ, mệt mỏi) và yêu cầu sức khỏe (chế độ dinh dưỡng, calo qua Nutritionix API), ngân sách.
  * Tích hợp Google Places API để lọc các quán ăn chất lượng gần vị trí của người dùng đang thực sự mở cửa.
