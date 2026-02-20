# Choosing the database to use?
There are two types of database: relational database or non-relational database
CSDL quan hệ thể hiện và lưu trữ dữ liệu trong các bảng và hàng
CSDL không quan hệ lưu trữ dữ liệu theo 4 dạng: key-value, graph, column, document.

Nếu hệ thống có một số yêu cầu dưới đây, việc sử dụng No-SQL có thể là một lựa chọn tốt:
- Ứng dụng yêu cầu độ trễ thấp
- Dữ liệu không có cấu trúc cụ thể, hoặc không có quan hệ giữa các dữ liệu
- Chỉ cần serialize hoặc deserialize dữ liệu (JSON, XML, YAML,...)
- Cần lưu trữ một lượng lớn data

# Vertical scaling vs Horizontal scaling
**Vertical scaling**: nghĩa là thêm năng lực xử lý ở server ( CPU, RAM, ...)
**Horizontal scaling**: nghĩa là tăng thêm số lượng server

Vertical scaling phù hợp cho trường hợp traffic nhỏ, vì tính dễ dàng trong triển khai, tuy nhiên có một số nhược điểm:
- Có giới hạn về số lượng CPU và RAM
- Không có cơ chế failover và redundancy

Horizontal scaling phù hợp cho các app lớn do vượt qua các limit của Vertical Scaling

# Load balancer
![[Pasted image 20250417155507.png]]

Load balancer chia các request đến các server khác nhau nhằm đảm bảo tải giữa các server
Web server sẽ không được truy cập trực tiếp từ internet.
Các server sử dụng private IP để giao tiếp với nhau.

Việc thêm load balancer sẽ xử lý vấn đề failover issue và tăng cường khả năng availability của app.

# Database replication
