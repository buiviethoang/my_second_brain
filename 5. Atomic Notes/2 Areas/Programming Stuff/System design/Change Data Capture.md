2025-09-11 21:47
Status: 
Topic: 
Tags: [[microservices]] [[system design]]
## Main

CDC là một kỹ thuật trong hệ thống cơ sở dữ liệu/dữ liệu lớn để **theo dõi và ghi lại những thay đổi (INSERT, UPDATE, DELETE)** trong dữ liệu nguồn, sau đó **đẩy các thay đổi này** đến hệ thống đích (ví dụ: data warehouse, message queue, hay microservices khác).


### Nguyên lý hoạt động

- **Theo dõi thay đổi**: Hệ thống quan sát transaction log (binlog của MySQL, WAL của PostgreSQL, redo log của Oracle, v.v.) hoặc trigger trong DB để phát hiện thay đổi.
    
- **Ghi nhận sự kiện**: Khi có thao tác trên bảng (INSERT/UPDATE/DELETE), CDC sẽ tạo ra một sự kiện.
    
- **Đẩy dữ liệu**: Các sự kiện được đẩy đến **message broker** (Kafka, Pulsar), hoặc **ETL pipeline** (Debezium, Apache Flink, Airbyte).
    
- **Đồng bộ hóa**: Hệ thống đích nhận sự kiện và cập nhật tương ứng (ví dụ: Elasticsearch để search, Data Lake để phân tích).


### Lợi ích

- **Realtime replication**: Giúp đồng bộ dữ liệu từ DB nguồn đến các hệ thống khác theo thời gian thực.
    
- **Event-driven architecture**: Phục vụ microservices, khi một thay đổi xảy ra sẽ phát sự kiện cho các service khác xử lý.
    
- **Giảm tải ETL batch**: Thay vì chạy batch định kỳ, dữ liệu được cập nhật liên tục.

### Các công cụ phổ biến

- **Debezium** (trên Kafka Connect) → đọc binlog, WAL, redo log.
    
- **AWS DMS** → dịch vụ CDC của Amazon.
    
- **Oracle GoldenGate** → giải pháp thương mại mạnh cho Oracle DB.
    
- **SQL Server CDC** → tích hợp sẵn từ SQL Server 2008.
    
- **Airbyte / Fivetran** → CDC như một phần của ETL SaaS.



## References