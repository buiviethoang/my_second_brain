2025-07-26 22:23
Status: #baby
Tags: [[system design]]
## Main

### What? 
**Horizontal scaling** (also known as **scale-out**) is the process of adding **more machines or nodes** to your system to handle increased load or traffic. This is in contrast to **vertical scaling** (scale-up), which means upgrading the existing machine (e.g., more CPU, RAM).

### 🏗 Example:

Imagine you run a web application.

- **Vertical scaling**: You upgrade your single server from 8 GB RAM to 32 GB.
    
- **Horizontal scaling**: You add **more servers**, each with 8 GB RAM, and distribute the load across them.


### 🔄 Key Characteristics:

- Involves **adding instances** of services or servers.
    
- Often uses **load balancers** to distribute traffic.
    
- More fault-tolerant: if one machine fails, others can still serve traffic.
    
- Common in **cloud environments** (AWS, GCP, Azure) using auto-scaling groups.

### 📌 When to Use:

- When your system hits hardware or performance limits on a single machine.
    
- For web apps, microservices, or distributed systems.
    
- To support high availability and redundancy.


## References