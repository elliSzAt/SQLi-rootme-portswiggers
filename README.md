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

    - Error-based SQLi  
    - Union-based SQLi

  - Inferential SQLi (Blind SQLi)
  - Blind-boolean-based SQLi 

    - Time-based-blind SQLi  

  - Out-of-band SQLi  

**In-band SQLi**

  - Đây là dạng tấn công phổ biến nhất và cũng dễ để khai thác lỗ hổng SQL Injection nhất.  
  - Xảy ra khi hacker có thể tổ chức tấn công và thu thập kết quả trực tiếp trên cùng một kênh liên lạc.  
  - In-Band SQLi chia làm 2 loại chính:  

    - Error-based SQLi.  
    - Union-based SQLi.  

*Error-based SQLi*  

  - Là một kỹ thuật tấn công SQL Injection dựa vào thông báo lỗi được trả về từ Database Server có chứa thông tin về cấu trúc của cơ sở dữ liệu.  
  - Trong một vài trường hợp, chỉ một mình Error-based là đủ cho hacker có thể liệt kê được các thuộc tính của cơ sở dữ liệu.  

*Union-based SQLi* 

  - Là một kỹ thuật tấn công SQL Injection dựa vào sức mạnh của toán tử UNION trong ngôn ngữ SQL cho phép tổng hợp kết quả của 2 hay nhiều câu truy vấn SELECTION trong cùng 1 kết quả và được trả về như một phần của HTTP response.  

**Inferential SQLi (Blind SQLi)**  

  - Không giống như In-band SQLi, Inferential SQL Injection tốn nhiều thời gian hơn cho việc tấn công do không có bất kì dữ liệu nào được thực sự trả về thông qua web application và hacker thì không thể theo dõi kết quả trực tiếp như kiểu tấn công In-band.
  - Thay vào đó, kẻ tấn công sẽ cố gắng xây dựng lại cấu trúc cơ sở dữ liệu bằng việc gửi đi các payloads, dựa vào kết quả phản hồi của web application và kết quả hành vi của database server.  
  - Có 2 dạng tấn công chính.  

    - Blind-boolean-based.  
    - Blind-time-based SQLi.  

*Blind-boolean-based*  

  - Là kĩ thuật tấn công SQL Injection dựa vào việc gửi các truy vấn tới cơ sở dữ liệu bắt buộc ứng dụng trả về các kết quả khác nhau phụ thuộc vào câu truy vấn là True hay False.  
  - Tuỳ thuộc kết quả trả về của câu truy vấn mà HTTP reponse có thể thay đổi, hoặc giữ nguyên.  
  - Kiểu tấn công này thường chậm (đặc biệt với cơ sở dữ liệu có kích thước lớn) do người tấn công cần phải liệt kê từng dữ liệu, hoặc mò từng kí tự.  

![image](https://user-images.githubusercontent.com/125866921/231047782-941b4a01-976a-4049-b1b7-afbdc9ef5d19.png)

*Time-based Blind SQLi*

  - Time-base Blind SQLi là kĩ thuật tấn công dựa vào việc gửi những câu truy vấn tới cơ sở dữ liệu và buộc cơ sở dữ liệu phải chờ một khoảng thời gian (thường tính bằng giây) trước khi phản hồi.  
  - Thời gian phản hồi (ngay lập tức hay trễ theo khoảng thời gian được set) cho phép kẻ tấn công suy đoán kết quả truy vấn là TRUE hay FALSE.  
  - Kiểu tấn công này cũng tốn nhiều thời gian tương tự như Boolean-based SQLi.  

**Out-of-band SQLi**  

  - Out-of-band SQLi không phải dạng tấn công phổ biến, chủ yếu bởi vì nó phụ thuộc vào các tính năng được bật trên Database Server được sở dụng bởi Web Application.  
  - Kiểu tấn công này xảy ra khi hacker không thể trực tiếp tấn công và thu thập kết quả trực tiếp trên cùng một kênh (In-band SQLi), và đặc biệt là việc phản hồi từ server là không ổn định.  
  - Kiểu tấn công này phụ thuộc vào khả năng server thực hiện các request DNS hoặc HTTP để chuyển dữ liệu cho kẻ tấn công.  
  - Ví dụ như câu lệnh xp_dirtree trên Microsoft SQL Server có thể sử dụng để thực hiện DNS request tới một server khác do kẻ tấn công kiểm soát, hoặc Oracle Database’s UTL HTTP Package có thể sử dụng để gửi HTTP request từ SQL và PL/SQL tới server do kẻ tấn công làm chủ.  

# SQL injecttion hoạt động như thế nào?  

Có nhiều kiểu tấn công bằng SQL Injection tuỳ thuộc vào Database Engine. Trước tiên mình sẽ giới thiệu về các thức tấn công thông qua Dynamic SQL Statement. Dynamic SQL Statement là câu lệnh SQL được tạo ra trong quá trình chạy chương trình với các parameters được truyền vào tự động thông qua một form của website. Bạn có thể xem một đoạn code đơn gian bằng PHP mô tả môt form đăng nhập hệ thống ở dưới đây:  

    <form action='signin.php' method="post">

        <input type="email" name="email" required="required"/>

        <input type="password" name="password"/>

        <input type="submit" value="Submit"/>

    </form>

Người dùng nhập vào địa chỉ Email, mật khẩu và submit lên signin.php. Giả sử trong file PHP signin.php xử lý logic như sau:  

    SELECT * FROM leo.users WHERE email = '$_POST['email']' AND password = 'md5($_POST['password'])';

Đoạn mã trên thực hiện việc truy vấn dữ liệu từ bảng users với điều kiện là emai và password là những giá trị nhập vào từ form phía trên. Nhập vào ô email với nội dụng: ``em@khongbiet.com’ OR 1 = 1 LIMIT 1 — ‘ ]``. Nhập vào ô password với nội dụng bất kỳ, sau đó click vào nut Login.  

