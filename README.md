### Hệ Thống Quản Lý Cửa Hàng Phụ Tùng Xe Máy Tài

> Dự án môn **Quản Trị Cơ Sở Dữ Liệu** | Trường Đại Học Kinh Tế Đà Nẵng | 01/2025 - 05/2025 

---

### Giới thiệu

Dự án xây dựng hệ thống cơ sở dữ liệu quản lý toàn bộ hoạt động kinh doanh của **Cửa hàng phụ tùng xe máy Tài** (Thị trấn Di Lăng, Sơn Hà, Quảng Ngãi) — một cửa hàng quy mô nhỏ đang gặp khó khăn trong việc theo dõi nhập xuất hàng, kiểm soát công nợ và quản lý giá bán.

Trọng tâm của dự án là việc chuyển đổi các quy trình nghiệp vụ thủ công tại cửa hàng thành một Mô hình dữ liệu quan hệ (Relational Model) chuẩn hóa, đảm bảo tính nhất quán và tối ưu hiệu suất truy vấn.

---

### Mục tiêu hệ thống

- Quản lý quy trình **nhập hàng** từ nhà cung cấp
- Kiểm soát **tồn kho** và giá bán theo thời gian
- Quản lý quy trình **bán hàng** và xuất hóa đơn
- Theo dõi **công nợ khách hàng** theo từng lần thanh toán
- Đảm bảo **bảo mật** và **tính sẵn sàng** của hệ thống

---

### Các bảng dữ liệu chính

| Bảng | Mô tả |
|---|---|
| `NHACUNGCAP` | Thông tin nhà cung cấp |
| `HANGHOA` | Danh mục hàng hóa / phụ tùng |
| `QUANLYGIA` | Lịch sử giá bán theo thời gian |
| `HD_NHAP` | Hóa đơn nhập hàng |
| `CTHD_NHAP` | Chi tiết hóa đơn nhập |
| `KHACHHANG` | Thông tin khách hàng |
| `NHANVIEN` | Thông tin nhân viên |
| `HD_BAN` | Hóa đơn bán hàng |
| `CTHD_BAN` | Chi tiết hóa đơn bán |
| `SOGHINO` | Sổ ghi nợ khách hàng |
| `CT_SOGHINO` | Chi tiết thanh toán công nợ |
| `CT_KHTRA` | Chi tiết hàng khách trả lại |

---

### Tính năng kỹ thuật

### Trigger tự động
- `spSLTonKho` — Tự động cập nhật số lượng tồn kho khi có giao dịch nhập/bán
- `TUDONG_APDUNG_GIA` — Tự động áp dụng giá bán hiện hành khi tạo hóa đơn
- `tQuanLy_CongNo` — Tự động cập nhật công nợ khách hàng sau mỗi giao dịch

### Stored Procedures
- Xử lý các nghiệp vụ nhập hàng, bán hàng, thanh toán nợ
- Sử dụng tham số hóa truy vấn để chống SQL Injection

### Bảo mật
- Phân quyền theo vai trò (Role-based Access Control):
  - `QuanLy` — toàn quyền
  - `NhanVien` — xem và thao tác nghiệp vụ, hạn chế thông tin nhạy cảm khách hàng
- Xác thực đăng nhập qua SQL Server Authentication
- Áp dụng mã hóa đối xứng bảo vệ dữ liệu nhạy cảm
- Phòng chống SQL Injection qua stored procedures và xác thực đầu vào

### Tính sẵn sàng
- Backup tự động theo lịch (Full / Differential).
- Phân vùng dữ liệu (Partition) — giải pháp khi dữ liệu vượt quá dung lượng một ổ đĩa.
- Đề xuất giải pháp đảm bảo hoạt động 24/7.

---

### Công nghệ sử dụng

| Công nghệ | Mục đích |
|---|---|
| **SQL Server** | Hệ quản trị cơ sở dữ liệu chính |
| **T-SQL** | Viết trigger, stored procedure, query |
| **ERD (Draw.io)** | Thiết kế mô hình dữ liệu |
| **Python (Faker)** | Tự động sinh dữ liệu mẫu thực tế |

---

### Thành viên nhóm

