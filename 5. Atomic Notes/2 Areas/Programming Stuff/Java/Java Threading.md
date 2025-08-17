2025-08-16 21:59
Status: #baby
Tags: [[java]]
## Main
### What
Threading in Java is about **executing multiple tasks concurrently** within a single program. A **thread** is the smallest unit of execution, and Java provides strong support for multithreading through the `java.lang.Thread` class and the `java.util.concurrent` package.

## 🔹 Key Concepts

1. **Process vs. Thread**
    
    - **Process**: An independent program with its own memory.
        
    - **Thread**: A lightweight sub-process that shares the same memory space of a process but runs independently.
        
2. **Multithreading**
    
    - Running multiple threads in parallel to improve performance (especially for I/O-bound tasks).
        
    - Example: Handling multiple client requests on a server.


## 🔹 Thread Lifecycle

A thread goes through these states (`Thread.State` enum):

1. **NEW** – created but not started.
    
2. **RUNNABLE** – ready to run, waiting for CPU.
    
3. **RUNNING** – executing.
    
4. **WAITING / TIMED_WAITING** – paused, waiting for another thread.
    
5. **TERMINATED** – finished execution.

![[Pasted image 20250816220155.png]]

#### Priority
Every Java thread has a priority that helps the operating system determine the order in which threads are scheduled.
Java thread priorities are in the range between MIN_PRIORITY (a constant of 1) and MAX_PRIORITY (a constant of 10). By default, every thread is given priority NORM_PRIORITY (a constant of 5).


## 🔹 Useful Thread Methods

- `start()` → starts a new thread.
    
- `run()` → contains the code to run (called by JVM).
    
- `sleep(ms)` → pauses the thread.
    
- `join()` → waits for another thread to finish.
    
- `yield()` → hints that the thread is willing to yield CPU.
    
- `interrupt()` → signals a thread to stop.
	

### Thread pools
## What is a ThreadPool?

- A **ThreadPool** manages a group of reusable worker threads.
    
- Instead of creating a new thread for each task, you submit tasks to the pool, and it schedules them for execution.
    
- This improves **performance** (avoids thread creation overhead) and **resource management** (limits max number of threads).

## 🔹 Executors Utility Class

Java provides the `Executors` factory to create thread pools:
Common factory methods:

- `newFixedThreadPool(n)` → Pool with **n fixed threads**.
    
- `newCachedThreadPool()` → Expands/shrinks as needed, reuses idle threads.
    
- `newSingleThreadExecutor()` → One worker thread, executes tasks sequentially.
    
- `newScheduledThreadPool(n)` → Schedule tasks with delay or periodically.

## 🔹 Tuning ThreadPools with `ThreadPoolExecutor`

Under the hood, `Executors` returns a `ThreadPoolExecutor`. You can configure it directly:

`ThreadPoolExecutor executor = new ThreadPoolExecutor(         2,      // core pool size         4,      // max pool size         60,     // idle thread timeout         TimeUnit.SECONDS,         new ArrayBlockingQueue<>(10) // task queue );`

- **Core pool size** → always alive threads.
    
- **Max pool size** → maximum allowed threads.
    
- **Keep-alive time** → how long extra threads stay alive when idle.
    
- **Work queue** → where waiting tasks are stored.

## 🔹 Best Practices

✅ Use a **fixed thread pool** for CPU-bound tasks (size = #cores).  
✅ Use a **cached pool** for short-lived, I/O-bound tasks.  
✅ Always **shutdown** the pool to free resources.  
✅ Consider `CompletableFuture` for async workflows.  
✅ For production, prefer creating `ThreadPoolExecutor` with custom parameters instead of `Executors` factory (because defaults may not fit).

### Synchronization
When multiple threads access **shared mutable state**, race conditions may occur (e.g., two threads updating the same variable at once).
### ✅ The `synchronized` keyword

It ensures that only **one thread at a time** executes the synchronized block or method.



### Future, CompletableFuture, Async
A `Future<T>` represents the **result of an asynchronous computation**.

- You submit a task (usually a `Callable<T>`) to an `ExecutorService`.
    
- You get back a `Future<T>`.
    
- You can later call `future.get()` to block until the result is ready.

Problem: `Future.get()` **blocks** until result is ready. No easy way to **chain tasks**.

# `CompletableFuture`

Introduced in **Java 8**, it extends `Future` and adds:

- **Non-blocking async callbacks** (like JavaScript Promises).
    
- **Chaining** (`thenApply`, `thenAccept`, `thenCompose`).
    
- **Combining multiple futures** (`allOf`, `anyOf`).

**Async in Java**

Async means **non-blocking execution** — tasks run in background threads while main thread continues.


Ways to run async in Java:
ExecutorService + Future
CompletableFuture (preferred)
Custom Executor with CompletableFuture

When to Use What?

- **Future** → simple async result, but blocking. ✅ Good for older Java code.
    
- **CompletableFuture** → modern, async, non-blocking, supports chaining & composition. ✅ Preferred in Java 8+.
    
- **Async with Executor** → fine-grained control over thread pools. ✅ Needed for performance tuning.
## References