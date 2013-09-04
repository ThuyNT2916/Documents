3. Swift Architectural Overview (kiến trúc) - part 5
====================================================

* Object Server 
===============
Server Object là một blob lưu trữ server mà có thể lưu trữ, truy xuất và xóa các đối tượng được 
lưu trữ trên các thiết bị địa phương. Đối tượng được lưu trữ như các tập tin nhị phân trên 
filesystem với siêu dữ liệu được lưu trữ trong các thuộc tính mở rộng của tập tin (xattrs).
Điều này đòi hỏi: filesystem lựa chọn cho các object servers hỗ trợ xattrs trên các tập tin.
Một số filesystem, như ext3, có xattrs tắt theo mặc định.

Mỗi đối tượng được lưu trữ bằng cách sử dụng một đường dẫn có nguồn gốc từ dữ liệu hỏng của tên
đối tượng và dấu thời gian của hoạt động. Lần ghi cuối luôn thành công, và đảm bảo rằng đối 
tượng phiên bản mới nhất sẽ được phục vụ. Xóa là một version (thế hệ) của tập tin. Điều này đảm
bảo rằng các tập tin đã xóa được nhân rộng một cách chính xác và các phiên bản cũ hơn không xuất
hiện trở lại do các failure.

* Partitions (Phân vùng)
========================

Phân vùng là một tập hợp các dữ liệu được lưu trữ, bao gồm databases account, databases Container,
và các object. Phân vùng là cốt lõi để hệ thống sao chép.

Xem một phân vùng như là một thùng di chuyển qua một nhà kho trung tâm. Đơn đặt hàng riêng lẻ được
đặt vào thùng. Hệ thống xử lý rằng thùng này như một thực thể gắn kết khi nó di chuyển trên toàn hệ
thống. Một thùng đầy sẽ tiết kiệm được các pha hoạt động trên toàn hệ thống.

Replication và update object hoạt động trên phân vùng. Khi hệ thống quy mô hơn, số lượng của phân 
vùng là một số cố định.

Việc thực hiện các phân vùng là khái niệm rất đơn giản - một phân vùng chỉ là một thư mục trên một
đĩa với một bảng băm tương ứng của những gì nó chứa.

![ScreenShot](http://4.bp.blogspot.com/-bJ4UmaUKZpE/UiFuZZM7pyI/AAAAAAAAAdM/iwhhdiylxZs/s1600/phan+vung.png)

Phân vùng Swift có chứa tất cả các dữ liệu trong hệ thống.
