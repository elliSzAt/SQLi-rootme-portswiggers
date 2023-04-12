![image](https://user-images.githubusercontent.com/125866921/231358036-ce005a56-353b-479d-a3e9-d71fb31706f1.png)

  - Ở lab này cũng tưởng tự như ở lab lv7.  
  - Chỉ có điều là lần này chúng ta thực hành lab với ``Microsoft`` và ``MySQL``.  
  - Ta sử dụng câu lệnh truy vấn giống ở lab trước, nhưng có 1 xíu thay đổi:  

        ' UNION SELECT 'Trongdeptrai', 'sapcongiu' #
        
![image](https://user-images.githubusercontent.com/125866921/231359493-7060e875-ca07-43d5-a315-ea59e4b0c3d1.png)

  - Như này chứng tỏ mình đã đi đúng hướng.  
  - Giờ chỉ việc tìm trên ``SQL cheat sheet`` câu lệnh truy vấn nào hợp lí dễ gắn vào thôi.  
  - Ở đây mình có như sau:  

        'UNION SELECT @@version, NULL# 
        
![image](https://user-images.githubusercontent.com/125866921/231359915-1174d7b9-5fea-4786-ab7a-b2126cb343a1.png)
