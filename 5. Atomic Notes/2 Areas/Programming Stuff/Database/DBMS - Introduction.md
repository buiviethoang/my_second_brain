2025-07-12 17:37
Status: #baby
Tags: [[computer science]] [[database]]
## Main
### When to use RDBMS - NOSQL
|Feature|RDBMS|NoSQL|
|---|---|---|
|Schema|Fixed|Flexible|
|Transactions|Strong ACID|Often eventual consistency|
|Data Type|Structured|Semi/Unstructured|
|Scaling|Vertical|Horizontal|
|Query Language|SQL|Varies (JSON-style, key-based, etc.)|
|Examples|MySQL, PostgreSQL|MongoDB, Cassandra, DynamoDB|

## ✅ Use **RDBMS** (e.g., PostgreSQL, MySQL, Oracle) when:

### 1. **Data is Structured and Relational**

- You have clearly defined **tables**, **columns**, and **relationships** (e.g., foreign keys).
    
- Examples:
    
    - Banking systems
        
    - Inventory management
        
    - Enterprise applications (HR, ERP)
        

### 2. **Strong Consistency is Important (ACID)** [[ACID]]

- You need **strict transactional guarantees**, like in:
    
    - Financial systems (money transfers)
        
    - Order processing systems
        

### 3. **Fixed Schema**

- Your data model doesn’t change frequently.
    
- You benefit from **schema validation**, **JOINs**, and **SQL queries**.
    

### 4. **Data Volume is Moderate**

- RDBMS can scale **vertically** (strong single-node performance), but not always as easy to **scale horizontally**.

## ✅ Use **NoSQL** (e.g., MongoDB, Cassandra, Redis, DynamoDB) when:

### 1. **Data is Semi-structured or Unstructured**

- JSON, XML, text blobs, or variable formats.
    
- Examples:
    
    - User profiles with custom fields
        
    - Product catalogs with dynamic attributes
        

### 2. **High Scalability and Performance**

- You need to handle **large-scale**, **high-traffic** applications.
    
- NoSQL is designed for **horizontal scaling** (adding more servers).
    

### 3. **Flexible Schema**

- You want to **freely change the data model** without altering the schema.
    
- Useful in rapid development or agile teams.
    

### 4. **Eventual Consistency is Acceptable**

- You're okay with a **delay** in data becoming consistent across nodes.
    
- Examples:
    
    - Social media feeds
        
    - Analytics data
        
    - Caching systems (like Redis)


## References
ChatGPT