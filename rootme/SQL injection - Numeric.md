![image](https://user-images.githubusercontent.com/125866921/232437195-85c0aa7a-6a14-4f1e-9c61-82e4855054be.png)

  - Khi vào challenge ta chọn phần ``News``, tại đây URL sẽ xuất hiện tham số và khi đó ta có thể thực hiện SQLi.  
  - Ta cùng thử vài câu truy vấn cơ bản như ``or 1=1 --``. Trang web vẫn hoạt động bình thường.  
  - Tiếp theo ta sử dụng ``order by``  và tăng dần giá trị, khi đạt giá trị 4 thì xuất hiện lỗi. Do đó ở challenge này chỉ có 3 cột.  

![image](https://user-images.githubusercontent.com/125866921/232437996-6df10464-7d20-4fd3-b8d2-2f55e2a65f6c.png)

  - Tiếp theo ta sử dụng câu truy vấn ``union select 1,2,3 --``, có thể thấy cột 1 đã bị ẩn đi. 
  - Do đó ta chỉ có thể khai thác SQLi lên cột 2 và 3.  
  - Do ở challenge lần này ta phải tìm được tài khoản admin và log vào để hoàn thành challenge, vì vậy cùng thử vài câu lệnh như sau: ``union select 1, username, password from users --``.  

![image](https://user-images.githubusercontent.com/125866921/232438596-d5c28eb1-5865-402e-ab9f-7828add59c10.png)

  - Tài khoản admin đã xuất hiện rồi, giờ chỉ việc log vào và hoàn thành challenge thôi. 
