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
### Hợp nhất các lớp và hệ thống con
1. **Hợp nhất ChargeNumList với IProjectManagementDatabase**: Danh sách mã dự án có thể được quản lý như một phần của IProjectManagementDatabase thay vì một lớp riêng.
2. **Tinh giản TimecardController**: TimecardController có thể gộp logic liên quan đến kiểm tra thẻ chấm công và giao tiếp với hệ thống lưu trữ để giảm số lượng bước trung gian.
3. **Tích hợp xử lý trạng thái thẻ chấm công**: Tích hợp logic kiểm tra và cập nhật trạng thái thẻ vào một phương thức duy nhất trong TimecardController.
