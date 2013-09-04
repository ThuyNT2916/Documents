3. Swift Architectural Overview (kiến trúc) - part 6
====================================================

* Replication (tạo bản sao)
===========================
       
Replication được thiết kế để giữ cho hệ thống trong một trạng thái ổn định khi đối mặt với các 
điều kiện lỗi tạm thời như mất mạng hoặc ổ đĩa thất bại.

Các quá trình Replication so sánh local data với mỗi bản sao từ xa để đảm bảo tất cả Replication
đều có chứa phiên bản mới nhất. Đối tượng sao chép sử dụng một danh sách băm để nhanh chóng so sánh
các phần phụ của mỗi phân vùng.

Replication cũng đảm bảo việc dữ liệu được xóa khỏi hệ thống, khi một mục (object, container, 
hoặc account) bị xóa, thì tombstone được thiết lập như là phiên bản mới nhất của item đó. Replication
cho thấy những tombstone và đảm bảo rằng mục đó đã được xóa khỏi toàn bộ hệ thống.

![ScreenShot](http://1.bp.blogspot.com/-vPXCKUVjbeQ/UiFwBP_s1kI/AAAAAAAAAdY/RZoA2M0G1u0/s1600/zone.png)

Nếu một Zone có dấu hiệu hỏng, một trong các nút có chứa bản sao sẽ thông báo và chủ động sao chép
dữ liệu đến một địa điểm bàn giao

* Updaters
==========

Khi dữ liệu container hoặc account không thể được cập nhật ngay lập tức, điều này thường xảy ra trong 
các failure hoặc khoảng thời gian load lớn. Nếu bản cập nhật không thành công, cập nhật được xếp hàng 
đợi tại local trên filesystem, và update sẽ xử lý các bản update không thành công trước đó. Đây là nơi
cuối cùng có khả năng đi vào để hoạt động. 

Ví dụ: giả sử một container server tải và một object mới được đưa vào hệ thống. Các object ngay lập tức
có sẵn cho lần đọc ngay sau khi các proxy server đáp ứng cho client. Tuy nhiên, các container server đã
không cập nhật danh sách object, do đó, bản cập nhật sẽ được xếp hàng đợi cho một bản cập nhật sau đó. 
Vì thế danh sách Container có thể tại thời điểm đó không có các object mới được đưa vào hệ thống.

* Auditors (Kiểm toán viên)
===========================

Auditors thu thập dữ liệu local server để kiểm tra tính toàn vẹn của các object, container, và account. 
Nếu sai xót được tìm thấy (trong trường hợp của bit rot (mục nát, hỏng)), tập tin được cách ly, và 
replication sẽ thay thế các tập tin lỗi bằng bản sao khác. 
