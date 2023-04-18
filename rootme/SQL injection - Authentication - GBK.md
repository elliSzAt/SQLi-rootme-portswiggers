![image](https://user-images.githubusercontent.com/125866921/232783982-6a446220-36bb-47bd-ad13-8a22a6b9ee3b.png)

  - Bước vào challenge thì có 1 form đăng nhập khá là bình thường và 1 list tài khoản thì có tài khoản admin trong đó, do đó có thể username ở challenge này là admin.  
  - Mình đã thử 1 vài câu lệnh cơ bản như ``admin ' --`` hay ``' or 1=1 --``.  Nhưng không có gì xảy ra.  

![image](https://user-images.githubusercontent.com/125866921/232784816-fd4c9bfe-b3b3-4b4c-a6ba-20ea9780cecf.png)

  - Proxy trang web lên burpsuite và thử lại các câu lệnh đó nhưng nó vẫn không có gì xảy ra.  
  - Thử lần lượt thay đổi phần login và password thành mảng.  

![image](https://user-images.githubusercontent.com/125866921/232785413-8b263e40-08a1-42e7-91c2-8496a5883a3f.png)

  - Nó trả về lỗi, ta có thể thấy được ở phần login đã qua xử lí bởi hàm ``addslashes()``, còn password thì bị xử lí bởi hàm băm ``md5``.  

      - Hàm ``addslashes()`` là một hàm trong PHP được sử dụng để thêm các ký tự gạch chéo vào trước các ký tự đặc biệt trong chuỗi, để tránh các lỗ hổng bảo mật và giúp chuỗi trở thành chuỗi an toàn khi sử dụng trong các câu lệnh SQL hoặc truy vấn đến cơ sở dữ liệu.  
      - Các ký tự đặc biệt bao gồm các ký tự như dấu nháy đơn ``'``, dấu nháy kép ``"``, dấu gạch chéo ngược ``\``,....  
      - Ví dụ, nếu chuỗi đầu vào là ``I'm a programmer``, hàm addslashes() sẽ thêm một ký tự gạch chéo vào trước dấu nháy đơn, trả về chuỗi ``I\'m a programmer``.  

  - Dấu ``\`` sau khi encode sẽ là %5c, ta cần thêm ở đây thêm 1 kí tự đặc biệt để khi kết hợp với ``%5c`` sẽ tạo thành 1 kí tự khác và không bị filter bới server.  
  - Ở dây mình ``%af``, sau khi nó kết hợp với ``%5c`` thì sẽ tạo ra 1 kí tự tiếng Trung gì gì đó.  

![image](https://user-images.githubusercontent.com/125866921/232788237-3734abac-e7c5-4c81-a74d-7174045c5e36.png)

  - Thử với payload sau: ``admin%af%27 or 1%3D1 --``.  
  - Sau đó Follow Rediction.  

![image](https://user-images.githubusercontent.com/125866921/232788416-9c5ca30e-b293-448f-bd53-34df0886d23a.png)
