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
![Diagram](https://www.planttext.com/api/plantuml/png/d9DHQiCm38RVVGezBj1Se8nGQ3SOb3siku2QQC7Ws47s2c7iP7lOaNQ5EOdZr4qPs_8G54lwz4jMlZu-DzOXkzT62L4gj1QUg3Ni3gIeTDBeUyCDl0aO7jAEU0pOilIsn1iUFf-xbbPmf5hg7Jflagw2qRJAT4IFs93D0gYIjbNOZQY0oCHxgc5hj6EZ574KK39vQ9Bskyh5LDdYASrVmOjKGynexKs9VUDJmWcLh6BH_xPzqLfeA8SPiuQ3Owdhu8ZCDVJlS1hmwTbvfJNifNMt8we84Lu-9dY0cZJnFCeikgFGku2DKhNdBoYkhtejVGHxcNX4I_42_pn-NoA9VzWDmxosfNbUB3P7B5PfZlh9DmaFCODdceYuwEsCA3R-XlgVwHi00F__0m00)

#### 4.3. Biểu đồ Lớp


---
### 5. Maintain Employee Info
---
### 6. Run Payroll
---
## II. Viết code Java mô phỏng ca sử dụng Maintain Timecard
