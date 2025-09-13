2025-08-26 21:48
Status: #baby
Tags: [[database]]
## Main

### Type
### 1. **B-Tree Index (Default)**

- Most common and default in almost all databases.
    
- Keeps keys in a **balanced tree structure**.
    
- Great for:
    
    - Equality lookups (`=`).
        
    - Range queries (`<`, `<=`, `BETWEEN`, `>`).
        
    - Sorting (`ORDER BY`).

Weakness: Not efficient for high-cardinality range scans on unsorted data.

```sql
CREATE INDEX idx_customer_name ON customers(name);
```
### 2. **Hash Index**

- Uses a **hash function** → maps key values to slots.
    
- Very fast for **exact matches (`=`)**.
    
- Not useful for ranges or sorting.

```sql
CREATE INDEX idx_customer_email_hash ON customers USING HASH(email);
```

Caveats:

- PostgreSQL: hash indexes are now WAL-logged (safe).
    
- MySQL: MEMORY engine uses hash indexes by default.


### 3. **Bitmap Index** (Oracle, PostgreSQL extension)

- Stores a **bitmap for each distinct value** (bit=1 if row has that value).
    
- Very efficient for:
    
    - Low-cardinality columns (few distinct values, e.g., gender, status).
        
    - Complex `AND`/`OR` queries.

- Weakness: Not good for high-cardinality columns or frequent updates (bitmaps become large).
```sql
-- Oracle
CREATE BITMAP INDEX idx_gender ON customers(gender);
```

### 4. **GiST (Generalized Search Tree) Index** (PostgreSQL)

- Flexible index structure, supports custom data types.
    
- Used for:
    
    - Full-text search.
        
    - Geospatial queries.
        
    - Range types.
```sql
CREATE INDEX idx_location ON places USING GIST (coordinates);
```

### 6. **SP-GiST (Space-Partitioned GiST)** (Postgres)

- Useful for partitioning search space into **non-balanced trees**.
    
- Good for:
    
    - Geometric data.
        
    - Phone number ranges, IP subnets.

### 7. **BRIN (Block Range Index)** (Postgres)

- Very compact → stores **summary of ranges of pages**, not individual rows.
    
- Great for:
    
    - Huge tables with natural ordering (timestamps, auto-increment IDs).
        
    - Append-only workloads.

```sql
CREATE INDEX idx_date_brin ON logs USING BRIN (created_at);
```


### 8. **Clustered Index** (SQL Server, MySQL InnoDB)

- Determines the **physical order of rows** in the table.
    
- Each table can have only **one clustered index**.
    
- `PRIMARY KEY` is often clustered.
    
- Range queries are super fast.
    
- Downside: updating clustered key is expensive.

### 9. **Non-Clustered Index**

- A separate structure that stores index + a pointer to the actual row.
    
- Can include additional columns (**covering index**).
    
- Example (SQL Server, MySQL):

```sql
CREATE INDEX idx_order_customer ON orders(customer_id);
```


### 10. **Full-Text Index**

- Specialized for **searching text** with linguistic processing.
    
- Allows `MATCH ... AGAINST` in MySQL, `to_tsvector` in PostgreSQL.

```sql
-- MySQL
CREATE FULLTEXT INDEX idx_content ON articles(content);
```

|Index Type|Best For|Not Good For|
|---|---|---|
|**B-Tree**|Equality, ranges, ORDER BY|Very wide text search|
|**Hash**|Exact match (`=`)|Range queries|
|**Bitmap**|Low-cardinality columns, complex boolean filters|High-cardinality, frequent updates|
|**GiST**|Geospatial, text search|Simple equality lookups|
|**GIN**|JSON, arrays, full-text|Single-value lookups|
|**SP-GiST**|Hierarchical data, ranges|General-purpose queries|
|**BRIN**|Huge tables, sequential data|Random data|
|**Clustered**|Range scans, primary key lookups|Frequent key updates|
|**Non-Clustered**|Flexible lookups, covering indexes|Extra storage overhead|
|**Full-Text**|Natural language search|Exact match lookups|

### Design Strategies

# 🔹 1. Single-Column Index

- Index on **one column only**.
    
- Simplest and most common type.
    
- Good when queries filter or join on that one column.

