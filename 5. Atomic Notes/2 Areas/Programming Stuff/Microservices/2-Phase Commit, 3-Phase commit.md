2025-09-22 08:55
Status: 
Topic: 
Tags: [[microservices]] 
## Main

Two-Phase Commit is a **distributed transaction protocol** used in databases and distributed systems to ensure **atomicity** (all-or-nothing execution) across multiple participants (nodes, databases, or services).

It’s coordinated by a **Transaction Coordinator** and executed by multiple **Participants** (or resource managers, e.g., databases).


### Why? 
Imagine you want to **transfer money from Bank A to Bank B**:

- Debit from A.
    
- Credit to B.  
    If Bank A succeeds but Bank B fails, you’d end up with inconsistent data.  
    2PC ensures either **both succeed** or **both rollback**.


### How? 
#### **Phase 1: Prepare (Voting phase)**

1. **Coordinator** sends a `PREPARE` message to all participants.
    
2. Each **Participant** executes the transaction locally (but does not commit yet).
    
3. Each participant replies with:
    
    - ✅ **Vote-Commit** (ready to commit), if local execution succeeded.
        
    - ❌ **Vote-Abort**, if something went wrong (e.g., constraint violation, failure).
        

#### **Phase 2: Commit (Decision phase)**

- If **all participants replied with Vote-Commit** →  
    Coordinator sends `COMMIT` to all, and each participant commits.
    
- If **any participant replied with Vote-Abort** →  
    Coordinator sends `ROLLBACK` to all, and each participant rolls back.

### 📌 Pros

- Ensures **strong consistency**.
    
- All-or-nothing guarantee across distributed systems.
    

### 📌 Cons

- **Blocking protocol**: If coordinator crashes after sending `"PREPARE"`, participants may hang in uncertain state.
    
- **Slow** compared to local commit (extra network round trips).
    
- Doesn’t handle network partitions well (can cause indefinite blocking).



## 3PC
**Three-Phase Commit** is an extension of the **Two-Phase Commit (2PC)** protocol.  
It was designed to **reduce blocking** problems in 2PC when the coordinator or participants crash.

It adds an **extra phase (pre-commit)** between _prepare_ and _commit_ to give participants more certainty about the final decision.

### 📌 Phases of 3PC

### **1. CanCommit? (Voting phase)**

- Coordinator sends `CAN_COMMIT?` to all participants.
    
- Participants reply:
    
    - ✅ **Yes** (if they can commit).
        
    - ❌ **No** (if they cannot commit).
        

### **2. PreCommit (Prepare-to-commit phase)**

- If **all said Yes**, coordinator sends `PRE_COMMIT` (a promise to commit).
    
- Participants write to log and send an acknowledgment back, but they **don’t commit yet**.
    
- If any participant said No → coordinator sends `ABORT`.
    

### **3. DoCommit (Final phase)**

- After receiving acknowledgments from all participants, the coordinator sends `DO_COMMIT`.
    
- Participants then **actually commit** the transaction.


### 📌 Key Difference vs 2PC

- In **2PC**, if coordinator crashes after “prepare” but before “commit/abort,” participants can be stuck in uncertainty.
    
- In **3PC**, the **extra PRE_COMMIT phase** ensures participants know the coordinator’s intent before the final commit.
    
- This makes 3PC a **non-blocking protocol** under certain assumptions (like reliable message delivery and bounded delay).


### 📌 Example Flow

1. Coordinator → P1, P2: `"CAN_COMMIT?"`
    
2. P1: `"Yes"`, P2: `"Yes"`
    
3. Coordinator → P1, P2: `"PRE_COMMIT"`
    
4. P1, P2 log the action and reply `"ACK"`
    
5. Coordinator → P1, P2: `"DO_COMMIT"`
    
6. P1, P2 commit.
    

If any node said **No** in step 2 → Coordinator sends `"ABORT"` directly.


## 📌 Pros & Cons

✅ **Advantages**

- Avoids indefinite blocking (participants can decide based on PRE_COMMIT state).
    
- Improves reliability compared to 2PC.
    

❌ **Disadvantages**

- More **network overhead** (extra phase).
    
- Still not perfect under **network partitions** (can lead to split-brain decisions).
    
- More complex implementation.


## 📌 Real-world use

- Rarely used in practice today.
    
- Modern distributed systems (Google Spanner, CockroachDB, etc.) prefer **consensus protocols (Paxos, Raft)** instead of 3PC.
    
- In microservices, people often choose **SAGA pattern** [[SAGA]] for business workflows.



## References

https://viblo.asia/p/distributed-transaction-two-phase-commit-naQZRBemZvx