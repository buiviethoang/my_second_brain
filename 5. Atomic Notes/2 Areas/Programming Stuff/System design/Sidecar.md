2025-10-31 15:16

TARGET DECK: [[system design]] 
START
Basic
Sidecar
Back:
## Main

### 1. What Is the Sidecar Pattern?

The **Sidecar pattern** is a **deployment design pattern** where you run a **helper service (the “sidecar”) alongside a main service (the “application container”)** within the same environment — usually the same **pod** in Kubernetes or the same **VM/container**.

The sidecar is **tightly coupled in deployment** but **loosely coupled in functionality**.  
It _extends or enhances_ the main service without modifying its code.

### 2. The Core Idea

Think of a sidecar attached to a motorcycle:

- The motorcycle = your main service.
    
- The sidecar = an auxiliary unit that adds features (storage, communication, monitoring, etc.) without changing the main vehicle’s mechanics.
    

The two share:

- The same **lifecycle** (start/stop together),
    
- The same **network namespace**, and often
    
- The same **storage volumes**.

### 3. Why Use It?

The Sidecar pattern enables **separation of concerns** and **reusability**:

- You can keep your main service focused only on **business logic**.
    
- You offload **infrastructure-related tasks** (like logging, service discovery, authentication, rate limiting, etc.) to the sidecar.

### 4. Common Use Cases

| Use Case                           | Description                                                                                                                    |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **Service Mesh Proxy**             | A sidecar proxy (like Envoy) handles all inbound/outbound network traffic for the app. Used in Istio, Linkerd, Consul Connect. |
| **Logging Agent**                  | A Fluentd or Vector sidecar collects logs from the main app and ships them to Elasticsearch, Loki, etc.                        |
| **Metrics/Monitoring**             | A Prometheus exporter runs as a sidecar, exposing metrics from the main app.                                                   |
| **Configuration Synchronizer**     | A sidecar watches config changes in a central store (e.g., Consul or etcd) and updates the main app’s config.                  |
| **Security / TLS Termination**     | A sidecar manages certificates, performs mTLS, or injects auth headers.                                                        |
| **Data Synchronization / Caching** | A local cache (Redis, SQLite) runs as a sidecar to accelerate reads/writes.                                                    |

### 5. Architecture Diagram (Conceptually)

![[Pasted image 20251031152153.png]]



## References
END

DELETE
ID: 
