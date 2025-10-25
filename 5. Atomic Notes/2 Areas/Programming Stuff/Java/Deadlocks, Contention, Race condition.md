2025-07-27 15:19
Status: #baby
Tags: [[java]]
## Main
## 🧠 Overview Table: **Race Condition vs Contention vs Deadlock**

| Aspect        | **Race Condition**                                                                                                      | **Contention**                                                | **Deadlock**                                                                            |
| ------------- | ----------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| 🔍 Definition | Two or more threads access shared data **without synchronization**, and the **order of execution affects correctness**. | Multiple threads/processes **compete** for a shared resource. | Two or more threads **wait forever** for each other to release locks/resources.         |
| 📌 Example    | Two threads increment the same counter at the same time.                                                                | Many threads try to write to the same file/database row.      | Thread A holds Lock 1 and waits for Lock 2; Thread B holds Lock 2 and waits for Lock 1. |
| 🧯 Symptoms   | **Incorrect results**, unexpected behavior                                                                              | **Slow performance**, high CPU or I/O wait                    | Program **hangs**, threads never proceed                                                |
| 💣 Impact     | Corrupted data, bugs that are **hard to reproduce**                                                                     | Reduced throughput, **scalability bottlenecks**               | **System freeze**, requires restart or intervention                                     |
| ⚒️ Detection  | Usually via tests or race detectors (e.g. ThreadSanitizer)                                                              | Observed via performance metrics or profiling tools           | Use thread dump tools, lock graph analysis                                              |
| ✅ Prevention  | Use locks, atomic operations, or synchronization primitives                                                             | Minimize shared access, use lock-free or batch processing     | Lock ordering, try-locks with timeouts, deadlock detection                              |
| ✅ Recovery    | Fix code to ensure atomicity                                                                                            | Redesign to reduce resource sharing                           | Kill one thread or release one lock forcibly                                            |


## 📌 Visual Analogy

### 🏃‍♂️ Race Condition:

> Two runners share a baton — but no one says **who grabs it first**. Sometimes it works, sometimes it fails.  
> → **Nondeterministic bugs**

### 🤼 Contention:

> Everyone lines up to use the same bathroom.  
> → **Long wait, slow progress, but eventually you go.**

### 🔗 Deadlock:

> Two people enter narrow hallways from opposite ends and refuse to back up.  
> → **Both are stuck forever.**

## 🧩 When They Occur

| Situation             | Race Condition | Contention        | Deadlock      |
| --------------------- | -------------- | ----------------- | ------------- |
| Concurrent updates    | ✅ Likely       | ✅ Possible        | ❌ Unlikely    |
| High request volume   | ❌ Unlikely     | ✅ Very likely     | ❌ Unlikely    |
| Nested locks          | ❌ Rare         | ✅ Possible        | ✅ Common risk |
| Shared counters/flags | ✅ Common       | ✅ If many threads | ❌             |

## ✅ Summary (In 1 Sentence Each):

- **Race Condition**: Happens when shared data is accessed concurrently without proper synchronization, leading to **unpredictable bugs**.
    
- **Contention**: Happens when multiple threads/processes **compete for the same resource**, leading to **slowness**.
    
- **Deadlock**: Happens when threads **wait on each other in a cycle**, causing a **complete freeze**.


### Coffman's conditions 

It states that a **deadlock** can occur in a system if **all four of the following conditions hold simultaneously**:

- **Mutual Exclusion**
    
    - At least one resource must be held in a non-sharable mode.
        
    - Only one process can use the resource at a time.
        
- **Hold and Wait**
    
    - A process is holding at least one resource and waiting to acquire additional resources that are currently being held by other processes.
        
- **No Preemption**
    
    - Resources cannot be forcibly taken away from a process holding them.
        
    - A process must release resources voluntarily after completing its task.
        
- **Circular Wait**
    
    - A circular chain of processes exists, where each process is waiting for a resource that is held by the next process in the chain.


**Key point**: If all four conditions are true at the same time, deadlock can occur.  
To prevent deadlock, at least one of these conditions must be eliminated (for example, by preventing circular wait through ordering resources, or allowing preemption).


## References