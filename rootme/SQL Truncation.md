![image](https://user-images.githubusercontent.com/125866921/232430974-1edc8693-6cd9-4a70-902d-57c2912b3d48.png)

  - Bước vào chall thì ta thấy là có 1 form register và admin.  
  - Mình thử đăng kí 1 tài khoản với username là ``admin`` và password là ``123456789`` thì nhận lại được phản hồi như ảnh trên. Chứng tỏ đã có 1 tài khoản admin đã tạo từ trước.  

![image](https://user-images.githubusercontent.com/125866921/232431773-56ae6694-49e6-4df0-8106-b532d82f5fba.png)

  - Như đề bài đã nói đây là ``SQL truncation``, thì sau 1 hồi gu gồ thì mình đã biết nó là gì. Cùng tham khảo link sau nhé.  

      - https://resources.infosecinstitute.com/sql-truncation-attack/#gref

  - Truncation có nghĩa là cắt bớt, tức là ô input chỉ lấy 1 khoảng kí tự nào đó, như ở bài này là 12 kí tự.  
  - Giờ việc ta cần làm là ghi đè lên tài khoản admin ở phần ``register form``.

        login: admin       hihihihi
        password: hihihihi

  - Do login của mình đã vượt quá 12 kí tự, nên khi gửi về server thì nó sẽ tự động cắt bớt những phần sau đi và chỉ còn lại admin.  
  - Sau khi tạo xong tài khoản ở phần ``register`` thì ta chỉ việc nhập phần mật khẩu mà ta vừa tạo vào phần ``admin`` để lấy flag.  

![image](https://user-images.githubusercontent.com/125866921/232435397-dc4127f4-46f6-4a6b-853a-ee323bfe1ef3.png)
