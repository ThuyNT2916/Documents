Lựa chọn một cơ sở dữ liệu phụ trợ cho Ceilometer không nên bị xem nhẹ vì một số lý do sau:

* Không phải tất cả các trình điều khiển phụ trợ đều được triển khai và thử nghiệm. Để lựa 
chọn một cách dễ dàng, bảng dưới đây sẽ cung cấp một số điều về tình trạng của từng trình điều
khiển có sẵn trong trunk.

* Có thể không phải là một ý hay cho việc sử dụng cùng một máy chủ (host) như là một cơ sở 
dữ liệu khác (database) cho Ceilometer vì Ceilometer có thể thực hiện việc ghi dữ liệu rất nhiều.
Lý do này thường được khuyến cáo, nếu việc triển khai Ceilometer nhằm mục đích sản xuất (thương mại)
thì nên sử dụng một máy chủ chuyên dụng (dành riêng) cho nó, hoặc ít nhất là sử dụng một máy ảo có
khả năng di chuyển sang máy chủ vật lý trong trường hợp cần thiết. Bảng sau đây có thể cung cấp 
thông tin về volumes mà Ceilometer có thể tạo ra.

Link:

    https://docs.google.com/spreadsheet/ccc?key=0AtziNGvs-uPudDhRbEJJOHFXV3d0ZGc1WE9NLTVPX0E#gid=0

![ScreenShot](http://1.bp.blogspot.com/-ZN62BBG3JZ4/UiM986kl1uI/AAAAAAAAAeE/YTbYxXgd6ig/s1600/Untitled.png)

* Nếu bạn đang định dùng phụ trợ này (backend) để lập hóa đơn cho khách hàng, bạn sẽ thấy rằng
khả năng doanh thu mà bạn đạt được liên qua rất nhiều đến độ tin cậy của nó và nó có vẻ như là 
một yếu tố quan trọng cho các nhà quản lý.

Sau đây là bảng về một số đặc điểm đáng chú ý của từng trình điều khiển cơ sở dữ liệu (database drivers):

Driver  | Toàn bộ API | Toàn bộ Storage  | Sử dụng sản xuất                                                                                              |
------------- | ----------------- | --------------- | ------------------                                                                                             |
MongoDB        | Có            |  Có   | Nhiều |
mysql, postgresql| Không            | Có     |/  |
HBASE | Không             | Có     |/  |

Chú thích: "/" là không rõ thông tin.
