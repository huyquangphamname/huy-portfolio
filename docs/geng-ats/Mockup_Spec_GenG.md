# Đặc tả Mockup / Wireframe chi tiết — GenG ATS (Project C)

> Khắc phục feedback: *"Chưa có link mockup/prototype, màn mockup bản tĩnh trong tài liệu có độ chi tiết chưa cao."*
> Tài liệu này nâng độ chi tiết từng màn (field-level + state + validation). **Bước tiếp theo bắt buộc:**
> dựng prototype tương tác trên Figma rồi dán link vào đây và vào portfolio.
>
> 🔗 **Figma prototype:** `[[CHƯA CÓ LINK — Recruiter/BA tạo và dán vào]]`

Ký hiệu state mỗi màn: **Empty** (rỗng) · **Loading** · **Error** · **Success**. Mã lỗi tham chiếu ER01–ER08.

---

## M0. Đăng nhập (Login) — RBAC
- **Field:** Email (bắt buộc, định dạng email), Mật khẩu (bắt buộc), [tuỳ chọn] MFA/2FA OTP.
- **Action:** Đăng nhập → định tuyến theo vai trò (Recruiter → Dashboard; Admin → Admin Console).
- **Validation/Error:** sai thông tin → ER06 (Unauthorized); khoá tạm sau N lần sai.
- **State:** Loading khi xác thực; Error hiển thị dưới ô nhập.

## M1. Dashboard / Danh sách ứng viên
- **Layout:** thanh tìm kiếm trên cùng; bộ lọc (Vị trí, Ngày tạo, Từ khoá); bảng danh sách ứng viên; nút "＋ Tải lên CV".
- **Cột bảng:** Họ tên · Email · Vị trí · Số năm KN · Kỹ năng (tag) · Trạng thái · Ngày tạo · Hành động.
- **State Empty:** "Chưa có hồ sơ — hãy tải lên CV đầu tiên".
- **State Loading:** skeleton rows. **Error:** ER04 nếu lỗi tải dữ liệu.

## M2. Tải lên CV (Upload modal)
- **Vùng kéo-thả** + nút chọn file. Hỗ trợ `.pdf, .doc, .docx` (và ảnh scan nếu in-scope).
- **Hiển thị:** tên file, dung lượng, tiến trình upload.
- **Validation:** sai định dạng → ER03; vượt dung lượng (vd >10MB — *cần chốt*) → ER05.
- **Open Question (ghi rõ trên màn):** có cho **bulk upload** không? Giới hạn MB?
- **Success:** "Tải lên thành công" → tự chuyển sang M3.

## M3. Màn Review kết quả Parsing
- **5 trường (editable)** đúng đặc tả FRS:
  | Trường | Kiểu | Bắt buộc | Sửa được | Kiểu dữ liệu |
  |---|---|---|---|---|
  | Họ và tên | TEXT BOX | Có | Có | VARCHAR |
  | Email | TEXT BOX | Có | Có | VARCHAR |
  | Vị trí công việc | TEXT BOX | Có | Có | VARCHAR |
  | Số năm kinh nghiệm | TEXT BOX | Có | Có | DECIMAL |
  | Kỹ năng | SELECT (tag) | Có | Có | VARCHAR |
- **Trạng thái thiếu trường:** ô trống được **highlight** cảnh báo, yêu cầu nhập tay.
- **Trùng email:** cảnh báo ER07 (merge hay tạo mới — *cần chốt*).
- **Action:** "Lưu ứng viên" → gán trạng thái `New`.

## M4. Pipeline / Kanban (quản lý trạng thái)
- **5 cột:** New · Screening · Interview · Hired · Rejected; mỗi cột hiển thị **số đếm** (vd Screening: 10).
- **Tương tác:** kéo-thả thẻ hoặc menu thả xuống → cập nhật **1-click**, **real-time** (không reload).
- **Phân quyền:** chỉ Recruiter/Manager đổi trạng thái (ER06 nếu không đủ quyền).
- **Thẻ ứng viên:** tên, vị trí, kỹ năng nổi bật, ngày tạo.

## M5. Chi tiết hồ sơ ứng viên
- **Hiển thị** đầy đủ 5 trường + lịch sử trạng thái + nguồn file CV (link tải, đã mã hoá).
- **Hành động nhạy cảm** (xem thông tin cá nhân) → ghi **Audit Log**.
- **Consent:** hiển thị trạng thái đồng ý của ứng viên; nút yêu cầu xoá dữ liệu.

## M6. Tìm kiếm & Lọc
- **Ô tìm:** theo tên (M-search) hoặc từ khoá kỹ năng/KN; **case-insensitive**.
- **Bộ lọc:** Vị trí (vacancy), Ngày tạo (sắp xếp). Kết quả < 3s.
- **Empty result:** "Không tìm thấy ứng viên phù hợp với từ khóa".

## M7. Tạo từ khoá vị trí (Manager)
- **Field:** Vị trí + danh sách từ khoá (tag). **Action:** Lưu → dùng cho lọc/tìm.

## M8. Admin Console (RBAC, Audit, Consent)
- **Quản lý người dùng** (tạo/sửa vai trò Recruiter/Admin), **Audit Log** (user, thời gian, hành động),
  **Quản lý Consent**, **Yêu cầu xoá dữ liệu** (xử lý ≤72h theo luật BVDLCN).

---
### Checklist mockup đạt yêu cầu
- [ ] Đủ 8–9 màn chính ở trên · [ ] Mỗi màn có state Empty/Loading/Error/Success
- [ ] Field-level spec khớp FRS (5 trường, kiểu dữ liệu) · [ ] Thể hiện validation & mã lỗi ER01–ER08
- [ ] **Link Figma prototype tương tác** đã chèn · [ ] Link cập nhật vào trang portfolio
