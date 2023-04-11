![image](https://user-images.githubusercontent.com/125866921/231247782-1a0b7110-b63c-4a01-b4f9-4e76296c049e.png)

  - Ở lab này ta cần phải tìm được tài khoản và mật khẩu qua các câu truy vấn.  
  - Đầu tiên ta phải xác định được sô1 lượng cột mà sau khi truy vấn trả về.  
        
        ' UNION SELECT 'Trongdeptrai', 'sapcongiu' --  
        
![image](https://user-images.githubusercontent.com/125866921/231248839-d1253372-490a-41c8-a6a6-cc2e8cd28509.png)

  - Ta thấy cửa hàng thả trả về 2 string mà ta đã nhập.  
  - Như trên lab đã gợi ý, có 2 cột là ``username`` và ``password`` được cất trong bảng ``users``.
  - Vì vậy ta cần sử dụng lệnh truy vấn để trả về tài khoản để login vào cửa hàng.  
  - Ở đây ta sẽ sử dụng lệnh truy vấn sau:

        ' UNION SELECT password, username FROM users --  
        
![image](https://user-images.githubusercontent.com/125866921/231250475-bb27d19b-c6d2-4444-99bc-dec9606d8faa.png)

  - Ta thấy rằng có 1 tài khoản là ``administrator`` đã hiện ra.  
  - Đó là tài khoản mà ta cần tìm, giờ thì chỉ việc đăng nhập vào thôi.  

![image](https://user-images.githubusercontent.com/125866921/231250982-571660e2-4e64-4f50-8d2f-fe3f3ac2e0b1.png)
