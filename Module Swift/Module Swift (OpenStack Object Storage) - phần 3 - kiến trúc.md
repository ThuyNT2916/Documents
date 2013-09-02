3. Swift Architectural Overview (kiến trúc) - part 1
====================================================

* Building Blocks
=================

Các thành phần cho phép Swift để cung cấp tính sẵn sàng cao, độ bền cao và đồng thời cao là:

- Proxy Servers: xử lý tất cả các yêu cầu API.
- Rings: Maps tên logic của dữ liệu đến các địa điểm trên đĩa cụ thể.
- Zones: Mỗi Zone cô lập dữ liệu từ các zone khác. Một thất bại trong một zone không ảnh hưởng 
đến phần còn lại của cluster vì dữ liệu được nhân rộng trên các zone.
- Accounts & Containers: Mỗi tài khoản và container là cơ sở dữ liệu cá nhân được phân phối trên
cluster. Một cơ sở dữ liệu Account có chứa danh sách các Containers trong Account đó. Một cơ sở
dữ liệu Container chứa danh sách các đối tượng trong Container đó.
- Objects: Các dữ liệu của chính các đối tượng.
- Partitions: phân vùng lưu trữ các đối tượng, cơ sở dữ liệu Account và cơ sở dữ liệu container. 
Đây là một trung gian 'vùng chứa' giúp quản lý vị trí, nơi dữ liệu sống trong cluster.

Swift cung cấp các nhóm tên miền không gian trong tài khoản như container.

Swift sử dụng các nhóm server để lưu trữ dữ liệu tĩnh, chẳng hạn như tài liệu, hình ảnh hình ảnh,
trên cơ sở lâu dài. Hệ thống hoạt động bằng cách sử dụng một thuật toán băm để cung cấp một định
danh duy nhất cho mỗi đối tượng hoặc tập tin, được lưu trữ trên một node / server dữ liệu. Việc bổ 
sung các node / server mới cho phép các hệ thống mở rộng theo chiều ngang.

Siêu dữ liệu cho từng object thường trú trên tất cả các server trong cluster và phần mềm OpenStack 
đảm bảo sao chép dữ liệu. File yêu cầu đi tới Swift, Swift ủy quyền server, server dịch các yêu cầu,
xác định vị trí các đối tượng theo các thẻ băm và siêu dữ liệu của họ, sau đó lấy các đối tượng và 
các tập tin.

Administrators chỉ định một hoặc nhiều server tới một zone, và mỗi zone có một bản sao của mọi đối
tượng. Hệ thống yêu cầu tối thiểu là ba zone để đảm bảo một sự cân bằng tối ưu giữa hiệu quả chi phí
và phòng chống mất dữ liệu (theo Beth Cohen, một kiến trúc sư đám mây cao cấp tại Boston-Cloud Technology
Partners Inc (cloudTP))

* Proxy Servers
===============

Proxy Server là giao diện chung của Swift và xử lý các yêu cầu đến tất cả các API, có trách nhiệm 
liên kết các phần còn lại của kiến ​​trúc Swift. Với mỗi yêu cầu, nó sẽ tìm kiếm vị trí của account,
container, hoặc object trong Ring và định tuyến theo yêu cầu cho phù hợp. Các API công cộng cũng 
được tiếp xúc thông qua Proxy Server.

Khi một Proxy Server nhận được yêu cầu, nó sẽ xác định các nút lưu trữ dựa trên URL của đối tượng,
ví dụ như:

    https://swift.example.com/v1/account/container/object

Một số lượng lớn những failure cũng được xử lý trong các Proxy Server. Ví dụ, nếu một server là
không có sẵn cho một object PUT, nó sẽ yêu cầu Ring cho một handoff server (chuyển giao server khác)
và tuyến đường có thay thế.

Khi đối tượng được trực tiếp đến hoặc từ một object server thì sẽ được truyền trực tiếp thông qua 
proxy server.

Proxy Servers sử dụng một kiến ​​trúc được chia sẻ và có thể mở rộng khi cần thiết trên cơ sở khối 
lượng công việc dự kiến. Có ít nhất hai máy chủ Proxy cần được triển khai để dự phòng. Nếu một máy
chủ proxy thất bại, những máy khác sẽ giành quyền điều khiển.
