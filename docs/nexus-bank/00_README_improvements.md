# Nexus Bank — Bản cải thiện hướng near-production

Nexus Bank = ứng dụng tài chính/ngân hàng thông minh (eKYC onboarding, QR transfer, quản lý tài chính cá nhân; Đầu tư & ESG ở Phase 2).
Dự án đã đạt **điểm qualified** ở barem giám khảo. Thư mục `_improved/` bổ sung những gì cần để tiến gần **sản phẩm production**,
học best-practice từ nhóm vô địch **LAHO**. **Không sửa file gốc.**

## Nội dung
| File | Nội dung |
|---|---|
| `Nexus_TestCases_Traceability_Readiness.xlsx` | **28 test case** (format LAHO) + ma trận **Traceability** (Epic→FR→US→NFR→TC) + **Production-Readiness scorecard** (trọng số) |
| `Nexus_Diagrams.drawio` | **ERD** + 3 **Sequence Diagram**: eKYC Onboarding, QR Transfer (+MFA), Auto-categorize & Budget Alert |
| `Nexus_ProductionReadiness_and_Compliance.md` | **Gap analysis** MVP→production + **tuân thủ ngân hàng** (SBV, eKYC, AML, bảo vệ dữ liệu 2025, PCI-DSS) + bảo mật + vận hành |
| `DISCLAIMER.md` | Cảnh báo học thuật/chưa kiểm chứng production + license view-only |

## Tóm tắt gap đã đóng (so với bản gốc)
- ➕ Bộ **Test Cases** bài bản (gốc thiếu) — gồm load/perf, DR, security, compatibility.
- ➕ **Sequence Diagrams** + **ERD** (gốc chưa có rõ).
- ➕ **Traceability** Epic→FR→US→NFR→TC.
- ➕ **Production-Readiness scorecard** có trọng số (7 chiều: functional, security/compliance, performance, reliability/DR, UX, docs, test coverage).
- ➕ **Compliance ngân hàng** (giấy phép SBV, eKYC, AML, Luật BVDLCN 2025, PCI-DSS) — phần quan trọng nhất để "near-production".

## Việc cần làm tiếp (để thật sự production-ready)
- Chạy **load test** (10k user/100 TPS), **DR drill** (RPO=0/RTO≤15'), **pen-test** độc lập.
- Hợp tác đối tác **được cấp phép/SBV**; hoàn thiện **AML** & **bảo vệ dữ liệu 2025**.
- Tự động hoá test + **CI/CD gates**, observability (logging/metrics/alerting).
- Xây Phase 2 (Investment & Wealth, ESG) — đã có user stories US 14–22.

> ⚠️ Mọi số liệu là **mục tiêu/giả định**, chưa đo thực tế. Phần pháp lý là định hướng, KHÔNG phải tư vấn pháp lý — phải xác minh với chuyên gia trước khi dùng thật.
