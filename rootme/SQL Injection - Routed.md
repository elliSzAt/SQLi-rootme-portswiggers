![image](https://user-images.githubusercontent.com/125866921/232447295-5f10882b-f6bc-445b-8371-ce1e2fe061c2.png)

  - Ta vào form ``search`` của challenge, tại đây ta có thể thực hiện SQLi.
  - Sau 1 hồi thử các cách khác nhau thì có vẻ nó đã bị filter.  
  - Sau 1 hồi tham khảo SQli trên hacktrick mình đã tìm ra payload sau: ``-1' union select 0x2d312720756e696f6e2073656c656374206c6f67696e2c70617373776f72642066726f6d2075736572732d2d2061 -- a``

![image](https://user-images.githubusercontent.com/125866921/232447913-5540a49e-a4dd-4bf7-800e-398ee5511716.png)

  - Có 1 id là ``admin`` đã xuất hiện, và phần email cũng chính là flag.  
  - Challenge lần này bắt buộc chúng ta phải encode câu truy vấn của mình để bypass filter.  

![image](https://user-images.githubusercontent.com/125866921/232448444-e008d9b9-295d-4025-a976-315a795d2a61.png)

  - Payload khi được giải mã nó sẽ như thế này.  
