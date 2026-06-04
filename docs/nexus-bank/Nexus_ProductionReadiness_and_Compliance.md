# Nexus Bank — Production-Readiness Gap Analysis & Banking Compliance

> Mục tiêu: phân tích khoảng cách (gap) đưa Nexus Bank từ đặc tả MVP tiến gần **sản phẩm production** theo **chuẩn ngành ngân hàng**.
> Nexus = ứng dụng tài chính/ngân hàng thông minh (eKYC onboarding, QR transfer, quản lý tài chính cá nhân, đầu tư & ESG ở Phase 2).
>
> ⚠️ Đây là **dự án ý tưởng (conceptual)**, các con số là **mục tiêu/giả định**, **chưa kiểm chứng production** — xem `DISCLAIMER.md`.

## 1. Nexus đã có (điểm mạnh — giữ)
- BRD đầy đủ (context, scope MVP/Phase 2, business drivers), 23 **User Stories** chuẩn BDD + Acceptance Criteria + DoD.
- **FR-1.x** (Onboarding/eKYC/Auth), **FR-2.x** (QR transaction), **FR-3.x** (PFM); **NFR-001..012** (perf, security, DR, uptime).
- **WBS** chi tiết (man-hours theo BA/UIUX/FE/BE/Test/PM), BPMN luồng mở tài khoản (nhanh & thường), FDD, Wireframe.

## 2. Gap → production (theo chuẩn ngành)
| Hạng mục | Trạng thái Nexus | Gap để "near-production" | Đã bổ sung ở đây |
|---|---|---|---|
| **Test Cases** | Thiếu bộ test riêng | Cần bộ test bài bản (functional/security/perf/DR) | ✅ `Nexus_TestCases_..xlsx` (28 case) |
| **Sequence Diagram** | Chưa thấy | Mỗi luồng chính cần sequence | ✅ `Nexus_Diagrams.drawio` (eKYC, QR transfer, auto-categorize) |
| **ERD / Data model** | Chưa rõ | Cần mô hình dữ liệu | ✅ ERD trong `Nexus_Diagrams.drawio` |
| **Traceability** | Rời rạc | Epic→FR→US→NFR→TC | ✅ sheet Traceability |
| **Tiêu chí trọng số** | — | Scorecard nghiệm thu | ✅ sheet Production-Readiness |
| **Load/Perf test** | NFR mục tiêu (10k user, 100 TPS, ≤3s) | Cần kịch bản & kết quả đo thật | TC 19–20 (cần chạy thật) |
| **DR drill** | RPO=0, RTO≤15m (NFR) | Cần diễn tập khôi phục | TC 27 (cần chạy thật) |
| **Pen-test / security** | Mã hoá, MFA (NFR) | Cần kiểm thử xâm nhập độc lập | mục 4 |
| **Compliance/licensing** | Đề cập eKYC | Ngân hàng cần giấy phép & tuân thủ SBV | mục 3 |
| **Observability/CI-CD** | CI/CD trong WBS | Logging/monitoring/alerting, CI gates | mục 5 |

## 3. Tuân thủ ngành ngân hàng (BẮT BUỘC trước production)
> ⚠️ Đây là tóm tắt định hướng để BA nghiên cứu tiếp — **không phải tư vấn pháp lý**; phải xác minh với chuyên gia/cơ quan có thẩm quyền.
- **Giấy phép & giám sát:** dịch vụ ngân hàng/trung gian thanh toán tại VN chịu quản lý của **Ngân hàng Nhà nước (SBV)**;
  cần hợp tác/được cấp phép phù hợp (không thể tự phát hành dịch vụ thanh toán nếu chưa được cấp phép).
- **eKYC:** tuân thủ quy định eKYC của SBV (định danh điện tử, lưu trữ bằng chứng xác thực, ngưỡng giao dịch cho tài khoản eKYC).
- **AML/CFT:** phòng chống rửa tiền — sàng lọc, giám sát giao dịch đáng ngờ, báo cáo.
- **Bảo vệ dữ liệu cá nhân:** **Luật Bảo vệ Dữ liệu Cá nhân 2025** (hiệu lực 01/01/2026, thay Nghị định 13/2023 đã hết hiệu lực) — quyền chủ thể dữ liệu, đồng ý, lưu trữ/xoá.
- **An toàn thanh toán:** cân nhắc chuẩn **PCI-DSS** nếu xử lý dữ liệu thẻ; mã hoá, tokenization.

## 4. Bảo mật (nâng từ NFR sang hành động kiểm thử)
- Mã hoá: TLS 1.3 (in-transit), AES-256 (at-rest) — NFR-004; PIN hash (không plaintext); ảnh/video eKYC xoá sau 24h.
- Xác thực: MFA/Smart-OTP cho giao dịch > 2.000.000đ (NFR-005); session timeout 5'; xác minh thiết bị mới.
- **Cần thêm:** penetration test độc lập, chống fraud/anti-bot, rate-limiting, giám sát bất thường, audit log bất biến,
  quản lý khoá (KMS/HSM), secure SDLC + SAST/DAST trong CI.

## 5. Vận hành & độ tin cậy (production hardening)
- Observability: logging tập trung, metrics, tracing, alerting (SLO/SLA cho NFR-007 uptime 99.9%).
- DR/BC: backup, RPO=0 cho dữ liệu giao dịch, RTO≤15' — cần diễn tập thật (TC-27).
- CI/CD: pipeline có cổng test/security; blue-green/canary; rollback.
- Khả năng mở rộng: kiến trúc chịu 10k user đồng thời / 100 TPS (NFR-002) — cần load test thực tế (TC-20).

## 6. Lộ trình đề xuất (MVP → Production)
1. **MVP (đã có):** Onboarding/eKYC, login, QR transfer, PFM cơ bản.
2. **Hardening:** test suite tự động + CI gates, pen-test, load/DR drill, observability.
3. **Compliance:** làm việc với đối tác được cấp phép/SBV, AML, bảo vệ dữ liệu 2025, (PCI-DSS nếu cần).
4. **Phase 2:** Investment & Wealth, ESG/Carbon (đã có user stories US 14–22).

### Nguồn tham khảo
- Chuẩn ngành: hướng dẫn eKYC/AML, Luật Bảo vệ dữ liệu cá nhân 2025, PCI-DSS, thông lệ kiểm thử (functional/security/perf/DR).
