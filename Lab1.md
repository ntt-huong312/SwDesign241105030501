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
   - **PaymentForm**: Giao diện người dùng cho nhân viên, cho phép họ chọn phương thức thanh toán.
     
- **Control**: 
   - **PaymentController**: Thành phần điều khiển xử lý logic, nhận yêu cầu từ **PaymentForm** và quản lý thông tin thanh toán.

- **Entity**: 
   - **EmployeeDatabase**: Cơ sở dữ liệu lưu trữ thông tin về nhân viên, bao gồm phương thức thanh toán và thông tin cá nhân.
    
### 3.2. Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/b9C_JiCm58Ttd-9TW0ime4hXtm0I0mECZckHICbpv3f8cHaH0oUW0I54HIK6fcHWCEezV0Akm7DBcmIf9Psiv-ZtwVU-9D_rvs1ak3PvcZ0kZD9ma6Q9AgHaeSfno7K1Pxn89Pf3fLCc51gjakLTi1WJgHcZCJR5Ah_F3G_vI3Asl86TlJOBTk7KrG-GsZ52PDym0X6v-WuXYsRlinAlmD3yAkZWzD0eMo9h0nfUquEebtQIWt3LIzw7r8eIxszxmfsuwhcWfFtmd1W18_k8S1tRoHf8TydZsDKtE6zm2yAMOflzLkuwQ_Nmj5vwy7-uZ-KZLq_ZjfOM0BxkxTDlozwU0rTDCv9BXzd-nNLtlF2QvoZqoXekzHtx3ysttk3wVB5MQ4kr8J-GEFG_pWy0003__mC0)
### 3.3. Biểu đồ lớp
![Diagram](https://www.planttext.com/api/plantuml/png/j591JiCm4Bpx5QkUKebKuff3LOc2r0C2gV00usnRIuvjl1jGX7WP1vx45t1C32dDjKVlpCxixFhhutD5B0EtZH7AI2AuRhnn7IAy2O0IS7XkrXLeowbcPOCLR3bekqy5Bxi6BJzqVbm783Ie-Fu7lKK-kBgOYtSnM0t0ZGjDSWEeDNaZkm6uywoTfTZIOtlCIjia6w5YVcIddDtfq3pwMZ9E65qvoy4PWs6mYv8vxiRkNF4lR5JFSAAtIVWuJcxvervChMCqJEQj9SidIJZC4Z0IyGKpVEvXVkyykvn1MIwFhf4SCKZ51A-Q3s8CBXRBYOrMyTgsffZZkKMAVUp4AQllFLb01L8f948IOXL5-i_u3G00__y30000)

---
#### Lớp `Employee`

- **Mô tả**: Lớp `Employee` đại diện cho nhân viên trong hệ thống, bao gồm các thuộc tính cơ bản và phương thức để chọn phương thức thanh toán.
- **Thuộc tính**:
  - `employeeID`: ID của nhân viên.
  - `name`: Tên của nhân viên.
  - `paymentType`: Phương thức thanh toán đã chọn của nhân viên, chẳng hạn "PickUp", "Mail", hoặc "DirectDeposit".
- **Phương thức**:
  - `selectPaymentMethod()`: Cho phép nhân viên chọn một phương thức thanh toán.

#### Lớp `PaymentForm`

- **Mô tả**: Lớp `PaymentForm` đại diện cho biểu mẫu nơi nhân viên thực hiện thao tác chọn phương thức thanh toán.
- **Phương thức**:
  - `displayPaymentOptions()`: Hiển thị các phương thức thanh toán khả dụng.
  - `getPaymentSelection()`: Nhận lựa chọn phương thức thanh toán từ nhân viên và trả về một chuỗi (`String`) biểu diễn phương thức đó.
  - `confirmUpdate()`: Xác nhận lại việc cập nhật phương thức thanh toán đã hoàn tất.

#### Lớp `PaymentController`

- **Mô tả**: Lớp `PaymentController` xử lý logic của hệ thống khi nhân viên chọn phương thức thanh toán.
- **Phương thức**:
  - `getEmployeeInfo(employeeID: int)`: Lấy thông tin nhân viên từ `EmployeeDatabase` dựa trên `employeeID`.
  - `updatePaymentMethod(employee: Employee, paymentType: String)`: Cập nhật phương thức thanh toán của nhân viên trong cơ sở dữ liệu.

#### Lớp `EmployeeDatabase`

- **Mô tả**: Lớp `EmployeeDatabase` đóng vai trò là cơ sở dữ liệu, lưu trữ và quản lý thông tin của nhân viên.
- **Phương thức**:
  - `retrieveEmployee(employeeID: int)`: Truy xuất thông tin nhân viên từ cơ sở dữ liệu dựa trên `employeeID`.
  - `updatePaymentMethod(employee: Employee, paymentType: String)`: Cập nhật phương thức thanh toán của nhân viên trong cơ sở dữ liệu.

#### Giải thích quan hệ
 - **Employee → PaymentForm**: Nhân viên (Employee) mở giao diện thanh toán (PaymentForm) để chọn phương thức thanh toán. Nhân viên tương tác với giao diện này để thực hiện các thao tác như chọn phương thức thanh toán.

- **PaymentForm → PaymentController**: Giao diện thanh toán (PaymentForm) gửi yêu cầu đến bộ điều khiển thanh toán (PaymentController) để lấy thông tin nhân viên và xử lý các hành động liên quan đến việc chọn phương thức thanh toán.

- **PaymentController → EmployeeDatabase**: Bộ điều khiển thanh toán (PaymentController) truy cập vào cơ sở dữ liệu nhân viên (EmployeeDatabase) để lấy thông tin nhân viên và cập nhật phương thức thanh toán của họ.
  
## 4. Phân tích ca sử dụng Maintain Timecard
### 4.1. Xác định các lớp phân tích
- **Boundary**: 
   - **TimecardForm**: Giao diện người dùng cho nhân viên, cho phép họ mở thẻ chấm công, nhập giờ làm việc và nộp thẻ chấm công.
   - **Project Management**: Actor cung cấp danh sách mã dự án cho **TimecardController**, giúp nhân viên ghi nhận giờ làm việc cho các dự án phù hợp.

- **Control**: 
   - **TimecardController**: 
     - Thành phần điều khiển logic, xử lý yêu cầu từ **TimecardForm**, lấy thẻ chấm công hiện tại, cập nhật giờ làm việc và lưu thẻ chấm công.

- **Entity**: 
   - **Timecard**: 
     - Thực thể lưu trữ thông tin thẻ chấm công, bao gồm ngày, giờ làm việc và mã dự án.
   - **Employee**: 
     - Thực thể đại diện cho nhân viên, lưu trữ ID và tên của họ.

### 4.2. Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/d9G_JiCm5CPtd-AfEnTWG9NAFmcA63h0w3fM4nJRbMCZCZCmS086H2k4a12LG6Ag1uP8tCCdu0euRTCs8auXIoHRx_lbUzzxoRVvR2SAIwLPZ31HGi8U6yOYfHJrXUO1bYdq8aO9bi6-a0mHmPKKyVAoCp_7L2BALQHMvSMvLH1RW1DOuvvASK69wcAE1vIvwbsiS1ydTE6ajIY0LSKCyKk7KF4AsDefsOLjw5hp02mRSGYpLnw22ktK077F9mOa--03L5Ai4LQzESwn4wGLQWWZQsuuA3iTHwX2we3KwOzSsJK39N53I77xRo-rRHtcjdZEChTrsPIzU4UtD1TWbtMIZKdemd-4m9ftoCOS-PLLM8VhIPt2bNPGjO7axV70cadaTLIVzcABIZ6Lv7MxT-AId0nXuCJt46SZ1fVvWCZVHjEPYNdEK3KCxvQKz1MZhND-dhre87Rwh27-UjFDlveDOl-AUuIrSLjpDsnizSojnZmj3ZmdDJVPfZp8_wW_0000__y30000)
### 4.3. Biểu đồ lớp
![Diagram](https://www.planttext.com/api/plantuml/png/X5HDImCn4BtlhvXZ2oszBr8ghQ9WHQZWURePs-WcMIRPbYB-CW_-9F-2IVQZkwt5Is0dRsRUUpFPdw_lcNN8hbHvakLeBToe8ZS78lX80CP0zUVz8WMfNOnfL9J2oh7K6ny0C0NfPwaeGnQtXjLW6CEa7V6TATc-67udKOTjkLRIDNWV_4pgtjqQiJ-0aBR8yT11XwZKHUbYvS4mXPsHeggCEpeYEnUPqQ-IrIfqjbOQtK_RclqJcpVAtDm8ieCid2ayIEkkAfdJ1d_6jVOfkhX0vuq9P-MT5YUHxT6C59PON8MRKJ1s2Z2PU4yDawrWi8yuA8X1u27c5pNBBVA67akr9ZxX6GMX49Kvecq_geh68PvQrZSZJcTmKU_SQCScppshQa8RSlEIsG-xjRvPchJT9b-kkOr9PH6eLIHTVN64ZE1_uZlCPK1TQx4A6iwhUFJQc9nGnmGcxn3jg3VfuObxhTmQjKID6r9UdEU2QxHKgswgzKRnLxdsFOt7q_w2f_7TsAGNxA8wLaVvn9WvlnVIRPC_CDrKdw0YTNi9ULbWsegppS91V179p6zq-5Fy0W00__y30000)

---

#### Lớp Employee:

- **Thuộc tính:**
  - **employeeID**: ID của nhân viên.
  - **name**: Tên của nhân viên.

- **Phương thức:**
  - **openTimecardForm()**: Mở màn hình thẻ chấm công.
  - **enterHoursWorked()**: Nhập giờ làm việc vào thẻ chấm công.
  - **submitTimecard()**: Nộp thẻ chấm công.

#### Lớp TimecardForm:

- **Phương thức:**
  - **displayTimecard()**: Hiển thị thẻ chấm công hiện tại.
  - **inputHours()**: Nhận dữ liệu giờ làm việc từ người dùng.
  - **saveTimecard()**: Lưu thẻ chấm công vào hệ thống.
  - **confirmSubmission()**: Xác nhận việc nộp thẻ chấm công.
  - **showProjectCodes(codes: List<String>)**: Hiển thị danh sách mã dự án.

#### Lớp Timecard:

- **Thuộc tính:**
  - **startDate**: Ngày bắt đầu của thời gian chấm công.
  - **endDate**: Ngày kết thúc của thời gian chấm công.
  - **hoursWorked**: Bản đồ lưu trữ giờ làm việc theo từng ngày.
  - **projectChargeNumbers**: Danh sách mã dự án liên quan đến thẻ chấm công.

- **Phương thức:**
  - **addHours(date: Date, hours: int)**: Thêm giờ làm việc cho một ngày cụ thể.
  - **save()**: Lưu thẻ chấm công.
  - **submit()**: Nộp thẻ chấm công.

#### Lớp TimecardController:

- **Phương thức:**
  - **getCurrentTimecard(employee: Employee)**: Lấy thẻ chấm công hiện tại của nhân viên.
  - **updateHours(timecard: Timecard, date: Date, hours: int)**: Cập nhật giờ làm việc cho thẻ chấm công.
  - **validateAndSave(timecard: Timecard)**: Kiểm tra tính hợp lệ và lưu thẻ chấm công.
  - **retrieveProjectCodes()**: Truy xuất mã dự án từ cơ sở dữ liệu.

#### Lớp ProjectManagementDatabase:

- **Phương thức:**
  - **retrieveChargeNumbers()**: Truy xuất danh sách mã dự án từ cơ sở dữ liệu quản lý dự án.

#### Mối Quan Hệ Giữa Các Lớp
- **Employee → TimecardForm**: Nhân viên mở giao diện thẻ chấm công.
- **TimecardForm → TimecardController**: Giao diện thẻ chấm công tương tác với điều khiển để quản lý thẻ chấm công.
- **TimecardController → Timecard**: Điều khiển thẻ chấm công thực hiện các thao tác như cập nhật và lưu.
- **TimecardController → ProjectManagementDatabase**: Điều khiển truy xuất mã dự án từ cơ sở dữ liệu quản lý dự án.

## 5. Hợp nhất kết quả
![Diagram](https://www.planttext.com/api/plantuml/png/l5NDRjim3BxdAOYS4Y1fiQjH11tI3IkmR0NIOMV5PXEjjgH9SefWs9Fji4VQAuoI9VadJh7J0iG7aXzDVln8__dr-zPOfcrTbHF5ycUsHvXk61UM_l38AyoPBgRmOmAGbymOU5UfKfuGlGbW2HWCztSP42vO1QimWwtLNEoz2K0g537ZUwchsJmuK5ZK7sIjpLUfdx583bFlAcuZnfj_Jb8btLoX6e226rMoKm_ZVboeslftpEOP72KluZlO4TledYkNuedhQkkgC8PBCOGUvCk3bjymjsjPe9dbxfd1HsxiJTFwgaMCL9uuz3EuOvOeSy_8h2ZER8UMfWmsJDquty8HlmAulYR6fKRJXC6BZmE56Wfs2XbKgFZ0z1u_rTKEzQ3cq1uhYeQm8XMnQ1BxGP_JEAJ7Js_sAWDhAQoMPKaLnWdkqQvhhKaKQInHObbI7oMDtW2hbIkpATW6LnkqW7zfuiXAxkBUYcBh-ZdFG_4xAKja8a0q4cTun9uEvcTyTbeFaHicQDagQfDgOZjcC34GS_P6T2bfsiVbSjLVYSnldA6OdhaRrw7Vqu6QvPPqm-sX0-j4TS44gNmJvdBivMQprAQ9aWI_FnDgAvsY1tPogEu12gQnhG-kpyhIifgq-wIeuDbYIUy9czmxJc7NltWL3IzDG8-BDGxWNZp9sU0Opbl5zcGQ4cxG7kIOl1UWceZ7aqfdT51KZBqednZmVufAEfo-cJQZxynfH5nTzzNLQeJZ30nTG4FzVA_H4DBA5jU9S-WpCZ9WUOx6U3tTKXxtXViB003__mC0)

### Tài liệu Mô tả Kết quả Hợp nhất Biểu đồ Lớp

#### 1. Tóm tắt
Kết quả hợp nhất của hai sơ đồ lớp cho hệ thống quản lý thời gian làm việc (*Maintain Timecard*) và phương thức thanh toán (*Payment*) cung cấp một cái nhìn tổng thể về các chức năng của hệ thống. Hệ thống cho phép nhân viên nhập, cập nhật và gửi thông tin thời gian làm việc cũng như phương thức thanh toán của họ. 

#### 2. Luồng Sự kiện

##### 2.1. Luồng cơ bản
1. **Mở biểu mẫu**: Nhân viên mở biểu mẫu thời gian làm việc hoặc phương thức thanh toán.
2. **Lấy thông tin**: Hệ thống lấy và hiển thị thông tin hiện tại cho nhân viên.
   - Nếu không có thời gian làm việc hiện tại, hệ thống tạo một bản mới với ngày bắt đầu và kết thúc được xác định.
   - Đối với phương thức thanh toán, hệ thống hiển thị các tùy chọn phương thức hiện có.
3. **Nhập thông tin**: Nhân viên nhập thông tin giờ làm việc và chọn mã dự án (đối với thời gian làm việc) hoặc chọn phương thức thanh toán (đối với thanh toán).
4. **Lưu thông tin**: Hệ thống lưu thông tin và cho phép nhân viên xác nhận việc cập nhật.
5. **Gửi thông tin**: Nhân viên có thể yêu cầu hệ thống gửi thông tin thời gian làm việc hoặc xác nhận phương thức thanh toán.
6. **Xác nhận và thông báo**: Hệ thống xác nhận và thông báo thành công việc lưu và gửi thông tin.

##### 2.2. Luồng thay thế
- **Thông tin không hợp lệ**: Nếu nhân viên nhập số giờ không hợp lệ (>24 giờ) hoặc vượt quá giới hạn cho phép, hệ thống sẽ hiển thị thông báo lỗi và yêu cầu nhập lại.
- **Thông tin đã được gửi**: Nếu thời gian làm việc đã được gửi, hệ thống hiển thị bản sao chỉ đọc và thông báo rằng không thể thay đổi thông tin.
- **Cơ sở dữ liệu không khả dụng**: Nếu cơ sở dữ liệu không khả dụng, hệ thống thông báo lỗi và cho phép nhân viên chọn tiếp tục (không có mã chi phí để chọn) hoặc hủy bỏ thao tác.

##### 3. Các yêu cầu đặc biệt
- Không có yêu cầu đặc biệt nào.

##### 4. Điều kiện tiên quyết
- Nhân viên phải đăng nhập vào hệ thống trước khi bắt đầu ca sử dụng này.

##### 5. Hậu điều kiện
- Nếu ca sử dụng thành công, thông tin thời gian làm việc và phương thức thanh toán của nhân viên sẽ được lưu vào hệ thống. Nếu không, trạng thái hệ thống không thay đổi.

##### 6. Điểm mở rộng
- Không có điểm mở rộng nào.

