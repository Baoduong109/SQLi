### Inferential SQLi (Blind SQL Injection)
* **Blind-boolean-based SQLi** là kĩ thuật tấn công SQL Injection dựa vào việc gửi các truy vấn tới cơ sở dữ liệu bắt buộc ứng dụng trả về các kết quả khác nhau phụ thuộc vào câu truy vấn là True hay False.

**Payload:** ```' AND 1=1--```, ```' AND 1=2--      ```

**Hành động:** Chèn và so sánh trạng thái HTTP (ví dụ: 200 so với 404), độ dài nội dung hoặc văn bản trang trong Burp.

**Mong đợi:** Phản hồi khác nhau mà không có dữ liệu đầu ra (ví dụ: "Đăng nhập thành công" so với "Thông tin đăng nhập không hợp lệ").

**Mục tiêu:** Khai thác dữ liệu từ database ngay cả khi ứng dụng không hiển thị lỗi hoặc kết quả truy vấn trực tiếp.


<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/14831188-857f-4a87-a818-ac7d4d472d7d" />
</p>

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/3622cd94-32c2-4dce-9767-64097b3835e8" />
</p>

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/15bb0ede-2c4d-4e1f-be18-b26084cf1a60" />
</p>



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

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/6cb3e73b-6389-49a6-9795-ed7bcbd06d94" />
</p>

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/21be7669-5ad2-4905-ad22-469a70c8c6af" />
</p>

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/6dcbd57f-fd38-4330-8849-88b5c634e400" />
</p>

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/00b71f0a-22e1-430a-88d0-5b70e2bce8ce" />
</p>


<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/4caa0229-0f58-423d-b763-d9deccb30669" />
</p>
