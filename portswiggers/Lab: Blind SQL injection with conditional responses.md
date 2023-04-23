![image](https://user-images.githubusercontent.com/125866921/233824982-3d27fffb-e8e7-4a7b-9027-8ca761f18f2d.png)

  - Vào lab này nhiệm vụ của chúng ta vẫn tiếp tục là đăng nhập vào với vai trò là admin.  
  - Vào phần ``My Account`` ta thấy nó sẽ xuất hiện ``Welcome back!``. Chứng tỏ là đã từng đăng nhập trang web này.  

![image](https://user-images.githubusercontent.com/125866921/233825103-d5fb841a-4cf2-4ea7-9e6e-6707e9d8e8b2.png)

  - Proxy trang web lên burpsuite, ở đây ta có thể inject vào phần ``TrackingID``.
  - Ta cũng thử với câu lệnh ``' AND '1'='1``, chuỗi ``Welcome back!`` vẫn còn do điều kiện trả về luôn đúng.
  - Tiếp theo ta thử với ``' AND '1'='2`` thì chuỗi ``Welcome back!`` đã biến mất.  

![image](https://user-images.githubusercontent.com/125866921/233825202-b4a767fa-1a7b-40bd-ae63-caa866ffa0eb.png)

  - Tiếp theo ta dùng câu lệnh truy vấn ``' AND (SELECT 'a' FROM users LIMIT 1)='a``. Kết quả trả về xuất hiện ``Welcome back!``.  
  - Câu truy vấn này là một ví dụ của một chuỗi điều kiện trong câu truy vấn SQL. Điều kiện này sử dụng một truy vấn con để truy xuất giá trị đầu tiên của cột 'a' trong bảng 'users' và so sánh nó với giá trị 'a'. Nếu giá trị đó bằng 'a', điều kiện sẽ trả về giá trị True và chuỗi điều kiện này sẽ được coi là đúng.  

![image](https://user-images.githubusercontent.com/125866921/233825390-524b5017-96cc-4956-ace3-f789604797b4.png)

  - Tiếp theo ta sẽ kiểm tra xem có username nào là ``administrator`` trong bảng ``users`` hay không bằng câu lệnh ``' AND (SELECT 'a' FROM users WHERE username='administrator')='a``. Kết quả trả về vẫn xuất hiện ``Welcome back!`` chứng tỏ có 1 username như thế.  

![image](https://user-images.githubusercontent.com/125866921/233825507-83803418-5e23-44e4-8f9c-f349f52a242d.png)

  - Do ta biết được username, việc cần làm bây giờ là tìm ra password.  
  - Việc cần làm đầu tiên đó là check xem chuỗi password có bao nhiêu kí tự.
  - Với câu lệnh sau ``' AND (SELECT 'a' FROM users WHERE username='administrator' AND LENGTH(password)>1)='a``. Nếu độ dài của password lớn hơn 1 thì sẽ trả về kết quả đúng và chuỗi ``Welcome back!`` sẽ xuất hiện.  
  - Ta tiếp tục tăng độ dài so sánh của password lên đến khi lên đến giá trị 20 thì kết quả trả về sai. Do đó ta có thể suy ra chuỗi password này có 20 kí tự.  

![image](https://user-images.githubusercontent.com/125866921/233825727-f6b572a7-cba5-4e11-beab-668268d6db01.png)

  - Bước cuối cùng ta ``send to intruder``, sau đó clear hết tất cả các kí tự ``$`` và sửa câu truy vấn thành ``' AND (SELECT SUBSTRING(password,1,1) FROM users WHERE username='administrator')='§a§``.  
  - Qua phần payload ở đây ta chọn ``Brute forcer`` và ``Min length``, ``Max length`` có giả trị là 1.  
  - Ở phần setting (Grep - Match), ta clear toàn bộ và thêm chuỗi ``Welcome back!`` sau đó tiến hành tấn công và thu được password.  
  - Sau khi đã có được password ta chỉ cần đăng nhập vào và hoàn thành lab.  
