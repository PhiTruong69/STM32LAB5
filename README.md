# STM32LAB5 — Flow & Error Control in Communication

Repo này triển khai bài lab **Flow and Error Control** trong giao tiếp UART trên STM32. Dự án mô phỏng việc truyền nhận dữ liệu giữa STM32 và terminal (Proteus) với cơ chế kiểm soát lỗi đơn giản dựa trên **ACK**, **timeout**, và **retransmit**.

##  Tóm tắt chức năng
- Giao tiếp **UART 9600 8N1** giữa STM32 ↔ Terminal.  
- Terminal gửi lệnh điều khiển dạng `!CMD#`.  
- Hỗ trợ các lệnh:
  - `!RST#` — yêu cầu STM32 gửi giá trị ADC.
  - `!OK#` — xác nhận đã nhận đúng dữ liệu (ACK).
- STM32 đọc giá trị **ADC (PA0)**, trả về gói tin dạng:  
- Nếu STM32 không nhận được `!OK#` trong **3 giây**, nó sẽ tự động **gửi lại** gói tin.

##  Thành phần chính
- **Command Parser FSM**: đọc ký tự UART và nhận diện lệnh (`RST`, `OK`).
- **UART Communication FSM**: điều khiển gửi dữ liệu, chờ ACK, timeout & retransmit.
- **ADC Reader**: đọc giá trị cảm biến trên PA0.
- **Proteus Simulation**: terminal mô phỏng, POT cho ADC, LED hiển thị.


