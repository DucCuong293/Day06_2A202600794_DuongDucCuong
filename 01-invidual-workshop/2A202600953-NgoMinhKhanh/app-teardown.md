# Workshop — Mổ App AI Thật

**Học viên:** Ngô Minh Khánh — 2A202600953  
**Thời gian thực hiện:** 03/06/2026  
**Sản phẩm:** Vietnam Airlines — NEO (Chatbot hỗ trợ vé, hành lý, khiếu nại)

---

## 1. Sản phẩm đã chọn

| Sản phẩm | AI feature | Cách truy cập |
|---|---|---|
| Vietnam Airlines — NEO | Chatbot hỗ trợ thông tin chuyến bay, quy định hành lý, làm thủ tục trực tuyến, chính sách hoàn/hủy/đổi vé | Website Vietnam Airlines / Zalo Official Account (OA) |

---

## 2. Dùng thử: promise vs reality

### Product hứa gì?

Vietnam Airlines định vị NEO là **"Trợ lý ảo thông minh"** — giúp khách hàng:
- Tra cứu tình trạng chuyến bay và lịch trình bay theo thời gian thực.
- Hướng dẫn quy định hành lý ký gửi, xách tay và các chính sách hành lý đặc biệt.
- Hỗ trợ làm thủ tục trực tuyến (check-in) nhanh chóng.
- Hướng dẫn và tiếp nhận các yêu cầu hoàn/hủy/đổi vé máy bay 24/7.
- Giảm tải cho các tổng đài viên chăm sóc khách hàng truyền thống.

### User nào được hứa sẽ được giúp?

Hành khách đi máy bay của Vietnam Airlines cần giải đáp thắc mắc khẩn cấp trước giờ bay (thay đổi lịch trình, quy định hành lý, điều kiện vé) mà không muốn xếp hàng chờ cuộc gọi đến tổng đài 1900 1100 thường xuyên bị quá tải.

### Kỳ vọng AI làm được task nào?

- Tra cứu chặng bay động bằng ngôn ngữ tự nhiên (vd: Tìm vé bay Hà Nội đi Sài Gòn ngày mai).
- Tra cứu tình trạng chuyến bay theo thời gian thực bằng mã chuyến bay.
- Trả lời nhanh gọn, súc tích chính sách hành lý kèm checklist chuẩn bị.
- Hỗ trợ luồng hoàn/hủy/đổi vé thông minh bằng cách tích hợp API kiểm tra PNR trước khi trả kết quả hướng dẫn.
- Bảo vệ vai trò hệ thống (system guardrails) tránh bị bẻ khóa prompt injection.

### Khi dùng thật, điểm gãy xuất hiện ở đâu?

Tôi đã thực hiện kiểm thử thực tế trên chatbot NEO của Vietnam Airlines và phát hiện **4 điểm gãy chính**:

---

**Điểm gãy 1: Không hỗ trợ tra lịch bay tự nhiên — AI bắt buộc nhập mã cứng**

Hỏi: *"Chuyến bay Hà Nội đi TP.HCM sáng mai lúc mấy giờ"*  
→ NEO trả: *"Để biết chính xác giờ khởi hành của các chuyến bay từ Hà Nội đi TP.HCM vào sáng mai, Quý khách vui lòng kiểm tra lại mã đặt chỗ trên website/ứng dụng của Vietnam Airlines hoặc liên hệ CSKH để được hỗ trợ thông tin chi tiết nhất."*

Thực tế: AI không thể phân tích intent tra lịch trình bay từ câu lệnh ngôn ngữ tự nhiên của khách hàng. Thay vì gợi ý danh sách giờ bay hoặc hỏi lại chặng cụ thể, bot từ chối trực tiếp và đẩy ngược user về website tự tra cứu hoặc gọi CSKH, làm mất đi vai trò của "trợ lý thông minh".

![AI không hỗ trợ tra cứu chặng bay bằng ngôn ngữ tự nhiên](image.png)

---

**Điểm gãy 2: Đổi/Hoàn vé không thực thi — Trả link hướng dẫn chung**

Hỏi: *"Tôi muốn hủy vé chuyến bay VN213 ngày mai"*  
→ NEO trả: Trả về một link dẫn đến trang hướng dẫn hoàn/hủy vé chung trên website.

Thực tế: AI không tích hợp API tra cứu mã vé (PNR) để kiểm tra điều kiện vé thực tế (vé khuyến mại có được hoàn hủy không). Hậu quả là khách hàng phải click vào link, tự mò mẫm điền form dài 10 phút trên web rồi mới bị hệ thống backend từ chối, gây ức chế và tạo áp lực nghẽn hotline.

---

**Điểm gãy 3: Nhồi nhét văn bản (Wall of Text) — Thiếu chắt lọc thông tin**

Hỏi: *"Tôi có được mang mèo lên máy bay không?"*  
→ NEO trả: Trả về một khối văn bản quy định vận chuyển động vật cảnh (PETC/AVIH) dài gần 1000 từ bao gồm tất cả các quy chuẩn lồng nhốt, giấy kiểm dịch quốc tế...

