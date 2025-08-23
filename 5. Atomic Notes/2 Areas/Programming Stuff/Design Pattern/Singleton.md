2025-08-23 11:09
Status: #baby
Tags: [[design pattern]]
## Main
## 📌 Definition

The **Singleton Pattern** ensures that:

1. A class has **only one instance** in the entire application.
    
2. It provides a **global access point** to that instance.



## 📌 When to Use

- When you want **only one instance** of a class controlling some resource.
    
- Examples:
    
    - Database connection pool
        
    - Logging system
        
    - Configuration manager
        
    - Thread pool manager



```java
public class Singleton {
    // Step 1: private static instance (volatile for thread-safety in double-checked locking)
    private static volatile Singleton instance;

    // Step 2: private constructor (no one else can create it)
    private Singleton() {
        System.out.println("Singleton instance created!");
    }

    // Step 3: public method to provide access
    public static Singleton getInstance() {
        if (instance == null) { // First check
            synchronized (Singleton.class) {
                if (instance == null) { // Second check
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }

    public void showMessage() {
        System.out.println("Hello from Singleton!");
    }
}


public class Main {
    public static void main(String[] args) {
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();

        System.out.println(s1 == s2); // true (same instance)
    }
}

```


## 📌 Key Variations

1. **Eager Initialization**
    
    - Instance is created at class load time.
        
    - Simple but wastes memory if never used.
        
    
    `public class Singleton {     private static final Singleton instance = new Singleton();     private Singleton() {}     public static Singleton getInstance() {         return instance;     } }`
    
2. **Lazy Initialization**
    
    - Create instance only when first requested.
        
3. **Thread-safe Singleton**
    
    - Uses **synchronized** or **double-checked locking**.
        
4. **Enum Singleton (Best in Java)**
    
    - Safe against serialization & reflection.
        
    
    `public enum Singleton {     INSTANCE;     public void showMessage() {         System.out.println("Hello from Enum Singleton!");     } }`
    


## 📌 Pros & Cons

✅ Only one instance (controlled access).  
✅ Saves memory/resources.  
✅ Global access point.

❌ Harder to unit test (global state).  
❌ Hidden dependencies (like global variables).  
❌ Can become a **God object** if abused.

### Singleton vs Static Class
|Feature|**Singleton**|**Static Class**|
|---|---|---|
|**Instance**|One single **object instance**|No instance — class itself is used|
|**OOP Principles**|Can implement interfaces, inherit, and be passed around as an object|Cannot be inherited (in Java), no interfaces|
|**State**|Can maintain **state** (fields, configuration)|Only has static variables/methods, no true object state|
|**Lazy Loading**|Can be created **on demand** (lazy initialization)|Loaded automatically when the class is loaded|
|**Memory**|Object lives in heap|Loaded in **method area (class area)**|
|**Flexibility**|More flexible — can switch to multiple instances if needed later|Rigid — cannot change to non-static easily|
|**Thread Safety**|Needs care for concurrency (double-checked locking)|Thread safety is simpler, as no instance exists|
|**Testing**|Mocking possible (since it’s an object)|Hard to mock in unit tests|
|**Example**|Database Connection Manager, Logger, Configuration Manager|`Math` class in Java, `Collections` utility methods|


## 📌 Example Analogy

- **Singleton** = _President of a country_ (a real person, single object).
    
- **Static class** = _Math book_ (just formulas & rules, no object needed).


## 📌 When to Use

- Use **Singleton** when you need:  
    ✅ A single object with state (logger, config, cache).  
    ✅ Lazy loading or controlled initialization.  
    ✅ Dependency injection & testing flexibility.
    
- Use **Static class** when you need:  
    ✅ Pure **utility/helper methods** (e.g., `Math.sqrt()`, `Collections.sort()`).  
    ✅ No state, no object, just behavior.



```java
// Singleton: Logger with state
public class Logger {
    private static Logger instance; // only one instance
    private int logCount = 0;       // state (keeps count)

    private Logger() {} // private constructor

    public static synchronized Logger getInstance() {
        if (instance == null) {
            instance = new Logger();
        }
        return instance;
    }

    public void log(String message) {
        logCount++;
        System.out.println("Log #" + logCount + ": " + message);
    }
}
public class Main {
    public static void main(String[] args) {
        Logger logger1 = Logger.getInstance();
        Logger logger2 = Logger.getInstance();

        logger1.log("App started");
        logger2.log("User logged in");

        System.out.println(logger1 == logger2); // true
    }
}
```

```java
// Static class: MathUtils with no state
public class MathUtils {

    // private constructor to prevent instantiation
    private MathUtils() {}

    public static int add(int a, int b) {
        return a + b;
    }

    public static int square(int x) {
        return x * x;
    }
}



public class Main {
    public static void main(String[] args) {
        System.out.println(MathUtils.add(5, 3));   // 8
        System.out.println(MathUtils.square(4));   // 16
    }
}

```
# 🔹 Key Difference in Code

- **Singleton**: `Logger.getInstance().log("...")` → object-based, keeps **state**.
    
- **Static**: `MathUtils.add(5, 3)` → **no object**, purely functional.

## References