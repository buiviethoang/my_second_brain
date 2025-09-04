2025-07-14 22:22
Status: #baby
Tags: [[java]]
## Main

|Use Case|Use `Mono<T>`|Use `Flux<T>`|
|---|---|---|
|Single result|✔️ Yes|❌ No|
|Multiple results|❌ No|✔️ Yes|
|No result (but async)|✔️ `Mono<Void>`|✔️ `Flux.empty()` (but rare for void)|
|HTTP GET /users/{id}|✔️ (return one user or not found)|❌|
|HTTP GET /users|❌|✔️ (return list/stream of users)|
|Database save/update/delete|✔️ (return result or `Mono<Void>`)|❌|
|Streaming large data|❌|✔️|

- Prefer `Mono` when in doubt — it simplifies logic and makes error handling easier.
    
- Use `Flux` only when you genuinely have **more than one item** to deal with.

|Aspect|`Mono<List<T>>`|`Flux<T>`|
|---|---|---|
|**When it emits**|Emits **once**, after the entire list is ready|Emits **each item** as it's available|
|**Memory usage**|Must **hold the whole list in memory**|Streams one item at a time — **low memory footprint**|
|**Backpressure**|Cannot apply per-item backpressure|Supports **fine-grained backpressure**|
|**Latency**|Waits until **all data is collected**|Can start processing **before all data is fetched**|
|**Use case**|You want a **complete list** as a single unit|You want to **stream** or process **item by item**|

#### Use `Mono<List<T>>`:

- When you need the **entire result in memory** to process it at once.
    
- You want to apply logic to the **whole list at once** (e.g., sort, aggregate).
    
- It’s a small or predictable-sized result set (e.g., top 10 users).

#### Use `Flux<T>`:

- When the result set is **large**, or unknown in size.
    
- When you want to **start processing early** (streaming, piping).
    
- When **reactive backpressure** matters.
    
- For integration with WebFlux endpoints using `Flux<T>` return types.

### Anti-Pattern Warning

If you do this:

```java
Flux<User> usersFlux = userRepository.findAllUsers()
    .collectList()
    .flatMapMany(list -> Flux.fromIterable(list));
```
Then you’re defeating the point of `Flux<T>`. You might as well just use `Mono<List<T>>`

### Backpressure

**Backpressure** is the mechanism by which a **subscriber tells a publisher**:

> "Don't send more data than I can handle."

This helps avoid **out-of-memory errors**, **slow consumers getting overwhelmed**, or **dropping messages**.

At the core:
A Subscriber tells the Publisher how many items it can handle via .request(n).

The Flux respects this and only emits that many.

## References