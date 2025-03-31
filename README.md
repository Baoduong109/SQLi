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

Để thực hiện một cuộc tấn công SQL Injection, trước tiên kẻ tấn công phải tìm thấy dữ liệu đầu vào dễ bị tấn công của người dùng trong trang web hoặc ứng dụng web. Một trang web hoặc ứng dụng web có lỗ hổng SQL Injection sử dụng dữ liệu đầu vào của người dùng đó trực tiếp trong truy vấn SQL. Kẻ tấn công có thể tạo nội dung đầu vào. Nội dung đó thường được gọi là tải trọng độc hại và là phần chính của cuộc tấn công. Sau khi kẻ tấn công gửi nội dung này, các lệnh SQL độc hại sẽ được thực thi trong cơ sở dữ liệu.
## Tác động của một cuộc tấn công SQL Injection

Nhiều ứng dụng web và trang web lưu trữ tất cả dữ liệu trong cơ sở dữ liệu SQL. Trong một số trường hợp, có thể sử dụng lệnh SQL để chạy lệnh hệ điều hành. Do đó, một cuộc tấn công SQL Injection thành công có thể gây ra hậu quả rất nghiêm trọng.

Kẻ tấn công có thể sử dụng SQL Injection để tìm thông tin đăng nhập của người dùng khác trong cơ sở dữ liệu. Sau đó, chúng có thể mạo danh những người dùng này. Người dùng mạo danh có thể là quản trị viên cơ sở dữ liệu với tất cả các đặc quyền cơ sở dữ liệu.
SQL cho phép chọn và xuất dữ liệu từ cơ sở dữ liệu. Lỗ hổng SQL Injection có thể cho phép kẻ tấn công có quyền truy cập hoàn toàn vào tất cả dữ liệu trong máy chủ cơ sở dữ liệu.
SQL cũng cho phép thay đổi dữ liệu trong cơ sở dữ liệu và thêm dữ liệu mới. Ví dụ, trong ứng dụng tài chính, kẻ tấn công có thể sử dụng SQL Injection để thay đổi số dư, hủy giao dịch hoặc chuyển tiền vào tài khoản của họ.
Có thể sử dụng SQL để xóa bản ghi khỏi cơ sở dữ liệu, thậm chí xóa bảng. Ngay cả khi người quản trị thực hiện sao lưu cơ sở dữ liệu, việc xóa dữ liệu có thể ảnh hưởng đến tính khả dụng của ứng dụng cho đến khi cơ sở dữ liệu được khôi phục. Ngoài ra, bản sao lưu có thể không bao gồm dữ liệu gần đây nhất.
Trong một số máy chủ cơ sở dữ liệu, ta có thể truy cập hệ điều hành bằng máy chủ cơ sở dữ liệu. Điều này có thể là cố ý hoặc vô tình. Trong trường hợp như vậy, kẻ tấn công có thể sử dụng SQL Injection làm vectơ ban đầu và sau đó tấn công mạng nội bộ đằng sau tường lửa.

## Các loại SQLi
### In-band SQLi (Classic SQL Injection)
* ***Error-based SQLi*** dựa vào thông báo lỗi được trả về từ Database Server có chứa thông tin về cấu trúc của cơ sở dữ liệu.
![image](https://github.com/user-attachments/assets/fef6d346-ab24-4ba7-8182-5e908fb6ba82)

Lỗi hiển thị trong ảnh cho thấy ứng dụng đang sử dụng MySQL, vì thông báo lỗi thuộc cú pháp của MySQL. Lỗi xuất hiện do dấu ' dư thừa sau số 15324, cho thấy tham số id không được kiểm soát đúng cách. Điều này chứng tỏ ứng dụng không xử lý đúng đầu vào của người dùng, dẫn đến lỗi cú pháp SQL. Nếu dấu ' có thể gây ra lỗi, đây là dấu hiệu mạnh mẽ cho thấy ứng dụng có thể bị khai thác bằng Error-based SQL Injection, cho phép kẻ tấn công trích xuất thông tin từ cơ sở dữ liệu thông qua thông báo lỗi.
