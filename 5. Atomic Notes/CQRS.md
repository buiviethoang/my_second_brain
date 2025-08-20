2025-08-19 21:54
Status: #baby
Tags: [[system design]]
## Main
QRS stands for **Command Query Responsibility Segregation**. It’s an architectural pattern in software design that separates **reading** data from **writing** data. The main idea is that the models used to **update information** (commands) are separate from the models used to **read information** (queries).

### 1. **Core Concept**

- **Command**: Any operation that **modifies state**. For example: creating an order, updating a user profile.
    
- **Query**: Any operation that **retrieves data** without modifying it. For example: getting order details, listing users.
    

By separating these responsibilities, you can optimize each side independently.

### 2. **Why Use CQRS?**

- **Scalability**: Read and write workloads can scale independently.
    
- **Performance**: Read models can be optimized for queries without affecting write models.
    
- **Simplicity of logic**: Commands focus only on validations and business logic, queries focus on reporting/aggregation.
    
- **Event-driven possibilities**: Often used with **Event Sourcing** [[Event Sourcing]], where every change is an event that can update read models asynchronously.

### 3. **Typical Architecture**

![[Pasted image 20250819215727.png]]



## References
https://viblo.asia/p/cqrs-design-pattern-trong-kien-truc-microservices-PAoJexlZ41j