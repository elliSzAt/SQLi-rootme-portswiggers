![image](https://user-images.githubusercontent.com/125866921/234199088-c719c73b-1bcd-46b2-8bc5-c3024702f995.png)

  - Ở lab này ta tiếp tục tìm tài khoản ``administrator`` để đăng nhập và hoàn thành lab.  

![image](https://user-images.githubusercontent.com/125866921/234201416-21aaa4ec-c468-4684-9843-733fb02bcb6d.png)

  - Proxy trang web lên burpsuite, ta tiếp tục inject vào phần ``TrackingID``.  

        '%3BSELECT+CASE+WHEN+(1=1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END--  
        '%3BSELECT+CASE+WHEN+(1=2)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END-- 
        
  - Với câu lệnh truy vấn trên, nếu điều kiện đúng thì sẽ trả về ``pg_sleep(10)`` được thực thi, nếu điều kiện đúng thì trả về ``pg_sleep(0)``.  
  - Sau khi thử trên burpsuite thì ta nhận thấy thấy rằng khi điều kiện đúng thì kết quả trả về sẽ có độ trễ nhất định, còn nếu điều kiện sai thì kết quả trả về sẽ không có độ trễ.  
  - Do đó ta có thể lợi dụng việc này để khai thác những trường hợp liên quan đến tài khoản của ``administrator`` và căn cứ vào độ trễ để xác định.  

![image](https://user-images.githubusercontent.com/125866921/234205039-1dece90b-e6e0-4aa5-b2a1-9960f70f1514.png)

  - Ta sử dụng câu lệnh truy vấn sau để xem xét liệu rằng có username nào là ``administrator`` không.  

        '%3BSELECT+CASE+WHEN+(username='administrator'+AND+LENGTH(password)>1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--  
        
  - Nếu có tồn tại username nào là ``administrator`` và độ dài của chuỗi password > 1 thì khi đó, kết quả trả về sẽ có độ trễ.
  - Nếu 1 trong 2 điều kiện không đúng thì kết quả trả về sẽ không có độ trễ, do đó ta đã biết được rằng username là ``administrator`` và độ dài của chuỗi password phải lớn hơn 1.  
  - Ta tiếp tục thử đển khi giá trị độ dài của chuỗi password ``> 20`` thì khi đó kết quả trả về sẽ không có độ trễ. Do đó ta có thể suy ra được độ dài của chuỗi bao gồm 20 kí tự.  

![image](https://user-images.githubusercontent.com/125866921/234206525-a0c03f2d-1eb8-4774-b437-a73b08dc86a4.png)

  - Tiếp theo ta ``send to intruder`` và thêm kí tự $ vào kí tự a, sửa lại câu 1 chút ở câu truy vấn. 

        '%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,1,1)='§a§')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
        
  - Với câu lệnh này ta sẽ đi bruteforce từng kí từ trong chuỗi password.  
  - ở phần ``payloads`` ta chọn ``Bruteforcer`` và ``Minlength``, ``Maxlength`` có giá trị bằng 1. Tiến hành attack.

![image](https://user-images.githubusercontent.com/125866921/234208027-c3b3d48a-b9ed-464d-9840-401fe6291763.png)

  - Ta thấy rằng kí tự ``c`` này chưa trả ngay lập tức mà có độ trễ. Do đó đây chính là kí tự đầu tiên trong chuỗi password.  
  - Tiếp theo ta chỉ cần thay đổi vị trí của kí tự trong chuỗi password và attack, đến khi nào có đủ 20 kí tự thì ta sẽ đăng nhập vào và hoàn thành lab.
