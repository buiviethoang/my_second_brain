2025-08-26 21:26
Status: #baby
Tags: [[database]]
## Main
### WAL (Write-ahead Logs)
A **Write-Ahead Log (WAL)** is a **sequential log file** where **all changes are written before they are applied to the database**.

- The principle:  
    **“Log first, then modify data.”**
    
- This guarantees **Atomicity** and **Durability** in ACID.
    
- If the database crashes, it can replay or roll back operations from the WAL.



## 🔹 How it Works (Step by Step)

1. **Start a Transaction**
    
    - The DB keeps the changes in memory (buffer pool).
        
2. **Modify Data in Memory (not yet in disk)**
    
    - Example: `UPDATE accounts SET balance = balance - 100 WHERE id = 1`.
        
3. **Log the Change into WAL (append-only, sequential write)**
    
    - The change (before/after values, page IDs, etc.) is written into WAL on disk.
        
    - WAL writes are **fast** because they’re sequential.
        
4. **Commit the Transaction**
    
    - The database flushes WAL records to durable storage (disk/SSD).
        
    - Now the transaction is considered committed.
        
5. **Apply Changes to Data Files (later, asynchronously)**
    
    - Actual data pages are updated on disk later (checkpointing).
        
    - If a crash happens, WAL is used to **redo/undo** changes.

## 🔹 Why WAL is Useful

- **Crash Recovery**: If the DB crashes, it replays WAL to restore a consistent state.
    
- **Durability**: Once WAL is written, the commit is guaranteed.
    
- **Performance**: Sequential disk writes are much faster than random writes.
    
- **Replication**: WAL can be shipped to replicas (e.g., PostgreSQL streaming replication).

Say we transfer **$100 from A → B**:

1. WAL entry logged:
    
    - `Debit A: -100`
        
    - `Credit B: +100`
        
2. WAL flushed to disk → **Commit succeeds**.
    
3. Later, actual data files for accounts A & B are updated.
    
4. If the server crashes before step 3, WAL is replayed → transaction is restored.

### Redo Logs
A **redo log** is a log file that stores information needed to **reapply (redo)** changes to the database in case of a crash, ensuring **durability**.

- If a transaction **commits** but data pages are not yet written to disk → redo log ensures the changes can still be applied.
    
- Contrast with **undo logs**, which store info to **roll back** uncommitted transactions (for atomicity).

## 🔹 Redo Logs in MySQL (InnoDB)

In InnoDB, redo logs are implemented as **log files (`ib_logfile0`, `ib_logfile1`, etc.)**.

**Workflow:**

1. You update data → change goes into **buffer pool** (memory).
    
2. InnoDB writes a **redo entry** (what to redo if crash) into the **redo log buffer**.
    
3. On **COMMIT**, the redo log buffer is flushed to disk → transaction is durable.
    
4. Actual data pages (from buffer pool) are written later during **checkpointing**.
    
5. If MySQL crashes → InnoDB replays redo logs to ensure committed transactions are applied.
    

So, **redo log = guarantees durability**, **undo log = rollback uncommitted changes**.


## 🔹 WAL vs Redo Logs

They sound similar but aren’t identical:

- **PostgreSQL**: Uses **WAL (Write-Ahead Log)** → sequential log of changes, doubles as a redo log.
    
- **MySQL (InnoDB)**: Uses both **redo logs** and **undo logs**.
    
    - **Redo logs** → guarantee durability (replay committed work).
        
    - **Undo logs** → rollback failed/uncommitted work.
        

👉 You can think of WAL as a **general technique** (“log first, then write”), while redo/undo logs are **concrete implementations** of that technique.

## 🔹 Redo Logs vs Binary Logs

In MySQL:

- **Redo log** (InnoDB) → crash recovery (ensures data durability).
    
- **Binary log (binlog)** → replication + point-in-time recovery.

✅ So:

- PostgreSQL → WAL = redo logging.
    
- MySQL (InnoDB) → redo log + undo log → together provide ACID.



## References