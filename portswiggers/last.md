![image](https://user-images.githubusercontent.com/125866921/231441969-558c0a23-42fd-4ba9-a06f-8abb4cc0af5f.png)

  - Ta sẽ chiếu trang web lên burpsuite.  
  - Chọn phần ``View details`` sau đó ``check stock``.  

![image](https://user-images.githubusercontent.com/125866921/231442312-20e7542b-ccaf-41bc-aa6c-101eb7f84a36.png)

  - Thử 1 cuộc tấn công SQLi vào phần ``product ID`` và ``store ID``.  
  - Kết quả nó trả về là như nhau nhưng ở đây mình sẽ lấy phần ``storeID``.  

![image](https://user-images.githubusercontent.com/125866921/231443564-bda41978-62fe-4eea-a566-35d5059435dc.png)

  - Sử dụng phần ``extensions`` để encode câu lệnh truy vấn dưới dạng ``dec_entities``.  

![image](https://user-images.githubusercontent.com/125866921/231444453-963041d6-f32b-4ac3-9131-62d00d122ba6.png)

  - Quan sát thấy kết quả trả về là ``0 units``.
  - Ta thấy ở đây nó xuất hiện dấu hiệu của SQLi, mà ở đây thứ ta cần tìm là tài khoản để đăng nhập vào cửa hàng.
  - Như lab ở lv6, ở đây chúng ta sử dụng câu lệnh truy vấn như sau:  

        1 UNION SELECT username || '~' || password FROM users
        
![image](https://user-images.githubusercontent.com/125866921/231445167-cf910f6f-5b9a-4530-a09c-1b2151ff41ee.png)

  - Đã hiện ra 1 số tài khoản và trong đó có ``admin``.  
  - Giờ ta chỉ việc đăng nhập vào và hoàn thành lab thôi.  
