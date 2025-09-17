2025-08-14 07:02
Status: #baby
Tags: [[database]]
## Main
### **1. Purpose**

- **OLTP**: Optimized for **transactional workloads** — lots of short, fast inserts, updates, deletes. Think: day-to-day operations.
    
- **OLAP**: Optimized for **analytical workloads** — complex queries, aggregations, trend analysis. Think: decision support.

### **2. Data Operations**

- **OLTP**: CRUD operations (Create, Read, Update, Delete).
    
- **OLAP**: Read-heavy, aggregate operations (SUM, AVG, GROUP BY, JOIN across large tables).

### **3. Query Characteristics**

- **OLTP**: Simple queries, typically touch a few records at a time (e.g., inserting a new order).
    
- **OLAP**: Complex queries scanning millions of rows (e.g., monthly sales trend across all regions).


### **4. Data Volume**

- **OLTP**: Current, operational data. Usually MB–GB scale.
    
- **OLAP**: Historical data. Usually GB–TB–PB scale.

### **5. Database Design**

- **OLTP**: Highly normalized schemas (3NF) to reduce redundancy and maintain data integrity.
    
- **OLAP**: Denormalized schemas (star schema, snowflake schema) for faster querying.

### **6. Performance Focus**

- **OLTP**: Low latency, high concurrency. Many users doing small transactions simultaneously.
    
- **OLAP**: High throughput for complex queries. Fewer users running large analytical queries.

### **7. Examples**

- **OLTP**: Banking systems, e-commerce order systems, airline booking.
    
- **OLAP**: Data warehouses, BI dashboards, reporting systems.

### **8. Tech Stack Examples**

- **OLTP**: MySQL, PostgreSQL, MongoDB (transactional side).
    
- **OLAP**: Snowflake, BigQuery, Redshift, ClickHouse, Apache Hive.

👉 Quick analogy:

- **OLTP = ATM machine** (many small, real-time transactions).
    
- **OLAP = Financial analyst’s report** (summarizing years of transactions into insights).


## References
https://viblo.asia/p/oltp-va-olap-co-gi-khac-nhau-maGK786BZj2