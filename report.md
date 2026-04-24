# BÁO CÁO KẾT QUẢ THỰC HIỆN DỰ ÁN DATA PIPELINE

**Họ tên:** Nguyễn Hữu Huy  
**MSSV:** 2A202600166  
**Ngày báo cáo:** 24/04/2026

---

## 1. Mục tiêu
Xây dựng một đường ống dữ liệu (Data Pipeline) hoàn chỉnh để xử lý dữ liệu phi cấu trúc (PDF, Video Transcript) thành dạng chuẩn hóa, phục vụ cho hệ thống cơ sở tri thức (Knowledge Base).

## 2. Các công việc đã thực hiện

### 2.1. Định nghĩa Cấu trúc Dữ liệu (Schema)
- Thực hiện tại file `starter_code/schema.py`.
- Sử dụng **Pydantic** để xây dựng model `UnifiedDocument` với các trường:
    - `document_id`: Mã định danh tài liệu.
    - `source_type`: Loại nguồn (PDF/Video).
    - `author`: Tên tác giả/người tạo.
    - `category`: Danh mục nội dung.
    - `content`: Nội dung văn bản đã làm sạch.
    - `timestamp`: Thời gian tạo/xuất bản.

### 2.2. Xây dựng quy trình ETL (Extract - Transform - Load)
- Thực hiện tại file `starter_code/process_unstructured.py`.
- **Làm sạch dữ liệu PDF:** Sử dụng biểu thức chính quy (Regex) để loại bỏ các thông tin nhiễu như `HEADER_PAGE_X` và `FOOTER_PAGE_X`.
- **Chuẩn hóa Video:** Trích xuất thông tin từ transcript và metadata của video để chuyển đổi sang định dạng chung.

### 2.3. Kiểm soát chất lượng (Quality Check)
- Thực hiện tại file `starter_code/quality_check.py`.
- Triển khai hàm `run_semantic_checks` để lọc dữ liệu rác:
    - Loại bỏ tài liệu có nội dung quá ngắn (< 10 ký tự).
    - Phát hiện và loại bỏ các lỗi hệ thống/OCR (ví dụ: "Null pointer exception", "Traceback").

### 2.4. Điều phối hệ thống (Orchestration)
- Thực hiện tại file `starter_code/orchestrator.py`.
- Tự động hóa việc đọc dữ liệu từ thư mục `raw_data`, gọi các hàm xử lý tương ứng và thực hiện kiểm tra chất lượng.
- Xuất kết quả cuối cùng ra file `processed_knowledge_base.json`.

## 3. Kết quả
- Toàn bộ pipeline hoạt động ổn định.
- Dữ liệu thô đã được làm sạch và cấu trúc hóa thành định dạng JSON chuẩn, sẵn sàng cho các giai đoạn tiếp theo của dự án.
