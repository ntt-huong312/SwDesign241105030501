# Lab 2
## I. Phân tích tất cả các ca sử dụng còn lại trong hệ thống Payroll System
### 1. Create Employee
#### 1.1. Xác định các lớp phân tích
- **Boundary**:
  - **ReportSelectionForm**: Lớp giao diện để kết nối và tương tác với ProjectManagementDatabase, giúp ReportController truy xuất thông tin charge numbers từ cơ sở dữ liệu dự án khi Employee chọn loại báo cáo "Total Hours Worked for a Project".
  - **ProjectDatabaseInterface**: Giao diện trung gian giữa ReportController và ProjectManagementDatabase, hỗ trợ truy xuất charge numbers khi báo cáo yêu cầu thông tin dự án.
- **Control**:
  - **ReportController**: Quản lý logic nghiệp vụ cho việc tạo báo cáo, bao gồm xử lý thông tin từ **ReportSelectionForm**, truy xuất dữ liệu qua **ProjectDatabaseInterface**, và điều khiển quá trình lưu báo cáo nếu Employee yêu cầu.
- **Entity**:
  - **Employy**: Đại diện cho thông tin của nhân viên.
  - **Report**: Thực thể chứa các loại báo cáo, các tiêu chí báo cáo và kết quả của báo cáo.
  - **ProjectManagementDatabase**: Cơ sở dữ liệu chứa charge numbers và thông tin dự án, hỗ trợ cho việc tạo báo cáo liên quan đến các dự án.
