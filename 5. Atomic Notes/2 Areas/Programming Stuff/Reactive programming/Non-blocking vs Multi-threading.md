2025-07-14 21:44
Status: #baby
Tags: [[java]]
## Main

**Non-blocking** and **multi-threading** are both strategies to achieve **concurrency** (doing multiple things at once), but they work **very differently**.

| Concept        | **Non-Blocking**                               | **Multi-Threading**                           |
| -------------- | ---------------------------------------------- | --------------------------------------------- |
| Core Idea      | Don’t wait → continue and use a callback       | Use separate threads to do things in parallel |
| Threads Used   | Few threads (usually event loop)               | Many threads                                  |
| Blocking Calls | Avoided (I/O must be async)                    | Allowed (each thread can block)               |
| Scalability    | Highly scalable (low memory)                   | Limited by thread count (RAM & CPU)           |
| Complexity     | Requires async mindset, callback/future chains | Easier with simple thread model               |
| Performance    | Excellent under I/O-heavy workloads            | Better for CPU-bound or blocking tasks        |
|                |                                                |                                               |


### 🧠 **What Is Multi-Threading?**

> Each **thread** runs in parallel, independently of others.

✅ Pros:

- Simple to understand.
    
- Good for **CPU-bound** or **blocking I/O** tasks.
    

❌ Cons:

- Threads are **heavyweight** (1MB+ stack, context switching).
    
- Limited number of threads (~1000s depending on system).
    
- Hard to manage: race conditions, deadlocks.


### ⚙️ **What Is Non-Blocking?**

> You **don’t wait** for something to complete. Instead, you register a **callback** to be notified **when it's ready**.

✅ Pros:

- **Lightweight**, uses **few threads**.
    
- Handles **thousands of concurrent I/O** requests efficiently.
    

❌ Cons:

- Code can be harder to follow (chaining, callbacks).
    
- Not ideal for **CPU-intensive** work

### 🧪 **Concrete Example**

Imagine you're a waiter in a restaurant.

- **Blocking/Multi-threading**:  
    Each waiter serves **one table** and **waits** until that table is finished eating. If you have 10 tables, you need 10 waiters.
    
- **Non-blocking (event loop)**:  
    One waiter takes an order, **hands it to the kitchen**, and while waiting, serves **other tables**. You only need **1-2 waiters** for 10 tables.

|Framework|Model Used|
|---|---|
|**Spring MVC**|Multi-threaded (Tomcat)|
|**Spring WebFlux**|Non-blocking (Reactor)|
|**Quarkus (Reactive)**|Non-blocking (Mutiny + Vert.x)|
|**Java EE**|Multi-threaded|

### Summary
|Feature|**Non-Blocking**|**Multi-Threading**|
|---|---|---|
|Threads|Few (event loop)|Many|
|Blocking Calls|Avoided|Common|
|I/O Efficiency|High|Lower|
|CPU-bound Suitability|Not ideal (should offload)|Better|
|Memory Usage|Low|High|
|Code Complexity|Higher (callbacks, futures)|Simpler (straight-line code)|
|Common In|Quarkus, Node.js, Netty, Vert.x|Tomcat, Spring MVC, Java Threads|


## References