2025-08-13 06:48
Status: #baby
Tags: [[java]]
## Main
**Functional Programming (FP)** in Java is a programming style where you focus on **what** to do, not **how** to do it.  
Instead of writing step-by-step instructions (imperative style), you write expressions that describe transformations on data, often using functions as **first-class citizens**.

Java wasn’t originally a functional language, but since **Java 8**, FP concepts have been introduced with **lambdas**, **streams**, and **method references**.

## **1. Core ideas in FP**

1. **Functions as values**
    
    - You can pass functions as parameters, return them from methods, and store them in variables.
        
    - Achieved in Java via functional interfaces (`Predicate`, `Function`, `Consumer`, etc.).
        
2. **Immutability**
    
    - Avoid changing data in place; instead, return new values.
        
    - This makes code easier to reason about and thread-safe.
        
3. **Pure functions**
    
    - The function’s output depends _only_ on its input — no side effects like modifying globals or printing to the console.
        
4. **Higher-order functions**
    
    - Functions that take other functions as arguments or return them.
        
5. **Declarative style**
    
    - You describe the **result** you want, not the step-by-step procedure.

## **2. Java example (imperative vs functional)**

### Imperative style (before Java 8)
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
List<String> result = new ArrayList<>();
for (String name : names) {
    if (name.startsWith("A")) {
        result.add(name.toUpperCase());
    }
}
System.out.println(result);
```

Functional style (Java 8+)
```java
List<String> result = Arrays.asList("Alice", "Bob", "Charlie", "David")
    .stream()
    .filter(name -> name.startsWith("A")) // Predicate
    .map(String::toUpperCase)             // Function
    .toList();                             // Immutable list

System.out.println(result);
```


**Here:**

- `filter` takes a **predicate** (function returning boolean).
    
- `map` takes a **function** (input → output).
    
- No mutable state (`result` is directly computed).

## **3. Functional Interfaces**

Java uses **functional interfaces** as the bridge to functional programming:

- `Predicate<T>` → `boolean test(T t)`
    
- `Function<T, R>` → `R apply(T t)`
    
- `Consumer<T>` → `void accept(T t)`
    
- `Supplier<T>` → `T get()`
    
- `UnaryOperator<T>` → `T apply(T t)`
    
- `BinaryOperator<T>` → `T apply(T t1, T t2)`


## **4. Benefits of FP in Java**

✅ More concise and readable code  
✅ Easier parallelization (Streams can be parallel)  
✅ Fewer bugs due to immutability and pure functions  
✅ Clearer intention of code

## **5. When to use FP in Java**

- Processing collections (`Stream API`)
    
- Data transformations
    
- Filtering, mapping, reducing large datasets
    
- Event handling with lambdas


![[Pasted image 20250813065155.png]]

## Functional Interface

A **Functional Interface** in Java is simply an interface that has **exactly one** abstract method.  
This makes it a perfect candidate for use with **lambdas** and **method references** in functional programming.

Think of it as a “contract” for a single behavior — the lambda provides the body.

```java
@FunctionalInterface
public interface Flyable {
    void fly();

    default boolean alive() {
        return true;
    }
}

```

### Built-in functional interfaces (java.util.function)

|Interface|Method signature|Example use|
|---|---|---|
|`Predicate<T>`|`boolean test(T t)`|Filtering|
|`Function<T,R>`|`R apply(T t)`|Mapping one type to another|
|`Consumer<T>`|`void accept(T t)`|Performing an action|
|`Supplier<T>`|`T get()`|Supplying values|
|`UnaryOperator<T>`|`T apply(T t)`|Transforming a value to the same type|
|`BinaryOperator<T>`|`T apply(T t1, T t2)`|Combining two values of the same type|

### Custom functional interfaces + lambda

```java
@FunctionalInterface
interface MathOperation {
    int operate(int a, int b);
}

public class Demo {
    public static void main(String[] args) {
        MathOperation add = (a, b) -> a + b;
        MathOperation multiply = (a, b) -> a * b;

        System.out.println(add.operate(3, 4));      // 7
        System.out.println(multiply.operate(3, 4)); // 12
    }
}

```
### **Rules for functional interfaces**

- Must have **exactly one** abstract method.
    
- Can have **default** and **static** methods (they don’t count toward the “one abstract method” rule).
    
- Can extend another functional interface if it doesn’t add new abstract methods.

## Lambda expressions

**Lambda expressions** in Java are a concise way to write implementations of **functional interfaces** — essentially a shortcut for creating anonymous classes with a single abstract method.

They let you pass **behavior** (a block of code) as a value.

### Why Lambda Expressions?
✅ Less boilerplate  
✅ More readable  
✅ Works naturally with **functional interfaces**

### **How Lambdas fit with Functional Interfaces**

A lambda is **not** a standalone feature — it needs a **target type** that is a functional interface.

### ** Key Points**

- Lambda expressions **must** target a functional interface.
    
- Variables used inside lambdas must be **final** or **effectively final**.
    
- Lambdas can capture variables from their enclosing scope (like closures in other languages).
    
- They make functional programming patterns in Java much cleaner.
## References
https://viblo.asia/p/hieu-hon-ve-functional-interface-trong-java-Az45b09qZxY