**Như tiêu đề của lab này, đây là dạng tấn công SQL mà kết quả trả về có độ trễ. Từ đó ta có thêm thời gian để thực thi câu lệnh SQL để thực hiện các cuộc tấn công khác.**

![image](https://user-images.githubusercontent.com/125866921/233793806-a399df75-7ae6-42ed-8232-53bbb7ad2b70.png)

  - Mục tiêu đã rõ ràng, ở lab này ta cần tìm 1 câu lệnh truy vấn đối với **time delays** hợp lí.  

![image](https://user-images.githubusercontent.com/125866921/233793986-45af1e80-ea5b-48bb-b9e6-bf28626cd644.png)

  - Proxy trang web lên burpsuite, sau đó ta sẽ inject vào phần ``TrackingId``.  

        https://portswigger.net/web-security/sql-injection/cheat-sheet
        
  - Tham khảo SQLi cheat-sheet đối với time delays, ban đầu mình thử với ``SELECT SLEEP(10)`` nhưng kết quả trả về không có độ trễ.
  - Ban đầu mình nghĩ rằng do không đúng hệ quản trị CSDL, nên đã thử lần lượt 3 trường hợp còn lại. Nhưng kết quả trả về vẫn là không có độ trễ.  
  - Sau khi nhận ra đó không phải là 1 câu lệnh của SQLi thì mình đã thay thế nó bằng chuỗi ``'||pg_sleep(10)--``.  
  - Kết quả nó sẽ giống như này.  

        SELECT * FROM users WHERE username = '' ||pg_sleep(10)--' AND password = ''
        
  - Khi câu lệnh SQL này được thực thi, nó sẽ chờ đợi 10 giây trước khi trả về kết quả. Sau khi trả về kết quả thì ta cũng đã hoàn thành lab này.
