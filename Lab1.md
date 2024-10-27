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
  ![Diagram](https://www.planttext.com/api/plantuml/png/T991JW8n58RtFSKBUox0mW0InKYYKLmOmwAM9pIC7MrVKM9SkN3X0Jm0CIOcnlqqX0KdwGcyWfr1mXInYwPfl-_rVqs_tRnkY6kormbZPYGLwDGW8qa9Waclw8vh1Ax5K18AiXhP3HSZFa2e76iqg8YJJ1Lq-0Hr1HuOX75nTj1RBdPJHJfD4jGzziZMRjCQgT0OwAG3AJRiKzHZAJ0sMfmuD8Gef0XlDOv-RykPIsusp6ROWHEqOTv8IJAHD84zgqJUX2cyF3nKgpjHUAZ1ldUV4lhUVK4YlNksB08AOvKyuEUB3ml2P-yMxeC9oMB6rkS5dGUFoQXwSRm4Ltq5kglj1CO-UrEij5-krzK-c_vNgfHm2nVdY_i_zDcSuDO6QKld-QFLe1tgF2cWeNSlC2e9RCjZ_mdKzkuLI7itPNLK_VnF_W000F__0m00)
## 2. Cơ chế phân tích
- **Persistency** (Cơ chế bền vững): Hệ thống cần đảm bảo mọi dữ liệu được ghi nhận (thông tin nhân viên, thời gian làm việc, thông tin lương) được lưu trữ bền vững trong database. Việc này giúp bảo vệ dữ liệu khỏi mất mát và đảm bảo có thể truy xuất lịch sử thông tin khi cần thiết.
  
- **Communication** (Cơ chế trao đổi dữ liệu): Ngoài việc trao đổi thông tin giữa các thành phần bên trong thì hệ thống cần có khả năng trao đổi dữ liệu với các hệ thống bên ngoài (ví dụ: ngân hàng để chuyển khoản tiền lương)

- **Information Exchange and Format Conversion** (Trao đổi thông tin và chuyển đổi định dạng): Hệ thống cần có khả năng trao đổi dữ liệu với các phần mềm khác (như phần mềm kế toán hoặc hệ thống quản lý nhân sự) và chuyển đổi giữa các định dạng dữ liệu khác nhau. Điều này giúp tăng tính tương tác và tích hợp của hệ thống.

- **Security** (Cơ chế bảo mật): Cần thiết lập các biện pháp bảo mật mạnh mẽ để bảo vệ dữ liệu cá nhân và tài chính của nhân viên. Điều này bao gồm xác thực đa yếu tố, mã hóa dữ liệu và kiểm tra quyền truy cập để ngăn chặn các cuộc tấn công từ bên ngoài.

- **Error Detection/Handling/Reporting** (Cơ chế phát hiện, xử lý và báo cáo lỗi): Hệ thống cần có cơ chế phát hiện lỗi trong quá trình tính toán lương hoặc trong giao tiếp dữ liệu, đồng thời cung cấp thông báo báo lỗi rõ ràng để hỗ trợ xử lý kịp thời. Điều này giúp duy trì tính ổn định và tin cậy của hệ thống.

- **Legacy Interface** (Cơ chế giao tiếp với hệ thống đã tồn tại): Hệ thống mới cần có khả năng giao tiếp với cơ sở dữ liệu hiện có (Cơ sở Dữ liệu Quản lý Dự án) mà không làm thay đổi hoặc làm mất dữ liệu hiện tại. Điều này giúp tối ưu hóa chi phí và thời gian triển khai hệ thống mới.

## 3. Phân tích ca sử dụng Payment
## 4. Phân tích ca sử dụng Maintain Timecard
## 5. Hợp nhất kết quả
