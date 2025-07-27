2025-07-10 21:13
Status: #baby
Tags: [[computer science]] [[java]]
## Main

### Why? 
Using Java Streams provides a **modern, declarative, and functional** way to work with collections and data processing in Java.
- Clean and Concise Code (Declarative Style): Traditional `for` loops can be verbose. Streams let you express **what** you want to do, not **how** to do it.
- Functional Programming Style: allow using **lambda expressions** and functional constructs like `map`, `filter`, `reduce`.
- Efficient and Lazy Evaluation: Intermediate operations like `filter`, `map`, etc., are **lazy**, meaning they are only executed when needed.
- Parallel Processing Made Easy: can convert a stream to **parallel** with `.parallelStream()` to leverage multiple CPU cores.
```java
list.parallelStream()
    .map(MyService::compute)
    .collect(Collectors.toList());
``` 
- Pipeline Pattern: Stream operations form a **pipeline** — transforming, filtering, and collecting data in a fluent and readable way.
```java
Stream.of("apple", "banana", "avocado")
    .filter(s -> s.startsWith("a"))
    .map(String::toUpperCase)
    .forEach(System.out::println);
```
- Avoids Side Effects: Encourages **stateless and side-effect-free operations**, which are easier to reason about and test
- Built-in Terminal Operations: Powerful collectors like `groupingBy`, `joining`, `counting`, `averagingInt`, etc., reduce boilerplate code.
- Integration with Optional: Stream API works well with `Optional`, improving null safety and chaining.

### Example

#### Traditional (Imperative) Code — With Side Effects

```java
List<String> names = List.of("Alice", "Bob", "Alex", "Charlie");
List<String> result = new ArrayList<>();

for (String name : names) {
    if (name.startsWith("A")) {
        // ⚠️ Side effect: modifying external list
        result.add(name.toUpperCase());
    }
}
System.out.println(result); // [ALICE, ALEX]

```

- `result` is modified from **outside** the loop.
    
- This is a **side effect** — external state is mutated.
    
- It can lead to **bugs** in concurrent/multithreaded code or make the logic harder to follow.

#### Stream (Functional) Code — Avoids Side Effects

```java
List<String> names = List.of("Alice", "Bob", "Alex", "Charlie");

List<String> result = names.stream()
    .filter(name -> name.startsWith("A"))
    .map(String::toUpperCase)
    .collect(Collectors.toList());

System.out.println(result); // [ALICE, ALEX]

```

#### Dangerous Stream (Bad Practice with Side Effects)

```java
List<String> result = new ArrayList<>();
names.stream()
    .filter(name -> name.startsWith("A"))
    .map(String::toUpperCase)
    .forEach(result::add); // ⚠️ Side effect here!

```

While this **uses streams**, it still **mutates external state** (`result`), which defeats the purpose.

### When not to use? 
- When performance is critical and overhead matters (like in tight loops).
- When readability suffers (deep nesting of lambdas).
- When operations involve side effects (e.g., updating global state).
## References
https://www.baeldung.com/java-8-streams
