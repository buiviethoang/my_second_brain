2025-08-26 21:42
Status: #baby
Tags: [[database]]
## Main

An **execution plan** is a roadmap the database engine generates to execute a SQL query.  
It shows which **access paths** (Seq Scan, Index Scan, etc.) and which **join algorithms** (Nested Loop, Hash Join, Merge Join) will be used.

# 🔹 Table Access Methods

### 1. **Sequential Scan (Seq Scan)**

- Reads the **entire table row by row**.
    
- Used when:
    
    - No useful index exists.
        
    - Query needs most rows anyway.
        
    - Table is small (seq scan is cheaper).
```sql
SELECT * FROM customers WHERE country = 'VN';
```

If no index on `country`, DB will scan all rows.

### 2. **Index Scan**

- Uses an **index** to find matching rows quickly.
    
- Still fetches rows from the table (heap lookup in PostgreSQL).
    
- Good when:
    
    - Predicate is selective (matches few rows).
        
    - Index exists on filter column(s).
    
```sql
SELECT * FROM customers WHERE id = 123;
```

- Uses **Index Scan** on `PRIMARY KEY`.

### 3. **Index Only Scan**

- Uses an index **without touching the table** (if index covers all required columns).
    
- Very efficient since it avoids extra I/O.

```sql
SELECT id, country FROM customers WHERE id = 123;
```

- If index on `(id, country)` exists → Index Only Scan.

### 4. **Bitmap Index Scan (Postgres)**

- Uses index to get **row locations**, then batches them together before fetching from table.
    
- Efficient when query returns **many scattered rows**.**


# 🔹 Join Algorithms

### 1. **Nested Loop Join**

- For each row in outer table → scan inner table for matches.
    
- Best when:
    
    - Outer table is small.
        
    - Inner table is indexed.

```sql
SELECT * 
FROM orders o
JOIN customers c ON o.customer_id = c.id;
```
If `customers.id` has an index → Nested Loop is efficient.


### 2. **Hash Join**

- Builds a **hash table** for one table (usually smaller).
    
- Probes the hash for each row of the other table.
    
- Best when:
    
    - Large tables with no good indexes.
        
    - Equality join conditions (`=`).


```sql
SELECT * 
FROM orders o
JOIN shipments s ON o.order_id = s.order_id;

```

### 3. **Merge Join**

- Requires both inputs to be **sorted** on join keys.
    
- Walks through both sorted lists at the same time.
    
- Best when:
    
    - Both tables already sorted (due to index).
        
    - Large datasets.

# Key Takeaways

- **Seq Scan** → scans whole table, good for small/unindexed.
    
- **Index Scan** → efficient for selective lookups.
    
- **Nested Loop** → great with indexes + small outer table.
    
- **Hash Join** → big tables, equality joins.
    
- **Merge Join** → sorted inputs, range queries.


# 🔹 Execution Plan Reading Checklist

### ✅ Step 1: Identify the **query goal**

- What is the query doing? (`SELECT`, `JOIN`, `GROUP BY`, `ORDER BY`…)
    
- Which columns and filters matter most?
    

---

### ✅ Step 2: Look at the **root node** (top of plan)

- The top operator (e.g., `Aggregate`, `Sort`, `Limit`) tells you the **final operation**.
    
- Ask: Is this necessary? (e.g., sorting could be avoided if index already provides order).
    

---

### ✅ Step 3: Scan **access paths**

- Check **Seq Scan vs Index Scan vs Index Only Scan**.
    
- **Red flag**: `Seq Scan` on a large table with a selective filter (maybe missing an index).
    
- ✅ Good sign: `Index Cond: ...` instead of `Filter: ...`.
    

---

### ✅ Step 4: Review **joins**

- Which join algorithm? (`Nested Loop`, `Hash Join`, `Merge Join`).
    
- Is it appropriate?
    
    - Small outer + indexed inner → Nested Loop.
        
    - Big tables, no indexes → Hash Join.
        
    - Pre-sorted inputs → Merge Join.
        
- **Red flag**: Nested Loop with millions of iterations and no index.
    

---

### ✅ Step 5: Check **filters and predicates**

- Look for `Filter:` conditions applied **after** scanning → wasteful.
    
- Try to move conditions into `Index Cond:` if possible.
    

---

### ✅ Step 6: Watch for **sorts & aggregations**

- `Sort` or `HashAggregate` may be expensive.
    
- Ask:
    
    - Can a **covering index** avoid the sort?
        
    - Can a **GROUP BY index** help aggregation?
        

---

### ✅ Step 7: Compare **row estimates vs actual rows** (if `EXPLAIN ANALYZE`)

- Big mismatch → optimizer statistics are outdated.
    
- Example: estimated 100 rows, actual 1,000,000 → consider running `ANALYZE` or updating stats.
    

---

### ✅ Step 8: Spot **parallelism**

- Look for operators like `Parallel Seq Scan`, `Gather`, `Parallel Hash`.
    
- ✅ Good sign on large tables.
    
- **Red flag**: parallelism on small tables adds overhead.
    

---

### ✅ Step 9: Evaluate **cost balance (I/O vs CPU)**

- Is the plan scanning too many pages (I/O bound)? → add indexes or partitioning.
    
- Is it hashing/sorting a lot (CPU bound)? → increase memory (e.g., `work_mem` in PostgreSQL).
    

---

### ✅ Step 10: Validate **final output operators**

- Are you sorting/aggregating more than needed?
    
- Could a `LIMIT` or early filtering push down reduce work?
    
- Are you retrieving only necessary columns?
    

---

# 🔹 Quick “Red Flag” Checklist

- ❌ Seq Scan on a large table with selective filter.
    
- ❌ Nested Loop without index on inner table.
    
- ❌ Sort on a large dataset when index could provide order.
    
- ❌ Huge difference between estimated vs actual rows.
    
- ❌ Filters applied after full table scan instead of via index.
    

---

# 🔹 Quick “Good Sign” Checklist

- ✅ Index Only Scan instead of Index Scan.
    
- ✅ Index Cond (filter pushed into index).
    
- ✅ Hash Join for large joins.
    
- ✅ Merge Join when inputs already sorted.
    
- ✅ Parallel query on big datasets.



## References