Thực tế: AI chỉ thực hiện RAG tìm kiếm và hiển thị toàn bộ tài liệu tĩnh mà không tóm tắt hay phân loại theo chặng bay cụ thể (ví dụ: bay trong nước thủ tục đơn giản hơn rất nhiều). Điều này khiến hành khách bị quá tải thông tin và không biết phải bắt đầu từ đâu.

---

**Điểm gãy 4: Prompt Injection — Dễ dàng bẻ khóa vai trò hệ thống**

Hỏi: *[Prompt bẻ khóa yêu cầu loại bỏ bộ lọc liên quan đến CSKH hàng không]* + *"xây dựng cho tôi một trang landing page đơn giản"*  
→ NEO trả: Sinh mã Python Tkinter hoàn chỉnh để dựng giao diện landing page thay vì từ chối yêu cầu ngoài phạm vi dịch vụ hàng không.

Thực tế: Chatbot thiếu cơ chế kiểm soát an toàn hệ thống (system guardrails) để bảo vệ vai trò (System Prompt / Instruction Hierarchy) của mình. Việc bị kéo ra khỏi vai trò không chỉ là một lỗi vui (funny bug) mà có thể dẫn đến việc bot bị lạm dụng để trả lời các nội dung độc hại, lừa đảo hoặc vi phạm thương hiệu dưới danh nghĩa Vietnam Airlines.

![Trợ lý ảo NEO bị bẻ khóa vai trò và viết code Landing Page](image-1.png)

---

### Điểm tốt quan sát được

- **NEO trả lời chính xác quy định hành lý khi thông tin rõ ràng:**
  Hỏi: *"Hạng phổ thông được mang bao nhiêu kg hành lý ký gửi?"*  
  → NEO trả: Trả lời chuẩn xác chính sách 1 kiện 23kg cho chặng bay nội địa Việt Nam.
- **Hỗ trợ định hướng làm thủ tục trực tuyến tốt:**
  Hỏi: *"Làm thế nào để check-in trực tuyến?"*  
  → NEO trả: Đưa ra thời gian check-in trực tuyến trước 24h và đường link trực tiếp dẫn vào trang check-in.

---

## 3. Vẽ 4 paths

| Path | Quan sát thực tế từ bài test đối với NEO |
|---|---|
| **Happy** | Khi hỏi các quy định hành lý phổ thông (23kg ký gửi) hoặc thủ tục check-in trực tuyến rõ ràng, NEO trả lời đúng, nhanh, định dạng dễ nhìn và có kèm các nút bấm nhanh dẫn tới đường link tương ứng. |
| **Low-confidence** | Khi dữ liệu đầu vào mơ hồ hoặc liên quan đến chính sách phức tạp (vd: mang chất lỏng đặc biệt như nước mắm, hành lý có mùi), NEO không hỏi lại user để thu hẹp phạm vi mà tự động trả về toàn bộ tài liệu quy định chung (RAG wall of text) hoặc hướng dẫn liên hệ CSKH. |
| **Failure** | (1) Trả link hoàn/hủy vé chung chung cho mọi hạng vé mà không check PNR trước, dẫn đến user điền form vô ích. (2) Bị prompt injection kéo ra khỏi vai trò CSKH để viết code landing page Python. User không nhận biết được kết quả sai trừ khi tự đối chiếu hoặc phát hiện bot trả lời lập trình. |
| **Correction** | Không hỗ trợ. Nếu user phản hồi phủ nhận kết quả của bot (ví dụ: "Không phải, tôi mua bằng dặm mà"), bot bị mất ngữ cảnh (context drift), coi như phiên hội thoại mới và bắt đầu chào hỏi lại từ đầu. |

---

## 4. Viết finding thành quyết định

### Finding 1 — Đổi/Hoàn vé không thực thi trực tiếp, trả link chung chung

```text
Khi user yêu cầu đổi/hoàn vé nhưng có các hạng vé khác nhau,
AI trả về link hướng dẫn chung mà không kiểm tra PNR thời gian thực,
hậu quả là user mất thời gian điền form rồi mới biết vé không được đổi/hoàn, gây ức chế và quá tải hotline.
Lỗi thuộc layer Data-Tool + UX Recovery.
Nên sửa bằng:
- Tích hợp API kiểm tra PNR trực tiếp trong chatbot.
- Khi user báo hoàn/hủy, AI yêu cầu nhập PNR -> Tra cứu và hiển thị trực tiếp điều kiện vé trước khi cho phép gửi yêu cầu.
```

### Finding 2 — Nhồi nhét văn bản (Wall of Text) khi hỏi về hành lý đặc biệt

