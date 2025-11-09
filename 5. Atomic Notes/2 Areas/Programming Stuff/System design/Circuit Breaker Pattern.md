2025-10-31 15:54

TARGET DECK: [[system design]]
START
Basic
Circuit Breaker Pattern
Back:
## Main
### What
The **Circuit Breaker pattern** is a **resilience pattern** used in **distributed systems** and **microservice architectures** to prevent cascading failures when a service or resource becomes unavailable or slow.

### 🧩 Concept

The idea comes from **electrical circuit breakers** — when there’s a surge (failure), the breaker trips and **stops the flow** to prevent further damage.

In software:

- When a **remote service** or **dependency** (like a database, API, or microservice) fails repeatedly, the circuit breaker **opens** and temporarily **stops requests** from being sent to that service.
    
- After a cooldown period, it tries again with limited traffic to see if the service has recovered.
### ⚙️ States of a Circuit Breaker

|State|Description|What Happens|
|---|---|---|
|**Closed**|Normal state|Requests flow normally. Failures are counted.|
|**Open**|Failure threshold reached|Requests are **blocked** immediately; fallback or error returned.|
|**Half-Open**|Recovery testing|Allows a few test requests to check if service is back. If successful → close again. If failed → open again.|

### 🔁 State Transition Diagram

![[Pasted image 20251031155753.png]]

### 🧠 Why Use It

Without this pattern, your system could:

- Keep sending requests to a failing service.
    
- Waste threads and resources waiting for timeouts.
    
- Cause **cascading failures** across other services.
    

Circuit breaker adds:  
✅ Fault isolation  
✅ Faster failure detection  
✅ System stability  
✅ Better user experience (via fallback responses)

### 🏗️ Example Use Case

Imagine you have:

- **Order Service** → depends on **Payment Service**
    

If the Payment Service goes down:

- Order Service tries several times → fails
    
- Circuit breaker opens → stops calling Payment Service temporarily
    
- After a while → tries again (half-open)
    
- If Payment Service recovers → resumes normal operations

### ## 🌐 In Kubernetes / Cloud Native Systems

Circuit breaker logic is often handled **at the network layer** via:

- **Service Meshes** like **Istio**, **Linkerd**
    
- These use **Envoy** proxies to track failure rates and open/close circuits automatically.

### 🧭 Related Patterns

|Pattern|Description|
|---|---|
|**Retry**|Try again after failure (Circuit Breaker often combines this).|
|**Timeout**|Limit how long to wait for a response.|
|**Bulkhead**|Isolate resources (e.g., threads) per service.|
|**Fallback**|Provide alternative response when failure occurs.|

## References
END

DELETE
ID: 
