# LAB 1: PHÂN TÍCH KIẾN TRÚC, CƠ CHẾ, CA SỬ DỤNG
## 1. Phân tích kiến trúc
- **Đề xuất kiến trúc:**  *3-Tier Architecture* 

- **Giải thích:**
  + **Phân tách nhiệm vụ rõ ràng:** Mỗi tầng có trách nhiệm cụ thể, dễ bảo trì và nâng cấp mà không ảnh hưởng đến toàn bộ hệ thống.
  
  + **Tăng cường bảo mật:** Chỉ Business Logic Layer có quyền truy cập vào Data Access Layer, tránh truy cập trực tiếp từ giao diện người dùng.
  
  + **Dễ mở rộng:** Các tầng hoạt động độc lập, có thể mở rộng một trong các tầng mà không cần thay đổi cấu trúc toàn hệ thống.

  + **Tính tổ chức cao:** Dữ liệu, xử lý nghiệp vụ và giao diện người dùng được phân tách rõ ràng, dễ dàng cho việc bảo trì, phát triển và quản lý.
 
- **Ý nghĩa các thành phần trong kiến trúc:**
  +  **Presentation Layer (Tầng giao diện):** Là tầng giao diện nơi người dùng tương tác trực tiếp với hệ thống. Tầng này chịu trách nhiệm thu thập dữ liệu đầu vào từ người dùng và hiển thị dữ liệu đầu ra từ hệ thống.
 
  +  **Business Logic Layer (Tầng Xử lý Nghiệp vụ):** Là tầng quan trọng nhất trong hệ thống, chứa toàn bộ logic nghiệp vụ. Nó xử lý dữ liệu từ Presentation Layer và quyết định cách xử lý, sau đó trả kết quả lại cho giao diện. Tầng này cũng chịu trách nhiệm thực hiện các quy tắc nghiệp vụ và kiểm tra tính hợp lệ của dữ liệu.
 
  +  **Data Access Layer (Tầng Truy cập Dữ liệu):** Là tầng chịu trách nhiệm tương tác trực tiếp với cơ sở dữ liệu. Tầng này thực hiện các thao tác như truy vấn, lưu trữ, cập nhật và xóa dữ liệu.
    
  +  **Base Reuse Layer (Tầng Tái sử dụng Cơ sở):** Đây là tầng bổ sung, cung cấp các dịch vụ, hàm tiện ích và thư viện dùng chung mà tất cả các tầng khác có thể sử dụng. Các chức năng trong Base Reuse Layer thường bao gồm các công cụ hỗ trợ, chức năng chung không phụ thuộc vào logic nghiệp vụ như xử lý định dạng ngày tháng, mã hóa, log hệ thống, và các hàm tiện ích khác.
 
