3. Swift Architectural Overview (kiến trúc) - part 4
====================================================

* Accounts & Containers
=======================

Mỗi account và container là một cơ sở dữ liệu SQLite riêng lẻ được phân phối trên cluster. Một
account database có chứa danh sách các container trong account đó. Một cơ sở dữ liệu container
chứa danh sách các đối tượng trong container đó.

![ScreenShot](http://1.bp.blogspot.com/-BW2CnuPujEU/UiFsXEBf4qI/AAAAAAAAAdA/UvA9SzJ-6ew/s1600/adafaf.png)

Để theo dõi vị trí của dữ liệu object, mỗi account trong hệ thống có một cơ sở dữ liệu, cơ sở dữ 
iệu đó tham chiếu đến tất cả các container, và mỗi cơ sở dữ liệu container tham chiếu đến mỗi object

** Container Server
===================

Công việc chính Server container là để xử lý danh sách các đối tượng. Nó không biết về đối tượng,
mà chỉ cần biết các đối tượng đang trong một container cụ thể. Danh sách được lưu trữ như là các 
tập tin cơ sở dữ liệu SQLite, và nhân rộng trên các cluster giống như đối tượng đó như thế nào, 
luôn theo dõi thống kê tổng số các đối tượng, và tổng dung lượng sử dụng cho container đó.

SQLite là hệ thống cơ sở dữ liệu quan hệ nhỏ gọn, hoàn chỉnh, có thể cài đặt bên trong các trình 
ứng dụng khác. SQLite được Richard Hipp viết dưới dạng thư viện bằng ngôn ngữ lập trình C.

** Account Server
=================

Account Server tương đối giống với Server container, ngoại trừ, nó chịu trách nhiệm về các danh
sách các container chứ không phải là các đối tượng.