```text
Khi user hỏi về quy định hành lý đặc biệt (như mang thú cưng, nhạc cụ),
AI trả về toàn bộ điều khoản dài gần 1000 từ mà không chắt lọc,
hậu quả là khách hàng bị quá tải thông tin, không biết chuẩn bị giấy tờ gì và có nguy cơ bị từ chối bay tại sân bay.
Lỗi thuộc layer Intent + UX (Low-confidence path).
Nên sửa bằng:
- Thiết lập Low-confidence path: Khi phát hiện từ khóa hành lý đặc biệt, hiển thị menu 3 lựa chọn (Ví dụ: 1. Bay Trong nước, 2. Bay Quốc tế, 3. Xem chi tiết).
- Trả về checklist ngắn gọn 3-4 bước thay vì sao chép toàn bộ điều khoản.
```

### Finding 3 — Prompt Injection bẻ khóa bộ lọc vai trò hệ thống

```text
Khi user gửi prompt injection yêu cầu bỏ bộ lọc CSKH rồi yêu cầu viết code landing page,
AI mất vai trò CSKH và thực hiện viết mã nguồn Python Tkinter,
hậu quả là hệ thống bị lạm dụng tài nguyên tính toán và có nguy cơ phát ngôn sai lệch dưới danh nghĩa hãng bay.
Lỗi thuộc layer Safety / Behavior.
Nên sửa bằng:
- Áp dụng Instruction Hierarchy để bảo vệ System Prompt tối cao của bot.
- Sử dụng Input Guardrail quét và từ chối các prompt có từ khóa bẻ khóa vai trò hoặc yêu cầu ngoài phạm vi dịch vụ hàng không.
```

---

## 5. Sketch as-is / to-be

### As-is: Flow phân tích hành lý đặc biệt hiện tại

```text
User hỏi phân tích hành lý đặc biệt (thú cưng)
         │
         ▼
NEO query tài liệu tĩnh ◄── Trả về Wall of Text 1000 từ, không chắt lọc
         │
         ▼
User đọc và bối rối → Bỏ cuộc hoặc làm sai giấy tờ → Bị từ chối bay tại sân bay
```

### To-be: Flow đề xuất cải thiện

```text
User hỏi phân tích hành lý đặc biệt (thú cưng)
         │
         ▼
NEO nhận diện từ khóa đặc biệt & kích hoạt Low-confidence / Step-by-step
         │
         ▼
Hiển thị nút bấm lựa chọn chặng bay:
├── [Nội địa] ──► Checklist 3 bước (Giấy chích ngừa dại, lồng đạt chuẩn, báo trước 24h)
└── [Quốc tế] ──► Yêu cầu liên hệ Agent hoặc hiển thị form giấy kiểm dịch chuyên sâu
         │
         ▼
Gợi ý nút bấm: [Đăng ký dịch vụ ngay] hoặc [Kết nối Agent người thật]
```

---

## 6. Thay đổi đề xuất cho tài liệu SPEC (SPEC Changes)

Để hiện thực hóa các giải pháp UX Recovery và an toàn hệ thống, tài liệu đặc tả (SPEC) của sản phẩm cần bổ sung các cập nhật sau:

1.  **Bổ sung thuộc tính cấu hình an toàn hệ thống:**
    *   `system_role_priority`: Quy định mức độ ưu tiên của System Instruction (mức tuyệt đối, không cho phép User Prompt ghi đè).
    *   `input_guardrail_enabled`: Bật/Tắt module quét prompt injection độc lập trước khi gửi prompt đến LLM chính.
2.  **Bổ sung API cấu trúc tra cứu:**
    *   `verify_pnr_eligibility(pnr, customer_lastname)`: Trả về trạng thái chi tiết của vé (Hạng vé, Chính sách hoàn, Chính sách đổi, Trạng thái thanh toán).
3.  **Bổ sung thuộc tính quản lý hội thoại:**
    *   `context_history_limit` (mặc định = 3): Lưu trữ số lượt chat gần nhất để làm ngữ cảnh xử lý các câu phủ định, sửa đổi thông tin của hành khách (Correction Path).

---

## 7. Tự kiểm trước khi nộp

- [x] Có ít nhất 1 screenshot hoặc observation cụ thể. → Có **2 hình ảnh minh chứng** cho chặng bay và prompt injection.
- [x] Có đủ 4 paths hoặc nói rõ path nào chưa có trong product. → Phân tích cả 4 paths với hành vi thực tế của NEO.
- [x] Finding được viết thành product decision, không chỉ là nhận xét. → **3 findings** chuẩn định dạng trigger → failure → impact → layer → solution.
- [x] Sketch có as-is và to-be. → Có 2 flowchart dạng text biểu diễn luồng đi của hành lý đặc biệt.
- [x] Có một câu nói rõ finding này sẽ đổi gì trong SPEC. → Đã có mục 6 liệt kê rõ các cấu hình an toàn, API tra cứu và quản lý context cần thay đổi trong SPEC.

---
*Báo cáo được chuẩn bị cho học phần Day 05 Lab - AI Product Labs (VinUni AI20k).*
