2025-08-25 21:32
Status: #baby
Tags: [[java]]
## Main

### Record
A **record** (introduced in **Java 14 preview, standardized in Java 16**) is a **special kind of class** designed to be a **transparent, immutable data carrier**.

Instead of writing verbose **POJOs** (Plain Old Java Objects) with fields, constructors, getters, `equals()`, `hashCode()`, and `toString()`, you can just declare a **record**, and Java generates all of that for you.

```java
public class Person {
    private final String name;
    private final int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String name() { return name; }
    public int age() { return age; }

    @Override
    public boolean equals(Object o) { /* boilerplate */ }
    @Override
    public int hashCode() { /* boilerplate */ }
    @Override
    public String toString() { /* boilerplate */ }
}

// With Record => 
public record Person(String name, int age) {}
```

That’s it. Java auto-generates:

- **Private final fields** (`name`, `age`)
    
- **Canonical constructor** (`Person(String name, int age)`)
    
- **Getters** (`name()`, `age()`)
    
- **equals()**, **hashCode()**, **toString()**

## 🔹 Key Properties of Records

1. **Immutable by default**
    
    - Fields are `final`.
        
    - You can’t change values after creation.
        
2. **Concise syntax**
    
    - Removes boilerplate.
        
3. **Still a class**
    
    - Can implement interfaces.
        
    - Can define methods, static fields, and even custom constructors.
        
4. **Not extendable**
    
    - Records are implicitly `final`.
        
    - They cannot extend other classes (but can implement interfaces).



## 🔹 When to Use Records

✅ Best for:

- DTOs (Data Transfer Objects)
    
- Value objects (in DDD)
    
- Immutable data carriers (configs, API responses, etc.)
    

❌ Not good for:

- Entities that need mutable state.
    
- Classes with complex behavior (not just data carriers).



#### Record vs Lombok 

|Feature|**Java Record** 🟢|**Lombok `@Data`** 🟡|**Lombok `@Value`** 🔵|
|---|---|---|---|
|**Boilerplate removal**|Built-in, no library needed|Yes (via annotations)|Yes (via annotations)|
|**Immutability**|Always immutable (all fields `final`)|Mutable (setters generated)|Immutable (fields `final`)|
|**Inheritance**|Cannot extend classes, only implement interfaces|Can extend classes|Can extend classes|
|**Final class**|Always `final`|Not final|Not final|
|**Constructors**|Canonical + compact constructors auto-generated|Can generate multiple (all args, no args, etc.)|All args constructor|
|**Framework support**|Fully supported in Java 16+|Requires Lombok dependency and IDE plugin|Same|
|**Code readability**|Very concise (built into language)|Concise but IDE needs Lombok plugin|Concise but IDE needs Lombok plugin|
|**Use cases**|DTOs, value objects, config|Entity models, mutable beans|Immutable DTOs, configs|

#### Example
```java
public record Person(String name, int age) {}
```

Generated:

- `private final String name;`
    
- `private final int age;`
    
- `public String name() { return name; }`
    
- `public int age() { return age; }`
    
- `equals()`, `hashCode()`, `toString()`


```java
@Data
public class Person {
    private String name;
    private int age;
}

```

Generated:

- `getName() / setName()`
    
- `getAge() / setAge()`
    
- `equals()`, `hashCode()`, `toString()`
    

⚠️ Mutable → you can call `person.setAge(30)`.


```java
@Value
public class Person {
    String name;
    int age;
}

```

Generated:

- All fields `private final`
    
- Only getters (`getName()`, `getAge()`)
    
- `equals()`, `hashCode()`, `toString()`
    
- All args constructor
    

Immutable, but still needs Lombok.



# 🔹 When to Choose What?

- **Use `record` (preferred)**
    
    - If you’re on Java 16+
        
    - For DTOs, configs, value objects
        
    - When you want _immutability and simplicity_ built-in
        
- **Use Lombok `@Data`**
    
    - If you need **mutable classes** (common in ORM like JPA/Hibernate)
        
    - For legacy codebases not on Java 16+
        
- **Use Lombok `@Value`**
    
    - If you want immutability but cannot use records (e.g., Java 8–15 projects)

👉 In modern projects (Java 17 LTS+), most teams **prefer `record`** over Lombok for data carriers, and only use Lombok for features `record` doesn’t cover (like builders, logging, `@Getter/@Setter` for mutable entities).


### Initializer Block

In Java, an **initializer block** is a block of code inside a class that runs when the class or an object is initialized.

There are two types:

1. **Instance Initializer Block (IIB)** → runs when an object is created (before the constructor).
    
2. **Static Initializer Block (SIB)** → runs once when the class is loaded into memory.

## 1. Instance Initializer Block (IIB)

- Declared with `{ ... }` inside the class (not inside methods).
    
- Runs **every time an object is created**, just before the constructor.
    
- Executes **in the order they appear** in the class.

```java
public class Car {
    private String model;

    // Instance initializer block
    {
        System.out.println("Instance Initializer Block executed");
        model = "Unknown";
    }

    public Car(String model) {
        System.out.println("Constructor executed");
        this.model = model;
    }

    public String getModel() { return model; }

    public static void main(String[] args) {
        Car c1 = new Car("Toyota");
        System.out.println(c1.getModel());

        Car c2 = new Car("Honda");
        System.out.println(c2.getModel());
    }
}

```

## 2. Static Initializer Block (SIB)

- Declared with `static { ... }`.
    
- Runs **once** when the class is loaded by the JVM.
    
- Often used for **static field initialization** or **loading resources**.

```java
public class DatabaseConfig {
    static String URL;

    static {
        System.out.println("Static Initializer Block executed");
        URL = "jdbc:mysql://localhost:3306/mydb";
    }

    public static void main(String[] args) {
        System.out.println("URL = " + DatabaseConfig.URL);
    }
}

```

## 3. Order of Execution

1. **Static Initializer Block** → runs once when class is loaded.
    
2. **Instance Initializer Block(s)** → run every time an object is created, before constructor.
    
3. **Constructor** → runs after instance initializers.


## References