Chúng ta đã đăng nhập thành công. Dù bạn không biết thông tin đăng nhập nhưng bạn cũng có thể dễ dàng vượt qua theo cách trên.  

Khi đăng nhập hệ thống, chương trình sẽ tự động tạo ra cậu lệnh truyên vấn dữ liệu với tham số được truyền vào từ form login.  

    SELECT * FROM leo.users WHERE email = $_POST['email'] AND password = md5($_POST['password']);

Với dữ liệu chúng ta vừa nhập, câu lệnh truy vấn sẽ là:  

    SELECT * FROM leo.users WHERE email = 'em@0biet.com' OR 1 = 1 LIMIT 1 -- ' ]' AND password = 'em_biet_tuot';

Sau ký tự ``-``, hệ thống sẽ hiểu đó là comment, chương trình sẽ không thực thi những gì phía sau nó. Câu truy vấn có thể rút gọn lại:  

    SELECT * FROM leo.users WHERE email = 'em@0biet.com' OR 1 = 1 LIMIT 1

Điều kiện của câu lệnh truy vấn: email = ``'em@0biet.com' OR 1 = 1``, nó luôn là true, đó là lý do vì sao chúng ta có thể vượt qua màn hình đăng nhập một cách dễ dàng.  

Đó là 1 trong những cách cơ bản nhất mà hacker có thể tận dụng để tấn công. Ngoài ra còn 1 số cách tấn khác như:  

  - Xoá dữ liệu.  
  - Cập nhật thay đổi dữ liệu.  
  - Thêm mới dữ liệu vào hệ thống.  
  - Thực hiện các commands trên server để tự động tải và cài đặt những phần mềm nguy hiểm hay virus.  
  - Lấy thông tin của khách hàng trên hệ thống như thông tin thẻ ngân hàng, thông tin đăng nhập.  

# Cách chống lại các cuộc tấn công SQL injection:  

Vậy để ngăn chặn hình thức tấn công SQL Injection chúng ta phải làm thế nào? Như mình đã nói ở trên, Hacker lợi dụng sự lỏng lẻo về thiết kế của chương trình để tấn công, chúng ta cần có các biện pháp ngăn ngừa:  

  - Dữ liệu nhập vào từ form giao diện người dùng phải được “làm sạch” (sanitized) trước khi đưa vào các logic code để tạo ra câu lệnh truy vấn. (Đối với PHP thì sử dụng 1 vài funtion để cắt hay xóa những ký tự đặc biệt hoặc thẻ tag).  
  - Prepared statements, đảm bảo dữ liệu đầu vào được lọc mà không ảnh hưởng đến cấu trúc của câu lệnh truy vấn.  
  - Phân quyền truy cập vào Database server với từng mức độ theo yêu cầu của từng chức năng.  
  - Khi có lỗi về việc truy cập, truy vấn database, hệ thống nên đưa ra thông báo chung như: “Sorry, we are experiencing technical errors. Please try again later”, thay vì hiển thị nội dung, lý do gây lỗi của quá trình thực thi câu lệnh truy vấn, Hacker sẽ dựa vào đây để phán đoán và tìm cách phá hoại.  