- **Biểu đồ:**
  ![Diagram](https://www.planttext.com/api/plantuml/png/T991IWCn58RtESMZ-rwW2sbhqOe5YzQ5I1Sn3Mrep6ZoKXp4bGiN7i035144SJz1kkX9SWAlO3ArT5BhB8OX-Ru__mlpxHPDWrIZlPQ4cAbGe3F32GgK7FeqrvcKqD9i8f0pj9gJ6ygcTCoXrjVSS8KKHQQWHtEkQt1F83oNvqV3rST-fZ16S3qa3sJZjgqHYXi3lMmis9PznlLCC9uQ7OeKMeoLKe9tMYU_fqNcYfejinrMu9JRyDvgYK8ApE70AXQ7CAKNoqEzlfUKXmOSUlSXOEJT9qZXtPCb2L0Qw-O1lrY-Ms2-UBDm5qoGoo-osI_fM3mba_HoUmMkvmhqGDiSPhvuLQIoNiqRQ5_C_ukgDDp1fVtI-OzziK2ujK7QCNcyj0PqGywZ0fnuzmpJYa1sNFQVGbtlNW2rTtFIv6eKVyaV0000__y30000)
## 2. Cơ chế phân tích
- **Persistency** _(Cơ chế bền vững)_: Hệ thống cần đảm bảo mọi dữ liệu được ghi nhận (thông tin nhân viên, thời gian làm việc, thông tin lương) được lưu trữ bền vững trong database. Việc này giúp bảo vệ dữ liệu khỏi mất mát và đảm bảo có thể truy xuất lịch sử thông tin khi cần thiết.
  
- **Communication** _(Cơ chế trao đổi dữ liệu)_: Ngoài việc trao đổi thông tin giữa các thành phần bên trong thì hệ thống cần có khả năng trao đổi dữ liệu với các hệ thống bên ngoài (ví dụ: ngân hàng để chuyển khoản tiền lương)

- **Information Exchange and Format Conversion** _(Trao đổi thông tin và chuyển đổi định dạng)_: Hệ thống cần có khả năng trao đổi dữ liệu với các phần mềm khác (như phần mềm kế toán hoặc hệ thống quản lý nhân sự) và chuyển đổi giữa các định dạng dữ liệu khác nhau. Điều này giúp tăng tính tương tác và tích hợp của hệ thống.

- **Security** _(Cơ chế bảo mật)_: Cần thiết lập các biện pháp bảo mật mạnh mẽ để bảo vệ dữ liệu cá nhân và tài chính của nhân viên. Điều này bao gồm xác thực đa yếu tố, mã hóa dữ liệu và kiểm tra quyền truy cập để ngăn chặn các cuộc tấn công từ bên ngoài.

- **Error Detection/Handling/Reporting** _(Cơ chế phát hiện, xử lý và báo cáo lỗi)_: Hệ thống cần có cơ chế phát hiện lỗi trong quá trình tính toán lương hoặc trong giao tiếp dữ liệu, đồng thời cung cấp thông báo báo lỗi rõ ràng để hỗ trợ xử lý kịp thời. Điều này giúp duy trì tính ổn định và tin cậy của hệ thống.

- **Legacy Interface** _(Cơ chế giao tiếp với hệ thống đã tồn tại)_: Hệ thống mới cần có khả năng giao tiếp với cơ sở dữ liệu hiện có (Cơ sở Dữ liệu Quản lý Dự án) mà không làm thay đổi hoặc làm mất dữ liệu hiện tại. Điều này giúp tối ưu hóa chi phí và thời gian triển khai hệ thống mới.

## 3. Phân tích ca sử dụng Payment
### 3.1. Xác định các lớp phân tích
- **Boundary**:
  + **EmployeeUI:** Làm nhiệm vụ tương tác với nhân viên và hệ thống, giúp nhân viên chọn phương thức thanh toán.
- **Control**:
  + **PaymentController:** Quản lý thao tác liên quan đến việc chọn phương thức thanh toán.
- **Entity:** Đại diện cho thông tin của nhân viên trong hệ thống, chứa thông tin cá nhân và các thuộc tính liên quan đến phương thức thanh toán.
    
### 3.2. Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/b98zJWCn48Lxdy9AjIcum1Oe_1KKY4WH1p2U2R6mFMOyYxHde-18N047bWrcjGhfREkzzxsn_V7slifYMBhWbR52h6z2yjGZgaVg8XZknvE7MsKf2fFNQzC7Z7BrlVN8gkoS7BHA_QpqsVclX5Pdz6Xb2BX3sH4qItLGxFMJ-5O_OUsvJ-8evcATYFyImUNaJJzZd-jfTqGPJ-wPc2pcNFasNoCNth6shUuI69bG_pjY4MmT1pEmghOLXl6bmomN05pADalTkArU1EFyOdWWXFchAJE-Ei3HVHnqQUBpDKh97s7Wk60qOABiv0HibQLM667_UJy1003__mC0)
### 3.3. Biểu đồ lớp
![Diagram](https://www.planttext.com/api/plantuml/png/V99BJiCm48RtESKiGKek4A6g4cA112rInG5SUoWMVk4PBoB4oLXm9Aw0arfH7WNlx6yU__pZdw_lBR68dAoff154S6U3yHqYV5IGJmDQjQ0TbviJ5biuSDJkL9w2w2mwVaH-zMh1X58HYHQlH-7UTkj2GagV7E-IFM8SsG0120rAVfhskhekB0Kb69ViirgCz7nVXWA8-9wG_YYdD0KZkWBtWRLtDD8Jyc7GWkhVz5llNdIqei-UgYb96NFqnc0SHUNAiugvPmiFclZcRCMcn8NePJPr5dkMrBUoiptKonNKA_VhoyOFaYVMDStcWlOM4Y5LQz27Zt-fBIkYQejEzP_j5m00__y30000)

**Giải thích**

#### Lớp Employee
- **Mô tả:** Đại diện cho thông tin của nhân viên trong hệ thống.
- **Thuộc tính:**
  + id: Mã định danh duy nhất cho mỗi nhân viên, dùng để phân biệt giữa các nhân viên khác nhau.
  + name: Tên của nhân viên, giúp người dùng nhận diện.
  + paymentMethod: Phương thức thanh toán hiện tại của nhân viên, có thể là "pick up", "mail", hoặc "direct deposit."
  + address: Địa chỉ mà séc sẽ được gửi đến nếu nhân viên **chọn phương thức** ***"mail"***
  + bankName: *Tên ngân hàng* được chỉ định nếu nhân viên chọn phương thức ***"direct deposit"***
  + accountNumber:*Số tài khoản ngân hàng* của nhân viên để thực hiện chuyển khoản nếu chọn ***"direct deposit"***
- **Phương thức:**
  + selectPaymentMethod(): Cho phép nhân viên chọn phương thức thanh toán mong muốn.
  + updatePaymentMethod(): Cập nhật thông tin phương thức thanh toán của nhân viên trong hệ thống.
  ---
#### Lớp EmployeeUI
- **Mô tả:** Đại diện cho giao diện người dùng nơi nhân viên tương tác với hệ thống.
- **Phương thức:**
  + requestPaymentMethod():Yêu cầu nhân viên chỉ định phương thức thanh toán mà họ muốn.
  + displayPaymentOptions(): Hiển thị danh sách các phương thức thanh toán có sẵn để nhân viên lựa chọn.
  + getSelectedPaymentMethod(): Lấy phương thức thanh toán mà nhân viên đã chọn sau khi họ đã thực hiện lựa chọn.
  + displayConfirmation(): Hiển thị thông báo xác nhận cho nhân viên sau khi họ đã chọn phương thức thanh toán.
  ---
#### Lớp PaymentController
- **Mô tả:** Quản lý logic liên quan đến lựa chọn phương thức thanh toán.
- Phương thức:
  + getPaymentMethods(): Trả về danh sách các phương thức thanh toán có sẵn mà nhân viên có thể chọn.
  + processPaymentMethodSelection(method, address, bankName, accountNumber): Xử lý lựa chọn của nhân viên, kiểm tra tính hợp lệ và cập nhật thông tin vào lớp Employee.

  #### Giải thích quan hệ
- EmployeeUI sử dụng PaymentController để:
  + Lấy danh sách các phương thức thanh toán có sẵn (thông qua getPaymentMethods()).
  + Gửi yêu cầu cập nhật thông tin phương thức thanh toán cho lớp Employee thông qua lớp PaymentController.
- PaymentController cập nhật thông tin cho Employee khi nhận được lựa chọn từ giao diện người dùng và xử lý logic nghiệp vụ.
  
## 4. Phân tích ca sử dụng Maintain Timecard
### 4.1. Xác định các lớp phân tích
- **Boundary**:
  + **EmployeeUI:** Làm nhiệm vụ tương tác với người dùng và hệ thống, giúp nhân viên nhập dữ liệu vào hệ thống và xác nhận gửi thông tin chấm công.
- **Control**:
  + **TimecardController:** Quản lý thao tác liên quan đến phiếu chấm công, gồm việc tạo phiếu chấm công mới, xử lý yêu cầu cập nhật giờ làm, kiểm tra số giờ hợp lệ, xác thực trước khi nộp phiếu chấm công.
- **Entity**:
  + **Timecard:** Đại diện cho thông tin chấm công của nhân viên trong kỳ trả lương, gồm ngày làm việc, giờ làm việc, mã thanh toán, trạng thái phiếu chấm công.
  + **Employee:** Đại diện cho nhân viên, chứa thông tin cá nhân và phân quyền trong hệ thống.
  + **ChargeNumber:** Đại diện cho mã thanh toán, xác định các dự án mà nhân viên có thể tính giờ làm việc của họ.

### 4.2. Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/T991JiCm44NtFiLSW0iW1LKgHM81I2qzWEjCYLN7JiVZLZaR2ux45HWdRUCWM7ZX-M_yvu_y_VcrYAo9K-kKDXm8LctdGey8EW8gjGl9rvhwMttxd9LabGcUAJXujoqQJVLol3ka3B1HwDboVzE7whMuR3Hzu6jgToDkl59L1I_QUfOpDJsvS8QgKWhXxa5iuHxUElHm3dI09YIIASMt1sb4sck3IY11sGYwncF2o60IaM30bsUL4Zb3mYmRD8T9cOGrCbay8SXM3A5c_4qPNsBEYbFOWncoWH_2nG6zZlveO-Tq_n-QLx3AESfu4dxAFggpDj2-BlWo_YRjMikbEANRTlKiKVQ-yDVQt7g33Wr3d3D_RNj0OhJ15tuRVIhT5kZh_Eb-0000__y30000)
### 4.3. Biểu đồ lớp
![Diagram](https://www.planttext.com/api/plantuml/png/f9DBJiCm48RtEOMNGMel4A6ggAr49M1J46it7hLM7JlCZ2jLY9Enu4XS0STvo85qHHQMFC_l7q--Fx-Mn1BPLoRBIYE9nAQgZRi0l6p5UoR2vsgmhmvFzyuZRIpZ9R-93gMfDlAoEaeym9Elze2K6qrSY8TmtgQEHPj2Vbzf7ghbPH9IY1sZjeUPE3Q-GgoTtnje4n7UF13lcdmYxMnW-EYHdtK5fKIrSe7E6GCOqUU2EqSnXCHY1-2LHmJBlJc7JlLMzHXztt21Cun5_bCCoJCCdITqTFHwO8dNluZH7DzlBHb2Zt2seLRzieGezZIkPnjfmVOewz5RpJhOHOILIbsJE4wQ45f9FDrHV3HcKDtSpj9e5S3Qaed-j5utWz8f654he19rpM451diea6pjVBwOs8XiOadIo6l-b2bRXi4slyeF0000__y30000)

#### Sơ đồ Lớp "Maintain Timecard"

#### Class EmployeeUI
- **Mô tả**: Giao diện người dùng
- **Phương thức**:
  - openWorkHoursEntry(): Mở giao diện để nhân viên nhập giờ làm việc.
  - displayChargeNumbers(list: List<ChargeNumber>): Hiển thị danh sách các mã thanh toán có sẵn cho nhân viên lựa chọn.
  - submitWorkHours(chargeNumber: String, hours: Double): Gửi giờ làm việc đã nhập đến TimecardController.
  - requestSubmission(): Yêu cầu nộp phiếu chấm công sau khi hoàn thành việc nhập giờ làm.

---

#### Class TimecardController
- **Mô tả**: Điều khiển (Control)
- **Thuộc tính**:
  - timecard: Timecard: Tham chiếu đến phiếu chấm công hiện tại.
- **Phương thức**:
  - getCurrentTimecard(employeeId: String): Lấy hoặc tạo phiếu chấm công hiện tại cho nhân viên dựa vào ID của họ.
  - retrieveChargeNumbers(): Lấy danh sách các mã thanh toán từ hệ thống Quản lý Dự án.
  - submitWorkHours(chargeNumber: String, hours: Double): Kiểm tra và cập nhật giờ làm việc trên phiếu chấm công.
  - saveTimecard(): Lưu và nộp phiếu chấm công, sau đó đánh dấu phiếu ở trạng thái chỉ đọc.

---

#### Class Timecard
- **Mô tả**: Thực thể (Entity)
- **Thuộc tính**:
  - id: String: Mã định danh duy nhất cho phiếu chấm công.
  - employeeId: String: ID của nhân viên gắn với phiếu chấm công.
  - startDate: Date: Ngày bắt đầu của kỳ trả lương.
  - endDate: Date: Ngày kết thúc của kỳ trả lương.
  - status: String: Trạng thái của phiếu chấm công (ví dụ: "đã nộp", "bản nháp").
  - entries: Map<ChargeNumber, Double>: Bảng ánh xạ giữa mã thanh toán và giờ làm việc đã ghi nhận.
- **Phương thức**:
  - addWorkHours(chargeNumber: ChargeNumber, hours: Double): Thêm giờ làm việc vào phiếu chấm công.
  - markAsSubmitted(): Đánh dấu phiếu chấm công là đã nộp và chuyển về trạng thái chỉ đọc.
  - validateHours(): Xác minh rằng giờ làm việc được nhập phù hợp với giới hạn cho phép.

---

#### Class ChargeNumber
- **Mô tả**: Thực thể (Entity)
- **Thuộc tính**:
  - code: String: Mã định danh duy nhất cho mã thanh toán.
  - description: String: Mô tả về dự án hoặc nhiệm vụ liên quan đến mã thanh toán.
- **Phương thức**: Không yêu cầu phương thức

#### Giải thích quan hệ
- **TimecardUI** sử dụng **TimecardController** để:
  - Lấy thông tin phiếu chấm công hiện tại của nhân viên (thông qua retrieveCurrentTimecard()).
  - Lưu phiếu chấm công khi nhân viên đã cập nhật (thông qua saveTimecard()).
  
- **TimecardController** tương tác với **Timecard** để:
  - Thực hiện các thao tác cần thiết như thêm mã thanh toán, xác thực và gửi phiếu chấm công.
  
- **Employee** tham chiếu đến **Timecard** để cập nhật thông tin thời gian làm việc của mình. ## 5. Hợp nhất kết quả
