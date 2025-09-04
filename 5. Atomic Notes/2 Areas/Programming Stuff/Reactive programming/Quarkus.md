2025-07-14 21:08
Status: #baby
Tags: [[java]]
## Main
### What? 

**Quarkus** is a modern, Kubernetes-native Java framework designed for building **cloud-native**, **container-first** applications with fast startup times and low memory usage. It's tailored for **GraalVM** and **HotSpot**, enabling both traditional JVM deployment and native compilation.

### Why use it? 

|Feature|**Quarkus**|**Spring Boot**|
|---|---|---|
|**Startup Time**|Very fast (esp. in native mode)|Slower due to reflection, autoconfig, and classpath scanning|
|**Memory Usage**|Very low (esp. in native mode)|Higher memory footprint|
|**Build Target**|Optimized for GraalVM native image|JVM-first, GraalVM support improving|
|**Developer Experience**|Live reload via `quarkus:dev`, fast builds|Strong tooling and ecosystem|
|**Community & Ecosystem**|Smaller but growing (Red Hat-backed)|Large, mature ecosystem with massive adoption|
|**Microservice Fit**|Excellent (designed for it)|Also great, but heavier|
|**Container & Cloud Ready**|Yes (lightweight, fast boot ideal for Kubernetes)|Yes, but needs tuning for resource-sensitive environments|
|**Reactive Support**|Built-in with Mutiny and Vert.x|Optional via Project Reactor|

Let’s say you have a microservice running in a container:

| Framework        | Startup Time | Memory Footprint |
| ---------------- | ------------ | ---------------- |
| Spring Boot      | 2.5 seconds  | 150 MB           |
| Quarkus (JVM)    | 1.0 seconds  | 90 MB            |
| Quarkus (Native) | 0.05 seconds | 20 MB            |
**Memory footprint** = how much memory (RAM) your app uses.


#### GraalVM

**GraalVM** is a **high-performance runtime** that supports multiple languages (like Java, JavaScript, Python, Ruby, R, and more) and provides powerful capabilities for **running Java programs faster** and **compiling them into native binaries**.

|Feature|What It Means|
|---|---|
|🔧 **JIT Compiler**|Just-In-Time compiler that improves performance of Java applications.|
|🧊 **Native Image**|Converts Java apps into **standalone native executables** (no JVM needed).|
|🧬 **Polyglot Support**|Run JavaScript, Python, Ruby, R, and more on the same runtime as Java.|
|🧩 **Interop Between Languages**|Different languages (e.g. Java + Python) can call each other inside GraalVM.|
|🌐 **Truffle Framework**|Enables building interpreters for new languages.|

##### 🆚 JVM vs Native Image (GraalVM)

|Feature|JVM (HotSpot)|GraalVM Native Image|
|---|---|---|
|Startup Time|1–3 seconds or more|< 100 milliseconds|
|Memory Usage|Higher (JVM overhead)|Lower (no JVM runtime)|
|Runtime Speed|Fast|Very fast startup; may be slower for long runs unless tuned|
|Size|Needs JVM installed|Single executable binary|
#### Vert.x
**Eclipse Vert.x** is a **toolkit for building reactive applications** on the Java Virtual Machine (JVM). It’s designed for **high concurrency** with **non-blocking, event-driven** architecture.

##### Key Features:

- **Asynchronous and non-blocking**: Handles many concurrent connections efficiently using a small number of threads.
    
- **Polyglot**: Supports multiple languages (Java, Kotlin, JavaScript, etc.).
    
- **Verticles**: Units of deployment and concurrency in Vert.x (like micro-units of logic).
    
- **Event Bus**: Lightweight messaging system for communication between components (even across JVMs).
    
- **Built on Netty**: Provides high-performance networking.
    

##### 🧠 When to use Vert.x:

- Real-time systems (e.g., messaging, chat apps)
    
- High-throughput APIs or services
    
- Microservices where performance and scalability are key

#### Mutiny
**Mutiny** is a **reactive programming library** created by the Quarkus team. It is built on top of **Reactive Streams**
Relationship to Vert.x:
Mutiny wraps Vert.x’s reactive types (Future, ReadStream, etc.) into its own unified API to make it easier and more readable. It's essentially "Reactive for Humans"

|Type|Purpose|
|---|---|
|`Uni<T>`|Represents a **single async item**|
|`Multi<T>`|Represents a **stream of items**|

| Aspect                   | **Vert.x**                        | **Mutiny**                            |
| ------------------------ | --------------------------------- | ------------------------------------- |
| Type                     | Toolkit / Framework               | Library                               |
| Purpose                  | Reactive apps, event-driven logic | Simplified reactive programming       |
| Style                    | More manual, lower-level          | More declarative and fluent           |
| Integration with Quarkus | Directly integrated               | Native part of Quarkus' reactive APIs |
## Why use Mutiny and Vert.x in **Quarkus**?

- Quarkus uses **Vert.x** under the hood for **I/O**, **web**, and **messaging**.
    
- Quarkus provides **Mutiny** as the main reactive API for developers.
    
- This combination offers:
    
    - 🚀 High performance (thanks to Vert.x)
        
    - 🧘‍♂️ Cleaner code and better DX (thanks to Mutiny)




## References