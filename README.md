# Day06-2A202600794-DuongDucCuong

## Day 05 Lab — Khởi Động Dự Án AI Product

**Học viên:** Dương Đức Cường — 2A202600794  
**Track:** Fintech / Quản lý tài chính cá nhân  
**Product:** MoMo — Moni (Trợ thủ tài chính AI)

### Cấu trúc repo

```
├── 01-invidual-workshop/
│   ├── app-teardown.md          ← Bài mổ app Moni (5 findings, 4 paths, as-is/to-be)
│   └── *.png                    ← 9 screenshot evidence từ 8 bài test
└── 02-group-spec/
    ├── evidence-pack-template.md  ← Evidence pack (self-use + review + competitor)
    ├── synthesis-decide-toolkit.md ← Từ evidence → insight → build slice
    └── thin-spec-template.md      ← Thin SPEC cam kết cho Day 06
```

### Tóm tắt bài lab

- **Pain chính:** Moni đưa nhận xét đánh giá sai lệch (false positive: "kiểm soát chi tiêu rất tốt!") khi data chi tiêu = 0đ — do user chi tiêu bằng tiền mặt/ngân hàng ngoài MoMo.
- **Build slice:** Prototype cải thiện flow phân tích chi tiêu: disclaimer nguồn data + phát hiện khoảng trống + proactive hỏi user bổ sung + KHÔNG nhận xét đánh giá khi data thiếu.
- **Evidence:** 9 screenshot từ 8 bài test thực tế + review public + 3 competitor analogs.
