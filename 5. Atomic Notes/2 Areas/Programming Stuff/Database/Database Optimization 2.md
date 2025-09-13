2025-09-11 21:13
Status: 
Topic: 
Tags: [[database]]
## Main

### InnoDB Buffer Pool

- The **InnoDB buffer pool** is a memory area that caches **data and indexes** from your tables.
    
- Instead of reading and writing directly from disk (which is slow), MySQL stores frequently accessed pages in RAM.
    
- This greatly improves performance because accessing RAM is much faster than disk I/O.


#### 🔹 What’s inside the buffer pool?

1. **Data pages** – table rows read from disk.
    
2. **Index pages** – B-Tree indexes used for searching.
    
3. **Undo logs** – used for transaction rollbacks.
    
4. **Insert buffer (change buffer)** – caches changes to secondary indexes.
    
5. **Adaptive hash index** – helps speed up searches.


#### Configuration

- The main setting is:
    
    `innodb_buffer_pool_size`
    
    This controls how much memory is allocated to the buffer pool.
    
- General rule:
    
    - On a **dedicated MySQL server**, set it to **60–75% of available RAM**.
        
    - Too small → frequent disk reads/writes → slow performance.
        
    - Too big → memory pressure on the OS → swapping → worse performance.

#### What if the value is too large? 

##### Starving the Operating System and Other Processes

- If MySQL grabs most of the RAM, the OS doesn’t have enough memory left for:
    
    - File system cache (used for MyISAM or binary logs, tmp files, etc.)
        
    - Other processes (web server, monitoring agents, etc.)

##### OS Starts Swapping

- If the buffer pool doesn’t fit in physical RAM, the OS will swap pages to disk.
    
- That means MySQL’s “cache” is actually stored on **slow disk**, which completely defeats the purpose of caching.
    
- This can cause **severe slowdowns** and high I/O wait.

##### Long Startup and Recovery Times

- The bigger the buffer pool, the longer it takes:
    
    - For MySQL to **initialize the buffer pool** at startup.
        
    - To **warm up the cache** (fill it with useful data).
        
- On crash recovery, flushing or refilling a massive buffer pool can be slow.
  
##### Diminishing Returns

- If your working dataset (tables + indexes) is smaller than the buffer pool, then allocating more memory provides **no additional benefit**.
    
- Example: dataset = 10 GB, buffer pool = 64 GB → 54 GB wasted.

##### Fragmentation / Inefficiency

- Extremely large buffer pools can suffer from **fragmentation** in internal structures.
    
- If not tuned (e.g., `innodb_buffer_pool_instances`), concurrency may decrease because threads fight for buffer pool access.

✅ **Rule of thumb**:

- On a dedicated MySQL server: **60–75% of total RAM** is safe.
    
- Don’t exceed available physical memory.
    
- Make sure to leave enough for the OS and other services.


### table_definition_cache

These settings/variables are about how MySQL handles **table metadata in memory**, not the actual data rows.

## 1. `table_definition_cache`

- This is the **maximum number of table definitions** MySQL can keep in memory.
    
- A **table definition** is basically the metadata (columns, indexes, schema info) loaded from the `.frm` (pre-MySQL 8) or data dictionary (MySQL 8+) files.
    
- When you run queries, MySQL must know the structure of each table. Instead of re-reading from disk every time, it caches this structure.
    
- Default might be low (e.g. 400), but on systems with many tables or many concurrent queries, you may need to increase it.
    

👉 If too small:

- Table definitions are frequently loaded/unloaded from disk → **extra disk I/O** and query latency.


## 2. `Open_table_definitions`

- This is a **status variable**, not a setting.
    
- Shows the **number of cached table definitions currently in use** (open).
    
- Think of it as “how many table definitions MySQL is actively keeping in memory right now.”


## 3. `Opened_table_definitions`

- This is also a **status variable**.
    
- Counts the **number of times MySQL had to open a table definition from disk** since the server started.
    
- A steadily increasing number = your cache is too small.


### temp table

## 1. Internal Temporary Tables (created by MySQL itself)

- These are **invisible to you** — MySQL automatically creates them when a query needs extra workspace.
    
- Common cases:
    
    - `GROUP BY`
        
    - `ORDER BY`
        
    - `DISTINCT`
        
    - `UNION` / `UNION ALL`
        
    - Complex joins and subqueries
        
- They hold **intermediate results** while MySQL is processing a query.
    
- Location:
    
    - First MySQL tries to put them in **RAM** (MEMORY/HEAP engine).
        
    - If they exceed the size limit (`tmp_table_size` / `max_heap_table_size`), they are converted into **on-disk MyISAM/InnoDB tables** (much slower).

```sql
SHOW GLOBAL STATUS LIKE 'Created_tmp%';
```

- `Created_tmp_tables` → total internal temp tables created.
    
- `Created_tmp_disk_tables` → how many of them ended up on disk.

## 2. User-Created Temporary Tables

- Explicitly created by you with:
    
    `CREATE TEMPORARY TABLE my_tmp (...) ENGINE=MEMORY;`
    
- Scope:
    
    - Visible only to your session/connection.
        
    - Automatically dropped when the session ends.
        
- Often used to:
    
    - Store intermediate results for complex procedures.
        
    - Break large queries into smaller steps.
        
- Controlled by `max_heap_table_size` (if using MEMORY engine).


✅ In short:

- A **temp table** is just a workspace table MySQL uses to hold intermediate query results.
    
- They can be **automatic (internal)** or **user-created**.
    
- If they fit in RAM → fast. If too big → written to disk → slower performance.

## 3. `max_heap_table_size`

- This sets the **maximum size of user-created MEMORY (HEAP) tables**.
    
- Example:
    
    `CREATE TEMPORARY TABLE t ENGINE=MEMORY;`
    
    This table can grow only up to `max_heap_table_size`.
    
- It does **not** affect MySQL’s internal temp tables directly.


## Signs You Need to Increase

- If you see a lot of **Created_tmp_disk_tables** (check with `SHOW GLOBAL STATUS LIKE 'Created_tmp%';`), it means queries are spilling temp tables to disk.
## . Caution

- These limits apply **per connection**.
    
- If you allow 1 GB temp tables and have 100 concurrent queries, you could theoretically consume 100 GB of RAM → server crash.
    
- Tune carefully depending on workload and available memory.


## References