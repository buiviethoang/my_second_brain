2025-09-11 21:34
Status: 
Topic: 
Tags: [[database]]
## Main

## What Happens When You Run a SQL Statement

1. **Parsing** – DBMS checks the SQL syntax, validates objects (tables, columns, permissions).
    
2. **Optimization** – DBMS decides the best execution plan (which index, join order, etc.).
    
3. **Execution** – Run the plan.

## Hard Parse

- Occurs when the SQL statement is **not already in the shared pool / plan cache**.
    
- Database must:
    
    - Parse SQL text from scratch.
        
    - Check schema objects and privileges.
        
    - Generate a **new execution plan**.
        
    - Store the plan in memory (shared pool / plan cache).
        
- **Costly**: consumes CPU and latches, can cause contention in high-concurrency systems.


## Soft Parse

- Occurs when the SQL statement **already has a cached execution plan** in memory.
    
- Database just **reuses the existing plan** instead of generating a new one.
    
- Much faster and lighter.


## 🔹 Example

Suppose you run:

`SELECT * FROM orders WHERE order_id = 101;`

### Case 1: Hard Parse

- First time this exact SQL runs → database parses, optimizes, creates a plan.

### Case 2: Soft Parse

- Next time you run the **same SQL string**:
    
    `SELECT * FROM orders WHERE order_id = 102;`


If you wrote it with a **bind variable**:

`SELECT * FROM orders WHERE order_id = :order_id;`


- → Database reuses the cached plan (soft parse).
    
- If you wrote it with a literal (`101` vs `102`), some databases may treat them as different queries, forcing a new hard parse.

## Why It Matters

- **Hard parses are expensive**. Too many of them = performance bottleneck.
    
- Best practice:
    
    - Use **bind variables / prepared statements** (so SQL text matches and plans can be reused).
        
    - Monitor parse-to-execute ratios.
        
    - Increase shared pool / plan cache size if it’s too small.


## References