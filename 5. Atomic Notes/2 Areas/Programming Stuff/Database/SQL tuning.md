2025-09-11 21:38
Status: 
Topic: 
Tags: [[database]]
## Main

SQL Tuning (hay **tối ưu hóa câu lệnh SQL**) là quá trình phân tích và điều chỉnh câu truy vấn, cấu trúc dữ liệu và môi trường cơ sở dữ liệu để đảm bảo hệ thống chạy nhanh, ổn định và sử dụng tài nguyên hiệu quả.

## 1. Hiểu rõ bài toán

- Mục tiêu của câu SQL là gì? (truy xuất, tính toán, cập nhật…).
    
- Khối lượng dữ liệu hiện tại và dự kiến tương lai.
    
- Tần suất chạy truy vấn (1 lần/ngày hay hàng nghìn lần/giây).
    

---

## 2. Phân tích câu truy vấn

- **EXPLAIN / EXPLAIN ANALYZE (PostgreSQL)** hoặc **EXPLAIN PLAN (Oracle/MySQL)** để xem cách DB Engine thực thi.
    
- Kiểm tra:
    
    - Full Table Scan có cần thiết không?
        
    - Có sử dụng Index không?
        
    - Join Method (Nested Loop, Hash Join, Merge Join).
        
    - Sort, Filter, Aggregation có chi phí lớn không?

## 3. Tối ưu hóa câu SQL

- **Viết lại câu truy vấn**: tránh lồng nhiều subquery phức tạp → thay bằng `JOIN` hoặc `WITH`.
    
- **Sử dụng Index đúng cách**:
    
    - `WHERE`, `JOIN`, `GROUP BY`, `ORDER BY` thường cần Index.
        
    - Cẩn thận với _function trên cột_ (ví dụ `WHERE YEAR(date_col) = 2025` sẽ bỏ qua index).
        
- **Giảm dữ liệu không cần thiết**:
    
    - Chỉ `SELECT` cột cần dùng.
        
    - Hạn chế `SELECT *`.
        
- **Sử dụng Partitioning** nếu bảng rất lớn.
    
- **Materialized View / Cache** nếu truy vấn lặp đi lặp lại.

### Using sargable queries

Một câu SQL được gọi là **SARGable** nếu trình tối ưu hóa có thể **sử dụng index** để lọc dữ liệu.

- “Search ARGument” nghĩa là điều kiện trong `WHERE` có thể dùng trực tiếp giá trị để tra cứu trong index.
    
- Ngược lại, **Non-SARGable** sẽ buộc DB phải **scan toàn bộ bảng** hoặc toàn bộ index.

#### ❌ Non-SARGable

`SELECT *  FROM orders WHERE YEAR(order_date) = 2025;`

- Vì có `YEAR(order_date)`, index trên `order_date` sẽ **không được dùng**.
    

#### ✅ SARGable

`SELECT *  FROM orders WHERE order_date >= '2025-01-01'   AND order_date <  '2026-01-01';`

- DB engine có thể **seek theo index** trên `order_date`.




## 4. Tối ưu hóa cấu trúc dữ liệu

- Chuẩn hóa dữ liệu hợp lý để giảm trùng lặp.
    
- Index:
    
    - B-Tree Index: cho tìm kiếm chính xác.
        
    - Hash Index: cho so sánh bằng.
        
    - Bitmap Index (Oracle): cho dữ liệu ít giá trị.
        
    - Full-text Index: cho tìm kiếm văn bản.
        
- Thêm **covering index** để truy vấn không cần quay lại bảng gốc.



## 5. Tối ưu hóa môi trường DB

- **Memory parameters**:
    
    - MySQL: `innodb_buffer_pool_size`, `query_cache_size`.
        
    - PostgreSQL: `work_mem`, `shared_buffers`.
        
- **Parallel query** (Postgres, Oracle, SQL Server).
    
- **Statistics**: cập nhật để optimizer đưa ra plan chính xác (`ANALYZE` / `DBMS_STATS`).
    
- **Connection pooling** để giảm overhead kết nối.

## 6. Quy trình tuning thực tế

1. Xác định **truy vấn chậm** (dùng `slow_query_log` trong MySQL hoặc `pg_stat_statements` trong Postgres).
    
2. Phân tích Execution Plan.
    
3. Thử viết lại SQL, thêm/bỏ Index.
    
4. Đo lường thời gian và tài nguyên trước – sau.
    
5. Triển khai vào production.




## References