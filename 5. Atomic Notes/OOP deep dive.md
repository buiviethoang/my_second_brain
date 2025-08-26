2025-08-25 21:24
Status: #baby
Tags: [[java]]
## Main
# 🔹 Object Life Cycle in OOP

An **object life cycle** describes all the phases an object goes through in a program — from creation, through use, to destruction/garbage collection.

## 1. **Definition / Class Blueprint**

- Objects start as **class definitions** (a blueprint, not yet instantiated).

```java
class Car {
    private String model;
    public Car(String model) {
        this.model = model;
    }
    public void drive() {
        System.out.println(model + " is driving...");
    }
}

```
## 2. **Instantiation (Object Creation)**

- An object is created in memory (usually via `new` in Java/C#, or directly in Python).
    
- This allocates memory and calls the **constructor**.
```java
Car myCar = new Car("Toyota");
```
## 3. **Initialization**

- After memory allocation, **constructor(s)** initialize the object’s state (fields, properties).
    
- Some languages allow multiple constructors (overloading).
```java
Car defaultCar = new Car("Unknown"); // initialized via constructor
```
## 4. **Active Lifetime (Object Usage)**

- The object is **alive** and can be used:
    
    - Call methods
        
    - Change attributes
        
    - Interact with other objects
```java
myCar.drive();  // Toyota is driving...
```

## 5. **Finalization (Optional Cleanup)**

- Before destruction, some languages allow cleanup:
    
    - In **Java**, there’s `finalize()` (deprecated now).
        
    - In **C++**, destructors (`~ClassName`) free memory/resources.
        
    - In **Python**, `__del__()` can act like a destructor.
        
    - Modern OOP prefers **automatic resource management** (`try-with-resources`, `using`, context managers).

## 6. **Destruction / Garbage Collection**

- When no references to the object remain, the runtime can free memory.
    
- **Managed languages** (Java, C#, Python):
    
    - Objects are destroyed automatically by the **garbage collector**.
        
- **Unmanaged languages** (C++):
    
    - Objects must be explicitly destroyed (or go out of scope).

```java
myCar = null; // now eligible for GC
```

# 🔹 Summary of Object Life Cycle

1. **Class definition** (blueprint exists)
    
2. **Instantiation** (object created in memory)
    
3. **Initialization** (constructor sets values)
    
4. **Active lifetime** (object is used)
    
5. **Finalization** (cleanup, optional)
    
6. **Destruction / GC** (memory reclaimed)


[Class Blueprint] 
      ↓
[Instantiation → Constructor]
      ↓
[Initialized Object in Heap]
      ↓
[Active Usage: Methods & State Changes]
      ↓
[Finalization (cleanup)]
      ↓
[Destruction (GC or manual free)]

⚡ Key Point: In modern **managed OOP languages** (Java, C#, Python), you rarely worry about destruction — **garbage collector handles it**. But in **C++**, you must manage memory carefully.

### Java Interfaces vs Abstract Classes
- **Interface**
    
    - A contract that specifies _what_ a class must do, but not _how_.
        
    - Introduced in Java 1.0, enhanced in Java 8+ with **default** and **static** methods.
        
- **Abstract Class**
    
    - A class that cannot be instantiated but can provide **partial implementation**.

| Feature                  | **Interface** 🟢                                        | **Abstract Class** 🔵                                                         |
| ------------------------ | ------------------------------------------------------- | ----------------------------------------------------------------------------- |
| **Purpose**              | Define a **contract** (capabilities).                   | Provide **common base** with shared behavior.                                 |
| **Instantiation**        | Cannot be instantiated.                                 | Cannot be instantiated.                                                       |
| **Constructors**         | ❌ No constructors.                                      | ✅ Can have constructors (called by subclasses).                               |
| **Fields**               | `public static final` (constants only).                 | Instance fields (variables, state).                                           |
| **Methods** (pre-Java 8) | Abstract only.                                          | Abstract + concrete methods.                                                  |
| **Methods** (Java 8+)    | Default + static methods allowed.                       | Normal concrete methods allowed.                                              |
| **Methods** (Java 9+)    | Private methods also allowed (helper for defaults).     | Same as regular classes.                                                      |
| **Inheritance model**    | A class can **implement multiple interfaces**.          | A class can **extend only one abstract class** (Java has single inheritance). |
| **Access modifiers**     | Methods are implicitly `public`.                        | Can use `public`, `protected`, `private`.                                     |
| **Best used for**        | “Can do” capabilities (e.g., `Runnable`, `Comparable`). | “Is a” base class (e.g., `Shape`, `Animal`).                                  |

# When to Use?

✅ **Use Interface** when:

- You want to define a capability (e.g., `Comparable`, `Serializable`).
    
- You need **multiple inheritance of type**.
    
- You are designing APIs that expose behavior but hide implementation.
    

✅ **Use Abstract Class** when:

- You want to provide a **common base** with **shared code + state**.
    
- You expect subclasses to share some implementation details.
    
- You need to enforce **common fields** (e.g., `id`, `name`).

# Analogy

- **Interface** = a **job contract** (it says “You must do X, Y, Z”).
    
- **Abstract class** = a **partially built house** (you get walls and foundation, but subclasses must finish the roof, paint, etc.).


### Static Binding & Dynamic Binding
## **1. Static Binding**

- Happens at **compile-time**.
    
- Used for:
    
    - **Static methods**
        
    - **Final methods**
        
    - **Private methods**
        
    - **Overloaded methods** (method overloading is resolved at compile-time).
        
- Since the compiler knows the exact type, it decides which method to call.

```java
class Animal {
    private void sound() {  // private → static binding
        System.out.println("Animal makes a sound");
    }

    static void run() {     // static → static binding
        System.out.println("Animal runs");
    }

    void eat(String food) {  // Overloading example
        System.out.println("Animal eats " + food);
    }

    void eat(int quantity) { // Overloaded method → compile-time decision
        System.out.println("Animal eats " + quantity + " units of food");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal a = new Animal();

        a.run();         // resolved at compile-time
        a.eat("meat");   // resolved at compile-time
        a.eat(5);        // resolved at compile-time
    }
}

```

## **2. Dynamic Binding**

- Happens at **runtime**.
    
- Used for:
    
    - **Overridden methods** (inheritance + polymorphism).
        
- The method to call is decided based on the **actual object** (not the reference type).

```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {   // Overriding → dynamic binding
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal a = new Dog();  // reference type = Animal, object type = Dog
        a.sound();             // Runtime: calls Dog’s sound()
    }
}

```

|Feature|Static Binding|Dynamic Binding|
|---|---|---|
|**When decided**|Compile-time|Runtime|
|**Applicable to**|Static, Final, Private, Overloaded methods|Overridden methods|
|**Performance**|Faster (no runtime overhead)|Slightly slower (runtime resolution needed)|
|**Polymorphism**|Does **not** support runtime polymorphism|Enables runtime polymorphism|
|**Example**|Method overloading|Method overriding|

✅ **Rule of Thumb:**

- **Overloading → Static Binding**
    
- **Overriding → Dynamic Binding**

### Pass by value and pass by reference

- **Pass by Value**: A _copy_ of the variable’s value is passed to a method. Changes inside the method do **not** affect the original variable.
    
- **Pass by Reference**: A _reference (address)_ to the actual variable is passed. Changes inside the method **do** affect the original variable.

👉 **Java is strictly _pass by value_**.  
But — when the variable is an **object**, the _value being passed_ is a **copy of the reference**. That’s why it _feels_ like pass by reference in some cases.
```java
public class Test {
    public static void main(String[] args) {
        int a = 5;
        changeValue(a);
        System.out.println(a); // Output: 5 (unchanged)
    }

    static void changeValue(int x) {
        x = 10; // only changes local copy
    }
}

```

✅ Here, primitives are clearly **pass by value**.


```java
class Dog {
    String name;
    Dog(String name) { this.name = name; }
}

public class Test {
    public static void main(String[] args) {
        Dog d = new Dog("Rex");
        changeName(d);
        System.out.println(d.name); // Output: "Max"
    }

    static void changeName(Dog dog1) {
        dog1.name = "Max"; // modifies the same object
    }
}


```

✅ The **reference itself** is passed by value, but both the original and method parameter point to the **same object** → changes reflect outside.


```java
class Dog {
    String name;
    Dog(String name) { this.name = name; }
}

public class Test {
    public static void main(String[] args) {
        Dog d = new Dog("Rex");
        reassign(d);
        System.out.println(d.name); // Output: "Rex"
    }

    static void reassign(Dog dog1) {
        dog1 = new Dog("Max"); // reassigns local reference only
        dog1.name = "Max Changed";
    }
}

```

❌ This doesn’t change the original object, because the method only updated its **local copy of the reference**.

## ✅ Summary

- **Java always passes by value.**
    
- For **primitives** → value itself.
    
- For **objects** → value of the reference (copy of address).
    
- You can modify the object’s fields, but you cannot change which object the caller’s reference points to.





## References