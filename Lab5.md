# Payroll System Subsystem Design
## 1. Distribute Subsystem Behavior to Subsystem Elements
Hệ thống được chia thành 4 hệ thống con chính, mỗi hệ thống con đảm nhiệm các chức năng cụ thể:

**a) Timecard Subsystem**
- Chức năng chính: Quản lý giờ làm việc và trạng thái thẻ chấm công.
- Thành phần chính:
  - `TimecardController`: Xử lý logic nghiệp vụ liên quan đến thẻ chấm công.
  - `TimecardForm`: Giao diện nhập liệu giờ làm việc và trạng thái thẻ.
  - `ProjectManagementDatabase`: Lấy danh sách mã dự án.
    
**b) Payroll Processing Subsystem**
- Chức năng chính: Tính toán và thực hiện thanh toán lương.
- Thành phần chính:
  - `PayrollController`: Quản lý logic nghiệp vụ liên quan đến tính toán lương.
  - `BankSystemProxy`: Kết nối với ngân hàng để chuyển khoản lương.
  - `PrinterServiceProxy`: In phiếu lương.
  - `PayrollDatabase`: Lưu trữ thông tin lương.
    
**c) Employee Management Subsystem**
- Chức năng chính: Quản lý thông tin nhân viên và trạng thái (đang làm việc, bị xóa, nghỉ việc).
- Thành phần chính:
  - `Employee`: Thực thể lưu trữ thông tin nhân viên.
  - `EmployeeDatabase`: Cơ sở dữ liệu nhân viên.
    
**d) Scheduler Subsystem**
- Chức năng chính: Kích hoạt quy trình tính lương theo lịch.
- Thành phần chính:
  - `SystemClock`: Kích hoạt quy trình Run Payroll theo thời gian định trước.
## 2. Document Subsystem Elements
Mô tả chi tiết về các hệ thống con:

### Timecard Subsystem
- Quản lý thông tin giờ làm việc của nhân viên.
- Lấy danh sách mã dự án từ cơ sở dữ liệu.
- Cập nhật trạng thái thẻ chấm công.
### Payroll Processing Subsystem
- Xử lý tính toán lương cho từng nhân viên dựa trên giờ làm việc và trạng thái.
- Thực hiện thanh toán qua ngân hàng hoặc in phiếu lương.
- Lưu thông tin lương vào cơ sở dữ liệu.
### Employee Management Subsystem
- Lưu trữ thông tin nhân viên.
- Cập nhật trạng thái nhân viên (đang làm việc hoặc bị xóa).
- Cung cấp thông tin cho các hệ thống con khác.
### Scheduler Subsystem
- Kích hoạt quy trình tính lương tự động vào thời gian được định trước.
## 3. Describe Subsystem Dependencies
Mối quan hệ phụ thuộc giữa các hệ thống con:
- Timecard Subsystem phụ thuộc vào Employee Management Subsystem để lấy thông tin nhân viên.
- Payroll Processing Subsystem phụ thuộc vào:
  - Employee Management Subsystem để lấy danh sách nhân viên.
  - Timecard Subsystem để lấy thông tin giờ làm việc.
- Scheduler Subsystem không phụ thuộc vào các hệ thống con khác nhưng kích hoạt Payroll Processing Subsystem.
### Subsystem Dependency Diagram
![Diagram](https://www.planttext.com/api/plantuml/png/Z99DJiCm48NtFiMe-rwW2rHHg402gL8giK1PJ9qXTUEVQkmW8iJ9M70ahe2R7ng8aLXwvitttepy-Vwnz04vr4QB8yeAIuBPLXcIo0LazSutFf2PmQi0U1mQAsS3Ews9yt5vxTYqXGsx0ybmZpRo3DbmXG5tw2aNR-Biiy7cH84eb-IzikN4iPVyChn4MsMjB8w-DBsdie4u8tvMaaRrZf1ES6sEsZL4S8uwYJ1eyl4ZZSladeewffn0khGhxMJLZgHE2VFvHS815h2c8FVm7VRMFZcHECs_0NVAXxy1gMW3ui5n1JUkPYz-xDHD9eWBsB8gotYIlYcMP8lJT_i2003__mC0)
## 4. Checkpoints
- **Phân chia hợp lý**: Mỗi hệ thống con có trách nhiệm riêng biệt, với các thành phần được phân bổ rõ ràng.
- **Phụ thuộc rõ ràng**: Mối quan hệ giữa các hệ thống con được thể hiện rõ qua sơ đồ và các phụ thuộc cụ thể.
- **Tính mở rộng**: Các hệ thống con có thể mở rộng hoặc thay đổi mà không ảnh hưởng đến toàn bộ hệ thống.
