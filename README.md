# SQL injecttion là gì?  

SQL viết tắt của Structured Query Language, nó được sử dụng để truy vấn, thao tác dữ liệu trong Database. SQL Injection là kỹ thuật tấn công nhằm biến các điều kiện trong câu lệnh SQL (SQL Statement) là luôn luôn đúng. Là một kỹ thuật cho phép những kẻ tấn công lợi dụng lỗ hổng của việc kiểm tra dữ liệu đầu vào trong các ứng dụng web và các thông báo lỗi của hệ quản trị cơ sở dữ liệu trả về để inject (tiêm vào) và thi hành các câu lệnh SQL bất hợp pháp. SQL injection có thể cho phép những kẻ tấn công thực hiện các thao tác delete, insert, update,... trên cơ sở dữ liệu của ứng dụng, thậm chí là server mà ứng dụng đó đang chạy. SQL injection thường được biết đến như là một vật trung gian tấn công trên các ứng dụng web có dữ liệu được quản lý bằng các hệ quản trị cơ sở dữ liệu như SQL Server, MySQL, Oracle, DB2, Sysbase,...   

# Nguồn gốc của SQL injection.  

Công cụ thông dụng nhất được sử dụng để lưu trữ dữ liệu cho các ứng dụng là các cơ sở dữ liệu quan hệ dạng SQL. Vì nhiều lý do khác nhau, các ứng dụng thường xuyên sử dụng các cơ sở dữ liệu SQL để lưu trữ, truy xuất, thêm mới hay chỉnh sửa các dữ liệu cần thiết. Các ứng dụng web cũng không ngoại lệ.  

Lỗ hổng xuất phát từ việc các ứng dụng cho phép người dùng nhập truy xuất dữ liệu được lưu trữ bằng một truy vấn động do người dùng nhập vào. Điều này cho phép các truy vấn độc hại có thể được thực thi trong quá trình truy vấn dữ liệu. Hậu quả là kẻ tấn công có thể truy xuất dữ liệu lưu trữ trái phép, thay đổi, thêm mới hay xóa dữ liệu trong cơ sở dữ liệu một cách trái phép. Khi đó mối đe dọa về việc lộ các dữ liệu nhạy cảm, quan trọng như thông tin khách hàng, các loại dữ liệu cá nhân, bí mật kinh doanh, sở hữu trí tuệ, ... là rất lớn.  

# Cơ sở dữ liệu quan hệ.  

Để hiểu rõ về SQLi, trước tiên, chúng ta sẽ nêu lại một chút về cơ sở dữ liệu quan hệ. Các cơ sở dữ liệu quan hệ và hệ sinh thái hỗ trợ cho chúng - các hệ quản trị cơ sở dữ liệu quan hệ (Relational Database Management Systems - RDBMS) đang phát triển rất mạnh. Tuy rằng chúng ta chỉ nói đến SQL injection một cách tổng quát, nhưng trên thực tế có nhiều khía cạnh liên quan của SQLi phụ thuộc vào đặc tính của RDBMS được sử dụng (ví dụ như Oracle Database, MySQL, MS SQL server, PostgreSQL, ...).  

Chúng ta cần tìm hiểu thêm một chút về SQL. Những động từ sau đây là những động từ SQL phổ biến nhất và được hỗ trợ rộng rãi bởi các RDBMS:  

  - ``SELECT`` - truy vấn dữ liệu từ một bảng.  
  - ``INSERT`` - thêm dữ liệu vào bảng.  
  - ``UPDATE`` - chỉnh sửa dữ liệu đã có.  
  - ``DELETE`` - xóa dữ liệu trong một bảng.  
  - ``DROP`` - xóa một bảng.  
  - ``UNION`` - ghép dữ liệu từ nhiều truy vấn với nhau.  

Tiếp theo chúng ta sẽ xét tới những từ khóa dùng để tùy chỉnh truy vấn hay gặp nhất trong SQL:  

  - ``WHERE`` - bộ lọc SQL được sử dụng khi có điều kiện đi kèm.  
  - ``AND/OR`` - kết hợp với từ khóa WHERE để làm truy vấn cụ thể hơn.  
  - ``LIMIT #1, #2`` - Giới hạn lượng dữ liệu trả về #2 bắt đầu từ vị trí #1 (Ví dụ LIMIT 3,2; sẽ trả về 2 dòng dữ liệu thứ 4 và 5.).  
  - ``ORDER BY`` - sắp xếp dữ liệu theo cột.  

Từ khóa WHERE được sử dụng ở khắp mọi nơi. Trên thực tế, vị trí từ khóa WHERE chính là nơi mà chúng ta dễ dàng tìm ra SQL injection nhất, vì đó là nơi mà dữ liệu đầu vào được cung cấp và tìm kiếm.  

# Các ký tự đặc biệt trong SQL.  

Mỗi RDBMS có hệ thống các ký tự đặc biệt riêng cho các mục đích cụ thể. Tuy nhiên có những mục đích có thể có nhiều ký tự cùng được sử dụng.   

![image](https://user-images.githubusercontent.com/125866921/231044714-40f60ac9-3e39-40a7-b6e2-222248f04d0c.png)

# Tính nguy hiểm của tấn công SQL Injection.  

Tùy vào mức độ tinh vi, SQL Injection có thể cho phép kẻ tấn công:  

  - Vượt qua các khâu xác thực người dùng.  
  - Chèn, xóa hoặc sửa đổi dữ liệu.  
  - Đánh cắp các thông tin trong CSDL.  
  - Chiếm quyền điều khiển hệ thống.  

# Phân loại các kiểu tấn công SQL Injection.  

![image](https://user-images.githubusercontent.com/125866921/231045452-51562c8a-9c11-4fd6-9ea1-4b00f40dce56.png)

 SQL Injection có thể chia nhỏ thành các dạng sau.  
 
  - In-band SQLi  
  --  Error-based SQLi
