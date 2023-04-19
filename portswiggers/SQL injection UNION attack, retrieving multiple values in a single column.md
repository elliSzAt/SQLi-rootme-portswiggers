![image](https://user-images.githubusercontent.com/125866921/231339951-333ab72b-fbe2-4ba0-a20b-c61f5ef35ba5.png)

  - Ta thấy trên URL đã xuất hiện tham số ``category``.  
  - Trong lab này, chúng ta sẽ thực hiện tấn công SQL injection UNION để lấy nhiều giá trị trong một cột đơn.  
  - Thử với câu lệnh truy vấn như ``' UNION SELECT NULL, NULL --``, ta thấy được đã xuất hiện lỗi truy vấn trả về.  
  - Thay giá trị ``NULL`` lần lượt bằng giá trị khác như ``Trongdeptrai``, ta thấy được rằng nó nằm ở cột thứ 2.  

![image](https://user-images.githubusercontent.com/125866921/231341104-9fdd1aff-1433-4172-a29f-177a7c0bc924.png)

  - Nhận ra rằng nó nằm ở cột thứ 2, ta tiếp tục thay đổi giá trị ``Trongdeptrai`` thành 1 lệnh truy vấn khác.  
  - Sau khi tìm hiểu từ nguồn ``https://portswigger.net/web-security/sql-injection/union-attacks``.  
  - Mình tìm ra câu lệnh truy vấn sau:  

        ' UNION SELECT username || '~' || password FROM users--  
        
![image](https://user-images.githubusercontent.com/125866921/231341486-693a91e3-88ee-4abf-8e01-6ac97d03a35b.png)

  - Câu lệnh trên truy vấn ``username`` và ``password`` từ bảng ``users``.  
  - chuỗi ký tự ``||`` được sử dụng để nối các giá trị tên đăng nhập và mật khẩu, và ký tự ``~`` được sử dụng để phân tách hai giá trị này.  

![image](https://user-images.githubusercontent.com/125866921/231342016-73ffda45-7bc6-4ac7-bc79-88b494c50832.png)

  - Đến đấy thì ta đã tìm được tài khoản của ``administrator``.  
  - Giờ chỉ việc đăng nhập vào thôi.  

![image](https://user-images.githubusercontent.com/125866921/231342189-dc9ba621-049d-4ab9-a656-232d2db69383.png)
