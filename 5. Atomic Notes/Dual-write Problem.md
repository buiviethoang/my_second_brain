2025-11-04 22:05

TARGET DECK: [[microservices]]
START
Basic
Dual-write Problem
Back:
## Main

The **Dual-write problem** (also called **dual-writes issue**) is a common challenge in **distributed systems** and **microservices architectures** — especially when two or more systems (like a database and a message queue, or two microservices) must be updated as part of a **single logical operation**.

## 🧩 The problem

A **dual-write** occurs when one service or process **writes to two different systems** separately — for example:

1. **Write #1:** Save data to a database.
    
2. **Write #2:** Send an event/message to a message queue (e.g., Kafka, RabbitMQ) to notify other services.
    

These two writes are **not atomic**, because they belong to **different systems** that do not share a single transaction boundary.

If the service crashes between the two writes — or if one write succeeds but the other fails — the systems become **inconsistent**

## ⚠️ Example

Imagine an **Order Service** that needs to:

1. Save an order in the database (`orders` table).
    
2. Publish an event `OrderCreated` to Kafka so other services (e.g., inventory, shipping) can react.

What could go wrong?

|Step|Action|Status|
|---|---|---|
|1|`saveOrderToDatabase(order)`|✅ success|
|2|`kafkaProducer.send()`|❌ failed (network issue)|

Now your DB says the order exists, but Kafka never sent the event → other services don’t know about it → **data inconsistency**.

The reverse order has the opposite risk: the event is published, but the database write fails → **ghost events**.

## 💣 Consequences

- **Inconsistent data** between systems
    
- **Lost messages** or **duplicate processing**
    
- **Hard-to-debug race conditions**
    
- Violated **data integrity** and **business invariants**

## 💡 Solutions

There are several design patterns to handle this problem depending on your architecture:

### 1. **Transactional Outbox Pattern**

Instead of sending directly to the message queue, you:

- Write the database record **and** the event message into the **same database transaction** (an “outbox” table).
    
- A background process or CDC (Change Data Capture) reads from the outbox and safely publishes to the message queue.
    

✅ Pros: atomic with DB  
❌ Cons: adds some latency

> → Very common and reliable for microservices.


### 2. **Change Data Capture (CDC)**

Tools like **Debezium** or **AWS DMS** can listen to database transaction logs and automatically publish changes to Kafka.

✅ Pros: No application changes required  
❌ Cons: More infra complexity, sometimes eventual consistency delay


### 3. **Distributed Transaction / Two-Phase Commit (2PC)**

Try to make both systems participate in a **single distributed transaction** (e.g., XA transaction).

✅ Pros: Atomic across systems  
❌ Cons: Heavy, slow, often not scalable for microservices

### 4. **Idempotent consumers + retry**

Make your consumers idempotent and allow retries in case one of the writes fails.

✅ Pros: Simpler to implement  
❌ Cons: Doesn’t guarantee atomicity, only mitigates side effects

|Approach|Atomic|Complexity|Common Use|
|---|---|---|---|
|Dual-write (naive)|❌ No|Low|Dangerous|
|Outbox pattern|✅ Yes|Medium|Most popular|
|CDC|✅ Yes|Medium–High|Modern event-driven|
|Distributed TX (2PC)|✅ Yes|High|Legacy enterprise systems|
|Retry + idempotent consumer|❌ No|Medium|Supplementary fix|

## References
END

DELETE
ID: 
