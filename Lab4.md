# Lab 4 - Thiết kế ca sử dụng cho hệ thống "Payroll System" dựa vào kết quả phân tích ca sử dụng và các phần tử thiết kế
## 1. Ca sử dụng: Timecard
### 1.1 Mô tả sự tương tác giữa các đối tượng thiết kế
  - Tác nhân: Nhân viên
### 1.2 Đơn giản hóa sơ đồ sequence bằng Subsystem
![Diagram](https://www.planttext.com/api/plantuml/png/h9JDIWCn58NtUOhx0ds1BgHGVz6AYovqcMP2PsHoCwIPGfVYmeLFu49iAIA81GLNauMBGDyZJ-0hcB4KMpe_MjmCPCZvEFUSIpxDHskWgTAfY0bbMYhO4qaiHvmJ9b4h6KCt4fnH5UnB9JP-jXVdc2lIaoa6L8tWw4p9IyvqXoBjSy5Hxr9DUtJ02LdIeR6p1cv2nva747QC4DeN3467BZF0_FTH0BFls2UhWbN0ZuacdFZxem8nX94pDmZQPPE8R2hBUCTUTYr0Axebj3oDfTc0-d47Ti92F_yK0cVUm4wGb2kXKUAsgrmsXQ4pLwNK8fSRPHmuCujg4OiUl7ZPQXCEyxWmZyhS5bLOiG2d_juiWRudt4DinmA6URhiLxMtlxMO8tG5ehxlDT3V1hYmpoambpsb4CzVqwqtk4PRFqCPeIfyP-wIRHsV-nLPH8Q0EUWVlBOu1lcZz0K00F__0m00)

### 1.3 Mô tả hành vi lưu trữ
Hệ thống thẻ chấm công sẽ lưu trữ những thông tin sau cho mỗi nhân viên:
- ID nhân viên
- Ngày, giờ vào ra
- Giờ làm việc
- Trạng thái thẻ chấm công

### 1.4 Tinh chỉnh mô tả luồng sự kiện
**Luồng sự kiện chính** (Chấm công và lưu trữ):
  1. Nhân viên mở màn hình thẻ chấm công:
     
     - TimecardForm hiển thị thẻ chấm công hiện tại.
     - TimecardController lấy dữ liệu từ cơ sở dữ liệu (hoặc cache) thông qua lời gọi đến IProjectManagementDatabase.
  2. Nhân viên nhập giờ làm việc:
     
     - TimecardForm nhận đầu vào từ nhân viên và gửi yêu cầu cập nhật đến TimecardController.
  3. Cập nhật giờ làm việc:
     
     - TimecardController kiểm tra tính hợp lệ của dữ liệu nhập.
     - TimecardController lưu thông tin vào cơ sở dữ liệu.
  4. Lưu hoặc nộp thẻ chấm công:
     - Khi nhân viên yêu cầu lưu hoặc nộp thẻ, TimecardController xác thực trạng thái thẻ.
     - TimecardController cập nhật trạng thái và ghi dữ liệu vào hệ thống lưu trữ.
**Luồng sự kiện phụ** (Lấy danh sách mã dự án):
  1. Khi nhân viên mở màn hình thẻ chấm công, TimecardController gửi yêu cầu tới IProjectManagementDatabase.
  2. Hệ thống trả về danh sách mã dự án để hiển thị.
### 1.5 Hợp nhất các lớp và hệ thống con
1. **Hợp nhất ChargeNumList với IProjectManagementDatabase**: Danh sách mã dự án có thể được quản lý như một phần của IProjectManagementDatabase thay vì một lớp riêng.
2. **Tinh giản TimecardController**: TimecardController có thể gộp logic liên quan đến kiểm tra thẻ chấm công và giao tiếp với hệ thống lưu trữ để giảm số lượng bước trung gian.
3. **Tích hợp xử lý trạng thái thẻ chấm công**: Tích hợp logic kiểm tra và cập nhật trạng thái thẻ vào một phương thức duy nhất trong TimecardController.

---
## 2. Ca sử dụng: RunPayroll
### 2.1 Mô tả sự tương tác giữa các đối tượng thiết kế
- SystemClock: Kích hoạt quy trình tính lương.
### 2.2 Đơn giản hóa sơ đồ sequence bằng Subsystem
![Diagram](https://www.planttext.com/api/plantuml/png/Z5EzJiCm4Dxz53V2q1V8WAgs0wWCbOfG9SHWagYswfv3uY3b6PYO65W8224X8fWJeGv6VGy_0Q-0qmObb1Jm42jtzzrtFvy_YaKtKZHKyLmGwYePmZY9b3_l2-dEAakFucnjhGoZaAFoGq82Y-Gk3oWg6D4ab4ACNUPxiR3U5cTVeYhl4jlWWSxU3xW3Gvsv39WqUQhWF4v0XVeP6IYTsQzOlYvJd99DN2DNpUP0p-Gl2jwlJFuOjsUeenif1bJHCnhv3XoQ_241ZrfWf5DR639zXt31zHEIZMZej1SnQ4SJ8MK09yUckE4mDyKrRxfF2TZploAFlZNMmFrLcJNP0TgDRoUhLU30n1GP2Fq6YfKjAQbJN27he6rCGvClodMQ_1wcd4hmJ77fib-8AxKvS80GC6xnyLUBi8EhNzUk5NVNATRHs-WdTlfskYRF43WI7ptI9e1MGUvBVOkWh12QUYHTcwHyFfy0003__mC0)

### 2.3 Mô tả hành vi lưu trữ
`Employee Table`:
- employeeId: Mã định danh nhân viên.
- name: Tên nhân viên.
- paymentMethod: Phương thức thanh toán (chuyển khoản/in phiếu).
- status: Trạng thái nhân viên (đang làm việc, bị xóa, nghỉ việc).
  
`Paycheck Table`:
- paycheckId: Mã phiếu lương.
- employeeId: Liên kết với nhân viên.
- amount: Số tiền thanh toán.
- date: Ngày thanh toán.
- status: Trạng thái thanh toán (chưa thanh toán/đã thanh toán).

**Hành vi lưu trữ**:
- Khi tính toán lương:
  - Dữ liệu về lương được lưu vào Paycheck Table.
  - Thông tin này được cập nhật trạng thái sau khi quá trình thanh toán hoặc in phiếu lương hoàn thành.
- Khi kiểm tra trạng thái:
  - PayrollController truy vấn vào cơ sở dữ liệu để lấy thông tin về trạng thái của nhân viên (đang làm việc hoặc đã bị xóa).
  - Nếu nhân viên bị đánh dấu bị xóa, không thực hiện tính lương và xóa hồ sơ nhân viên khỏi danh sách tạm.
### 2.4 Tinh chỉnh mô tả luồng sự kiện
Luồng sự kiện chính (Run Payroll):
1. Kích hoạt: SystemClock gửi lệnh kích hoạt đến PayrollScheduler để bắt đầu quy trình tính lương.
2. Lấy danh sách nhân viên: PayrollController truy vấn PayrollDatabase để lấy danh sách nhân viên đủ điều kiện thanh toán.
3. Tính toán và thanh toán lương:
   - Với mỗi nhân viên:
     - Tính toán khoản lương (bao gồm cả khấu trừ).
     - Nếu phương thức thanh toán là "Direct Deposit":
       - Gửi giao dịch chuyển khoản qua BankSystem.
       - Thử lại nếu giao dịch thất bại.
     - Nếu phương thức thanh toán là "Mail" hoặc "Pick-Up":
     - Gửi yêu cầu in phiếu lương qua Printer.
4. Cập nhật trạng thái: PayrollController cập nhật trạng thái thanh toán vào PayrollDatabase.
5. Hoàn tất: PayrollScheduler nhận thông báo từ PayrollController rằng quy trình tính lương đã hoàn tất.
### 2.5 Hợp nhất các lớp và hệ thống con
- **Tách biệt hệ thống con**: Logic cụ thể của việc retry giao dịch ngân hàng hoặc quản lý lỗi in phiếu lương đã được trừu tượng hóa trong BankSystemProxy và PrinterServiceProxy. Điều này đảm bảo PayrollController không cần quản lý chi tiết này.
- **Đơn giản hóa**: Loại bỏ xử lý trực tiếp với các chi tiết nhỏ như trạng thái của nhân viên (xóa hoặc không) trong sơ đồ chính. Thay vào đó, sử dụng các module hoặc lớp độc lập trong PayrollDatabase để thực hiện kiểm tra này.
