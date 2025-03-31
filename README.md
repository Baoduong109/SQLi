# SQLi, XSS, Path Traversal....
Chia sẻ kiến thức về các kỹ thuật tấn công, các phương thức tấn công( tự động/thủ công ), dấu hiệu nhận biết, kỹ thuật phòng chống...
___
# Truy vấn SQL là gì?

SQL là ngôn ngữ truy vấn được thiết kế để quản lý dữ liệu được lưu trữ trong cơ sở dữ liệu quan hệ. Bạn có thể sử dụng nó để truy cập, sửa đổi và xóa dữ liệu. Truy vấn SQL thường là các lệnh yêu cầu một tập hợp kết quả cụ thể từ cơ sở dữ liệu bằng cách sử dụng ```SELECT``` câu lệnh, mặc dù cũng có các câu lệnh khác để thực hiện các hoạt động cơ sở dữ liệu, như ```UPDATE```, ```DELETE```, hoặc ```DROP```.

Các ứng dụng kết hợp dữ liệu đầu vào của người dùng vào các truy vấn SQL để lấy dữ liệu cần thiết từ cơ sở dữ liệu phụ trợ của chúng. Ở mức đơn giản nhất, một câu lệnh SELECT để kiểm tra thông tin đăng nhập của người dùng so với bảng users có thể là:
```SELECT id FROM users WHERE username='user-input-here' AND password='user-input-here'```

<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/541d0315-bcb1-43a6-be0e-7868d97bb4aa" />

Điều này sẽ trả về ID người dùng nếu tên người dùng và mật khẩu được chỉ định kết hợp tồn tại và NULL(kết quả trống) nếu không.
## SQLi là gì
SQL Injection (SQLi) là lỗ hổng bảo mật trong đó kẻ tấn công chèn mã SQL độc hại vào truy vấn cơ sở dữ liệu của ứng dụng thông qua dữ liệu đầu vào của người dùng chưa được kiểm tra (ví dụ: trường biểu mẫu, tham số URL), cho phép thao tác truy vấn trái phép.
