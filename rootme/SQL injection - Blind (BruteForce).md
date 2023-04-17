![image](https://user-images.githubusercontent.com/125866921/232487577-6a48c1a6-a9ed-4a3e-9a43-b3ea0a78daa1.png)

  - Bước vào challenge ta thấy có 1 form login.  
  - Ta thử với ``login:admin`` và ``password:admin``. Nó trả về là không tìm thấy cái tài khoản mà mình đăng nhập.  

![image](https://user-images.githubusercontent.com/125866921/232492564-7ef2fe26-4d97-4330-b287-ca158426371c.png)

  - Proxy trang web lên burpsuite.  
  - Sau đó ta kiểm tra xem có bao nhiêu cột bằng lệnh ``order by`` và biết rằng có 2 cột tồn tại.  

![image](https://user-images.githubusercontent.com/125866921/232492925-4fa1683c-cde0-4d7b-beb9-23982edec7d3.png)

  - Sau khi biết được nó có 2 cột.  
  - Ta tiếp tục sử dụng câu lệnh truy vấn sau: ``AND SUBSTR((select password from users where username='admin'),1,1)>'a' -- -``.  

      - Hàm ``SUBSTR()`` được sử dụng để trích xuất một phần của một chuỗi.  
      - Trong trường hợp này sử dụng hàm ``SUBSTR()`` để lấy ký tự đầu tiên của trường ``password`` từ bảng ``users`` trong cơ sở dữ liệu.  
      - Sau đó, ký tự đầu tiên này được so sánh với chữ cái ``a`` bằng cách sử dụng toán tử so sánh ``>``.  

![image](https://user-images.githubusercontent.com/125866921/232494167-7817785c-8916-46f9-b8e7-02b08810fa0d.png)

  - Tiếp tục ta ``Send to Intruder``.  
  - Clear toàn bộ kí tự ``$`` và thêm vào kí tự ``a`` như trên.  
  - Payload cần phải sửa lại 1 tí, ta thay đổi ``>`` bằng ``=``

![image](https://user-images.githubusercontent.com/125866921/232494528-0ec1d1e6-5365-4275-945e-1ee1ce6d6a50.png)

  - Ở phần ``payload type`` ta chọn ``BruteForce``.  
  - Sau đó cho giá trị của ``Min length`` và ``Maxlength`` bằng 1.  
  - Sau đó start attack.  

![image](https://user-images.githubusercontent.com/125866921/232496954-531828ae-a6ab-409d-91d0-02e4a229934e.png)

  - Ta thấy rằng giá trị của ``length`` thay đổi duy nhất ngay tại kí tự ``e``.  
  - Đó là kí tự đầu tiên trong trường ``password``.  

![image](https://user-images.githubusercontent.com/125866921/232495398-43de0157-8633-47ae-89d2-28a796431a94.png)

  - Tiếp theo ta quay về vị trí ``Positions`` và thay đổi vị trí của kí tự thành 2 và tiếp tục attack.  

![image](https://user-images.githubusercontent.com/125866921/232497172-17ff72e8-89fe-4f22-9ed8-fb80a4ddfc8d.png)

  - Kí tự tiếp theo là ``2``
  - Cứ tiếp tục cho đến khi ``length`` không thay đổi giá trị nữa.
  - Ta nhận được 1 chuỗi giả trị ``password`` như sau: ``e2azO93i``. Giờ thì đăng nhập và lấy flag thôi.  
