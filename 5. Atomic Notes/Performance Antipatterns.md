2025-07-27 15:08
Status: #baby
Tags: [[computer science]] [[system design]]
## Main
### Chatty I/O
**Chatty I/O** refers to a communication pattern where a system (often a client or service) makes **many small input/output (I/O) requests** in rapid succession, rather than **batching them** or sending them in a more efficient manner.

#### 🧠 Characteristics of Chatty I/O

- Frequent, small I/O operations
    
- High **round-trip time (RTT)** cost per operation
    
- Poor **throughput**
    
- Can overload network or CPU with many small tasks
#### 🧱 Examples

### 1. **REST API**

Instead of:

`GET /user/1 GET /user/2 GET /user/3`

You should prefer:

`POST /users/batch Body: [1, 2, 3]`

### 2. **Database Access**

Bad:
`SELECT * FROM orders WHERE id = 1; SELECT * FROM orders WHERE id = 2;`

Better:
`SELECT * FROM orders WHERE id IN (1, 2);`

### 3. **Remote Procedure Calls (RPC)**

Calling a remote service for every small field update is chatty. Instead, group multiple updates into one payload.

## ✅ How to Avoid Chatty I/O

|Strategy|Description|
|---|---|
|**Batching**|Combine multiple requests into one|
|**Caching**|Avoid redundant data retrievals|
|**Async/Streaming APIs**|Use bulk or streamed data interfaces|
|**Protocol Optimization**|Prefer gRPC or binary protocols over REST|
|**Lazy Loading / Prefetch**|Load data only when needed, or pre-load it|

### No Caching

### Busy Database
....

## References

https://roadmap.sh/system-design