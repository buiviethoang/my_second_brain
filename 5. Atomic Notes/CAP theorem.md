2025-07-12 21:22
Status: #baby
Tags: [[computer science]] [[system design]]
## Main

### Definition

In any **distributed data system**, you can only **guarantee** **two out of the following three** properties at the same time:

### 🔹 C — **Consistency**

- **Every read receives the most recent write** (or an error).
    
- Equivalent to what you'd expect in a traditional single-node database.
    
- Example: If you write `x = 5`, any future read must return `5`.
    

---

### 🔹 A — **Availability**

- The system **always responds** (even if it’s not the most recent data).
    
- Every request receives a (non-error) response — **without guarantee that it contains the latest data**.
    
- Example: Even if one node is down, other nodes will still serve requests.
    

---

### 🔹 P — **Partition Tolerance**

- The system continues to operate **despite network partitions** (i.e., some nodes can’t talk to others due to network failure).
    
- Partition tolerance is a **must-have** in any practical distributed system (you can’t prevent network failures).

| Type   | Guarantees                         | Sacrifices          | Example Systems                           |
| ------ | ---------------------------------- | ------------------- | ----------------------------------------- |
| **CP** | Consistency + Partition Tolerance  | Availability        | HBase, MongoDB (in some modes)            |
| **CA** | Consistency + Availability         | Partition Tolerance | Not practical in real distributed systems |
| **AP** | Availability + Partition Tolerance | Consistency         | Cassandra, Couchbase, DynamoDB            |

### Example
## ✅ CAP Trade-offs in Popular NoSQL Databases

### 1. **Cassandra – AP (Availability + Partition Tolerance)**

- **Partition Tolerance**: Built for distributed environments, Cassandra handles network splits well.
    
- **Availability**: It continues to accept reads/writes even when some nodes are unreachable.
    
- **Consistency**: It’s **eventually consistent** by default — some nodes might return stale data temporarily.
    

#### 💡 How it works:

- You can **tune the consistency** level per operation (e.g., QUORUM, ONE, ALL).
    
- For example, write at `QUORUM` and read at `QUORUM` = stronger consistency.
    

#### 🧪 Use Case:

- High-write environments like IoT, messaging, or real-time analytics.
    
- Companies: Netflix, Instagram.
    

---

### 2. **MongoDB – CP (Consistency + Partition Tolerance)**

- **Consistency**: Strong consistency for **primary reads** (read/write to the same primary replica).
    
- **Partition Tolerance**: Survives network splits — elections will pick a new primary if needed.
    
- **Availability**: Sacrificed during failover — the system **refuses writes** until a new primary is elected.
    

#### 💡 How it works:

- **Replica sets** ensure durability and data consistency.
    
- Allows **read preference** like `secondaryPreferred` (can increase availability but reduce consistency).
    

#### 🧪 Use Case:

- E-commerce platforms, document stores, content management systems.
    

---

### 3. **DynamoDB – AP (Availability + Partition Tolerance)**

- **Partition Tolerance**: Fully distributed, globally available.
    
- **Availability**: Very high availability; always serves reads/writes.
    
- **Consistency**: Default is **eventual consistency**; **strong consistency** is optional with trade-offs in latency.
    

#### 💡 How it works:

- Writes propagate to replicas in the background.
    
- **Tunable consistency model** (similar to Cassandra but more abstracted).
    

#### 🧪 Use Case:

- Shopping carts, user sessions, low-latency global apps.
    

---

### 4. **HBase – CP (Consistency + Partition Tolerance)**

- **Consistency**: Strong consistency — follows HDFS model (write once, read many).
    
- **Partition Tolerance**: Survives node failures with automatic recovery.
    
- **Availability**: Sacrificed — if region servers or NameNode fail, reads/writes pause.
    

#### 🧪 Use Case:

- Batch processing, Hadoop ecosystems, OLAP workloads.


|Database|CAP Trade-off|Consistency Model|Tunable?|Best For|
|---|---|---|---|---|
|**Cassandra**|AP|Eventually Consistent|✅ Yes|Write-heavy, scalable systems|
|**MongoDB**|CP|Strong (primary reads)|✅ Partially|Flexible document-based apps|
|**DynamoDB**|AP|Eventually or Strong|✅ Yes|Global, low-latency applications|
|**HBase**|CP|Strong|❌ No|Big data batch processing|
## References
ChatGPT
