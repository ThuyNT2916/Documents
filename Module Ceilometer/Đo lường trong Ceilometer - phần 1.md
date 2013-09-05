* Đo lường (Measurements)
========================

Có 3 phép đo được định nghĩa trong Ceilometer:

1. Cumulative: tăng theo thời gian ( giờ chạy instance).

2. Gauge: các item riêng biệt (Floating IPs, upload image) và  các giá trị có tính biến động 
(nhập/xuất đĩa - disk I/O).

3. Delta: thay đổi theo thời gian (băng thông).

* Đơn vị
========

1. Bất cứ khi nào một volume được đo, SI chấp thuận các đơn vị đo (SI: hệ đo lường quốc tế) và 
các ký hiệu hoặc chữ viết tắt được sử dụng. Đơn vị thông tin phải được thể hiện trong bit ('b')
hoặc byte ('B').

2. Đối với một máy đo (đồng hồ đo - meter) nhất định, các đơn vị đo không bao giờ được thay đổi.

3. Khi một phép đo không đại diện cho một volume (does not represent a volume) thì việc mô tả đơn 
vị (unit) nên luôn luôn được mô tả đó là phép đo về gì (ví dụ: apples, đĩa (disk), routers, floating
IPs, v.v..).

4. Khi tạo một máy đo mới (create a new meter), nếu một máy đo đã tồn tại đang đo một cái gì đó 
tương tự thì nên sử dụng cùng một kiểu các đơn vị đo (same units) và độ chính xác.

5. Các phép đo và mẫu đo nên được tài liệu hóa lại các đơn vị của nó trong Ceilometer (API và 
tài liệu  - API and Documentation) và những mẫu mã mới không nên được kết hợp vào (merge) mà 
không có những tài liệu thích hợp.

* Đây là các kiểu đo cho các thành phần đang được triển khai.
============================================================

Kiểu (Dimension)  | Đơn vị | Ký hiệu  | Ghi chú                                                                                              |
------------- | ----------------- | --------------- | ------------------                                                                                             |
None        | N/A            |     | Giá trị nhỏ |
Volume| Byte            | B     |  |
Time (thời gian) | Seconds             | s     |  |
