Module Ceilometer là gì?
========================
Ceilometer là một dự án được phát triển nhằm mục đích cung cấp một điểm liên lạc duy nhất 
cho hệ thống thanh toán để có được tất cả các phép đo cần thiết để thiết lập việc thanh 
toán cho khách hàng, module hoạt động trên tất cả các thành phần chính hiện nay của OpenStack
và nó có thể hỗ trợ các thành phần mới của OpenStack trong tương lai.
Mục đích của Ceilometer là gì?
==============================
* Cung cấp một công cụ hiệu quả để đo dữ liệu, chi phí CPU và mạng.
* Cho phép người phát triển tích hợp hệ thống đo lường một cách trực tiếp hoặc bằng cách 
thay thế các thành phần.
* Dữ liệu có thể được thu thập bới các thông báo theo dõi (monitoring notifications) được 
gửi từ các dịch vụ đang hoạt động hoặc bằng cách thăm dò (polling) cơ sở hạ tầng.
* Cho phép người phát triển có thể cấu hình các loại dự liệu thu thập để phục vụ cho mục đích
hoạt động của hệ thống một cách phù hợp.
* Một số người dùng có thể thấy các dữ liệu thu thập được từ hệ thống đo lường thông qua một REST API.
* Các thông tin đo được đã được ký (signed) và không thể thoái thác (non-repudiable).
Kiến trúc hệ thống
==================
![ScreenShot](http://4.bp.blogspot.com/-jqnE9LeLhuo/Uh6mAY8giWI/AAAAAAAAAcM/dNRleOxTwO8/s1600/Untitled.png)

* Một "Compute Agent" chạy trên mỗi node Compute và tiến hành các cuộc khảo sát cho việc thống
kê sử dụng tài nguyên.
* Một "Central Agent" chạy trên một máy chủ quản lý trung tâm (central management server) để tiến
hành thăm dò cho việc thống kê sử dụng nguồn tài nguyên cho những tài nguyên không gắn với instances
hoặc node compute.
* Một "Collector" chạy trên một hoặc nhiều máy chủ quản lý trung tâm để giám sát các massage queues
(để thông báo và để tính toán các dữ liệu đến từ các agent).
* Một "Data Store" là một cơ sở dữ liệu có khả năng xử lý đồng thời ghi (từ một hoặc nhiều collector
instances) và đọc (từ máy chủ API).
* Một "Máy chủ API - API Server" chạy trên một hoặc nhiều máy chủ quản lý trung tâm để cung cấp khả
năng truy cập vào dữ liệu từ "data store".
