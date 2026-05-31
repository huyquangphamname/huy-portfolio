# Nghiên cứu Domain & Bảo mật — GenG ATS (Project C)

> Khắc phục feedback: *"Nghiên cứu và khảo sát thêm thông tin về các trường thông tin và process cần thiết
> của domain này trên thị trường, nhu cầu của end user khi sử dụng hệ thống, và bảo mật."*

## 1. Bối cảnh domain: ATS (Applicant Tracking System)
ATS là hệ thống số hoá và theo dõi hồ sơ ứng viên trong quy trình tuyển dụng. Sản phẩm tham chiếu trên thị trường:
- **Quốc tế:** Greenhouse, Lever, Workable, Ashby, Zoho Recruit — mạnh ở resume parsing, pipeline, scorecard, tích hợp job boards.
- **Việt Nam / khu vực:** Base Hiring (Base.vn), các module tuyển dụng trong HRM nội địa — phù hợp SME.
- GenG định vị: **Demo MVP cho SME**, 50–100 CV/đợt, tập trung 3 năng lực lõi: Parsing, Keyword Filter, Status Tracking (đúng đề bài GAP).

## 2. Trường thông tin chuẩn của domain (so với GenG)
Resume parser thị trường thường trích: **name, email, phone, work history, education, skills, certifications**
(pipeline điển hình: parsing engine → **NER (Named-Entity Recognition)** → classification map vào field chuẩn).

| Trường chuẩn thị trường | GenG hiện có? | Khuyến nghị |
|---|---|---|
| Họ tên | ✅ | giữ |
| Email | ✅ | giữ |
| **Số điện thoại** | ❌ | **Nên bổ sung** (liên hệ ứng viên) |
| Vị trí ứng tuyển | ✅ | giữ |
| Số năm kinh nghiệm | ✅ | giữ |
| Kỹ năng | ✅ | giữ (đang dùng cho lọc) |
| **Học vấn (Education)** | ❌ | cân nhắc bổ sung |
| **Chứng chỉ (Certifications)** | ❌ | cân nhắc bổ sung |

> GenG đang bóc tách **5 trường**; thị trường thường 7+. Việc thêm Phone/Education/Certifications sẽ tăng giá trị sàng lọc.

## 3. Chỉ số đo chất lượng Parsing (nên đưa vào tiêu chí nghiệm thu)
- **Parsing rate**: % CV xử lý thành công không cần can thiệp tay.
- **Error rate**: % trường thiếu/sai cần sửa tay.
- **Field completeness**: số trường trích trung bình mỗi CV.
- Tham chiếu: parser AI hiện đại đạt **>90% F1**; GenG đặt mục tiêu **≥95%** (NFR-002) → cần đo bằng tập 50–100 CV mẫu.

## 4. Nhu cầu end-user (persona)
| Persona | Mong muốn chính | Hệ quả thiết kế |
|---|---|---|
| **Recruiter** | Nhập liệu nhanh, tìm đúng người, thao tác ít | Parsing tự động, lọc <3s, Kanban 1-click, mobile-responsive |
| **Hiring Manager** | Nhìn tổng quan pipeline, so sánh ứng viên | Dashboard đếm số, lọc theo vacancy, (đề xuất) chấm điểm trọng số |
| **Admin** | Bảo mật, phân quyền, truy vết | RBAC, Audit Log, quản lý Consent |
| **Ứng viên (data subject)** | Được bảo vệ dữ liệu, phản hồi nhanh | Consent, quyền xem/sửa/xoá, mã hoá |

> Gợi ý khảo sát: phỏng vấn 3–5 recruiter SME về thời gian sàng lọc thực tế & lý do bỏ sót ứng viên để định lượng "before/after".

## 5. Bảo mật & Tuân thủ pháp lý
**GenG đã có (giữ & làm rõ):** RBAC (Recruiter/Admin), mã hoá **AES-256** at-rest & in-transit, MFA/2FA, **Audit Log**,
quản lý **Consent**, **Anonymization**, chống SQL Injection/XSS, sao lưu hàng ngày + khôi phục ≤24h.

**Quyền chủ thể dữ liệu (cần hiện trong luồng):** quyền truy cập, hạn chế xử lý, phản đối, sửa, xoá —
mọi yêu cầu hạn chế/phản đối phải xử lý trong **≤72 giờ**; với **dữ liệu nhạy cảm** phải thông báo cho chủ thể.

### ⚠️ Cập nhật pháp lý quan trọng (phát hiện khi nghiên cứu)
FRS/BRD của GenG đang trích **Nghị định 13/2023/NĐ-CP**. Tuy nhiên Nghị định 13/2023/NĐ-CP **đã hết hiệu lực từ 01/01/2026**,
được thay thế bởi **Luật Bảo vệ Dữ liệu Cá nhân 2025 (hiệu lực 01/01/2026)**.
→ **Hành động BA:** cập nhật tham chiếu pháp lý trong FRS/NFR-004 sang luật mới (xác minh số hiệu luật chính xác trước khi chốt).

### Khái niệm chống thiên kiến (điểm cộng cho domain tuyển dụng)
- **Blind Screening** (FRS đã đề cập): ẩn thông tin nhận dạng (tên, tuổi, giới, ảnh) khi sàng lọc để giảm định kiến → nên đưa thành tính năng có bật/tắt.

## 6. Việc cần làm tiếp (đưa vào FRS v1.2)
- [ ] Bổ sung trường Phone (và cân nhắc Education/Certifications) vào parsing.
- [ ] Thêm chỉ số Parsing rate / Error rate / Field completeness vào tiêu chí nghiệm thu.
- [ ] Cập nhật tham chiếu pháp lý (thay Nghị định 13/2023 đã hết hiệu lực).
- [ ] Làm rõ luồng quyền chủ thể dữ liệu (xoá ≤72h) + bật/tắt Blind Screening.
- [ ] Phỏng vấn 3–5 recruiter để định lượng before/after.

---
### Nguồn tham khảo
- [What is an ATS? Full 2025 Guide — Oleeo](https://www.oleeo.com/blog/what-is-an-applicant-tracking-system-ats/)
- [AI Resume Parser — MiHCM](https://mihcm.com/resources/blog/ai-resume-parser-enhance-applicant-data-accuracy/)
- [What ATS Looks for in Resumes (2025) — The Interview Guys](https://blog.theinterviewguys.com/what-ats-looks-for-in-resumes/)
- [ATS-Friendly Resume Format Checklist 2026 — Jobscan](https://www.jobscan.co/blog/20-ats-friendly-resume-templates/)
- [Nghị định 13/2023/NĐ-CP — Thư viện Pháp luật](https://thuvienphapluat.vn/van-ban/Cong-nghe-thong-tin/Nghi-dinh-13-2023-ND-CP-bao-ve-du-lieu-ca-nhan-465185.aspx)
- [ND 13/2023 hết hiệu lực từ 01/01/2026 — Thư viện Pháp luật](https://thuvienphapluat.vn/chinh-sach-phap-luat-moi/vn/ho-tro-phap-luat/chinh-sach-moi/102230/nghi-dinh-13-2023-nd-cp-ve-bao-ve-du-lieu-ca-nhan-het-hieu-luc-tu-01-01-2026)
