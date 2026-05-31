# Sequence Diagrams theo từng Use Case — GenG ATS (Project C)

> Khắc phục feedback: *"Chưa phân tách tốt Use case và vẽ được Sequence Diagram cho mỗi Use case."*
> Mỗi Use Case (UC-01..UC-08) có một Sequence Diagram riêng (SEQ-01..SEQ-08), khớp bảng Traceability.
> Participants bám kiến trúc trong FRS: Recruiter, Web UI, Backend API, OCR/NLP Engine, Cloud Storage, Database.

## SEQ-01 · UC-01 Tải lên CV (FR-001)
```mermaid
sequenceDiagram
    actor R as Recruiter
    participant UI as Web UI
    participant API as Backend API
    participant ST as Cloud Storage
    R->>UI: Kéo-thả/chọn file CV (.pdf/.doc)
    UI->>UI: Validate định dạng & dung lượng
    alt Sai định dạng/quá lớn
        UI-->>R: Báo lỗi ER03 / ER05
    else Hợp lệ
        UI->>API: Gửi file
        API->>ST: Lưu file (mã hoá at-rest AES-256)
        API->>API: Đẩy vào hàng đợi xử lý (Queue)
        API-->>UI: 200 OK (<1s)
        UI-->>R: "Tải lên thành công"
    end
```

## SEQ-02 · UC-01 Trích xuất CV / Parsing (FR-002)
```mermaid
sequenceDiagram
    participant API as Backend API
    participant OCR as OCR/NLP Engine
    participant DB as Database
    participant UI as Web UI
    actor R as Recruiter
    API->>OCR: Gửi file thô (REST API)
    OCR->>OCR: Tiền xử lý (OCR/Text Extraction)
    OCR->>OCR: NER + Regex bóc tách 5 trường
    OCR-->>API: JSON {Tên, Email, Vị trí, KN, Kỹ năng}
    alt Thiếu trường bắt buộc
        API-->>UI: Highlight trường trống
        UI-->>R: Yêu cầu nhập tay
    else Đủ trường (≥95%)
        API->>DB: Tạo hồ sơ, status = 'New'
        API-->>UI: Hiển thị màn Review
        R->>UI: Xác nhận "Lưu ứng viên"
    end
```

## SEQ-03 · UC-02 Sàng lọc theo Từ khoá (FR-003)
```mermaid
sequenceDiagram
    actor R as Recruiter
    participant UI as Web UI
    participant API as Backend API
    participant DB as Database
    R->>UI: Nhập từ khoá (vd "Java")
    UI->>API: GET /search?kw=java
    API->>DB: Query khớp (case-insensitive) trên trường Kỹ năng
    DB-->>API: Kết quả
    alt Có kết quả
        API-->>UI: Danh sách ứng viên (<3s)
    else Rỗng
        API-->>UI: "Không tìm thấy ứng viên phù hợp với từ khóa"
    end
```

## SEQ-04 · UC-03 Quản lý trạng thái Pipeline (FR-004, FR-009)
```mermaid
sequenceDiagram
    actor R as Recruiter/Manager
    participant UI as Web UI (Kanban)
    participant API as Backend API
    participant DB as Database
    R->>UI: Đổi trạng thái ứng viên (kéo thẻ/menu)
    UI->>API: PATCH /candidate/{id}/status
    API->>API: Kiểm tra quyền (RBAC)
    alt Không đủ quyền
        API-->>UI: 403 Unauthorized (ER06)
    else Đủ quyền
        API->>DB: Cập nhật status
        DB-->>API: OK
        API-->>UI: Đồng bộ real-time (không reload)
        UI-->>R: Cập nhật cột & số đếm pipeline
    end
```

## SEQ-05 · UC-04 Tìm theo tên (FR-005)
```mermaid
sequenceDiagram
    actor R as Recruiter
    participant UI as Web UI
    participant API as Backend API
    participant DB as Database
    R->>UI: Nhập tên ứng viên
    UI->>API: GET /search?name=...
    API->>DB: Query LIKE theo tên
    DB-->>API: Hồ sơ khớp
    API-->>UI: Hiển thị kết quả (<3s)
```

## SEQ-06 · UC-05 Lọc theo vị trí / Vacancy (FR-006)
```mermaid
sequenceDiagram
    actor R as Recruiter/Manager
    participant UI as Web UI
    participant API as Backend API
    participant DB as Database
    R->>UI: Chọn vị trí tuyển
    UI->>API: GET /candidates?vacancy=...
    API->>DB: Lọc theo trường Vị trí
    DB-->>API: Danh sách nhóm theo vacancy
    API-->>UI: Hiển thị
```

## SEQ-07 · UC-06 Lọc/Sắp xếp theo ngày (FR-007)
```mermaid
sequenceDiagram
    actor R as Recruiter/Manager
    participant UI as Web UI
    participant API as Backend API
    participant DB as Database
    R->>UI: Chọn sắp xếp theo ngày tạo
    UI->>API: GET /candidates?sort=created_desc
    API->>DB: ORDER BY created_at DESC
    DB-->>API: Danh sách đã sắp
    API-->>UI: Hiển thị (mới nhất lên đầu)
```

## SEQ-08 · UC-07 Tạo từ khoá vị trí (FR-008)
```mermaid
sequenceDiagram
    actor M as Manager
    participant UI as Web UI
    participant API as Backend API
    participant DB as Database
    M->>UI: Mở "Tạo từ khoá vị trí", nhập keyword set
    UI->>API: POST /job-keywords
    API->>API: Kiểm tra quyền (Manager)
    API->>DB: Lưu bộ từ khoá
    DB-->>API: OK
    API-->>UI: Xác nhận; dùng cho lọc/tìm
```

> UC-08 (Quản trị/RBAC/Audit) chủ yếu là luồng cấu hình + auth, đã thể hiện ở nhánh kiểm tra quyền của SEQ-04;
> nếu cần, bổ sung SEQ riêng cho "Đăng nhập + phân quyền" và "Ghi/đọc Audit Log".
