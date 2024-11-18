# Lab 2
## I. Phân tích tất cả các ca sử dụng còn lại trong hệ thống Payroll System
### 1. Create Employee
#### 1.1. Xác định các lớp phân tích
- **Boundary**:
  - **ReportSelectionForm**: Lớp giao diện để kết nối và tương tác với *ProjectManagementDatabase*, giúp *ReportController* truy xuất thông tin charge numbers từ cơ sở dữ liệu dự án khi Employee chọn loại báo cáo "Total Hours Worked for a Project".
  - **ProjectDatabaseInterface**: Giao diện trung gian giữa *ReportController* và *ProjectManagementDatabase*, hỗ trợ truy xuất charge numbers khi báo cáo yêu cầu thông tin dự án.
- **Control**:
  - **ReportController**: Quản lý logic nghiệp vụ cho việc tạo báo cáo, bao gồm xử lý thông tin từ **ReportSelectionForm**, truy xuất dữ liệu qua *ProjectDatabaseInterface*, và điều khiển quá trình lưu báo cáo nếu Employee yêu cầu.
- **Entity**:
  - **Employee**: Đại diện cho thông tin của nhân viên.
  - **Report**: Thực thể chứa các loại báo cáo, các tiêu chí báo cáo và kết quả của báo cáo.
  - **ProjectManagementDatabase**: Cơ sở dữ liệu chứa charge numbers và thông tin dự án, hỗ trợ cho việc tạo báo cáo liên quan đến các dự án.
#### 1.2. Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/d5N1Qjj04BtlLmmvnU3yWC4bn6vfgHDAeqElQtahgQnspNfLqB7qa4CfD8SU2p6b508XBRr9XnpMz3_s2_eBdPLYMQuarwr0mbxDU_jctipgLtvtlD1KwIJcXFfQAdWOpxbC6IDJcOWPLIayPtEfz3dZpDUH58-aYealXLQItxyRbVyuKnlKCoLV8M1CDPtI1NiYD5ClgSy84phIrVjJAcZ0ObnSHwu3Icf2XaCuiTcjXjMbpRuce6ssb30r-F3TOpWaQyrmzA1DxG3yqERlnKGYD3f1q0ZlmnvfYTrGR98QG6gkav7RtNERLmnyYx0F8Z1NQI5szS55twyyjTcTzaAJ-Jr2ADTmXWj9BGLkhk30i_b74K0GsVoJMubHjOIPpR-3MOe30dZzgSofxIhq0BZDlgHZAi9pi_J3K_DvZ6JcZS3C7LaNi4RQT6S0MYNfYmIfzIYaAc1dIJnbQh5DsWJ2qKwjixNCBTA_w6prQWTJM_bQ-oL44zuA3xlcNNVzzkow1cxlhWjiVXFLu77riuT3CYj6msjEGtUMWt9u_hz_-r3NK99ssM3psmcMyI9PynTw7nUL1UrAMvFjMhsgvyuSkfsgqcfklJLtrJwbFy1_VgiDutxMLWV21C6r4-MV_ELTs7RlNFZXQqpKK-Qc3zfS2pmpBkQRPYYCmjgYKtiTYwjByqC4DGd7oEG-1Ry1003__mC0)

