## Mới đầu ở TMS
- Học về Zk 
	- Ko có public API
	- Viết controller y hệt Java
	- Ngôn ngữ lạ, làm giao diện nhưng ko đẹp lắm, ko hữu dụng lắm
- Cài đặt setup môi trường
	- Proxy máy tính là gì? https://www.thegioididong.com/hoi-dap/proxy-la-gi-co-nhung-tinh-nang-gi-cach-cai-dat-proxy-tren-1306522#:~:text=Proxy%20%C4%91%C3%B3ng%20vai%20tr%C3%B2%20l%C3%A0,c%E1%BB%95ng%20truy%20c%E1%BA%ADp%20c%E1%BB%91%20%C4%91%E1%BB%8Bnh.
	- Dải 192.168.... https://viettuans.vn/192-168-1-1-la-gi
- Chạy maven + build với proxy. 
- Tìm hiểu về Procedure của Oracle
	- Lần đẩu tiên biết phải commit thì mới ăn Proc của Oracle
- 
## Sang BU lương ngày đầu
### Tìm hiểu hệ thống lương
### Làm con lương khối cơ quan

### Làm các chỉ tiêu tự động
- Khấu trừ 1381
	- DCN: Dynamic circuit network: https://en.wikipedia.org/wiki/Dynamic_circuit_network
	- HA Proxy: https://www.digitalocean.com/community/tutorials/an-introduction-to-haproxy-and-load-balancing-concepts
	- Telnet: https://www.totolink.vn/article/135-telnet-la-gi-tim-hieu-ve-giao-thuc-telnet.html
	- traceroute: https://viblo.asia/p/tim-hieu-lenh-ping-traceroute-trong-network-AZoJj0dOVY7
	- 
- Phụ cấp trưởng bưu cục
	- Test tải bằng Jmeter
	- Quét ZAP xem lỗ hổng bảo mật 
- Phụ cấp lễ bưu tá
	- Dual table: https://www.w3resource.com/sql/sql-dual-table.php
	- NGAY BETWEEN TO_DATE('01-JUL-23') AND TO_DATE('01-JUL-23') +1 -0.00001 => Query ngày theo kiểu này 
	    ```sql
	    select * from VTP.VTP_HOLIDAYS vh
		WHERE REGEXP_LIKE(vh.NGAY, '^[0-9]+$')
		AND vh.NAM = :year
		AND EXTRACT(MONTH FROM TO_DATE(NGAY, 'YYYYMMDD')) = :month
		
		SELECT *
FROM VTP_KETQUA_KHOAN
         INNER JOIN VTP.SUSERS su on VTP_KETQUA_KHOAN.TUYEN = su.USERID
WHERE LOAI = 'CHUYEN_CAN'
  AND NHOM_KHOAN = 2
  AND TYPE = 1
  AND NGAY IN (SELECT TO_DATE(NGAY
                          , 'YYYYMMDD')
               FROM VTP.VTP_HOLIDAYS vh
               WHERE REGEXP_LIKE(NGAY
                   , '^[0-9]$')
                 AND vh.NAM = : year
                 AND EXTRACT(MONTH FROM TO_DATE(NGAY
                   , 'YYYYMMDD')) = : month
                 AND EXTRACT(DAY FROM TO_DATE(NGAY
                   , 'YYYYMMDD')) between :startDay
                   and :endDay)
		```
- Lương công nợ
- Tỉ lệ giải quyết khiếu nại 
### Thành thục Jira, K8S, 1 loạt các yêu cầu về quy trình
## Tiếp nhận 1 loạt công việc
### Làm con 1919 - Tồn khai thác kết nối
- 
### Làm con lương khai thác tại Hub
- Apache Hive
- Hbase
- 
## Dự án tiêu biểu: Lương khoán Remake
