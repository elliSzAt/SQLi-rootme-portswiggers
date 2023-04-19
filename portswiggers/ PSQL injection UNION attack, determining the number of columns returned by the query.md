![image](https://user-images.githubusercontent.com/125866921/231243908-d8f33cb4-5074-434f-bbd5-319e77bc5fab.png)

  - Ta tiếp tục thử những kiến thức như ở lv1 là list ra các sản phẩm mà cửa hàng đã ẩn.  
  - Nhưng có vẻ chả có gì đặc biệt cả, nên ta sẽ thử cái khác.  
  - Cùng xem thử ở lab này sẽ có bao nhiêu cột, ta sẽ kiểm tra bằng lệnh truy vấn sau:  

        ' UNION SELECT NULL --  
        ' UNION SELECT NULL, NULL --  
        ' UNION SELECT NULL, NULL, NULL --  
        
  - Do không biết rõ là có bao nhiêu cột nên ta phải thử từng cái.  
 
![image](https://user-images.githubusercontent.com/125866921/231245400-5197afe1-ecc9-470c-b4dc-a76d6ac27bf4.png)

Và với câu lệnh truy vấn ``' UNION SELECT NULL, NULL, NULL --``. Ta đã hoàn thành lab.  
