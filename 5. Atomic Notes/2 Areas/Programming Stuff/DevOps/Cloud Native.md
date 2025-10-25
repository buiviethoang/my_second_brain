2025-09-21 10:53
Status: 
Topic: 
Tags: [[cloud]]
## Main

**Cloud Native** refers to building and running applications that **leverage the advantages of the cloud** — scalability, resilience, automation, and speed of deployment.

It’s not just "putting your app on AWS/GCP/Azure", but **designing applications to thrive in cloud environments**.

### **Key Characteristics of Cloud Native Applications**

1. **Microservices Architecture**
    
    - Applications are broken into small, independent services.
        
    - Each service can be developed, deployed, and scaled independently.
        
2. **Containerization**
    
    - Services are packaged with their dependencies into containers (Docker, Podman).
        
    - Ensures portability across environments (dev → test → prod).
        
3. **Dynamic Orchestration**
    
    - Use orchestrators like **Kubernetes** to handle scaling, load balancing, self-healing, and deployments.
        
4. **DevOps & CI/CD**
    
    - Automated pipelines for building, testing, and deploying.
        
    - Frequent, reliable releases.
        
5. **Observability**
    
    - Built-in monitoring, logging, and tracing (Prometheus, Grafana, ELK, OpenTelemetry).
        
    - Apps are designed to be monitored.
        
6. **Resilience & Scalability**
    
    - Auto-scaling to handle spikes.
        
    - Fault-tolerance (if a container crashes, it restarts automatically).

### **Cloud Native ≠ Cloud Hosted**

- **Cloud Hosted:** You take your old monolithic app and run it on a cloud VM.
    
- **Cloud Native:** You re-architect the app to take advantage of containers, microservices, auto-scaling, etc.


### **Why Cloud Native?**

- Faster development cycles (release multiple times a day).
    
- Better scalability (elastic scaling per service).
    
- Cost optimization (pay only for what you use).
    
- Easier recovery from failures (self-healing, redundancy).


In interviews, a good one-liner is:

> _“Cloud Native means designing applications that are containerized, dynamically orchestrated, resilient, observable, and built around microservices with CI/CD pipelines, so they can fully leverage the benefits of cloud environments.”_





## References