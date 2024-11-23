# Lab 3. Identify design elements: Xác định các phần tử thiết kế của hệ thống “Payroll System”
## 1. Subsystem context diagrams
### 1.1 Hệ thống con: Bank System
![Diagram](https://www.planttext.com/api/plantuml/png/j99BRiCW48RtFiKiKwdE0L1aHMqtNYIAb1DWF6bH35WmI4LjJzP5ZzGh5EmujMDtMHOyvl5_Cy3tvzVM4RVaLPDb48Tek7DmuC6QfdaqcjAA5ZORqH-A0jwwo7vOho_1gxlE_D7hI4reJrmWb0zSdu_14QgeShNVwDJO6YTfnQEQU45nPZ3ixfEOIIeCqbpgax6AapHwWknB_wKTh7aD4UbyvNfycop_1Hwo8X4rIPg2Sa3LDYOWbZM38rcfdqTEhepNn61dD8QHlUQ439xYlDpfgAI_k5KCstE5IrGX4dRlLOLsmM-DfsXPy5yAcRpj-tezktq6ChQDAbRcPXbvNbnlRT5vqs6MpVzb2XkdCQYbHK73kphev5ssHLsdN_u3003__mC0)
* **Giải thích**:
  - `IBankSystem` (interface): Đây là giao diện định nghĩa phương thức deposit, đại diện cho quy trình giao tiếp giữa hệ thống Payroll và Bank System.
  - `BankSystemProxy` (subsystem proxy): Lớp này triển khai IBankSystem, đóng vai trò làm cầu nối với hệ thống ngân hàng thực tế.
  - `Paycheck` (entity): Một thực thể lưu trữ thông tin phiếu lương, bao gồm mã nhân viên (employeeId), số tiền (amount), và ngày thanh toán (date).
  - `BankInformation` (entity): Một thực thể lưu trữ thông tin ngân hàng, bao gồm tên ngân hàng, số tài khoản, và số định tuyến.

### 1.2 Hệ thống con:  PrinterService Subsystem
![Diagram](https://www.planttext.com/api/plantuml/png/f9BDJiCm3CVlUGeVnw5xWAYg9i5b1wHAUuAGcb6HZofs9oAs9-F08_4AkAoD6DkD79BuR-TdnydNn-U6s2GUlLC0rXaYQ4rEqRdx67XQCK5TsxFHDF0kSUUHnZ27hkv4F2cP-i2Oder5sBRfnzXXElHYrtNnNL26AKmuzWNjwsgODneMgQ3duYweROflMT0qFb4cHYyuKVwLO9Q5Ye5x_Wsh0FtWOaRSTXfsBEHzSHaVny0Q7cF0NDJEC6fua7b9SzMOutfzyreQUic6NigW6-UggYd5AgMkNsqA-7j8mnu39Yc7O6a5gGs6Rle1tm000F__0m00)

* **Giải thích**:
  - `PayrollController` (Control): Gửi yêu cầu in phiếu lương (paycheck) đến hệ thống in thông qua giao diện IPrinterService.
  - `IPrinterService` (Interface): Giao diện định nghĩa phương thức printPaycheck(paycheck: Paycheck) cho hệ thống in phiếu lương.
  - `PrinterServiceProxy` (Subsystem Proxy): Đại diện cho lớp triển khai giao diện IPrinterService. Xử lý việc kết nối tới dịch vụ in hoặc mô phỏng việc in phiếu lương trong một số trường hợp.
  - `Paycheck` (Entity): Là lớp chứa thông tin về phiếu lương, được truyền từ PayrollController đến PrinterService.

### 1.3 Hệ thống con: ProjectManagementDatabase Subsystem
![Diagram](https://www.planttext.com/api/plantuml/png/h5BBIWD14BpFLpIvc0XPz1h24aWk0HKn_a3lR6SpiZkpTFT6W_fb7lmaVy799ZuIT45mJZFLrLHrzRozl4v4aRMfIcDEO4PBvmbiYI8aSEzq1QB457HJHm2pi2RJbk7MLMIHysdmog4iYM4yjhj7ciAZWNWAKh0DCta5tJVq1r-b5N8HzK9EieUREaUbOxBW-W1xDiRvQ6o9bc1-pU6Eh5wYnuAgg3L3nGo5egFv1-tJKoizRPMlcYeZbhvb5raEHx1GThuOZFRM8k72YMxrTbDtIKcJoIR6LK7DuM7pFuBJ0pZkw8PAL1Uyh5mjveSjzCwIvBG7ms7QNizxNG5zqrs4XYsPhZIVakJt1BewaoGzckGlN3CXds-_w3i0003__mC0)

* **Giải thích**:
  - `TimecardController` (Control): Quản lý logic nghiệp vụ và điều phối các tác vụ liên quan đến timecard.
  - `ChargeNumList` (Entity): Chứa danh sách mã chi phí (`chargeNumList`) được sử dụng trong hệ thống.
  - `IProjectManagementDatabase` (Interface): Đây là giao diện trung gian, định nghĩa các phương thức để các lớp khác sử dụng mà không cần biết chi tiết triển khai.
  -  `ProjectManagementDatabase` (Subsystem Proxy): Triển khai giao diện `IProjectManagementDatabase` và đóng vai trò kết nối hoặc tương tác với cơ sở dữ liệu hoặc các dịch vụ phụ trợ khác.

---
## 2. Analysis class to design element map
|  Analysis Class               | Design Element             |  
|-------------------------------|----------------------------|
| LoginForm                     | LoginForm                  |
| MaintainTimecardForm          | MainEmployeeForm           |
| TimecardController            | TimecardController         |
| PayrollController             | PayrollController          |
| PayCheck                      | PayCheck                   |
| BankInformation               | BankInformation            |
| SystemClockInterface          | SystemCLockInterface       |
| PayrollController             | PayrollController          |
| Employee                      | Employee                   |
| Timecard                      | TimecardEntity             |
| Payroll                       | PayrollProcessor           |
| BankSystem                    | BankSystemProxy            |
|                               | IBankSystem                |
| PrintService                  | PrinterServiceProxy        |
|                               | IPrinterService            |
| ProjectManagementDatabase     | ProjectManagementDatabase  |
|                               | IProjectManagementDatabase |



---
## 3. Design Element to Owning Package Map

| **Design Element**            | **Owning Package**         |
|-------------------------------|----------------------------|
| LoginForm                 | PresentationLayer (UI)     |
| MaintainTimecardForm      | PresentationLayer (UI)     |
| TimecardController        | PresentationLayer (Controller) |
| PayrollController         | PresentationLayer (Controller) |
| PayCheck                  | BusinessLogicLayer         |
| BankInformation           | BusinessLogicLayer         |
| SystemClockInterface      | BaseReuseLayer             |
| Employee                  | BusinessLogicLayer         |
| TimecardEntity            | BusinessLogicLayer         |
| PayrollProcessor          | BusinessLogicLayer         |
| BankSystemProxy           | DataAccessLayer (DAO)      |
| IBankSystem               | DataAccessLayer (DAO)      |
| PrinterServiceProxy       | DataAccessLayer (DAO)      |
| IPrinterService           | DataAccessLayer (DAO)      |
| ProjectManagementDatabase | DataAccessLayer (DAO)      |
| IProjectManagementDatabase| DataAccessLayer (DAO)      |

