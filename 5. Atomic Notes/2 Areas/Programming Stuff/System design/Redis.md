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

### Hot key problem

The **Hot Redis Key problem** occurs when a **single Redis key is accessed at very high frequency** (e.g., thousands or millions of times per second), which causes:

- **CPU/network bottlenecks** on the Redis server
    
- **Latency spikes or timeouts**
    
- **Uneven load** across Redis cluster nodes (if using Redis Cluster)
    
- Potential **DoS** (denial of service) if multiple clients hammer the same key

#### ✅ How to Detect a Hot Key

### 1. **Use `MONITOR` or `SLOWLOG`**

`redis-cli MONITOR | grep leaderboard:global`

Or:

`redis-cli SLOWLOG get`
### 2. **Use Redis `keyspace_hits`, `keyspace_misses`**

Track access stats per key.
#### 🔧 Mitigation Strategies

1. **Sharding / Key Hashing**

Instead of using one key, **split into multiple keys**:

`SET leaderboard:global:1 ... SET leaderboard:global:2 ...`

Then randomly or round-robin access among them.

2. **Local caching**
   If the hot key is **read-heavy**, cache it in the app:
   Use:
In-memory cache (e.g., Guava, Caffeine, LRU cache)
CDN or edge cache for frontend-related keys
3. **Use Batched Operations** 
4. Redis Cluster Partitioning
Use Redis Cluster with careful key distribution:
Avoid placing all traffic on one hash slot
Use hash tags only when needed ({tag} keeps keys on same slot)

5. Avoid Sorted Sets for Write-Heavy Workloads
Sorted Sets (ZADD) can be expensive under high write loads.
If you don't need ordering immediately, batch and insert later.

6. Use Streams or Pub/Sub for High-Write Events
For massive write workloads (e.g., logging, metrics), use:
Redis Streams (high throughput)
Kafka/RabbitMQ for real decoupling

🧠 Hot Key Rule of Thumb
🚫 Avoid any one key getting > 5–10% of total Redis ops/sec
✅ Use key-level metrics to spot hotspots early
🔄 Balance load before scaling Redis horizontally

|Strategy|When to Use|
|---|---|
|Shard keys|Any heavy-write or heavy-read key|
|Local cache|Frequent reads|
|Batch writes|High-frequency counters|
|Redis Streams / Queue|High write volume|
|Monitoring tools|Always|
|Redis Cluster balancing|Multi-node Redis deployments|

### Redis vs MongoDB
https://aws.amazon.com/vi/compare/the-difference-between-redis-and-mongodb/

| Feature                 | **Redis** 🟥                                                                  | **MongoDB** 🟩                                                      |
| ----------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| **Type**                | In-memory key-value store                                                     | Document-oriented database                                          |
| **Data Model**          | Key → Value (Strings, Hashes, Lists, Sets, Sorted Sets, Streams, etc.)        | JSON-like documents (BSON), nested fields, arrays                   |
| **Primary Use Case**    | Caching, real-time analytics, session store, pub/sub messaging                | Main application database, flexible schema storage                  |
| **Persistence**         | Optional (RDB snapshots, AOF logs, or both)                                   | Always persistent (journaling, WiredTiger engine)                   |
| **Performance**         | Extremely fast (sub-millisecond latency, 1M+ ops/sec)                         | Slower than Redis, but optimized for large persistent datasets      |
| **Scalability**         | Horizontal scaling via **Redis Cluster** (hash slots 0–16383)                 | Horizontal scaling via **Sharding**, replication with replica sets  |
| **Durability**          | Not strong by default (better for ephemeral/cache data)                       | Strong durability (designed as a system of record)                  |
| **Transactions**        | Atomic ops, MULTI/EXEC, Lua scripts                                           | ACID transactions (multi-document since v4.0)                       |
| **Advanced Features**   | Pub/Sub, Streams, Geo data, Bitmaps, HyperLogLog, Redlock (distributed locks) | Indexing, Aggregation pipelines, Geospatial queries, Change Streams |
| **Data Size**           | Limited by RAM (though Redis Enterprise supports disk-tiering)                | Handles very large datasets (terabytes → petabytes)                 |
| **Use in Architecture** | Usually a **supplementary store** (cache/queue alongside DB)                  | Usually the **primary database**                                    |
| **Best For**            | Speed, low latency, real-time workloads                                       | Flexible schema, persistence, complex queries                       |

Example: An **e-commerce app** might:

- Store **product catalog, orders, customers** → in **MongoDB**.
    
- Cache **hot products, shopping cart, user sessions** → in **Redis**.
    
- Use Redis for **real-time promotions / counters** (e.g., “X items left!”).


## References
https://redis.io/docs/latest/
ChatGPT