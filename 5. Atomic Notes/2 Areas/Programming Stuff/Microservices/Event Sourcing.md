2025-08-19 22:02
Status: #baby
Tags: [[system design]] [[microservices]]
## Main
## 1. **What is Event Sourcing?**

**Event Sourcing** is a pattern where instead of storing the **current state** of an entity (like a row in a database), you store **all the events that led to the current state**. The system reconstructs the current state by replaying these events.

- **State = replay(events)**
    
- Each event represents a **fact that happened** in the system.


### 2. **How It Works**

1. **Commands trigger events**
    
    - A command asks the system to do something.
        
    - Example: `PlaceOrder(orderId, items)`.
        
2. **Validation**
    
    - Business logic checks if the command is valid (e.g., items are in stock).
        
3. **Generate events**
    
    - If valid, events are created and stored.
        
    - Example events:
        
        - `OrderPlaced(orderId, userId, items)`
            
        - `OrderPaid(orderId, amount)`
            
4. **Event Store**
    
    - A specialized storage for events (like an append-only log).
        
    - Events are **immutable** and stored in order.
        
5. **Rebuild state**
    
    - When you need the current state, you **replay all events** for that entity.
        
    - Example:
        
        `Events: 1. OrderPlaced 2. OrderPaid 3. OrderShipped Rebuild → Order status = Shipped`
        

---

### 3. **Benefits of Event Sourcing**

- **Audit trail:** Every change is stored; you can see the full history.
    
- **Flexibility:** You can rebuild state or read models if needed.
    
- **Temporal queries:** You can query the state at any point in time.
    
- **Integration-friendly:** Events can be published to other systems or microservices.
    

---

### 4. **Drawbacks**

- More complex than storing current state.
    
- Event versioning: if events change structure, you must handle old events.
    
- Requires **replaying events** to rebuild state (can be slow if many events; snapshotting helps).
    

---

### 5. **Example**

Suppose we have an order system:

**Events:**

1. `OrderPlaced(orderId=123, userId=1, items=[a, b])`
    
2. `ItemAdded(orderId=123, item=c)`
    
3. `OrderPaid(orderId=123, amount=100)`
    

**Current state** is **not stored directly**. To get it, we replay events:

`Order 123: - Items: [a, b, c] - Paid: 100 - Status: Paid`

---

Event Sourcing works very well with **CQRS**, because the **write model stores events**, and **read models are updated from events** asynchronously.

![[Pasted image 20250819220953.png]]


## References
https://microservices.io/patterns/data/event-sourcing.html
https://viblo.asia/p/event-sourcing-la-gi-gwd43zDXVX9