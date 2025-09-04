2024-12-01 21:24
Status: #baby
Tags: [[big data]] 
## Main

- Là gì?
	- Là một hệ thống kho dữ liệu mã nguồn mở được xây dựng trên nền tảng Hadoop.
	- Cung cấp 
		- 1 cơ sở dữ liệu
		- 1 ngôn ngữ truy vấn HiveQL
	- Tương thích tốt với các thành phần trong hệ sinh thái Hadoop (HBase, Spark, Pig)

- Truy vấn như thế nào vs HiveQL?
	- Thay vì truy vấn theo kiểu Map-Reduce -> Truy vấn theo SQL-style 
	- Cú pháp: 
		- Nhận xét: Tương đối giống vs query sql bình thường
			- Create giống 
			- Insert giống
			- Select giống
			- Update giống
			- Delete giống
		- Khác biệt khi truy vấn với dữ liệu bán cấu trúc và phi cấu trúc
		  
Vd: **Dữ liệu đầu vào (JSON):**

Vs Native SQL: 

```sql
-- Tạo bảng "products" và thêm dữ liệu vào chúng 
CREATE TABLE products ( product_id INT PRIMARY KEY, product_name TEXT, description TEXT, price FLOAT, tags TEXT[] ); -- Trích xuất dữ liệu từ JSON và chèn vào bảng "products" 
INSERT INTO products (product_id, product_name, description, price, tags) VALUES (1, 'Laptop', 'A powerful laptop with a high-resolution display.', 1000.0, ARRAY['electronics', 'computing']); 
-- Truy vấn thông tin về sản phẩm và mô tả 
SELECT product_name, description FROM products;
```
Vs Hive: 

```sql
-- Tạo một bảng ảo với cấu trúc JSON 
CREATE EXTERNAL TABLE products_json ( product_id INT, product_name STRING, description STRING, price FLOAT, tags ARRAY<STRING> ) 
ROW FORMAT SERDE 'org.apache.hive.hcatalog.data.JsonSerDe' 
LOCATION '/path/to/json/files'; 
-- Truy vấn thông tin về sản phẩm và mô tả trực tiếp từ JSON 
SELECT product_name, description FROM products_json;
```

	- Một số function của các DBMS sẽ không có trên HiveQL 
	- Cung cấp: 
		- **Hive Command Line** -> chạy HQL commands
		- **JDBC/ODBC driver** -> Kết nối vs db bên ngoài. 

- Ưu điểm so với SQL
	- Xử lý được lượng dự liệu lớn (do khả năng phân tán và chia nhỏ công việc có được từ cụm Hadoop)
	- Schema on Read: Đọc được dữ liệu mà ko cần định nghĩa cấu trúc -> tốt cho khi làm việc với dữ liệu bán cấu trúc và phi cấu trúc 
	- Rất quen thuộc vs người dùng SQL truyền thống do sử dụng SQL-like query.
	- Cộng đồng support oke. 
- Nhược điểm
	- Tốc độ truy vấn có thể trễ hơn so với SQL native với những câu query phức tạp.
	- Ko phải lựa chọn tốt cho những ứng dụng cần khả năng xử lý thời gian thực hay các dữ liệu cần tương tác nhanh
	- Phụ thuộc vào cách thức xử lý của Hadoop -> debug khó khăn hơn và logic phức tạp hơn
	- Khó sử dụng cho người mới. 
- Cách kết nối? 
	- 2 cách
		- CLI -> bỏ
		- JDBC -> giống hệt các connect vs các datasouce khác. 
			- Mẫu: 

```sql
Class.forName("org.apache.hive.jdbc.HiveDriver"); 
Connection connection = DriverManager.getConnection("jdbc:hive2://<HIVE_SERVER>:<PORT>/default", "<USERNAME>", "<PASSWORD>"); 
Statement statement = connection.createStatement(); 
ResultSet resultSet = statement.executeQuery("SELECT * FROM your_table"); 
while (resultSet.next()) { // Process the query results here } 
resultSet.close(); 
statement.close(); 
connection.close();
```

- Một số khái niệm:
	- Internal table:   
Khi người dùng tạo một bảng trong Hive, theo mặc định, một bảng nội bộ được tạo trong thư mục **/user/Hive/warehouse** trong HDFS, đây là vị trí lưu trữ mặc định của nó. Dữ liệu có trong bảng nội bộ sẽ được lưu trữ trong thư mục này và được Hive quản lý hoàn toàn và do đó bảng nội bộ còn được gọi là bảng được quản lý.
	- Create: 
```sql
create Table orders_demo (
        order_id INT,
        order_date DATE,
        order_cust_id INT,
        order_status VARCHAR(30)
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    STORED AS TEXTFILE;
```
External table:
	  Khi người dùng tạo bảng trong Hive chỉ định từ khóa **External** thì bảng bên ngoài sẽ được tạo. Dữ liệu có trong bảng bên ngoài sẽ được HDFS quản lý hoàn toàn trái ngược với bảng nội bộ
	  
```sql
CREATE EXTERNAL TABLE deck_of_cards_external (
        color string,
        suit string,
        pip string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '|'
    STORED AS TEXTFILE
    LOCATION '/user/root/cards';
```
## References


