# GenG ATS — Business Analysis Document Set

GenG is an **Applicant Tracking System (ATS)** for SMEs (client brief by GAP Global): centralized candidate
management, automated CV parsing/screening, and a role-based hiring pipeline (New → Screening → Interview → Hired/Rejected).
This folder is the full BA package authored for the project — BRD/FRS, process models, use cases, test cases, and
supporting research. (Conceptual project — see `DISCLAIMER.md`.)

## Contents
| File | Nội dung |
|---|---|
| `GenG_FRS_v1.2.docx` | **FRS hợp nhất** (10 mục + 2 phụ lục, 19 bảng): 9 FR / 10 NFR, RBAC, đặc tả trường, error catalog |
| `GenG_Diagrams.drawio` | draw.io đa trang: **BPMN As-is**, **BPMN To-be**, **SEQ-01..08** (mỗi use case một sequence) |
| `BPMN_GenG_WEB-current_process_ATS.drawio.png` | Sơ đồ **BPMN 2.0 As-is** (swimlane HR / Ứng viên / Quản lý bộ phận) |
| `Test_Cases_GenG_ATS.xlsx` | **30 test case** (happy / alternate / negative), map tới AC & error code |
| `UseCase_UserStory_Traceability_GenG.xlsx` | UC-01..08 · US-01..09 · ma trận **Traceability** |
| `Sequence_Diagrams_GenG.md` | SEQ-01..08 — mỗi use case ↔ một sequence |
| `Mockup_Spec_GenG.md` | 9 màn hình, đặc tả field-level + state + validation |
| `Weighted_Criteria_GenG.xlsx` | Tiêu chí chất lượng hệ thống có **trọng số** + mô hình chấm điểm ứng viên |
| `Domain_Security_Research_GenG.md` | Nghiên cứu thị trường, trường dữ liệu, persona, pháp lý & bảo mật |

## Phạm vi & điểm nổi bật
- **Process modeling:** BPMN 2.0 As-is/To-be (swimlane theo actor, gateway, message flow, data store).
- **Requirements:** 9 FR + 10 NFR, RBAC (Recruiter / Admin), error catalog ER01–08.
- **Use Cases ↔ Sequences:** 8 use case, mỗi cái map 1–1 tới một sequence diagram; 9 user story + acceptance criteria.
- **Quality:** 30 test case phủ 100% use case; tiêu chí chấp nhận có trọng số; ma trận truy vết.
- **Compliance:** tham chiếu **Luật Bảo vệ Dữ liệu Cá nhân 2025** (thay cho Nghị định 13/2023/NĐ-CP hết hiệu lực 01/01/2026); consent, audit log, data-subject rights.

## Cách dùng
- File `.md` chứa sơ đồ **Mermaid** → render trực tiếp trên GitHub / VS Code.
- File `.xlsx` mở bằng Excel; `.drawio` mở bằng draw.io / diagrams.net.
