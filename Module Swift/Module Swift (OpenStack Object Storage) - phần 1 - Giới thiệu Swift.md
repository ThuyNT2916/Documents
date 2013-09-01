1.Giới thiệu Swift
==================
  Swift là mã nguồn mở phát hành theo giấy phép Apache 2.0. Swift để sao lưu web, nội dung di động
và bất kỳ dữ liệu phi cấu trúc khác, có thể phát triển mà không bị ràng buộc.

  Swift: đa người dùng (multi-tenant) có khả năng mở rộng cao, hệ thống lưu trữ dự phòng đối tượng
bền vững đã được thiết kế để lưu trữ một lượng lớn dữ liệu phi cấu trúc với chi phí thấp thông qua
một http RESTful API. "Khả năng mở rộng cao" có nghĩa là nó có thể mở rộng đến hàng ngàn máy với 
hàng chục ngàn của ổ đĩa cứng. Swift được thiết kế có khả năng mở rộng theo chiều ngang. Swift là 
lý tưởng để lưu trữ và phục vụ cho nhiều người, nhiều người sử dụng đồng thời - một đặc điểm phân 
biệt nó với các hệ thống lưu trữ khác.

"Dự phòng" có nghĩa là swift lưu trữ nhiều bản sao của mỗi thực thể trong hệ thống. Mỗi bản sao 
được lưu trữ sẵn trong khu vực vật lý riêng biệt, những thất bại phổ biến như các vấn đề về ổ cứng,
mạng không gây khó khăn, không gây mất dữ liệu hoặc thời gian chết.

"Lưu trữ dữ liệu phi cấu trúc" có nghĩa là Swift lưu trữ theo các bits. Swift không phải là một cơ
sở dữ liệu, không phải là một hệ thống lưu trữ khối cấp, Swift lưu trữ blobs (Binary large Object) 
của dữ liệu. 

Ngoài ra, vì Swift đảm bảo rằng các object sẽ có sẵn dữ liệu ngay khi chúng được ghi thành công, nên
Swift có thể được sử dụng để lưu trữ các nội dung thay đổi thường xuyên. Để thích ứng với những nhu
cầu thay đổi, hệ thống lưu trữ phải có khả năng để xử lý khối lượng công việc quy mô web với đồng 
thời nhiều reader và writer để lưu trữ dữ liệu. Một số dữ liệu thường viết ra và tìm kiếm, chẳng hạn
như: các tập tin cơ sở dữ liệu và hình ảnh máy ảo, dữ liệu khác như: văn bản, hình ảnh, tài liệu (và
sao lưu thường được ghi một lần và hiếm khi truy cập). Web và các dữ liệu di động cũng cần phải được
truy cập qua web thông qua một URL để hỗ trợ web / ứng dụng di động.

Sự khác biệt Swift với nhiều hệ thống lưu trữ khác là nó có nguồn gốc trong một môi trường sản xuất
quy mô lớn, có nghĩa là nó được thiết kế để chịu được các lỗi phần cứng mà không cần bất kỳ thời 
gian chết và cung cấp các nhóm hoạt động các phương tiện để duy trì, nâng cấp và tăng cường một 
cluster. Swift có quy mô tuyến tính để hoạt động có thể thêm dung lượng lưu trữ khi cần thiết mà 
không cần lo lắng về chi phí. 
