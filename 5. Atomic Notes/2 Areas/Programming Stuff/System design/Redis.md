2025-07-24 07:08
Status: #baby
Tags: [[computer science]] [[system design]] [[database]]
## Main
### What? 
Redis (REmote DIctionary Server) is an **in-memory data structure store** often used as a **database, cache, or message broker**. It is **fast**, **lightweight**, and supports rich data types.
### Why use? 
1. Blazing Fast Performance 🚀
Redis stores everything in memory → sub-millisecond read/write
Useful for real-time applications (web, gaming, analytics, etc.)
2. Powerful Data Structures
Beyond simple key-value:
Lists (queues, logs)
Hashes (objects, sessions)
Sets (tags, uniqueness)
Sorted Sets (leaderboards, priority queues)
Bitmaps, HyperLogLogs, Streams
Enables elegant solutions without a relational DB
3. Ideal for Caching 🔁
Cache database queries, HTTP responses, or sessions
Example:
Query a slow DB once → store result in Redis
Next requests use fast Redis instead of DB
4. Atomic Operations 🔒
All commands are atomic
Prevent race conditions in concurrent environments
5. Built-In Pub/Sub and Stream Messaging 📢
For event-driven or real-time systems (e.g. chat apps)
Lightweight alternative to Kafka/RabbitMQ for some use cases
6. Scalable and Distributed
Supports replication, clustering, high availability
Enterprise-grade setups are possible (e.g. Redis Sentinel, Redis Cluster)
7. Time-To-Live (TTL) Support
Auto-expire data (e.g. OTP, token, session)
SET key value EX 60 → expires in 60 seconds

### Use cases 

| Use Case        | Redis Feature                     |
| --------------- | --------------------------------- |
| Caching         | `EXPIRE`, `TTL`, `SETEX`          |
| Rate limiting   | Atomic INCR + TTL                 |
| Session storage | Simple `SET`, `GET`, expiration   |
| Message queues  | `LPUSH` + `BRPOP` (List as queue) |
| Pub/Sub         | `PUBLISH` / `SUBSCRIBE`           |

### ❓When Should You Use Redis?

Use Redis **when you need**:
- High performance and low latency
- Temporary data (cache, session, token)
- Real-time processing (chat, tracking, game scoreboards)
- Fast access to frequently used data
- Lightweight messaging (Pub/Sub)
- Non-relational storage for structured data


### 🚫 When **Not** to Use Redis

- When data **must** persist on disk forever (consider a database)
- If your dataset is **too large to fit in memory**
- If you need **complex queries or joins** (use relational DB)
- If you need strict **ACID transactions** (Redis is atomic but not fully ACID)

### Best practice

![[Pasted image 20250724213326.png]]
### Redis Sentinel vs Redis Cluster

**Redis Sentinel** is a built-in system that provides:

1. **Monitoring**: Checks if your Redis master or replicas are working.
    
2. **Automatic Failover**: If the master crashes, Sentinel promotes a replica to master.
    
3. **Notification**: Alerts your app or admin of issues.
    
4. **Service Discovery**: Your app can ask Sentinel for the current master address.
    

In short:

> 🛡️ **Sentinel keeps Redis available and self-healing** in case of failures.

| Feature                      | **Redis Sentinel**                                 | **Redis Cluster**                            |
| ---------------------------- | -------------------------------------------------- | -------------------------------------------- |
| 🧱 **Main Purpose**          | High Availability (failover + monitoring)          | High Availability **+** Data Partitioning    |
| 🧠 **Data Sharding**         | ❌ No                                               | ✅ Yes (via hash slots)                       |
| 🤕 **If master fails**       | Replica promoted, clients reconnected via Sentinel | Replica takes over slot range automatically  |
| 🔁 **Client Responsibility** | Uses Sentinel to discover master                   | Must handle redirects (`MOVED`)              |
| 🧮 **Horizontal Scaling**    | ❌ Limited (all nodes store full dataset)           | ✅ Yes (data split across nodes)              |
| 👥 **Replication**           | Master-replica (1 primary, N replicas)             | Each slot has master + replicas              |
| 📦 **Use Case**              | Small-medium datasets, cache, failover safety      | Large datasets, write-heavy, sharding needed |

![[Pasted image 20250724214625.png]]

o **retrieve data from a Redis Cluster**, your **client must be cluster-aware**, because Redis Cluster **partitions data** using **hash slots** (0 to 16,383), and different keys may live on different nodes.
## References
https://redis.io/docs/latest/
ChatGPT