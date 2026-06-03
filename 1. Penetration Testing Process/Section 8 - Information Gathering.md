# Information Gathering

Sau khi giai đoạn Pre-Engagement hoàn thành và tất cả các bên đã ký các điều khoản, thỏa thuận cần thiết, giai đoạn Information Gathering bắt đầu.

### Các nhóm Information Gathering

Thông tin thu thập được được chia thành 4 nhóm chính:

- Open-Source Intelligence (OSINT)
- Infrastructure Enumeration
- Service Enumeration
- Host Enumeration

### 1. Open-Source Intelligence (OSINT)

OSINT là quá trình thu thập thông tin công khai từ các nguồn mở nhằm xác định:

- Các sự kiện liên quan đến công ty
- Các mối liên hệ nội bộ và bên ngoài
- Các phụ thuộc của hệ thống
- Thông tin về tổ chức hoặc cá nhân

Mục tiêu là tận dụng các nguồn thông tin công khai để tìm kiếm các dữ liệu có giá trị cho quá trình đánh giá bảo mật.

Trong quá trình này có thể phát hiện:

- Mật khẩu
- Hash
- Khóa mã hóa
- Token
- Các thông tin nhạy cảm khác

Những thông tin này đôi khi xuất hiện trên:

- Kho mã nguồn công khai
- Nền tảng phát triển phần mềm
- Diễn đàn kỹ thuật
- Các trang hỏi đáp dành cho lập trình viên

Nếu phát hiện các thông tin nhạy cảm như mật khẩu hoặc khóa SSH công khai, đây được xem là lỗ hổng nghiêm trọng và phải được báo cáo theo quy trình được quy định trong Rules of Engagement (RoE).

### 2. Infrastructure Enumeration

Trong giai đoạn này, pentester cố gắng xây dựng cái nhìn tổng thể về hạ tầng của công ty trên Internet hoặc mạng nội bộ.

Hoạt động này sử dụng:

- Kết quả OSINT
- Các kỹ thuật quét chủ động (active scanning)

Mục tiêu là xác định:

- DNS servers
- Mail servers
- Web servers
- Cloud instances
- Các hệ thống khác thuộc hạ tầng của tổ chức

Kết quả cuối cùng là một danh sách chính xác các host và địa chỉ IP để đối chiếu với phạm vi kiểm thử (scope).

Ngoài ra, pentester còn cố gắng xác định các biện pháp bảo vệ hiện có như:

- Firewall
- Web Application Firewall (WAF)
- Các cơ chế bảo mật khác

Thông tin này đặc biệt quan trọng trong các bài kiểm thử né tránh phát hiện (Evasive Testing), giúp pentester hiểu được những hoạt động nào có thể kích hoạt cảnh báo bảo mật.

Infrastructure Enumeration có thể được thực hiện:

- Từ bên ngoài hệ thống (External)
- Từ bên trong hệ thống (Internal)

Enumeration nội bộ thường cung cấp nhiều thông tin chi tiết hơn về các máy chủ và người dùng trong mạng.

### 3. Service Enumeration

Service Enumeration tập trung vào việc xác định các dịch vụ đang hoạt động trên các host.

Các mục tiêu chính bao gồm:

- Dịch vụ nào đang chạy
- Phiên bản dịch vụ
- Thông tin dịch vụ cung cấp
- Mục đích sử dụng của dịch vụ

Sau khi hiểu được vai trò và chức năng của dịch vụ, pentester có thể đưa ra các kết luận về những hướng tấn công tiềm năng.

Một trong những yếu tố quan trọng nhất là xác định phiên bản phần mềm.

Thông qua lịch sử phiên bản, pentester có thể:

- Xác định phần mềm đã được cập nhật hay chưa
- Tìm kiếm các lỗ hổng đã biết (known vulnerabilities)
- Đánh giá mức độ rủi ro của hệ thống

Tài liệu nhấn mạnh rằng nhiều quản trị viên thường ngại nâng cấp các ứng dụng đang hoạt động ổn định vì lo ngại ảnh hưởng tới hệ thống, dẫn đến việc tồn tại các lỗ hổng chưa được vá.

### 4. Host Enumeration

Sau khi có danh sách chi tiết về hạ tầng, pentester sẽ tiến hành kiểm tra từng host trong phạm vi được phép.

Mục tiêu bao gồm xác định:

- Hệ điều hành đang sử dụng
- Các dịch vụ đang chạy
- Phiên bản dịch vụ
- Cấu hình hệ thống
- Vai trò của host trong mạng

Bên cạnh các kỹ thuật quét chủ động, pentester cũng có thể sử dụng OSINT để hiểu rõ hơn cách host được cấu hình.

Trong quá trình này, pentester cố gắng xác định:

- Vai trò của host hoặc server
- Các thành phần mạng mà host giao tiếp
- Các dịch vụ được sử dụng
- Các cổng mạng liên quan

Đối với Internal Host Enumeration (sau khi đã có quyền truy cập hệ thống), pentester sẽ tiếp tục tìm kiếm:

- Tập tin nhạy cảm
- Dịch vụ nội bộ
- Script
- Ứng dụng
- Thông tin cấu hình
- Các dữ liệu có thể hỗ trợ leo thang đặc quyền

Đây là một phần quan trọng của giai đoạn Post-Exploitation.

### Pillaging

Pillaging là hoạt động thu thập dữ liệu nhạy cảm **trên hệ thống đã bị khai thác thành công**.

Hoạt động này chỉ diễn ra sau khi pentester đã có quyền truy cập vào mục tiêu.

Thông tin thu thập được phụ thuộc vào:

- Vai trò của hệ thống
- Vị trí của hệ thống trong mạng doanh nghiệp
- Các biện pháp bảo mật đang được áp dụng

Dữ liệu thu được có thể:

- Chứng minh mức độ ảnh hưởng của cuộc tấn công
- Hỗ trợ leo thang đặc quyền (Privilege Escalation)
- Hỗ trợ di chuyển ngang trong mạng (Lateral Movement)

Tài liệu lưu ý rằng HTB Academy không có module riêng cho Pillaging vì đây không phải là một giai đoạn độc lập.

Pillaging được xem là:

- Một phần của Information Gathering
- Một phần của Privilege Escalation
- Một hoạt động được thực hiện cục bộ trên các hệ thống đã bị khai thác

Kiến thức về Pillaging được phân bổ trong nhiều module khác nhau như:

- Network Enumeration with Nmap
- Getting Started
- Password Attacks
- Active Directory Enumeration & Attacks
- Linux Privilege Escalation
- Windows Privilege Escalation
- Attacking Common Services
- Attacking Common Applications
- Attacking Enterprise Networks