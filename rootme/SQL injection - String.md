![image](https://user-images.githubusercontent.com/125866921/232441462-7d9c9387-82d1-4cd3-a316-f24a5dc0a43a.png)

  - Khi vào challenge, ta đi đến phần search, tại đây có dấu hiệu có thể khai thác SQLi.  
  - Ta cùng thử với câu truy vấn sau ``1' order by``, khi tăng dần giá trị đến 3 thì xuất hiện lỗi.  

![image](https://user-images.githubusercontent.com/125866921/232443528-8ce5f37d-6d4c-418c-b4bd-2e472c738be1.png)

  - Sử dụng câu truy vấn ``union select 1,2 --``. Khi nhận kết quả trả về ta thấy có thể khai thác ở cả 2 cột.  
  - Tương tự như challenge **Numeric**, ta sử dụng câu truy vấn sau: ``union select username, password from users --``.

![image](https://user-images.githubusercontent.com/125866921/232444047-cf2f67d9-b8ff-4ecd-8000-feff557367fc.png)

  - Giờ chỉ việc đăng nhập và hoàn thành challenge thui.  
