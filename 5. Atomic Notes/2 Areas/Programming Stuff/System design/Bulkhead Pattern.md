2025-10-31 16:03

TARGET DECK: [[system design]]
START
Basic
Bulkhead Pattern
Back:
## Main

### What
The **Bulkhead pattern** is a **resilience and isolation** pattern used in **system design** (especially microservices and distributed systems) to **prevent cascading failures** and **improve fault isolation**.
### 🧱 Concept

The term **“bulkhead”** comes from ship design — ships are divided into watertight compartments called _bulkheads_.  
If one compartment floods, the others remain intact and the ship doesn’t sink.

In software, the **Bulkhead pattern** does the same:

> It isolates different parts (or resources) of a system so that a failure in one part doesn’t bring down the whole system.
### 💡 Key Idea

You **divide your system into isolated pools** (threads, connections, services, etc.).  
Each pool handles a subset of requests or features.  
If one pool becomes overloaded or fails, others can continue functioning normally.

### 🏗️ Example Scenarios

#### 1. **Thread Pool Isolation**

Suppose your application makes external API calls to:

- **Payment Service**
    
- **Notification Service**
    

You create:

- Thread pool A → for Payment requests
    
- Thread pool B → for Notification requests
    

✅ If Payment service hangs, its thread pool gets blocked,  
but Notification service still works (because it uses a different pool).

#### 2. **Connection Pool Isolation**

A microservice connects to multiple databases or downstream services.  
Each has its **own connection pool** — this prevents one failing connection from exhausting all connections globally.

---

#### 3. **Microservice Isolation**

At a larger scale, each service (like `Order`, `Inventory`, `Billing`) can be deployed in **separate containers or pods** with their own CPU/memory quotas.  
If `Billing` crashes due to a spike, `Order` and `Inventory` remain healthy.


### ⚙️ Implementation Approaches

| Layer               | Example Implementation                                       |
| ------------------- | ------------------------------------------------------------ |
| **Code Level**      | Separate thread pools, async queues                          |
| **Network Level**   | Connection pool per downstream dependency                    |
| **Container Level** | Kubernetes pods with resource limits (`cpu`, `memory`)       |
| **Service Level**   | Independent microservices with separate autoscaling policies |

### 🧩 When to Use

Use the **Bulkhead pattern** when:

- You have **multiple remote dependencies** that may fail independently.
    
- You want to **avoid one bad dependency affecting all traffic**.
    
- You’re designing **high-availability systems** or **mission-critical APIs**.

### ⚠️ Trade-offs

|Pros|Cons|
|---|---|
|Fault isolation|More configuration complexity|
|Improved resilience|May underutilize resources if not balanced|
|Easier to recover|More monitoring required per partition|
### 🧠 Often Used With

The **Bulkhead pattern** is commonly combined with:

- **Circuit Breaker** 🧯 → stops calls to failing components
    
- **Retry + Timeout policies** ⏱️ → handle transient failures
    
- **Queue-based load leveling** 📨 → manage request spikes gracefully

### 💬 In Kubernetes or Cloud Environments

You can enforce the Bulkhead pattern by:

- Setting **CPU/memory limits** per pod (`resources.limits` in YAML)
    
- Using **separate deployments or namespaces**
    
- Applying **PodDisruptionBudgets** to control failure impact
    
- Configuring **different service meshes** for traffic segmentation

## References
END

DELETE
ID: 
