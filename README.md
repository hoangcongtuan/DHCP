# Tìm hiểu về DHCP

### 1. Khái niệm

*DHCP là gì? Ưu điểm của DHCP*

**DHCP** là viết tắt của **Dynamic Host Configuration Protocol**, là giao thức Cấu hình Host Động được thiết kế làm giảm thời gian chỉnh cấu hình cho mạng TCP/IP bằng cách tự động gán các địa chỉ IP cho khách hàng khi họ vào mạng. Dich vụ DHCP là một thuận lợi rất lớn đối với người điều hành mạng. Nó làm yên tâm về các vấn đề cố hữu phát sinh khi phải khai báo cấu hình thủ công. Nói một cách tổng quan hơn DHCP là dich vụ mang đến cho chúng ta nhiều lợi điểm trong công tác quản trị và duy trì một mạng TCP/IP như: 

- Tập chung quản trị thông tin về cấu hình IP. 
- Cấu hình động các máy. 
- Cấu hình IP cho các máy một cách liền mạch 
- Sự linh hoạt 
- Khả năng mở rộng. 

### 2. Chức năng: 
- Mỗi thiết bị trên mạng cơ sở TCP/IP phải có một địa chỉ IP duy nhất để truy cập mạng và các tài nguyên của nó. Không có DHCP, cấu hình IP phải được thực hiện một cách thủ công cho các máy tính mới, các máy tính di chuyển từ mạng con này sang mạng con khác, và các máy tính được loại bỏ khỏi mạng. 
- Bằng việc phát triển DHCP trên mạng, toàn bộ tiến trình này được quản lý tự động và tập trung. DHCP server bảo quản vùng của các địa chỉ IP và giải phóng một địa chỉ với bất cứ DHCP client có thể khi nó có thể ghi lên mạng. Do là cơ chế động nên các IP đã được cấp phát nhưng trong một khoảng thời gian nhất định mà không còn hoạt động sẽ được thu hồi và cấp lại cho máy khác khi tham gia mạng.

### 3. Các thuật ngữ trong DHCP:

- **DHCP Server:** máy quản lý việc cấu hình và cấp phát địa chỉ IP cho Client
- **DHCP Client:** máy trạm nhận thông tin cấu hình IP từ DHCP Server
- **Scope:** dải IP được sử dụng để cấp phát cho Client.
- **Exclusion Scope:** là dải địa chỉ nằm trong Scope không được cấp phát động cho Clients.
- **Reservation:** Địa chỉ đặt trước dành riêng cho máy tính hoặc thiết bị chạy các dịch vụ (tùy chọn này thường được thiết lập để cấp phát địa chỉ cho các Server, Printer,…..)*
- **Scope Options:** các thông số được cấu hình thêm khi cấp phát IP động cho Clients như DNS Server(006), Router(003)*

"*" Tùy chọn trên Windows Server

### 5. Các thông điệp DHCP:

- **DHCP Discover**: Một DHCP Client khi mới tham gia vào hệ thống mạngg, nó sẽ yêu cầu thông tin địa chỉ IP từ DHCP Server bằng cách  broadcast một gói DHCP Discover. Địa chỉ IP nguồn trong gói là 0.0.0.0 bởi vì client chưa có địa chỉ IP. 
- **DHCP Offer**: Khi DHCP server nhận được gói DHCP Discover từ client, nó sẽ gửi lại một gói DHCP Offer chứa địa chỉ IP, Subnet Mask, Gateway,... Có thể nhiều DHCP server gửi lại với gói DHCP Offer nhưng Client sẽ chấp nhận gói DHCP Offer đầu tiên nó nhận được.
- **DHCP Request**: Khi DHCP client nhận được một gói DHCP Offer, nó đáp lại bằng việc broadcast gói DHCP Request để xác nhận hoặc để kiểm tra lại các thông tin mà DHCP server vừa gửi.
- **DHCP Acknowledge**: Server kiểm tra và xác nhận lại sự chấp nhận trên bằng gói tin DHCP Acknowledge, Client có thể tham gia trên mạng TCP/IP và hoàn thành hệ thống khởi động.
- **DHCP Nak**: Nếu một địa chỉ IP đã hết hạn hoặc đã được đặt một máy tính khác, DHCP Server gửi gói DHCP Nak cho Client, như vậy Client phải bắt đầu tiến trình thuê bao lại.
- **DHCP Decline**: Nếu DHCP Client nhận được bản tin trả về không đủ thông tin hoặc hết hạn, nó sẽ gửi gói DHCP Decline đến các Server và Client phải bắt đầu tiến trình thuê bao lại.
- **DHCP Release**: Client gửi bản tin này đến server để ngừng thuê IP. Khi nhận được bản tin này, server sẽ thu hồi lại IP đã cấp cho Client, khi đó client sẽ không được cấu hình IP.

### 6. Cơ chế hoạt động

<img src="http://i1363.photobucket.com/albums/r714/HoangLove9z/33550_zpsi3bzo3ua.jpg" />

- **Bước 1**: Client gửi một bản tin Discover - có chứa thông tin client (MAC, Tên máy tính,...) với dạng Broadcast để "truy tìm" một DHCP Server để xin cấp phát địa chỉ IP
- **Bước 2**: Khi DHCP Server nhận được một bản tin Discover sẽ gửi lại cho Client một bản tin Offer - chứa những thông tin IP,thời hạn cho thuê, GW, DNS Server,... dưới dạng Unicast
- **Bước 3**: Client gửi lại một bản tin Request cho Server, để xác nhận lại các thông tin
- **Bước 4**: Server trả về bản tin ACK để hoàn tất quá trình

### 7. Tham khảo:
- http://vdo.vn/cong-nghe-thong-tin/cac-khai-niem-co-ban-ve-dhcp.html
- https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol
