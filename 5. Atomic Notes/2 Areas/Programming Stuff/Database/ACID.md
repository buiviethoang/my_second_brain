2025-08-19 22:23
Status: #baby
Tags: [[database]]
## Main
**ACID** is a set of properties that ensure reliable processing of **database transactions**. Each letter stands for one key property:

### 🔹 A – **Atomicity**

- A transaction is **all or nothing**.
    
- If one part of the transaction fails, the **entire transaction fails**, and the database state is **unchanged**.
    
- Example: Transferring money between two bank accounts — if the debit succeeds but the credit fails, the whole transaction is rolled back.
    

---

### 🔹 C – **Consistency**

- A transaction must bring the database **from one valid state to another valid state**.
    
- All data must follow **defined rules, constraints, and cascades**.
    
- Example: If your system says every order must have a valid customer ID, a transaction must ensure that it doesn’t create an order without one.
    

---

### 🔹 I – **Isolation**

- **Concurrent transactions** should not interfere with each other.
    
- The final result should be as if **transactions were executed one after the other**, even if they're processed in parallel.
    
- Example: Two people trying to buy the last item online — isolation ensures only one actually succeeds.
    

---

### 🔹 D – **Durability**

- Once a transaction is committed, its result is **permanently stored**, even in case of a system crash.
    
- It is written to **non-volatile storage** (like disk).
    
- Example: After a successful payment, the record stays safe, even if power goes out.

| Property    | What it ensures                         |
| ----------- | --------------------------------------- |
| Atomicity   | All or nothing execution                |
| Consistency | Valid data state before & after         |
| Isolation   | No side-effects from concurrent actions |
| Durability  | Committed data won’t be lost            |






## References