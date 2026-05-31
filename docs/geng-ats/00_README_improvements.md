# Project C — GenG ATS · Bản cải thiện theo Feedback giám khảo

Thư mục `_improved/` chứa **artifact thật** bổ sung cho dự án GenG ATS (Applicant Tracking System, Demo MVP của GAP),
do Agent 1 tạo, bám đúng FRS/BRD/Use Case/AC gốc. **Không sửa/ghi đè file gốc** của dự án.

## Bản đồ Feedback → Artifact

| # | Feedback giám khảo | Artifact đã tạo | Trạng thái |
|---|---|---|---|
| 1 | BPMN thiếu As-is/To-be + diễn giải cải tiến | `BPMN_AsIs_ToBe_GenG.md` (2 sơ đồ Mermaid + bảng cải tiến) | ✅ |
| 2 | **Chưa có Test Case** | `Test_Cases_GenG_ATS.xlsx` (**30 test case**: happy/alternate/negative, map AC & ER) | ✅ |
| 3 | Use Case / User Story / Test Case còn yếu | `UseCase_UserStory_Traceability_GenG.xlsx` (UC-01..08, US-01..09, ma trận truy vết) | ✅ |
| 4 | Use Case ↔ Sequence chưa 1–1 | `Sequence_Diagrams_GenG.md` (SEQ-01..08, mỗi UC một sequence) | ✅ |
| 5 | Chưa có mockup/prototype, màn tĩnh sơ sài | `Mockup_Spec_GenG.md` (9 màn, field-level + state + validation) | ✅ spec — ⏳ *cần dán link Figma* |
| 6 | Thiếu tiêu chí có trọng số | `Weighted_Criteria_GenG.xlsx` (tiêu chí hệ thống + đề xuất chấm điểm ứng viên) | ✅ |
| 7 | Thiếu nghiên cứu domain & bảo mật | `Domain_Security_Research_GenG.md` (thị trường, trường dữ liệu, persona, pháp lý) | ✅ |

## Phát hiện đáng chú ý khi rà soát (nên sửa trong FRS/BRD v1.2)
1. **Pháp lý lỗi thời:** FRS trích **Nghị định 13/2023/NĐ-CP** — văn bản này **đã hết hiệu lực từ 01/01/2026**
   (thay bằng Luật Bảo vệ Dữ liệu Cá nhân 2025). → Cập nhật NFR-004.
2. **Lỗi copy-paste trong BRD:** mục *4. Business Drivers* và *Appendix A* của `MasterPlan_ATS_GenG.xlsx` còn lẫn nội dung
   của dự án khác (ngân hàng/ESG "cố vấn tài chính cá nhân", "quản lý tài chính cho học sinh") — **không thuộc ATS**, cần xoá/sửa.
3. **Thiếu trường dữ liệu so với thị trường:** GenG parse 5 trường; nên cân nhắc thêm **Số điện thoại / Học vấn / Chứng chỉ**.
4. **TestCase sheet trong MasterPlan đang để trống (item 6.0 = False)** — nay đã có bộ test case riêng ở file trên.

## Cách dùng
- File `.md` chứa sơ đồ **Mermaid** → render trực tiếp trên GitHub hoặc VS Code (ext. Markdown Preview Mermaid).
- File `.xlsx` mở bằng Excel; ô có công thức `=W×S/5` tự tính điểm khi nhập cột Điểm.
- **Việc còn lại của bạn (Huy):** (a) dựng prototype Figma từ `Mockup_Spec_GenG.md` rồi dán link;
  (b) chuyển BPMN/Sequence sang draw.io bản chính thức nếu cần nộp; (c) cập nhật FRS theo 4 phát hiện trên;
  (d) đưa link các artifact này vào trang portfolio (Agent 1 phần B).

## Bản chính thức đã xuất (cập nhật)
- **`GenG_FRS_v1.2.docx`** — FRS hợp nhất hoàn chỉnh (10 mục + 2 phụ lục, 19 bảng): gộp toàn bộ artifact + đã vá 3 lỗi
  (pháp lý ND13, copy-paste BRD, thiếu trường). Số liệu nạp trực tiếp từ các .xlsx nên khớp 100%.
- **`GenG_Diagrams.drawio`** — file draw.io đa trang (10 trang): BPMN As-is, BPMN To-be, SEQ-01..08.
  Mở bằng draw.io / diagrams.net; mỗi sequence một trang riêng.
