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