```sql
CREATE INDEX idx_customer_name ON customers(name);
```

⚠️ Limitation:

- Doesn’t help if query filters on **multiple columns** (unless DB can combine indexes with _index intersection_, supported in some systems like Postgres).

# 2. Composite (Multi-Column) Index

- Index built on **two or more columns**.
    
- Order matters: `(a, b)` can optimize queries filtering on `a` or on both `a` and `b`, but **not only `b`**.

```sql
CREATE INDEX idx_customer_city_name ON customers(city, name);

-- Uses idx_customer_city_name
SELECT * FROM customers WHERE city = 'Hanoi' AND name = 'Alice';

-- Uses prefix (city)
SELECT * FROM customers WHERE city = 'Hanoi';

-- ❌ Won’t use it efficiently
SELECT * FROM customers WHERE name = 'Alice';
```


⚠️ Rule of thumb: **leftmost prefix rule** → only the leftmost columns (or their combination) can be used for efficient lookups.


# 3. Covering Index

- An index that contains **all the columns needed by a query**.
    
- DB can answer the query **just from the index** → no need to fetch rows from the table (called an **Index Only Scan** in Postgres).


```sql
CREATE INDEX idx_orders_customer_date 
ON orders(customer_id, order_date)
INCLUDE (status, total_amount);

SELECT customer_id, order_date, status, total_amount
FROM orders
WHERE customer_id = 123
ORDER BY order_date DESC;
```

- Here the covering index has all needed columns → no table lookup → much faster.
    

⚠️ Trade-off:

- Covering indexes can get **wide** (take more storage).
    
- Updates/inserts are slower because index maintenance is heavier.


|Index Type|Description|Best For|Limitation|
|---|---|---|---|
|**Single-Column**|Index on one column|Simple lookups|Won’t help with multi-column filters|
|**Composite**|Multi-column index|Queries filtering on multiple columns (esp. prefix-based)|Order of columns matters|
|**Covering**|Index includes all needed columns|Avoids table lookups → fastest|Larger storage, slower writes|

# 🔹 Rule of Thumb (Design Strategy)

1. If queries filter on **one column often** → single-column index.
    
2. If queries filter on **two+ columns together** → composite index (put the most selective column first).
    
3. If queries **only read a subset of columns** → covering index (include those columns).
    
4. Don’t over-index → every index slows down `INSERT/UPDATE/DELETE`.


### Maintenance cost
### 🔹 1. **Write Operations (INSERT, UPDATE, DELETE)**

- **INSERT**: Every new row must be added to **all indexes** on that table.
    
    - Example: If you insert a new customer, and the table has 3 indexes, the row must be written to all 3.
        
- **UPDATE**: If an indexed column changes, the DB must **delete the old index entry** and **insert a new one**.
    
- **DELETE**: The corresponding entries must be removed from every index.  
    👉 More indexes = slower writes.


### 🔹 2. **Storage & Memory Overhead**

- Indexes consume **extra disk space** (sometimes even more than the table if poorly designed).
    
- They also compete for **cache memory** (buffer pool in MySQL/InnoDB, shared buffers in PostgreSQL).  
    👉 Having too many or large indexes can push useful table data out of memory.


### 🔹 3. **Index Fragmentation**

- Over time, inserts/updates/deletes cause **page splits** (in B-Tree indexes), leading to fragmentation.
    
- This makes index scans slower and increases I/O.
    
- DBs sometimes need **REINDEX** (Postgres) or **OPTIMIZE TABLE** (MySQL) to reclaim space.


### 🔹 4. **Query Planner Complexity**

- Each index increases the **search space for the optimizer**.
    
- Too many indexes can confuse the optimizer and sometimes lead it to pick a suboptimal plan.

### 🔹 5. **Locking/Concurrency**

- Index updates may require **locks/latches** on index structures.
    
- Heavy write workloads with many indexes can lead to contention.

### 📌 Rule of Thumb:

- **Read-heavy workloads**: More indexes are good (carefully chosen).
    
- **Write-heavy workloads**: Minimize indexes, keep only the most beneficial ones.
    
- **Balance**: Always profile queries (`EXPLAIN`/`EXPLAIN ANALYZE`) and monitor write latency.
## References