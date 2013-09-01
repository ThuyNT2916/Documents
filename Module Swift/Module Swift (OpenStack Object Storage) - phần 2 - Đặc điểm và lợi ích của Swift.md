2. Đặc điểm và lợi ích của Swift
================================

* Đặc điểm
==========
Các đặc tính quan trọng của Swift bao gồm:
- Tất cả các đối tượng được lưu trữ trong Swift có một URL.
- Tất cả các đối tượng được lưu trữ được nhân rộng 3x trong các zone (coi như là duy nhất), 
có thể được định nghĩa là một nhóm các ổ đĩa, một nút, một rack.
- Tất cả các đối tượng có siêu dữ liệu của riêng mình.
- Các nhà phát triển tương tác với hệ thống lưu trữ đối tượng thông qua một HTTP RESTful API.
- Dữ liệu object có thể được đặt bất cứ nơi nào trong cluster.
- Cluster mở rộng bằng cách thêm các nút bổ sung mà không hy sinh hiệu suất, cho phép nâng 
cấp hiệu quả chi phí lưu trữ mở rộng tuyến tính.
- Dữ liệu không phải di chuyển đến một hệ thống lưu trữ hoàn toàn mới.
- Các nút mới có thể được thêm vào cluster mà không có thời gian chết.
- Các nút và ổ đĩa bị hỏng có thể được hoán đổi với thời gian nghỉ dưỡng.
- Chạy trên phần cứng tiêu chuẩn công nghiệp, chẳng hạn như Dell, HP, Supermicro…

![ScreenShot](http://2.bp.blogspot.com/-LGCLea0tqOw/UiC-qQR1G4I/AAAAAAAAAcc/KH3ifUbcQzg/s1600/1231231.png)

Để có được một danh sách của tất cả các container trong một account, sử dụng lệnh GET trên tài khoản:

    GET http://swift.example.com/v1/account/
   
Để tạo container mới, sử dụng lệnh PUT với tên của các container mới:

    PUT http://swift.example.com/v1/account/new_container
   
Để liệt kê tất cả các đối tượng trong một container, sử dụng lệnh GET trên container:

    GET http://swift.example.com/v1/account/container/
   
Để tạo các đối tượng mới với một PUT trên đối tượng:

    PUT http://swift.example.com/v1/account/container/new_object
   
Lệnh POST được sử dụng để thay đổi siêu dữ liệu container và objects.
 
* Lợi ích  của Swift
====================
** Đối với các nhà phát triển ứng dụng
======================================
- Dữ liệu được lưu trữ và phục vụ trực tiếp qua HTTP.
- Truy cập để lưu trữ trong vài phút.
- Một hệ thống lưu trữ multi-tenant (đa người dùng) cho tất cả các ứng dụng.
- Một hệ sinh thái phong phú của các công cụ và thư viện.

** Đối với các nhóm IT
======================
- Sử dụng chi phí thấp, máy chủ và ổ đĩa tiêu chuẩn công nghiệp.
- Quản lý nhiều dữ liệu hơn và các case sử dụng một cách dễ dàng.
- Kích hoạt các ứng dụng mới một cách nhanh chóng.
- Kiến trúc độ bền cao.
- Không có nhà cung cấp lock-in.
