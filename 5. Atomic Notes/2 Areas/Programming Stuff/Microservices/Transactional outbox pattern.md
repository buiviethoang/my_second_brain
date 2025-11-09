2025-09-22 09:15
Status: 
Topic: 
Tags: [[microservices]]
## Main
The **Transactional Outbox pattern** is a technique used to ensure **reliable communication** between a service’s database and external systems (e.g., message brokers, event streams, or other microservices). It solves the **dual-write problem** [[Dual-write Problem]]: how to update your local database _and_ publish an event/message atomically without inconsistencies.


## 🔹 The Problem

Imagine a service that:

1. Updates its own database (e.g., create an order).
    
2. Publishes an event to Kafka/RabbitMQ (e.g., `OrderCreated`).
    

If these two steps are done separately:

- The database update may succeed, but message publishing fails → external systems never know about the new order.
    
- The message may be published, but the database update fails → consumers react to an event that never truly happened.
    

This creates **inconsistencies**.


## 🔹 The Solution: Transactional Outbox

Instead of trying to commit to both the DB and the broker in one transaction (which is not possible across distributed systems without 2PC), you use your database as the **source of truth**.

1. **Write the business entity + an "outbox entry"** into the same database transaction.
    
    - Example: Insert `Order` row and an `Outbox` row (`event_type = OrderCreated, payload = {...}`).
        
    - Since it’s a single transaction, both succeed or fail together.
        
2. **A separate process (poller/relay)** reads the outbox table and publishes the events/messages to the broker.
    
    - This is usually **idempotent** (to avoid duplicate sends).
        
    - Once published successfully, the outbox entry is marked as sent (or deleted).

## 🔹 Flow Example

1. User creates an order → service inserts:
    
    - `orders` table: new order row.
        
    - `outbox` table: new row with `{ eventType: "OrderCreated", payload: {...} }`.
        
2. Transaction commits → data and event are guaranteed consistent.
    
3. Outbox publisher service/process reads the outbox table.
    
4. Publishes `OrderCreated` to Kafka.
    
5. Marks outbox entry as processed.


## 🔹 Benefits

- **Atomicity**: DB write and event persistence happen together.
    
- **Reliability**: No lost events.
    
- **Decoupling**: External systems rely on events, not direct DB calls.
    
- **Scalability**: Outbox processor can batch events.

## 🔹 Challenges

- **Outbox table growth** → requires cleanup strategy (TTL, archiving).
    
- **Delivery semantics**:
    
    - At least once → duplicates possible, need idempotent consumers.
        
    - Exactly once → harder, often left to consumers to deduplicate.
        
- **Latency**: Slight delay between DB commit and event publishing.


## 🔹 Variants

- **Polling publisher**: Periodically polls the outbox table.
    
- **Change Data Capture (CDC)**: Tools like **Debezium** stream DB changes directly to Kafka → no custom poller needed.
    
- **Event streaming DBs**: Some databases natively support event publishing.


### TOP vs Saga [[SAGA]]

|Feature / Aspect|**Transactional Outbox**|**Saga Pattern**|**Two-Phase Commit (2PC)**|
|---|---|---|---|
|**Problem solved**|Reliable event publishing (DB + message consistency).|Distributed transaction consistency across multiple services.|Distributed transaction atomicity across multiple databases/resources.|
|**Scope**|**Within a single service** (local DB + outbox + event broker).|**Across multiple services** (workflow with compensations).|**Across multiple resources** (databases, queues) in one global transaction.|
|**Approach**|Write DB + outbox in one transaction, later publish event.|Sequence of local transactions with compensation on failure.|Coordinator asks all participants: Prepare → Commit/Rollback.|
|**Consistency type**|Atomic local consistency (no lost events).|Eventual consistency across services.|Strong consistency (all-or-nothing).|
|**Failure handling**|Retry outbox publishing; idempotency needed.|Compensation logic (undo steps).|Rollback coordinated by transaction manager.|
|**Complexity**|Medium (extra outbox + publisher/CDC).|High (requires design of compensations, orchestration/choreography).|Very high (distributed locks, global coordinator).|
|**Performance**|High throughput (async publishing).|Moderate (many services, retries, compensations).|Low (blocking, poor scalability).|
|**Scalability**|Scales well (decoupled event publishing).|Scales well (async, no global locks).|Poor (global coordinator is bottleneck).|
|**Typical use case**|Order service saves DB + emits `OrderCreated` reliably.|Order workflow: Order → Payment → Inventory → Shipping (with rollback if payment fails).|Bank transfer between two accounts in different databases (strict atomicity).|
|**Trade-offs**|Slight latency; requires cleanup of outbox.|Complex error handling; eventual consistency.|Strong consistency but bad availability & scalability.|

### CDC related [[Change Data Capture]]

## References