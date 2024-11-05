# Lab 2
## I. Phân tích tất cả các ca sử dụng còn lại trong hệ thống Payroll System
### 1. Create Employee
#### 1.1. Xác định các lớp phân tích
- **Boundary**:
  - **ReportSelectionForm**: Giao diện người dùng cho **Employee** để chọn loại báo cáo, nhập thông tin báo cáo (như loại báo cáo, ngày bắt đầu, ngày kết thúc) và hiển thị kết quả báo cáo.
  - **ProjectDatabaseGateway**:
- **Control**:
  - **ReportController**: Điều khiển logic nghiệp vụ của quy trình tạo báo cáo, bao gồm xử lý các thông tin báo cáo từ **Employee**, truy xuất dữ liệu từ **Project Management Database** khi cần, và điều khiển quá trình lưu báo cáo. 
- **Entity**:
  - **Employy**: Đại diện cho thông tin của nhân viên.
  - **Report**: Thực thể báo cáo, chứa các loại báo cáo khác nhau, các tiêu chí báo cáo và kết quả của báo cáo.
  - **ProjectManagementDatabase**: Cơ sở dữ liệu chứa thông tin các charge numbers của dự án.
#### 1.2. Biểu đồ Sequence
#### 1.3. Biểu đồ lớp
### 2. Maintain Purchase Order
### 3. Login
### 4. Create Administrative Report
### 5. Maintain Employee Info
### 6. Run Payroll
## II. Viết code Java mô phỏng ca sử dụng Maintain Timecard
