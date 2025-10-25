2025-09-22 08:50
Status: 
Topic: 
Tags: [[microservices]] 
## Main
The **SAGA pattern** is a **distributed transaction management pattern** used in **microservices architectures**.

Instead of a traditional 2-phase commit [[2-Phase Commit, 3-Phase commit]] (which is heavy and doesn’t scale well in distributed systems), a SAGA breaks a long-lived transaction into a **series of local transactions**. Each service updates its own data and then publishes an **event** or calls the next service.

If one local transaction fails, the SAGA executes **compensating transactions** to undo the preceding steps.

### 🔑 Key Ideas

- **Chained local transactions:** Each service commits independently.
    
- **Compensation instead of rollback:** Instead of rolling back everything (like in databases), failed steps are undone by compensating actions.
    
- **Asynchronous or synchronous:** Services can communicate via events (asynchronous) or direct API calls (synchronous).


### 🛠️ Two Common Saga Execution Styles

1. **Choreography (Event-driven)**
    
    - No central coordinator.
        
    - Each service listens for events and decides what to do.
        
    - Simpler, but can get messy with too many events.
        
    
    Example:
    
    - Order Service → `OrderCreated` event
        
    - Payment Service → listens, reserves payment → `PaymentReserved`
        
    - Inventory Service → listens, decreases stock → `StockDecreased`
        
    - Shipping Service → listens, prepares shipment
        
    
    If one fails, compensation events are triggered (e.g., release payment, restock).


![[Pasted image 20250922085433.png]]
    
2. **Orchestration (Central controller)**
    
    - A central **Saga Orchestrator** coordinates the workflow.
        
    - Orchestrator tells each service what to do and interprets responses.
        
    - Easier to follow but introduces a single coordination point.
        
    
    Example:
    
    - Orchestrator → calls Payment Service
        
    - Orchestrator → calls Inventory Service
        
    - Orchestrator → calls Shipping Service
        
    - If Payment fails, orchestrator calls “cancel order”.


![[Pasted image 20250922085458.png]]



### 🧩 Example in E-commerce

Imagine placing an order:

1. **Order Service**: Create an order (pending).
    
2. **Payment Service**: Reserve funds.
    
3. **Inventory Service**: Deduct stock.
    
4. **Shipping Service**: Schedule delivery.
    

If **Inventory Service fails**, then:

- Payment Service → refund payment (compensation).
    
- Order Service → mark order as "canceled".


### ✅ When to Use

- Long-lived transactions across microservices.
    
- Business processes where steps can be **compensated**.
    
- High availability systems where **blocking locks (2PC)** are unacceptable.


### Saga vs 2PC vs 3PC

| Feature              | **2PC (Two-Phase Commit)**                             | **3PC (Three-Phase Commit)**                        | **SAGA Pattern**                                                                                       |
| -------------------- | ------------------------------------------------------ | --------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| **Main Goal**        | Strong consistency across distributed systems          | Reduce blocking issues in 2PC                       | Long-running business transactions across microservices                                                |
| **Phases**           | 2 (Prepare → Commit/Rollback)                          | 3 (CanCommit → PreCommit → DoCommit)                | Sequence of local transactions + compensating actions                                                  |
| **Consistency**      | ✅ Strong (all-or-nothing)                              | ✅ Strong (all-or-nothing)                           | ⚠️ Eventual consistency                                                                                |
| **Availability**     | ❌ Can block if coordinator fails                       | ✅ Non-blocking (under assumptions)                  | ✅ High availability (no global lock)                                                                   |
| **Performance**      | ❌ Slower (2 network round trips)                       | ❌ Even slower (3 round trips)                       | ✅ Faster (each service commits locally)                                                                |
| **Failure Handling** | Blocking if coordinator crashes after prepare          | Safer than 2PC, but still complex under partitions  | Compensating transactions handle failures                                                              |
| **Use Cases**        | Distributed databases, financial transactions          | Rare in practice (academic interest)                | Microservices, e-commerce, workflows                                                                   |
| **Example**          | Bank A debit + Bank B credit in one atomic transaction | Same as 2PC but more resilient to coordinator crash | Order service + Payment service + Inventory service with compensations (cancel order, refund, restock) |
| **Complexity**       | Medium                                                 | High                                                | Medium-High (compensations must be defined)                                                            |


## References
