### Inferential SQLi (Blind SQL Injection)
* **Blind-boolean-based SQLi** là kĩ thuật tấn công SQL Injection dựa vào việc gửi các truy vấn tới cơ sở dữ liệu bắt buộc ứng dụng trả về các kết quả khác nhau phụ thuộc vào câu truy vấn là True hay False.

**Payload:** ```' AND 1=1--```, ```' AND 1=2--      ```

**Hành động:** Chèn và so sánh trạng thái HTTP (ví dụ: 200 so với 404), độ dài nội dung hoặc văn bản trang trong Burp.

**Mong đợi:** Phản hồi khác nhau mà không có dữ liệu đầu ra (ví dụ: "Đăng nhập thành công" so với "Thông tin đăng nhập không hợp lệ").

**Mục tiêu:** Khai thác dữ liệu từ database ngay cả khi ứng dụng không hiển thị lỗi hoặc kết quả truy vấn trực tiếp.


* **Time-based Blind SQLi** là kĩ thuật tấn công dựa vào việc gửi những câu truy vấn tới cơ sở dữ liệu và buộc cơ sở dữ liệu phải chờ một khoảng thời gian (thường tính bằng giây) trước khi phản hồi.



**Payload:**
``` 
Oracle: 
'; BEGIN DBMS_LOCK.SLEEP(5); END;--

MySQL: 
'; SELECT SLEEP(5)--

MSSQL: 
'; WAITFOR DELAY '0:0:5'--

PostgreSQL: 
'; SELECT pg_sleep(5)--
```
**Hành động:**  Kiểm tra tất cả các trường, đo thời gian phản hồi.

**Mong đợi:** Độ trễ 5 giây cho biết đây là Blind SQL Injection

**Mục tiêu:** Phát hiện các lỗ hổng mà không có đầu ra hiển thị.
