2025-07-14 21:32
Status: #baby
Tags: 
## Main

### What? 
The **event loop** is a programming construct that **waits for events**, picks them up when they occur, and **processes them one at a time**, in a loop.
### Where? 
The event loop is used in non-blocking, asynchronous environments like:
JavaScript / Node.js
Vert.x
Quarkus (with Mutiny) using Vert.x under the hood
Python’s asyncio
Operating systems (I/O event loops)
### How It Works (Technical View)
#### Components:

1. **Event Queue**: Stores tasks (callbacks, I/O events, timers).
    
2. **Event Loop Thread**: Continuously checks the queue and executes events.
    
3. **Callbacks/Handlers**: Code that runs when an event is handled.

### Why It Matters in Reactive Systems (like Quarkus / Vert.x)

In **reactive frameworks**, the event loop is the **core execution model**:

- **Non-blocking**: It does not wait (block) for I/O to complete. It sets a callback and moves on.
    
- **Single-threaded**: Usually runs on a **small set of threads** (even 1 per CPU core).
    
- **Efficient**: High concurrency with **low thread usage**.
    
- **Scalable**: No need to spawn many threads for thousands of requests.

### ❗️Important Rules for Event Loop Threads

If you block the event loop thread (e.g., by calling `Thread.sleep()` or a database that takes time), everything else **stalls**. That’s why you must:

- Use **asynchronous I/O**.
    
- Offload **blocking tasks** to worker threads.

### Vs Thread pool
|Feature|Event Loop|Thread Pool|
|---|---|---|
|Model|One thread per loop|Many threads|
|Concurrency|High (async)|High (parallel)|
|Blocking Tasks|Should avoid blocking|Designed for blocking|
|Context Switching|Low (fewer threads)|Higher (more threads)|
|Examples|Node.js, Vert.x, Quarkus|Java Executors, Tomcat Threads|

## References