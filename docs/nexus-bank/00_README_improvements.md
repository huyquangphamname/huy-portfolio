# Nexus Bank — Bộ tài liệu BA & phân tích production-readiness

Nexus Bank = ứng dụng tài chính/ngân hàng thông minh (eKYC onboarding, QR transfer, quản lý tài chính cá nhân; Đầu tư & ESG ở Phase 2).
Bộ tài liệu này đặc tả end-to-end theo vai trò Business Analyst và bổ sung phần phân tích khoảng cách (gap) để tiến gần **sản phẩm production** theo **chuẩn ngành ngân hàng**.

## Nội dung
| File | Nội dung |
|---|---|
| `Nexus_TestCases_Traceability_Readiness.xlsx` | **28 test case** + ma trận **Traceability** (Epic→FR→US→NFR→TC) + **Production-Readiness scorecard** (trọng số) |
| `Nexus_Diagrams.drawio` | **ERD** + 3 **Sequence Diagram**: eKYC Onboarding, QR Transfer (+MFA), Auto-categorize & Budget Alert |
| `Nexus_ProductionReadiness_and_Compliance.md` | **Gap analysis** MVP→production + **tuân thủ ngân hàng** (SBV, eKYC, AML, bảo vệ dữ liệu 2025, PCI-DSS) + bảo mật + vận hành |
| `DISCLAIMER.md` | Cảnh báo dự án ý tưởng/chưa kiểm chứng production + license view-only |

## Phạm vi tài liệu
- Bộ **Test Cases** bài bản — gồm load/perf, DR, security, compatibility.
- **Sequence Diagrams** + **ERD**.
- **Traceability** Epic→FR→US→NFR→TC.
- **Production-Readiness scorecard** có trọng số (7 chiều: functional, security/compliance, performance, reliability/DR, UX, docs, test coverage).
- **Compliance ngân hàng** (giấy phép SBV, eKYC, AML, Luật BVDLCN 2025, PCI-DSS) — phần quan trọng nhất để tiến gần production.

## Việc cần làm tiếp (để thật sự production-ready)
- Chạy **load test** (10k user/100 TPS), **DR drill** (RPO=0/RTO≤15'), **pen-test** độc lập.
- Hợp tác đối tác **được cấp phép/SBV**; hoàn thiện **AML** & **bảo vệ dữ liệu 2025**.
- Tự động hoá test + **CI/CD gates**, observability (logging/metrics/alerting).
- Xây Phase 2 (Investment & Wealth, ESG) — đã có user stories US 14–22.

> ⚠️ Mọi số liệu là **mục tiêu/giả định**, chưa đo thực tế. Phần pháp lý là định hướng, KHÔNG phải tư vấn pháp lý — phải xác minh với chuyên gia trước khi dùng thật.
