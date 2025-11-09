2025-10-31 15:34

TARGET DECK: [[system design]]
START
Basic
Leader Election
Back:
## Main

### What? 

The **Leader Election Pattern** is a **distributed systems design pattern** used to ensure that, among a group of nodes (or services) in a cluster, **exactly one node acts as the “leader”** at any given time. The leader is responsible for coordinating actions or making decisions, while the others act as **followers** or **standby nodes**.

### Core Idea

When multiple instances of the same service are running (for redundancy, load balancing, or high availability), they often need a **single authoritative instance** to:

- Coordinate tasks (e.g., job scheduling, consensus, metadata updates)
    
- Manage distributed locks or shared state
    
- Avoid conflicts or duplicated work
    

Leader election ensures **only one instance** takes that role.

### How It Works

1. **All nodes start equally.**
    
    - Each node is capable of being a leader.
        
2. **Election process begins.**
    
    - Nodes communicate using a coordination system (like ZooKeeper, etcd, or Consul).
        
3. **One node is chosen as leader.**
    
    - Based on agreed criteria (e.g., lowest ID, fastest response, or first registration).
        
4. **Followers monitor the leader.**
    
    - If the leader fails or disconnects, the election restarts.
        
5. **New leader takes over.**

### Common Implementations

|Tool|Mechanism|Notes|
|---|---|---|
|**ZooKeeper**|Uses ephemeral znodes; the first node to create a znode becomes leader|Common in Apache Kafka, Hadoop|
|**etcd**|Uses Raft consensus algorithm|Kubernetes uses this|
|**Consul**|Uses distributed locks and sessions|Often used in service discovery|
|**Redis**|Uses Redlock for distributed lock-based leader election|Simpler setup|
|**Kubernetes**|Uses “LeaseLock” via API server|Common in controllers, operators|

## References
END

DELETE
ID: 
