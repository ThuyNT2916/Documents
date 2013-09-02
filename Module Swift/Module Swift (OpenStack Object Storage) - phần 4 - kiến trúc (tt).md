3. Swift Architectural Overview (kiến trúc) - part 2
====================================================

* Ring
======

Một Ring đại diện cho một ánh xạ giữa tên của các thực thể được lưu trữ trên đĩa và vị trí địa lý 
của chúng. Có Ring riêng biệt cho các account, container, và các object. Khi các thành phần khác 
cần phải thực hiện bất kỳ hoạt động trên một container, object, hoặc account, thì cần phải tương 
tác với Ring thích hợp để xác định vị trí của nó trong cluster.

Cấu trúc dữ liệu Ring bao gồm ba phần chính: một danh sách các thiết bị trong cluster, một danh sách
các danh sách id thiết bị để phân vùng tập thiết bị, và một số nguyên cho biết số bit để tính toán 
băm để phân vùng.

Dữ liệu có thể được cô lập với nội dung của zone trong Ring. Mỗi bản sao của một phân vùng được đảm 
bảo để thường trú trong một zone khác nhau. Một zone có thể đại diện cho một ổ đĩa, một server, 
cabinet, một switch, hoặc thậm chí một trung tâm dữ liệu.

Các phân vùng của Ring được chia đều giữa tất cả các thiết bị trong quá trình cài đặt Swift. 
Khi phân vùng cần phải được di chuyển xung quanh (ví dụ nếu một thiết bị được thêm vào cluster),
Ring đảm bảo rằng một số lượng tối thiểu các phân vùng được chuyển tại một thời điểm, và chỉ có
một bản sao của một phân vùng được di chuyển tại một thời điểm.

Trọng lượng có thể được sử dụng để cân bằng sự phân bố của các phân vùng trên ổ đĩa trên cluster.
Điều này có thể hữu ích, ví dụ, khi ổ đĩa có kích thước khác nhau được sử dụng trong một cluster.

Ring được sử dụng bởi các Proxy Server và một số tiến trình nền (như sao chép).

Bản đồ Ring phân vùng đến các địa điểm vật lý trên đĩa. Ring duy trì lập bản đồ này bằng cách sử dụng
các zone, thiết bị, phân vùng, và bản sao. Mỗi phân vùng trong Ring được tái bản, theo mặc định, 3 lần
qua cluster, và các địa điểm cho một phân vùng được lưu trữ trong các Map. Ring cũng chịu trách nhiệm
xác định những thiết bị được sử dụng cho handoff (bàn giao) khi failure.

![ScreenShot](http://3.bp.blogspot.com/-D4WbTAwv5Ho/UiFpr6bK6wI/AAAAAAAAAcs/0hCTPZzmFJQ/s1600/fdsfsd.png)

Bản đồ Ring  phân vùng đến các địa điểm vật lý trên đĩa.
