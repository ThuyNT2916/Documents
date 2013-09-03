3. Swift Architectural Overview (kiến trúc) - part 3
====================================================

* Zone: Failure Boundaries (không ranh giới)
============================================

Swift cho phép zone được cấu hình để cô lập các ranh giới thất bại. Mỗi bản sao của dữ liệu nằm
trong một zone riêng biệt, nếu có thể. Ở cấp độ nhỏ nhất, một zone có thể là một ổ đĩa đơn hay 
nhóm của một vài ổ đĩa. Nếu có năm object servers lưu trữ, thì mỗi máy chủ sẽ đại diện cho zone
riêng của mình. Phát triển lớn hơn thì sẽ có một rack (hoặc nhiều rack) của object servers, mỗi
rack đại diện cho một zone. Mục tiêu của zone là để cho phép các cluster chịu mất các object 
server quan trọng mà không bị mất tất cả các bản sao của dữ liệu.

Tất cả mọi thứ trong Swift được lưu giữ, theo mặc định là ba bản sao. Swift sẽ đặt mỗi bản sao
"như là duy nhất" để vừa đảm bảo tính sẵn sàng cao và độ bền cao. Điều này có nghĩa là khi lựa
chọn một vị trí bản sao, Swift sẽ lựa chọn một máy chủ trong khu vực không sử dụng, và trong 
khu vực đó đã có một bản sao của dữ liệu.

![ScreenShot](http://2.bp.blogspot.com/-7sb19tIWLtk/UiFrPwk7yII/AAAAAAAAAc4/qghtB9Cua6c/s1600/d%E1%BA%A5dasd.png)

Khi một ổ đĩa hỏng, bản sao dữ liệu được tự động phân phối cho các zone khác để đảm bảo có ba bản sao của dữ liệu
