2025-07-26 22:15
Status: #baby
Tags: [[computer science]] [[algorithm]]
## Main
### What? 
**Round-robin** is a scheduling algorithm commonly used in various systems like **CPU scheduling**, **load balancing**, **network packet handling**, and **task allocation**. It works by giving **each process or task a fixed time slice or turn in a circular order**, ensuring **fairness** and **equal opportunity** for all tasks.

### 🔁 Basic Concept:

- Each task is placed in a queue.
    
- The scheduler starts at the top of the queue.
    
- Each task is given a **time slice** (also called **quantum**) to run.
    
- After its turn, the task is moved to the **back of the queue** if it’s not done.
    
- The next task gets its turn, and so on.

### 👨‍💻 Example (CPU Scheduling):

Imagine three processes:

- `P1`: needs 8ms
    
- `P2`: needs 4ms
    
- `P3`: needs 6ms  
    And time slice is **2ms**
    

|Time|Process|
|---|---|
|0-2|P1|
|2-4|P2|
|4-6|P3|
|6-8|P1|
|8-10|P2 (done)|
|10-12|P3|
|12-14|P1|
|14-16|P3 (done)|
|16-18|P1 (done)|

✅ All get fair CPU time in order, without starvation.


### ⚖️ Advantages:

- **Fair**: Every task gets equal opportunity.
    
- **Simple**: Easy to implement.
    
- **Responsive**: Good for time-sharing systems or user-facing apps.
    

---

### ❌ Disadvantages:

- Not always efficient — frequent context switches if time slice is too small.
    
- Not suitable for tasks with very different workloads unless combined with priorities.


## References