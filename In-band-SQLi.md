
### In-band SQLi (Classic SQL Injection)
* **Error-based SQLi** dựa vào thông báo lỗi được trả về từ Database Server có chứa thông tin về cấu trúc của cơ sở dữ liệu.

**Payload:** ```'```

**Hành động:** Đưa vào các tham số URL(```?id=1'```), dữ liệu POST, tiêu đề, cookie,...

**Mong đợi:** Thông báo lỗi (ví dụ: "SQL syntax error near '''", "unclosed quotation mark").

**Mục tiêu:** Xác nhận đầu vào ảnh hưởng đến câu truy vấn mà không được xử lý.

<p align="center">
<img width="801" alt="Ảnh chụp Màn hình 2025-03-31 lúc 15 12 58" src="https://github.com/user-attachments/assets/e4df8c7b-4bfb-4260-b90f-93620dec167c" />
</p>

> Lỗi hiển thị trong ảnh cho thấy ứng dụng đang sử dụng MySQL, vì thông báo lỗi thuộc cú pháp của MySQL. Lỗi xuất hiện do dấu ' dư thừa sau số 15324, cho thấy tham số id không được kiểm soát đúng cách. Điều này chứng tỏ ứng dụng không xử lý đúng đầu vào của người dùng, dẫn đến lỗi cú pháp SQL. Nếu dấu ' có thể gây ra lỗi, đây là dấu hiệu mạnh mẽ cho thấy ứng dụng có thể bị khai thác bằng Error-based SQL Injection, cho phép kẻ tấn công trích xuất thông tin từ cơ sở dữ liệu thông qua thông báo lỗi.

* **Union-based SQLi** dựa vào sức mạnh của toán tử UNION trong ngôn ngữ SQL cho phép tổng hợp kết quả của 2 hay nhiều câu truy vấn SELECTION trong cùng 1 kết quả và được trả về như một phần của HTTP response.

**Payload:** ```?id=1 ORDER BY 1--+```,```?id=1 ORDER BY 2--+```,```?id=1 ORDER BY 3--+``` tăng đến khi gặp lỗi, số cột hợp lệ là ```n-1```

**Hành động:** Xác định được số cột( giả sử dố cột hợp lệ là 3), kết hợp ```UNION``` để truy vấn dữ liệu mong muốn ```?id=-1 UNION SELECT 1,username,password FROM users--```

**Mong đợi:** Trả về các giá trị cột mong muốn có trong bảng truy vấn.

**Mục tiêu:** Xác nhận có thể sử dụng UNION để tác động ảnh hưởng đến câu truy vấn.
<p align="center">
<img width="1141" alt="Ảnh chụp Màn hình 2025-03-31 lúc 16 12 34" src="https://github.com/user-attachments/assets/31b09273-cbfa-4d61-875e-1a3dc397e9c1" />
</p>

> Câu truy vấn trên trả về tất cả nội dung có trong bảng news bao gồm id và content.

> Đặt giá trị id cho câu truy vấn là -1 hoặc bất kì giá trị nào khác không tồn tại trong CSDL. Tuy nhiên, giá trị âm là một phỏng đoán tốt vì một định danh trong cơ sở dữ liệu hiếm khi là số âm. Kết hợp toán tử ```UNION``` để có thể truy vấn giá trị cột từ các bảng khác.
<p align="center">
<img width="775" alt="Ảnh chụp Màn hình 2025-03-31 lúc 16 13 06" src="https://github.com/user-attachments/assets/bda9e10c-9e0c-409d-a3a7-e8972b1e98b5" />
</p>