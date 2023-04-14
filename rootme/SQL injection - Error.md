![image](https://user-images.githubusercontent.com/125866921/231938826-85a12e93-c220-4c1d-a25d-43d70e8defaa.png)

  - Ta thấy lỗi của bài này xuất hiện ở page ``Contents``. Khi ta thêm kí tự ``'`` vào cuối URL sẽ xuất hiện lỗi.  
  - Do đó ta có thể khai thác SQLi từ page này, sử dụng ``sqlmap`` với URL ta sử dụng ``-u``.  

        python3 sqlmap.py -u "http://challenge01.root-me.org/web-serveur/ch34/?action=contents&order=ASC" --dbs  
        
          - Trong ngoặc kép là phần URL cần được khai thác.  
          - ``--dbs`` là để lấy dữ liệu từ database.  

![image](https://user-images.githubusercontent.com/125866921/231939709-bbaea358-9c88-4e36-afb2-504615a433dc.png)

  - Kết quả trả về cho ta thấy được là ở bài này có 2 cách khai thác là ``blind`` và ``error``.  
  - Kết quả trả về cũng cho ta được 3 database, nhưng ở đây ta chỉ cần chú ý vào ``database public``.  
  - Ta thực hiện lấy các tables có trên database này:  

        python3 sqlmap.py -u "http://challenge01.root-me.org/web-serveur/ch34/?action=contents&order=ASC" -D public --tables
        
          - ``--tables`` được sử dụng để lấy các bảng.  
          - ``-D public`` dùng để lấy kết quả trong `database public``.  

![image](https://user-images.githubusercontent.com/125866921/231940117-c952c875-b154-4bdf-b669-4ec6d5e3093b.png)

  - Ta thấy có 1 bảng rất đáng nghi là ``m3mbr35t4bl3``. Vì thế ta sẽ thực hiện lấy dữ liệu của bảng đó.  

        python sqlmap.py -u "http://challenge01.root-me.org/web-serveur/ch34/?action=contents&order=ASC" -D public -T m3mbr35t4bl3 --dump  
        
          - ``-T`` là chỉ vào bảng cần lấy dữ liệu.  
          - ``--dump`` là lấy toàn bộ dữ liệu của bảng.  

![image](https://user-images.githubusercontent.com/125866921/231940471-103a7248-6c9c-4f2d-bf7c-98f11d646dee.png)

  - Kết quả trà về ta thấy có 1 tài khoản ``admin``.  
  - Mật khảu của tài khoản cũng chính là flag mà ta cần tìm.  
