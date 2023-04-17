![image](https://user-images.githubusercontent.com/125866921/232553495-7a172a31-a93e-49d7-abfa-ac2b1cfa6203.png)

  - Ở challenge này mình phải tìm được phần mật khẩu của admin.  
  - Mình đã thử 1 số cách cơ bản và nhận ra là ở challenge này đã filter ``order by`` và các kí tự như ``'`` chẳng hạn...

![image](https://user-images.githubusercontent.com/125866921/232557208-86b0efc6-ba46-4ddb-bd79-63c4c6e45fae.png)

  - Vì ``order by`` đã bị filter nên không thể kiểm tra xem có bao nhiêu cột bằng cách đó được.  
  - Nên ta sẽ dùng payload sau: ``%09UNION%09SELECT%09*%09FROM%09(SELECT%091)a1%09JOIN%09(SELECT%09pass%09FROM%09membres%09LIMIT%091)a2%09JOIN%09(SELECT%093)a3%09JOIN%09(SELECT%094)a4``

      - ``%09`` là white space.  
      - ``JOIN`` được sử dụng để kết nối các bảng.  
      - Do ``order by`` đã bị filter nên mình phải thử với ``UNION SELECT`` xem có bao nhiêu cột, và tất cả đều trả về ``no result`` chỉ có payload trên là thành công nên từ đó ta có thể biết có bao nhiêu cột.  

![image](https://user-images.githubusercontent.com/125866921/232559791-6151408c-74b5-4812-a5ec-689708236845.png)

  - Check phần source code ta thấy rằng, có 1 bảng ``membres`` và 3 trường lần lượt là ``username``, ``pass``, ``email``.  
  - Vì ta đã biết ``username`` và ``email`` của admin rồi nên chả cần quan tâm nó làm gì. Ta chỉ cần tìm pass là xong.  

![image](https://user-images.githubusercontent.com/125866921/232560566-6c0b78d7-9e6e-49d3-8736-eb80e8a33241.png)

  - Ta sử dụng payload sau: ``%09UNION%09SELECT%09*%09FROM%09(SELECT%091)a1%09JOIN%09(SELECT%09pass%09FROM%09membres%09LIMIT%091)a2%09JOIN%09(SELECT%093)a3%09JOIN%09(SELECT%094)a4``.

      - ``(SELECT pass FROM membres LIMIT 1) a2`` tạo một bảng tạm với một cột "pass" và một hàng, được đặt tên là "a2", và lấy giá trị trong cột "pass" của bảng "membres" để truyền vào.  