| Họ tên | Vai trò |
|---|---|
| Hoàng Thị Kim Dung | Nhóm trưởng |
| Đặng Như Trầm | Thành viên |
| Đinh Trương Đan Thuy | Thành viên |
| **Lê Thị Nhung** | Thành viên |
| Huỳnh Ngọc Thủy Tiên | Thành viên |

---
## Đóng Góp Cá Nhân — Lê Thị Nhung

### 1. Phân tích dữ liệu nghiệp vụ (R1 — Xây dựng CSDL)

- Thực hiện **Bước 1 — Chọn lọc thông tin** cho phân hệ Hóa đơn nhập: sàng lọc các trường từ hồ sơ/chứng từ thực tế, xác định từ rõ nghĩa và ký hiệu viết tắt chuẩn (ví dụ: `MAHD_NHAP`, `DONGIA_NHAP`, `TONGTIENHANG`, `TONGCONG`, ...).
- Thực hiện **Bước 2 — Xác định thực thể và thuộc tính** cho phân hệ nhập hàng, bao gồm các thực thể: `NHACUNGCAP`, `NHANVIEN`, `HANGHOA`, `HD_NHAP`.

### 2. Thiết kế & Chuẩn hóa dữ liệu (R1 — Xây dựng CSDL)

- Chuyển đổi các thực thể thành **mô hình quan hệ** (Relational Model): xác định khóa chính, khóa ngoại, ràng buộc toàn vẹn cho các bảng `HD_NHAP` và `CTHD_NHAP`.
- Thực hiện **chuẩn hóa dữ liệu** (1NF → 2NF → 3NF) đảm bảo tính nhất quán và loại bỏ dư thừa.
- Thiết kế **thiết kế mức vật lý** cho bảng `HD_NHAP` và `CTHD_NHAP` (kiểu dữ liệu, ràng buộc, câu lệnh `CREATE TABLE`).
  
### 3. Xây dựng logic nghiệp vụ — Trigger & Stored Procedure (R2 — Lập trình CSDL)

Thiết kế và cài đặt các module tự động hóa nghiệp vụ cốt lõi:

| Module | Tên đối tượng | Chức năng |
|---|---|---|
| Module 1 | Trigger trên `CTHD_NHAP` | Tự động tính `THANHTIEN`, cập nhật `TONGTIENHANG`/`TONGCONG` trong `HD_NHAP`, cộng dồn tồn kho vào `HANGHOA`, thêm giá nhập mới vào `QUANLYGIA`, cập nhật công nợ `NHACUNGCAP` |
| Module 2 | `spSLTonKho` | Kiểm tra hàng tồn trước khi bán, tự động cập nhật `SL_TON` trong `HANGHOA` sau giao dịch bán |
| Module 4 | `TUDONG_APDUNG_GIA` | Tự động áp dụng giá bán hiện hành từ `QUANLYGIA` khi tạo hóa đơn bán |

### 4. Phòng chống SQL Injection (R3 — Bảo mật CSDL)

Tham gia xây dựng và triển khai các biện pháp hạn chế tấn công SQL Injection:

- Tham số hóa truy vấn — Minh họa thực thi bằng C# (`SqlCommand` + `Parameters.Add`), đảm bảo giá trị đầu vào được xử lý như dữ liệu thuần túy, không bao giờ được nhúng trực tiếp vào câu lệnh SQL.
- Xác thực đầu vào — Áp dụng biểu thức chính quy (Regex) để kiểm soát và lọc dữ liệu người dùng nhập vào, chặn các ký tự nguy hiểm.
- Triển khai Stored Procedure — Toàn bộ nghiệp vụ xử lý dữ liệu đi qua stored procedure thay vì truy vấn trực tiếp, kết hợp với nguyên tắc đặc quyền tối thiểu.
---
### Thông tin đồ án

- **Môn học:** Quản Trị Cơ Sở Dữ Liệu  
- **Lớp:** 49K21.2 — Nhóm 49K212.08  
- **Trường:** Đại Học Kinh Tế Đà Nẵng  
- **Thời gian:** 01/2025  
- **Địa điểm khảo sát:** Cửa hàng phụ tùng xe máy Tài, Thị trấn Di Lăng, Sơn Hà, Quảng Ngãi.
