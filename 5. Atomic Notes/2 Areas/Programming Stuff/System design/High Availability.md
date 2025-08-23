2025-08-19 22:26
Status: #baby
Tags: [[system design]]
## Main

These terms usually refer to **application-level or system-level deployment** strategies (e.g., servers, services, or clusters):

### ✅ **Active-Active**

- **All nodes are active** and handle traffic simultaneously.
    
- Load is **balanced across all instances**.
    
- If one node fails, others keep running **without interruption**.
    
- Data must be synchronized (requires **conflict resolution** if writes happen at multiple places).
    

#### 🧪 Use Case:

- Load-balanced web servers, distributed databases with conflict-free writes (e.g., Cassandra).
    

#### 🔄 Pros:

- High availability
    
- Scalability
    
- Better resource utilization
    

---

### ✅ **Active-Standby**

- One node is **active**, others are **on standby** (hot/cold backup).
    
- If the active node fails, a **standby takes over** (manual or automatic failover).
    
- Simple to implement, no write conflicts.
    

#### 🧪 Use Case:

- PostgreSQL with streaming replication, or app servers with failover.
    

#### 🛠 Pros:

- Simpler conflict handling
    
- Ideal for **strong consistency**
    

---

## 🧩 2. **Master-Master vs Master-Slave (or Primary-Replica)**

These terms are **database-specific**, focusing on **data replication and synchronization**.

### ✅ **Master-Master (Multi-Master)**

- **Both (or all) nodes can accept writes**.
    
- Changes must be **synchronized between all masters**.
    
- May cause **conflicts** that require resolution (e.g., last write wins).
    

#### 🧪 Use Case:

- MySQL Cluster, CouchDB, LDAP, Active Directory
    

#### 🔄 Pros:

- Redundancy and fault tolerance
    
- Faster local writes in multi-region setups
    

#### ⚠️ Challenges:

- Conflict resolution
    
- Increased complexity
    

---

### ✅ **Master-Slave (Primary-Replica)**

- **Master (Primary)** handles all **writes**.
    
- **Slaves (Replicas)** handle **reads** and sync from the master.
    
- Slaves cannot accept writes (unless promoted).
    

#### 🧪 Use Case:

- MySQL replication, PostgreSQL read replicas, Redis replicas
    

#### 🛠 Pros:

- Simplifies consistency (no conflict)
    
- Great for **read-heavy** systems
    

#### ⚠️ Drawbacks:

- Master is a **single point of write failure**
    
- Lag between master and slave


| Concept            | Write Capability        | Failover    | Use Case                            | Conflict Risk |
| ------------------ | ----------------------- | ----------- | ----------------------------------- | ------------- |
| **Active-Active**  | All nodes handle writes | No downtime | Load-balanced systems, CDNs         | High          |
| **Active-Standby** | One node handles writes | Failover    | Traditional HA setups, DBs          | Low           |
| **Master-Master**  | All nodes can write     | Redundant   | Distributed DBs with sync (CouchDB) | Medium–High   |
| **Master-Slave**   | Only master writes      | Manual/auto | Read scaling (MySQL/PostgreSQL)     | Low           |

## References