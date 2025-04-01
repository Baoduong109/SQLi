# Truy vấn SQL là gì?

SQL là ngôn ngữ truy vấn được thiết kế để quản lý dữ liệu được lưu trữ trong cơ sở dữ liệu quan hệ. Bạn có thể sử dụng nó để truy cập, sửa đổi và xóa dữ liệu. Truy vấn SQL thường là các lệnh yêu cầu một tập hợp kết quả cụ thể từ cơ sở dữ liệu bằng cách sử dụng ```SELECT``` câu lệnh, mặc dù cũng có các câu lệnh khác để thực hiện các hoạt động cơ sở dữ liệu, như ```UPDATE```, ```DELETE```, hoặc ```DROP```.

Các ứng dụng kết hợp dữ liệu đầu vào của người dùng vào các truy vấn SQL để lấy dữ liệu cần thiết từ cơ sở dữ liệu phụ trợ của chúng. Ở mức đơn giản nhất, một câu lệnh SELECT để kiểm tra thông tin đăng nhập của người dùng so với bảng users có thể là:
```SELECT id FROM users WHERE username='user-input-here' AND password='user-input-here'```
<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/541d0315-bcb1-43a6-be0e-7868d97bb4aa" />
</p>

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
[In-band SQLi](In-band-SQLi.md)

[Inferential SQLi](Inferential-SQLi.md)

[Out-of-band SQLi](Out-of-band-SQLi.md)

### Tấn công SQL injection được điều khiển bằng bot như thế nào?
Tấn công SQL injection có thể được tự động hóa bằng bot, điều này có thể mở rộng quy mô các cuộc tấn công và khiến chúng trở nên nguy hiểm hơn. Dưới đây là cách bot có thể điều khiển các cuộc tấn công SQL injection:

* Thực thi tấn công tự động: Bot có thể được lập trình để tự động gửi các payload SQL injection đến các ứng dụng web. Chúng có thể kiểm tra các trường đầu vào khác nhau và thử các loại tiêm khác nhau ở tốc độ cao, điều mà con người khó có thể thực hiện thủ công.
* Khả năng mở rộng: Bot có thể thực hiện hàng nghìn lần thử nghiệm SQL injection đồng thời trên nhiều trang web hoặc ứng dụng. Khả năng mở rộng này tăng khả năng tìm thấy lỗ hổng và khiến các tổ chức khó phòng thủ hơn trước các cuộc tấn công như vậy.
* Kỹ thuật nâng cao: Bot có thể sử dụng các kỹ thuật nâng cao để tránh bị phát hiện, chẳng hạn như xoay địa chỉ IP, sử dụng proxy và sử dụng mã hóa. Chúng cũng có thể sử dụng các payload SQL phức tạp để vượt qua các biện pháp bảo mật thông thường.
* Thu thập dữ liệu: Một khi bot thành công trong việc tiêm mã SQL độc hại, nó có thể tự động hóa quá trình trích xuất dữ liệu nhạy cảm từ cơ sở dữ liệu.
* Khai thác liên tục: Bot có thể liên tục thăm dò các lỗ hổng và khai thác chúng liên tục theo thời gian. Chúng cũng có thể thích nghi với những thay đổi trong cấu trúc hoặc biện pháp bảo mật của ứng dụng, khiến tấn công này trở thành mối đe dọa dai dẳng.

Để chống lại các cuộc tấn công SQL injection do bot điều khiển, hãy áp dụng giới hạn khối lượng (rate limit) yêu cầu (request) từ các IP đơn lẻ và chặn các IP độc hại. Ngoài ra, sử dụng các công cụ phát hiện bot như CAPTCHA và phân tích hành vi để xác định và giảm thiểu lưu lượng bot.

## Các biện pháp giảm thiểu SQL Injeciton

### 1. Parameterized Queries:

**Truy vấn:** ```String query = "SELECT * FROM users WHERE id='" + input + "'";```

Kẻ tấn công có thể truy xuất thông tin nhạy cảm như username và password bằng UNION-based SQLi làm rò rỉ dữ liệu, hoặc xóa, sửa dữ liệu nếu có quyền ghi. Ngoài ra, nếu database có quyền cao, hacker có thể tạo backdoor để chiếm quyền điều khiển hệ thống. Những rủi ro này có thể dẫn đến mất dữ liệu, mất quyền truy cập, và thậm chí là chiếm toàn bộ server. Để ngăn chặn, cần sử dụng Prepared Statements thay vì nối chuỗi trực tiếp trong truy vấn SQL.

**Biện pháp**
```
PreparedStatement stmt = conn.prepareStatement("SELECT * FROM users WHERE id=?");
stmt.setString(1, input);
ResultSet rs = stmt.executeQuery();   
```
Tách mã khỏi dữ liệu giúp ngăn chặn hoàn toàn SQL Injection vì dữ liệu nhập vào không được thực thi như mã SQL 

### 2. Input Validation:

Sử dụng whitelist [A-Za-z0-9] để chặn các kí tự đặc biệt như `'`, `--`, `;`, `UNION`.

**Ví dụ:**
```
if (!input.matches("[A-Za-z0-9]+"))
{ throw new IllegalArgumentException("Invalid input"); }   
```
Mục đíc ngăn chặn các kí tự độc hại chèn vào câu truy vấn.

### 3. Phân quyền:

Giới hạn người dùng DB chỉ sử dụng các thao tác CRUD; vô hiệu hóa xp_cmdshell (MSSQL), UTL_FILE (Oracle), COPY (PostgreSQL). 

**Ví dụ:** 
```
GRANT SELECT, INSERT ON app_db TO 'app_user';   
```

Giảm tác động nếu bị tấn công.

### 4. Web Application Firewall (WAF):

Chặn ```'```, ```UNION```, ```SELECT```, ```EXEC```, ```SLEEP```.

**Ví dụ cấu hình:**
```
ModSecurity rule SecRule ARGS "@contains UNION" "deny"
``` 

Loại bỏ các mẫu SQLi phổ biến.

### 5. Giới hạn quyền tệp tin:

Từ chối quyền ghi DB vào var/www, C:\; set secure_file_priv (MySQL).

Ngăn chặn RCE thông qua việc ghi tệp.

### 6. Audit Logs:

Bật ghi nhật ký DB (ví dụ: Oracle Audit Trail, MySQL General Query Log) giúp phát hiện các cuộc tấn công để phân tích sau sự cố. 
