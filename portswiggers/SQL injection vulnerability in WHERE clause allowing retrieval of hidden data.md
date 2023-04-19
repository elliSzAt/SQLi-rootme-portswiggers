![image](https://user-images.githubusercontent.com/125866921/231197688-cfac952a-0c37-490c-8628-0716d69c09ea.png)

  - Bước vào lab đầu tiên ta thấy được đây là giao diện của 1 trang web bán hàng.  
  - Có các mục cho mình lựa chọn như là ``Lifestyle``, ``Techgift``...  
  - Nhưng theo tên của lab lần này thì mình nghĩ đây không phải là toàn bộ sản phẩm của cửa hàng, do đó mình cần làm gì đó cho nó hiện toàn bộ sản phẩm kể cả những thứ chưa phát hành ra.  
  - Thử chọn vào phần ``Techgift`` và ta thấy được trên URL đã xuất hiện tham số ``category``.  

![image](https://user-images.githubusercontent.com/125866921/231200027-944766e8-a53e-4eeb-ac85-a0e23e6abaf5.png)

  - Sau khi sửa đổi 1 tí ở phần tham số ``category`` thì ta có thể dễ dàng thấy được những thay đổi trên URL ảnh hưởng thế nào đến SQL.  
  - Do đó ta sẽ thực hiện 1 cuộc tấn công SQLi nhằm mục dích tìm ra các phần đã bị ẩn đi.  
  - Ta sẽ có 1 lệnh như sau:

        https://0a9b0079041129288273257600980015.web-security-academy.net/filter?category=ThanhTrongdeptrai' or 1=1 --  
        
![image](https://user-images.githubusercontent.com/125866921/231201004-474d82cd-0e72-4124-a9d6-323b78a9f302.png)