#### 1.2. Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/d5N1Qjj04BtlLmmvnU3yWC4bn6vfgHDAeqElQtahgQnspNfLqB7qa4CfD8SU2p6b508XBRr9XnpMz3_s2_eBdPLYMQuarwr0mbxDU_jctipgLtvtlD1KwIJcXFfQAdWOpxbC6IDJcOWPLIayPtEfz3dZpDUH58-aYealXLQItxyRbVyuKnlKCoLV8M1CDPtI1NiYD5ClgSy84phIrVjJAcZ0ObnSHwu3Icf2XaCuiTcjXjMbpRuce6ssb30r-F3TOpWaQyrmzA1DxG3yqERlnKGYD3f1q0ZlmnvfYTrGR98QG6gkav7RtNERLmnyYx0F8Z1NQI5szS55twyyjTcTzaAJ-Jr2ADTmXWj9BGLkhk30i_b74K0GsVoJMubHjOIPpR-3MOe30dZzgSofxIhq0BZDlgHZAi9pi_J3K_DvZ6JcZS3C7LaNi4RQT6S0MYNfYmIfzIYaAc1dIJnbQh5DsWJ2qKwjixNCBTA_w6prQWTJM_bQ-oL44zuA3xlcNNVzzkow1cxlhWjiVXFLu77riuT3CYj6msjEGtUMWt9u_hz_-r3NK99ssM3psmcMyI9PynTw7nUL1UrAMvFjMhsgvyuSkfsgqcfklJLtrJwbFy1_VgiDutxMLWV21C6r4-MV_ELTs7RlNFZXQqpKK-Qc3zfS2pmpBkQRPYYCmjgYKtiTYwjByqC4DGd7oEG-1Ry1003__mC0)
#### 1.3. Biểu đồ lớp
![Diagram](https://www.planttext.com/api/plantuml/png/V5D1JiCm4Bpt5Jd28H_80LLgGLG2LBNzmDQPfW773ckdKeHu6GUUn1UmwpWKaf3Rh6PtPpoRhu_FkR74jgdaJ4Wo9jcWrcota12srEfESvMypHB_cNCn47PjZQlhK8Uou2LPR4WLVJKlJIsf3NHNV9zr6zQidzqSrq1xCbZvxWC9n3K7M75S78aBF3NL7cmkkyEyXLQMjPJWhYlbNbR0PrjUL81G-GyG5yF3Ji7m-gFMO9TE6Ag_hMgfMqIrAJgyoWDML8KjIG4RoIjrq4CJKzBp-9G1Mcr9tkk6JS0d4kIZsPRYvG5EP2Yt8DvfRt9DxPJF0WhiAD6ZqnYqB66fb6OafqTILA1o8SV4Ob0CooLE6Cbgx8hIz6QONkQcl3Omjd_f0SNtJTvCDduka_oBOIF6ijwJBqs9wTBB_bxDF-JVBv4DVewvkq__3tu3003__mC0)

#### Mô Tả Use Case "Create Report"
#### Lớp `ReportSelectionForm`
- **Mô tả**: Giao diện người dùng cho **Employee** để chọn và nhập thông tin báo cáo.
- **Thuộc tính**:
  - `reportType`: Loại báo cáo mà **Employee** đã chọn (ví dụ: tổng giờ làm, giờ làm cho dự án, nghỉ phép, tổng lương).
  - `startDate` và `endDate`: Khoảng thời gian cho báo cáo.
  - `chargeNumber`: Mã dự án nếu **Employee** chọn báo cáo theo dự án.
- **Phương thức**:
  - `selectReportType()`: Cho phép **Employee** chọn loại báo cáo.
  - `enterDateRange()`: Cho phép **Employee** nhập ngày bắt đầu và kết thúc.
  - `displayReport()`: Hiển thị báo cáo đã tạo cho **Employee**.

#### Lớp `ProjectDatabaseInterface`
- **Mô tả**: Giao diện giữa **ReportController** và **ProjectManagementDatabase** để lấy thông tin dự án khi cần.
- **Phương thức**:
  - `fetchChargeNumbers()`: Lấy danh sách **charge numbers** từ **ProjectManagementDatabase** để cung cấp cho **ReportController** khi cần dữ liệu về dự án.


#### Lớp `ReportController`
- **Mô tả**: Điều phối và xử lý logic nghiệp vụ của việc tạo và lưu báo cáo.
- **Thuộc tính**:
  - `reportType`: Loại báo cáo mà **Employee** chọn.
  - `startDate`: Ngày bắt đầu của báo cáo.
  - `endDate`: Ngày kết thúc của báo cáo.
  - `chargeNumber`: Mã dự án nếu báo cáo là cho một dự án cụ thể.
- **Phương thức**:
  - `createReport()`: Kiểm tra thông tin từ **ReportSelectionForm**, truy xuất dữ liệu nếu cần, và tạo báo cáo.
  - `saveReport()`: Lưu báo cáo đã tạo vào vị trí được chỉ định nếu **Employee** yêu cầu.

#### Lớp `Employee`
- **Mô tả**: Đại diện cho thông tin của nhân viên.
- **Thuộc tính**:
  - `employeeId`: Mã định danh của nhân viên.
  - `name`: Tên của nhân viên.
- **Phương thức**:
  - `getEmployeeInfo()`: Truy xuất thông tin của nhân viên.

#### Lớp `Report`
- **Mô tả**: Thực thể lưu trữ thông tin của báo cáo được tạo ra.
- **Thuộc tính**:
  - `reportType`: Loại báo cáo.
  - `dateRange`: Khoảng thời gian của báo cáo.
  - `totalHours`: Tổng giờ làm việc (nếu là báo cáo tổng giờ làm).
  - `vacationSickLeave`: Thời gian nghỉ phép hoặc nghỉ bệnh (nếu báo cáo là nghỉ phép).
  - `yearToDatePay`: Tổng thu nhập năm-to-date (nếu báo cáo là lương).
  - `chargeNumber`: Mã dự án (nếu báo cáo là cho một dự án cụ thể).
- **Phương thức**:
  - `generate()`: Tạo báo cáo theo yêu cầu và thông tin được cung cấp.
  - `getReportDetails()`: Truy xuất chi tiết báo cáo.

#### Lớp `ProjectManagementDatabase`
- **Mô tả**: Cơ sở dữ liệu chứa thông tin về các dự án.
- **Phương thức**:
  - `retrieveChargeNumbers()`: Truy xuất danh sách các **charge numbers** từ cơ sở dữ liệu.
---

### 2. Maintain Purchase Order
### 3. Login
### 4. Create Administrative Report
### 5. Maintain Employee Info
### 6. Run Payroll
## II. Viết code Java mô phỏng ca sử dụng Maintain Timecard