#### 1.3. Biểu đồ lớp
![Diagram](https://www.planttext.com/api/plantuml/png/h5DBJiCm4Dtx55uMARq2gXH0GWA4A1UOEXCmyWzxKYb2d8m5H-8AE8d9fqcX2xBnoFDv7q--FZutWS1JfHKJ2aBWbzefMoFoDyRRBw12GG_ehAV7sk7gR9Auz_Ob7hajXep7rme3RM6FNL_ClBC4qDrissPfpPNr-c-iGWQde1w1tSX0X-a4vjlZ0WX-8vGGgvsM4n5kY6UiSsl8MwNGzvJJwDmZ44u8D08otjeRkSGGJT44Fz0badW-faYSFY_Z4yf9rwBt2QsnPWS1hmsXBq7WI0rvYNiSqGeB0sx1m1DgDFseVeAR2ZfqiA_x3u4hPGKqIvJnKYgy0zqzMR_3w_NvqhwnfHqSQeTNPhDdRwgEkSYEsZlgcbkt3D9TChQ99iI_yni00F__0m00)

#### Mô Tả Use Case "Create Report"
#### Lớp *ReportSelectionForm*
- **Mô tả**: Giao diện người dùng cho **Employee** để chọn và nhập thông tin báo cáo.
- **Thuộc tính**:
  - `reportType`: Loại báo cáo mà **Employee** đã chọn (ví dụ: tổng giờ làm, giờ làm cho dự án, nghỉ phép, tổng lương).
  - `startDate` và `endDate`: Khoảng thời gian cho báo cáo.
  - `chargeNumber`: Mã dự án nếu **Employee** chọn báo cáo theo dự án.
- **Phương thức**:
  - `selectReportType()`: Cho phép **Employee** chọn loại báo cáo.
  - `enterDateRange()`: Cho phép **Employee** nhập ngày bắt đầu và kết thúc.
  - `displayReport()`: Hiển thị báo cáo đã tạo cho **Employee**.

#### Lớp *ProjectDatabaseInterface*
- **Mô tả**: Giao diện giữa **ReportController** và **ProjectManagementDatabase** để lấy thông tin dự án khi cần.
- **Phương thức**:
  - `fetchChargeNumbers()`: Lấy danh sách **charge numbers** từ **ProjectManagementDatabase** để cung cấp cho **ReportController** khi cần dữ liệu về dự án.


#### Lớp *ReportController*
- **Mô tả**: Điều phối và xử lý logic nghiệp vụ của việc tạo và lưu báo cáo.
- **Thuộc tính**:
  - `reportType`: Loại báo cáo mà **Employee** chọn.
  - `startDate`: Ngày bắt đầu của báo cáo.
  - `endDate`: Ngày kết thúc của báo cáo.
  - `chargeNumber`: Mã dự án nếu báo cáo là cho một dự án cụ thể.
- **Phương thức**:
  - `createReport()`: Kiểm tra thông tin từ **ReportSelectionForm**, truy xuất dữ liệu nếu cần, và tạo báo cáo.
  - `saveReport()`: Lưu báo cáo đã tạo vào vị trí được chỉ định nếu **Employee** yêu cầu.

#### Lớp *Employee*
- **Mô tả**: Đại diện cho thông tin của nhân viên.
- **Thuộc tính**:
  - `employeeId`: Mã định danh của nhân viên.
  - `name`: Tên của nhân viên.
- **Phương thức**:
  - `getEmployeeInfo()`: Truy xuất thông tin của nhân viên.

#### Lớp *Report*
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

#### Lớp *ProjectManagementDatabase*
- **Mô tả**: Cơ sở dữ liệu chứa thông tin về các dự án.
- **Phương thức**:
  - `retrieveChargeNumbers()`: Truy xuất danh sách các **charge numbers** từ cơ sở dữ liệu.
---

### 2. Maintain Purchase Order
#### 2.1. Xác định các lớp phân tích
- **Boundary Classes**:
  - **PurchaseOrderForm**: Là lớp giao diện người dùng, cho phép *Commissioned Employee* nhập và hiển thị thông tin liên quan đến các đơn hàng mua, cũng như thực hiện các hành động tạo, cập nhật hoặc xóa đơn hàng.
- **Control Class**:
  - **PurchaseOrderController**: Điều khiển logic nghiệp vụ cho việc tạo, cập nhật và xóa các đơn hàng mua. *PurchaseOrderController* nhận yêu cầu từ *PurchaseOrderForm*, xử lý các yêu cầu này.
- **Entity Classes**:
  - **CommissionedEmployee**: Là subclass của Employee, đại diện cho nhân viên có quyền thực hiện các thao tác liên quan đến đơn hàng mua và nhận hoa hồng từ các đơn hàng đó.
  - **PurchaseOrder**: Thực thể đại diện cho đơn hàng mua, chứa thông tin về đơn hàng (khách hàng, sản phẩm, địa chỉ, ngày tháng, và mã đơn hàng).
  - **PurchaseOrderDatabase**: Cơ sở dữ liệu lưu trữ thông tin các đơn hàng mua, hỗ trợ các thao tác như thêm, cập nhật, xóa đơn hàng.
    
#### 2.2. Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/d98nImCn68Rt_8flLAXqlq4AyTH1Q0S7r_Gkz0ukISabuCqE3kBWxA27544f2ZfT1eUJ-n_v1Vu5SprBKwaTN99yoVE-UR-GB_Cno1MHIhCCaKW92LWmbkPvAZYDGpRDH44fa1nmYCP2yvZ80aPQHWd9wL36L1uAoLfWD6nNA19SIP6jCxZRpAZio5MDA5Uf-cNPGHkF3eWYOrTqoB9Qed-73nS0GZY4lVsVh07Wn9fh3YeX0bHTHh1pQgjIz03RQZu5dhX9zU2iVYExg1DrybK30HnPCq-Xg9yqHBPwrA1QZtxaMVJFdGDytZGbXwI-vnFaM_Y9ZbDhBjf4rboviNxd4r0fz-mtI9VF4C29hMQ5hrFMF4FKb91RSmUnDI-GkIikzLex0Ipwxljj-oxRamVmFvqNktdLMs4SkakqStLFC9i2gnzy79Wrjob20yhZzYT_0m00__y30000)
---

#### 2.3. Biểu đồ lớp
![Diagram](https://www.planttext.com/api/plantuml/png/d5JRIWCn47tVhmXzgc8BlYvIMheA1S6YNv0cOnl8PSqabI9-cGz-ahzWiZUQRTU2-x3Bp9avCsSosP-lxpawQfrNCikOf8XaQPGIYC9euFUgbEO0G3uo4Xzex5MHanTdXTxMVaqLf1vcjAFChVIhwO3FjiJQMxQZ24-MWtqmLhNyR6SCmeAvK7rybPEz4Rn6kC1IqaFaIm7ScVUAPrLqmFb2oz2IDLA2RSkLrZ10V8Ot3-XINcQ1EaW8ngQg4rf88dt91oABcmRa9qaS90ma_QsYxRq9xatTepEgbXgcdu8R8MKm5fpR83h5mYIuPovu7mMwktLjpevA5K56Jk9xeB40qKqmsWOj17xOdsXBafepf4bOB-RCt2xCg-x-w9IZUNbdIojOr6ZyHbOgprw5qUs8J2PaT3tg7KpUx0ncf_iTawRJMVKTMigSUEmd7y4THRzmD_YSK1Rt-Jya8LbHJRVzt4HkCzUyljr2OvRDGVFuy_W5003__mC0)

#### Lớp *CommissionedEmployee*
- **Mô tả**: Lớp đại diện cho nhân viên hoa hồng, người có thể tạo và quản lý các đơn hàng.
- **Thuộc tính**:
  - `employeeID`: Mã định danh của nhân viên.
  - `name`: Tên của nhân viên.
  - `contactInfo`: Thông tin liên lạc của nhân viên.
- **Mối quan hệ**: `CommissionedEmployee` có thể tạo nhiều `PurchaseOrder`.

#### Lớp *PurchaseOrderForm*
- **Mô tả**: Lớp giao diện giúp nhân viên hoa hồng chọn các thao tác liên quan đến đơn hàng và hiển thị thông tin cần thiết.
- **Phương thức**:
  - `chooseAction()`: Cho phép nhân viên chọn thao tác (tạo, cập nhật, xóa đơn hàng).
  - `displayInfo()`: Hiển thị thông tin chi tiết của đơn hàng.
  - `showOrderID()`: Hiển thị mã đơn hàng mới sau khi lưu.
- **Mối quan hệ**: `PurchaseOrderForm` sử dụng `PurchaseOrderController` để xử lý các yêu cầu.

#### Lớp *PurchaseOrderController*
- **Mô tả**: Lớp quản lý logic nghiệp vụ của việc tạo, cập nhật, và xóa đơn hàng.
- **Phương thức**:
  - `processRequest()`: Xử lý các yêu cầu từ giao diện.
  - `createPurchaseOrder(orderInfo)`: Tạo đơn hàng mới dựa trên thông tin từ nhân viên.
  - `updatePurchaseOrder(orderID, updatedInfo)`: Cập nhật đơn hàng dựa trên ID và thông tin mới.
  - `deletePurchaseOrder(orderID)`: Xóa đơn hàng dựa trên ID.
- **Mối quan hệ**: `PurchaseOrderController` sử dụng `PurchaseOrderDatabase` để lưu trữ và truy xuất dữ liệu và quản lý thông tin của `PurchaseOrder`.

#### Lớp *PurchaseOrder*
- **Mô tả**: Lớp lưu trữ thông tin chi tiết của đơn hàng.
- **Thuộc tính**:
  - `orderID`: Mã định danh của đơn hàng.
  - `customerContact`: Thông tin liên hệ của khách hàng.
  - `billingAddress`: Địa chỉ thanh toán của khách hàng.
  - `products`: Danh sách sản phẩm trong đơn hàng.
  - `orderDate`: Ngày tạo đơn hàng.
- **Mối quan hệ**: `PurchaseOrder` chứa danh sách `Product`.

#### Lớp *PurchaseOrderDatabase*
- **Mô tả**: Lớp đại diện cho cơ sở dữ liệu lưu trữ thông tin về đơn hàng.
- **Phương thức**:
  - `retrieveOrder(orderID)`: Lấy thông tin đơn hàng theo ID.
  - `saveOrder(order: PurchaseOrder)`: Lưu đơn hàng vào cơ sở dữ liệu.
  - `deleteOrder(orderID)`: Xóa đơn hàng theo ID.
- **Mối quan hệ**: `PurchaseOrderController` sử dụng `PurchaseOrderDatabase` để lưu trữ và truy xuất thông tin của `PurchaseOrder`.

#### Lớp *Product*
- **Mô tả**: Lớp đại diện cho sản phẩm trong đơn hàng.
- **Thuộc tính**:
  - `productID`: Mã định danh của sản phẩm.
  - `name`: Tên sản phẩm.
  - `price`: Giá của sản phẩm.
- **Mối quan hệ**: `PurchaseOrder` chứa danh sách `Product` để quản lý các sản phẩm thuộc đơn hàng.
---

### 3. Login
#### 3.1. Xác định các lớp phân tích
- **Boundary**:
  -  **EmployeeLoginForm**: Giao diện dành cho Employee để nhập thông tin đăng nhập.
  - **PayrollAdminLoginForm**: Giao diện dành cho Payroll Administrator để nhập thông tin đăng nhập.
- **Control**:
  - **LoginController**: Điều khiển logic xác thực đăng nhập, chịu trách nhiệm xác thực thông tin và xử lý đăng nhập.
- **Entity**:
  - **User**: Đại diện cho thực thể người dùng, lưu trữ thông tin tên và mật khẩu.
  - **UserDatabase**: Lớp quản lý và xác thực dữ liệu người dùng trong hệ thống.
#### 3.2. Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/x5GxJiD04Ett55Cc4hb09AD0W0gX207zn1xYLTQxPZyWrnJKd8622j5GEKKASX6VW2kmpeUOs2X1eiJ5sljsvhsPsIT_JAOzOr5RbmY6eLKQZfDKg8nekHrWffKG1r729JTMemVPK3aPeSw-Wa_LYCiJfPFrKJLnVHmgQJqCSwI_s0ZIZAJbDeDBG_e8BGxHK1LZB0ZWiCXVBSmUY_pP-TViNev0naN-aa8Gi5KfqDclbzK5JqQwhoagML6ObiI4zY15O-wKZjgibbCIRPJP1KqtZeoTupKAXiB2MP5F7TZu_SsNPxc4k9WyfI2AoGC3_snGbYhLhhjmYu97QAb4Qn8bGpLybTw5CAPmF5W6jhXCdHtKqg1Ja-FcgXHiO6xglnhTq4d3u2DkKe7PEHadRCkuC2HZ_An8U8sBzPZ6Yy_jqzggSOrSE4rjRw28iIO3bpID_jp19urv_rxvlLT-k80_zyjEEjyzq_Dh-KVy1000__y30000)
---

#### 3.3. Biểu đồ lớp
![Diagram](https://www.planttext.com/api/plantuml/png/n5H1JiCm4Bpx5RuH9FA17b2Xm8b3LCG3bdZLMZXssDqKHOYNSU19V84a9A5jBAW0YLmIxSwCPpshlBsypbc0f2gSKha3PdrPb2xKYFf9wUP9jOS2P_f6oFfLNoeRu6CWirFM6hqWBGXDys71SR9DFPcmZcTw4wnHpyFH6TGKd3ipXVMMXK02_OEDuGQkmyhwgq15xq5hOxbqK2-HAoS9TQ-3flcbL4TV12-j8D8eGlXG8KlNFd3A3-86d3KWUCj8tnFFGt08_jDFIxi0WJjW7CtyWUOFmixNcDzdVI-nlgma-_Aq8xr41sA3vxKjMOtxdgQdq-XLT2TRQ3HUDTsT5hkNduglHWovdtoBsRvzjHF5qEsgKsnCR3fn31KrB4hDqPlst_4E003__mC0)

#### Lớp **EmployeeLoginForm**
- **Mô tả**: Lớp giao diện người dùng để nhận thông tin đăng nhập từ Employee.
- **Thuộc tính và Phương thức**:
  - `enterCredentials(name: String, password: String)`: Nhận tên và mật khẩu từ Employee.
  - `displayResult(success: Boolean)`: Hiển thị kết quả đăng nhập cho Employee.
- **Quan hệ**: Tương tác với Employee và gửi yêu cầu đăng nhập đến `LoginController`.

#### Lớp *PayrollAdminLoginForm*
- **Mô tả**: Lớp giao diện người dùng dành riêng cho Payroll Administrator để đăng nhập vào hệ thống.
- **Thuộc tính và Phương thức**:
  - `enterCredentials(name: String, password: String)`: Nhận thông tin từ Payroll Administrator.
  - `displayResult(success: Boolean)`: Hiển thị kết quả đăng nhập.
- **Quan hệ**: Tương tác với Payroll Administrator và gửi yêu cầu đăng nhập đến `LoginController`.

#### Lớp *LoginController*
- **Mô tả**: Xử lý logic đăng nhập, xác thực thông tin đăng nhập.
- **Thuộc tính và Phương thức**:
  - `requestLogin(name: String, password: String)`: Thực hiện yêu cầu xác thực thông tin đăng nhập.
- **Quan hệ**: Nhận yêu cầu đăng nhập từ các lớp `EmployeeLoginForm` và `PayrollAdminLoginForm`, sử dụng `UserDatabase` để xác thực thông tin.

#### Lớp *User*
- **Mô tả**: Thực thể đại diện cho người dùng trong hệ thống, lưu trữ thông tin tên và mật khẩu.
- **Thuộc tính**:
  - `name: String`: Tên người dùng.
  - `password: String`: Mật khẩu người dùng.
- **Phương thức**:
  - `checkPassword(inputPassword: String): Boolean`: Kiểm tra mật khẩu nhập vào có khớp với mật khẩu đã lưu không.
- **Quan hệ**: Kết nối với `UserDatabase` để xác thực thông tin.

#### Lớp *UserDatabase*
- **Mô tả**: Quản lý dữ liệu người dùng và thực hiện xác thực đăng nhập.
- **Phương thức**:
  - `validateUser(name: String, password: String): Boolean`: Xác thực thông tin đăng nhập của người dùng.
- **Quan hệ**: Tương tác với `LoginController` để xác thực thông tin đăng nhập, sử dụng lớp `User` để kiểm tra thông tin mật khẩu.
---
### 4. Create Administrative Report
#### 4.1. Xác định các lớp phân tích
- **Boundary**:
  - **ReportSelectionForm**: Lớp giao diện người dùng cho Payroll Administrator để nhập các tiêu chí báo cáo và yêu cầu hệ thống tạo báo cáo.
- **Control**:
  - **ReportController**: Lớp xử lý logic nghiệp vụ để tạo báo cáo, lưu báo cáo và kiểm tra tính hợp lệ của các tiêu chí báo cáo.
- **Entity**:
  - **Report**: Lớp thực thể đại diện cho báo cáo được tạo ra, chứa thông tin và dữ liệu của báo cáo.
  - **Employee**: Lớp thực thể đại diện cho nhân viên trong hệ thống, có thể là đối tượng của báo cáo.
  - **ReportDatabase**: Lớp quản lý và lưu trữ các báo cáo đã tạo.

#### 4.2. Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/d5HBRjim4Dtp5BEqWUG21Xoa-NHL14MS2uofYKsK8bL-0kW4NUS8HHS52XJjeYjxaOM3t4Cdw1KwegcgCTJMZXR432M-3sT6FzSFfpwW2x7K0cMm3jvYxQpMhufI6UM3GzuKSnjDWQw6Qwgi2pFI98EovhLrfP3M13wItvrlCqrEa0agT6UUPnSOS8wUkjtBijAs9X9YEeMpPlKjmEDzi_eS8JIhZnRc6rvakqodGWnfXEEJ8NKJO0PoMPjJ72iSkPJUr1KTmPmMoh0U3iaKESXohh0aFnO3k3rTRtW2Zjv7yg5Z8sm_FvHDe0vmrQmUsBpQV8aWbvkli6pMdohGpVg307vskNiz4v0jCMspGybxR3WUjBWWGtpXLEIo_blCJYqAvIkDTPQs0yNEMx3UVIupFAzp6PlrlG7zz3tsRP5EzbBsBzKCx-Y20YhjH-CTb3qCfURw4-DMwNILHz16RwnCBR0FSZSI4_2CDtn5MzJ_utTOVxEUd31BSRZZNC9PqkYZ3YCVfIIVUuSqivxzdjPtoyqFiqZ5UX6LH9Ujv-fmtmgHI6xwsSWiUu_8iALBvwmRyHHuND1O9APJNjj_uoy0003__mC0)

#### 4.3. Biểu đồ Lớp
![Diagram](https://www.planttext.com/api/plantuml/png/d9DHQiCm38RVVGezBj1Se8nGQ3SOb3siku2QQC7Ws47s2c7iP7lOaNQ5EOdZr4qPs_8G54lwz4jMlZu-DzOXkzT62L4gj1QUg3Ni3gIeTDBeUyCDl0aO7jAEU0pOilIsn1iUFf-xbbPmf5hg7Jflagw2qRJAT4IFs93D0gYIjbNOZQY0oCHxgc5hj6EZ574KK39vQ9Bskyh5LDdYASrVmOjKGynexKs9VUDJmWcLh6BH_xPzqLfeA8SPiuQ3Owdhu8ZCDVJlS1hmwTbvfJNifNMt8we84Lu-9dY0cZJnFCeikgFGku2DKhNdBoYkhtejVGHxcNX4I_42_pn-NoA9VzWDmxosfNbUB3P7B5PfZlh9DmaFCODdceYuwEsCA3R-XlgVwHi00F__0m00)

#### Lớp *ReportSelectionForm*
- **Mô tả**: Giao diện người dùng cho Payroll Administrator để nhập thông tin cần thiết cho báo cáo hành chính.
- **Phương thức**:
  - `enterReportCriteria(reportType: String, beginDate: Date, endDate: Date, employeeNames: List<String>)`: Nhận các thông tin từ Payroll Administrator để tạo báo cáo.
  - `displayReport(report: Report)`: Hiển thị báo cáo sau khi được tạo ra.
  - `enterSaveDetails(fileName: String, fileLocation: String)`: Nhận thông tin về tên và vị trí lưu báo cáo nếu Payroll Administrator quyết định lưu báo cáo.
  - `confirmSave(save: Boolean)`: Xác nhận việc lưu báo cáo.
- **Quan hệ**: Tương tác với Payroll Administrator để nhận thông tin và gửi yêu cầu tạo báo cáo đến `ReportController`. Cũng nhận yêu cầu lưu báo cáo nếu cần.

#### Lớp *ReportController*
- **Mô tả**: Lớp xử lý logic nghiệp vụ để tạo và lưu báo cáo, đồng thời kiểm tra tính hợp lệ của các tiêu chí báo cáo.
- **Phương thức**:
  - `createReport(reportType: String, beginDate: Date, endDate: Date, employeeNames: List<String>)`: Tạo báo cáo dựa trên các tiêu chí đã nhập.
  - `saveReport(report: Report, fileName: String, fileLocation: String)`: Lưu báo cáo vào hệ thống.
  - `validateReportCriteria(reportType: String, beginDate: Date, endDate: Date, employeeNames: List<String>)`: Kiểm tra tính hợp lệ của các tiêu chí báo cáo.

#### Lớp *Report*
- **Mô tả**: Đại diện cho báo cáo được tạo ra với các thông tin liên quan đến báo cáo.
- **Thuộc tính**:
  - `reportType: String`: Loại báo cáo (Total Hours Worked hoặc Pay Year-to-Date).
  - `beginDate: Date`: Ngày bắt đầu của báo cáo.
  - `endDate: Date`: Ngày kết thúc của báo cáo.
  - `employeeNames: List<String>`: Danh sách nhân viên có trong báo cáo.
  - `data: String`: Dữ liệu báo cáo.
- **Phương thức**:
  - `generateReport()`: Tạo ra nội dung báo cáo dựa trên tiêu chí đã nhập.

#### Lớp *Employee*
- **Mô tả**: Lớp đại diện cho thông tin của nhân viên.
- **Thuộc tính**:
  - `name: String`: Tên nhân viên.
- **Phương thức**:
  - `getName()`: Trả về tên nhân viên.

#### Lớp *ReportDatabase*
- **Mô tả**: Lớp quản lý các báo cáo đã tạo và lưu trữ chúng.
- **Phương thức**:
  - `saveReport(report: Report, fileName: String, fileLocation: String)`: Lưu báo cáo vào hệ thống.
  - `getReport(reportID: String)`: Truy xuất báo cáo đã lưu.


---
### 5. Maintain Employee Info
#### 5.1. Xác định các lớp phân tích
- **Boundary Class**:
  - **EmployeeMaintenanceForm**: Là lớp boundary duy nhất để giao tiếp với Payroll Administrator. Lớp này cung cấp giao diện để Payroll Administrator chọn hành động (Add, Update, Delete), nhập thông tin nhân viên mới, cập nhật thông tin, hoặc xác nhận khi muốn xóa nhân viên.

- **Control Class**:
  - **EmployeeController**: Chịu trách nhiệm  tra dữ liệu đầu vào từ Payroll Administrator.

- **Entity Classes**:
  - **Employee**: Thực thể chứa thông tin của nhân viên, với các thuộc tính như employeeId, name, employeeType, address, SSN, deductions, phoneNumber, rate (bao gồm hourlyRate, salary, commissionRate, hourLimit, v.v.).
  - **EmployeeDatabase**: Đại diện cho cơ sở dữ liệu nhân viên, trong đó lưu trữ thông tin tất cả các nhân viên.
#### 5.2. Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/t5P1Qjj05DtFAJxPT9KB55nYdBPPjCKGjsGx7WtLW3JZIYCJBKiNfPH2IvVTn0qbO0WKcfMqo692xZ4dw1Nw9P5uP4ksbPGkkh6OaV_xRzv_pvxV-ULUh6caap0Wb6aLmP2caGg2lXSAAM8TqMAJnZ3iax5Af4UZ51w7aq2bd3-dGcekgMJyYOf2mfJKM7pxVb2j0nuHBhNGYyhbzJxLT4nZJiW3w7lUxJuSyZS9HtmoxCFkexREy106liq_ITWP-MOUmWlVV9VmIfYvt25jHGxUWYb2FRNvkO3Kp1DWDZjBre8wbGuUeeniDbCGsloRS2jXMkvetrp8rw251ERZKjZiKcy0lH49mPzT_qngg6KVilBDtROp7faP0-dRx5n2K80XeHFf0ojeDV9Og_w1iFaxYI0s_mYXEKNeWjkqWTlA510OXxiL1kdruEN4evglEWHwFRArImPuy0aAY0zTcojCpKcbosIPmr_mqPgsfIlQEcxsWyr-fAwfNEsqprK1tS4UeyXcfmMfjosWzxI80-hZ_dlSnxW8r2a_exK-sqpq0netHh7f9hBT9jSYvzKNd19pssu_fye0iZ80Gdo5-7hMIBLRX9cBMujo4Pbz7l1xH-R8_AB_C2eDxVxxYBWJFIxEtoK8oyLtdC5n6yn6WQy-cndQpaETaqPlOtBm9w2EsitcPVJmOz6dbU9QhKRLmCO6_w5BeTt8OBRLpJK8QlSWGlQuz8gxqXy0003__mC0)

#### 5.3. Biểu đồ Lớp
![Diagram](https://www.planttext.com/api/plantuml/png/Z5HBJiCm4Dtx55csYrwW2zIMW8G45Q9SO1fFMmj_WZskP25Ene8ZSGMIjCw_XMmilNdpPiRpd9-lxuKZiEILP8m4IKpkL4uXIGNiBIZ65gXv4MrecGJdacS8raYvv4feuSW26PjyiAJyBBvxTBJCI1WzWUgO9nkoGk-dx9ET9Of2qWJ49n2QK8FEyDvO5LMuSBc445aFUcScgFBoRCGgPcRqJbYLeiIgOidYFSuUgL7AFKscyxg1OKktHbCv7jOp0USnMEetoMTzdtCWl4hXPNyTIh_BsH6aQEiyy1vjdgoCaGXws7Fi5ElSc7N2DIZi8f7v6l9Uf9ZMedDTSBDPTm6Et5VBxH7pWz6uzcgBjXieND8hT33Uol1IuQdnMuadt8446xfOPfGIpXNrXlnIvr4eGRqKY-sjZ9Wl1O8jkFhs71olRx5bf5KOsKzjgl_QGe5zYr3X_qikBZeVVNEpsSsbbyGklR1sJcDrDkB-DlElUBnADhZRZihvXy9-0G00__y30000)

#### Lớp *PayrollAdministrator*
- **Mô tả**: Payroll Administrator thực hiện các hành động như thêm, cập nhật, hoặc xóa thông tin nhân viên.
- **Phương thức**:
  - `requestAction(action: String)`: Xác định hành động cần thực hiện. Nhận đầu vào là một chuỗi hành động ("Thêm", "Cập nhật", hoặc "Xóa") và chuyển yêu cầu đó đến hệ thống để xử lý.

#### Lớp *EmployeeMaintenanceForm*
- **Mô tả**: Lớp giao tiếp với Payroll Administrator, cung cấp giao diện hiển thị thông tin nhân viên và xác nhận xóa nhân viên.
- **Phương thức**:
  - `displayEmployeeInfo(empInfo: String)`: Hiển thị thông tin chi tiết của nhân viên để Payroll Administrator có thể xem hoặc cập nhật.
  - `confirmDeletion(empId: String)`: Xác nhận yêu cầu xóa nhân viên dựa trên mã nhân viên.
  - `getEmployeeInput()`: Thu thập thông tin của nhân viên mới từ Payroll Administrator khi thêm nhân viên.

#### Lớp *EmployeeController*
- **Mô tả**: Nhận các yêu cầu từ `EmployeeMaintenanceForm`, xử lý logic nghiệp vụ và chuyển tiếp yêu cầu tới cơ sở dữ liệu để cập nhật thông tin nhân viên.

- **Phương thức**:
  - `addEmployee(emp: Employee)`: Thêm một nhân viên mới vào hệ thống.
  - `updateEmployee(emp: Employee)`: Cập nhật thông tin của nhân viên đã có trong hệ thống.
  - `deleteEmployee(empId: String)`: Xóa một nhân viên khỏi hệ thống dựa trên mã nhân viên.
  - `validateEmployeeId(empId: String): Boolean`: Kiểm tra mã nhân viên có tồn tại và hợp lệ hay không.

#### Lớp *Employee*
- **Mô tả**: Chứa thông tin chi tiết của một nhân viên, bao gồm các thông tin cơ bản và thông tin về lương.
- **Thuộc tính**:
  - `employeeId`: Mã định danh duy nhất của nhân viên.
  - `name`: Tên của nhân viên.
  - `employeeType`: Loại nhân viên (theo giờ, hưởng lương cố định, hưởng hoa hồng).
  - `address`: Địa chỉ nhân viên.
  - `SSN`: Số an sinh xã hội của nhân viên.
  - `deductions`: Các khoản khấu trừ thuế và phí.
  - `phoneNumber`: Số điện thoại của nhân viên.
  - `rate`: Mức lương chung (dùng cho loại nhân viên chung).
  - `hourlyRate`: Mức lương theo giờ (dùng cho nhân viên theo giờ).
  - `salary`: Mức lương cố định (dùng cho nhân viên hưởng lương cố định hoặc hoa hồng).
  - `commissionRate`: Tỉ lệ hoa hồng (dùng cho nhân viên hưởng hoa hồng).
  - `hourLimit`: Giới hạn giờ làm (đối với nhân viên có giới hạn giờ làm việc).

 - **Phương thức**:
  - `createEmployee()`: Tạo một đối tượng nhân viên mới và khởi tạo các thuộc tính của nó.


#### Lớp *EmployeeDatabase*
- **Vai trò**: Là lớp entity quản lý cơ sở dữ liệu nhân viên, bao gồm các thao tác như lưu, truy xuất, cập nhật và đánh dấu xóa nhân viên.

- **Phương thức**:
  - `saveEmployee(emp: Employee)`: Lưu một nhân viên mới vào cơ sở dữ liệu.
  - `getEmployeeById(empId: String): Employee`: Truy xuất thông tin nhân viên dựa trên mã nhân viên.
  - `updateEmployee(emp: Employee)`: Cập nhật thông tin của nhân viên trong cơ sở dữ liệu.
  - `markEmployeeForDeletion(empId: String)`: Đánh dấu nhân viên cần xóa để hệ thống xóa sau khi tính bảng lương cuối cùng.

---
### 6. Run Payroll
#### 6.1. Xác định các lớp phân tích
- **Boundary Classes**:
  - **PayrollScheduler (System Clock)**: Kích hoạt quy trình tính lương theo lịch định kỳ.
  - **PayrollPrinter (Printer)**: Xử lý việc in phiếu lương cho các nhân viên nhận lương qua "mail" hoặc "pick-up".
  - **BankGateway (Bank System)**: Xử lý các giao dịch chuyển khoản cho các nhân viên nhận lương qua "direct deposit".
- **Control Class**:
  - **PayrollController**: Điều khiển quy trình tính lương, từ việc lấy dữ liệu nhân viên, tính toán lương đến việc quyết định phương thức thanh toán.
- **Entity Classes**:
  - **Employee**: Lưu trữ thông tin của nhân viên, bao gồm các thông tin về lương và phương thức nhận lương.
  - **PayrollDatabase**: Lưu trữ thông tin về nhân viên, giờ làm, và các purchase orders cần thiết cho việc tính lương.
    
#### 6.2. Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/Z5I_RjGm6D_p59zkWk5Uu0PKjKKjAa8djKAi9h7ELXmx90wG4Tt0m5GnCB1Sg4uLY1ELG4AAXmv6znv-0bw1pscuIzhI4CbsOldtv_iJ_pQNExaccIuI4P1GgmoEorpJP4-eC6vtfXcNccRjrowHyTMP8EYSXV43c98oKq8SXun6XQ3P18xiAcJ0bAih3I-A4dHclqe6sgvm5kkBTILdmNLSXsjFIUrNJxRhwcyQVfsw-hmO9Di2EspxH9Fd9ASJUEpgPGaHGM1kA_GecVqauIMtNwINCESuSsVU513ZybQ2PlwmLhQIS4_ExABi2zyFhed0-FOmzlzVD0Y4KYayTUOZXyIP3xmB2G2VMyDzcAH2bHJZFEdbnWE8q31bLniOb3EVmrvimYvWb10kHatTVeOmIdaOZujqrE3_ATfkjjqoWKSIKiPTVLdqzAd0r0mQY7X6GmqHJLNEzO2oRya3ekahKaxWm9aLXnad2Y9dtc6MGrQKpimbn3wWCxaXywaun3mtBaxH3POLayli0jzZPdyq2q8yqxBr__VfYDxmS89yAvWrJWJsVi_FXeNAAEYk0wKymfQO9zZq10UIDjcpoFtQVYURqZxfjTJwmfcp45ymiGprwsNHDDfy2nggv_QVUOOGmCZUGxwkRZIYZyAFEt_0pjLmg33DeD7I7JV33ZBwg-aF0000__y30000)

#### 6.3. Biểu đồ Lớp
![Diagram](https://www.planttext.com/api/plantuml/png/b5HBJiCm4Dtd55wcYruWGbKfBGY9GgNs0bDdIAqwTZHsG17YP2mu4bV0BdQQ9hI2B19xvisRVxu-FgV60jcwb4d29HZ3Lj2GbdBDTvZN4ecz9SmzOyPh8bHs3XOpvjy7EMEMH54W1RjqbBptg5OabEqGLT0uShxFFE1m2aoL1qPPEeHrg6UWzdSkXbTeMbvBe0nmAxJAsEPu2MfXhbz0IDXA5_zCQucWWcE3AkyOfEUOHW5FQAdvcq6_63TQMVyzhOUNz0exPYX58LoqYxAIka4q6NiGnbx5-wGjc-PepB41Fs8EajVIqJb5Yi4cOz4wmdAKQ5iVlmBxERWOOGi6smpmOeIkCw943fH7_IRSexwgYUySuHFbI16qwWfZhWNQHRyiQTvMRdIcHFz9Cee6sTtd6LkxQLT5K1YGG4t6bbfX4sHRLFWih4jY5av1aRjrEio4KytRyt44IhTRIxGxVUgbqyT7zClHzhS4sjzgcllK_0mUKXXixtWy6OvUCXp63YwszmmgrkSoILZwCw3E-YRzeJhnaIHJjvl-z_GD003__mC0)

#### Lớp *PayrollScheduler*
- **Mô tả**: Lớp này đại diện cho hệ thống định kỳ (lịch trình) để kích hoạt quy trình tính lương vào thời điểm cụ thể (mỗi thứ Sáu hoặc ngày làm việc cuối tháng).
- **Thuộc tính**:
  -`currentDate`: Date: Ngày hiện tại, được sử dụng để xác định thời điểm kích hoạt quy trình.
- **Phương thức**:
  - `triggerPayroll()`: Phương thức để kích hoạt quy trình tính lương.
#### Lớp *PayrollController*
- **Mô tả**: Lớp trung tâm điều khiển toàn bộ quy trình tính lương. Nó xử lý việc lấy dữ liệu nhân viên, tính toán lương, và thực hiện thanh toán cho từng nhân viên.
- **Thuộc tính**:
  - `payrollDate`: Date: Ngày tính lương hiện tại.
  - `eligibleEmployees`: List<Employee>: Danh sách nhân viên đủ điều kiện để nhận lương trong ngày.
- **Phương thức**:
  - `processPayroll()`: Xử lý toàn bộ quy trình tính lương từ bắt đầu đến kết thúc.
  - `calculatePay(employee: Employee)`: Tính toán lương (lương thực nhận) cho một nhân viên.
  - `deleteEmployee(employee: Employee)`: Xóa thông tin nhân viên sau khi đã xử lý (nếu nhân viên được đánh dấu để xóa).
#### Lớp *PayrollDatabase*
- **Mô tả**: Cơ sở dữ liệu lưu trữ thông tin liên quan đến quy trình tính lương, bao gồm danh sách nhân viên, thời gian làm việc (timecards), và các đơn mua hàng (purchase orders).
- **Thuộc tính**:
  - `employees: List<Employee>`: Danh sách các nhân viên trong cơ sở dữ liệu.
  - `timecards: List<Timecard>`: Danh sách các phiếu thời gian làm việc.
  - `purchaseOrders`: List<PurchaseOrder>: Danh sách các đơn mua hàng liên quan đến hoa hồng.
- **Phương thức**:
  **getEligibleEmployees(date: Date)**: List<Employee>: Lấy danh sách nhân viên đủ điều kiện để tính lương tại một ngày cụ thể.
  - `deleteEmployee(employee: Employee)`: Xóa thông tin nhân viên đã được xử lý.
#### Lớp *Employee*
- **Mô tả**: Lớp đại diện cho một nhân viên. Nó chứa các thông tin cần thiết để tính lương, như lương cơ bản, phúc lợi, các khoản khấu trừ, và phương thức thanh toán.
- **Thuộc tính**:
  - `employeeId`: String: Mã định danh duy nhất của nhân viên.
  - `salary`: Money: Lương cơ bản của nhân viên.
  - `benefits`: Benefits: Các khoản phúc lợi của nhân viên.
  - `deductions`: Deductions: Các khoản khấu trừ của nhân viên.
  - `paymentMethod`: String: Phương thức nhận lương của nhân viên (ví dụ: chuyển khoản, thư, hoặc nhận trực tiếp).
- **Phương thức**:
  - `calculateNetPay()`: Tính toán lương thực nhận của nhân viên sau khi áp dụng phúc lợi và khấu trừ.
  - `markForDeletion()`: Đánh dấu nhân viên để xóa sau khi đã xử lý.
#### Lớp *PayrollPrinter*
- **Mô tả**: Lớp này chịu trách nhiệm in phiếu lương cho nhân viên nếu phương thức thanh toán là gửi thư hoặc nhận trực tiếp.
- **Thuộc tính**:
  - `paycheck`: Paycheck: Thông tin phiếu lương cần in.
- **Phương thức**:
  - `printPaycheck(paycheck: Paycheck)`: In phiếu lương cho nhân viên.
#### Lớp *BankGateway*
- **Mô tả**: Lớp này giao tiếp với hệ thống ngân hàng để thực hiện các giao dịch chuyển khoản lương cho nhân viên.
- **Thuộc tính**:
  - `transaction`: Transaction: Giao dịch ngân hàng cần xử lý.
  - `isAvailable`: Boolean: Trạng thái khả dụng của hệ thống ngân hàng.
- **Phương thức**:
  - `sendTransaction(transaction: Transaction)`: Gửi giao dịch chuyển khoản tới hệ thống ngân hàng.
  - `retryTransaction(transaction: Transaction)`: Thử lại giao dịch nếu hệ thống ngân hàng không khả dụng.

---
## II. Viết code Java mô phỏng ca sử dụng Maintain Timecard
### 1. Lớp `EmployeeLoginForm` và `PayrollAdminLoginForm`


    public void displayForm() {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter admin username: ");
        String username = scanner.nextLine();
        System.out.print("Enter admin password: ");
        String password = scanner.nextLine();

        boolean success = loginController.requestLogin(username, password);
        if (success) {
            System.out.println("Admin login successful!");
        } else {
            System.out.println("Invalid credentials. Please try again.");
        }
    }
    public void displayForm() {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter username: ");
        String username = scanner.nextLine();
        System.out.print("Enter password: ");
        String password = scanner.nextLine();

        boolean success = loginController.requestLogin(username, password);
        if (success) {
            System.out.println("Employee login successful!");
        } else {
            System.out.println("Invalid credentials. Please try again.");
        }
    }

### 2. Lớp `LoginController`

    public boolean requestLogin(String username, String password) {
        return userDatabase.validateUser(username, password);
    }


### 3. Lớp `User`

    public User(String username, String password) {
        this.username = username;
        this.password = password;
    }

    public String getUsername() {
        return username;
    }

    public boolean checkPassword(String inputPassword) {
        return this.password.equals(inputPassword);
    }

### 4. Lớp `UserDatabase`

    public UserDatabase() {
        // Sample data
        users.add(new User("employee1", "password123"));
        users.add(new User("admin1", "adminPass"));
    }

    public boolean validateUser(String username, String password) {
        for (User user : users) {
            if (user.getUsername().equals(username) && user.checkPassword(password)) {
                return true;
            }
        }
        return false;
    }
}

