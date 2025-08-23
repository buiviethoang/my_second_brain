2025-08-23 11:05
Status: #baby
Tags: [[design pattern]]
## Main

👉 **Intent**:  
Create new objects by **cloning existing ones (prototypes)** instead of creating from scratch.

👉 **Why**:

- Object creation can be **expensive** (e.g., heavy DB load, network call, complex configuration).
    
- You want to avoid building from zero every time.
    
- Instead, you copy an already-prepared “prototype” object and tweak it.

```java
import java.util.HashMap;
import java.util.Map;

// Prototype
abstract class Shape implements Cloneable {
    String color;

    abstract void draw();

    public Shape clone() {
        try {
            return (Shape) super.clone();
        } catch (CloneNotSupportedException e) {
            throw new RuntimeException(e);
        }
    }
}

// Concrete Prototypes
class Circle extends Shape {
    int radius;

    Circle(int radius, String color) {
        this.radius = radius;
        this.color = color;
    }

    void draw() {
        System.out.println("Drawing Circle with radius " + radius + " and color " + color);
    }
}

class Rectangle extends Shape {
    int width, height;

    Rectangle(int width, int height, String color) {
        this.width = width;
        this.height = height;
        this.color = color;
    }

    void draw() {
        System.out.println("Drawing Rectangle " + width + "x" + height + " color " + color);
    }
}

// Prototype Registry
class ShapeRegistry {
    private static Map<String, Shape> shapes = new HashMap<>();

    static {
        shapes.put("big red circle", new Circle(10, "red"));
        shapes.put("small blue rectangle", new Rectangle(2, 4, "blue"));
    }

    public static Shape getPrototype(String key) {
        return shapes.get(key).clone();
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        Shape s1 = ShapeRegistry.getPrototype("big red circle");
        s1.draw();

        Shape s2 = ShapeRegistry.getPrototype("small blue rectangle");
        s2.draw();
    }
}

```

👉 Instead of creating from scratch, the client clones from the **registry of prototypes**.

## 🔹 Real World Examples in Software

1. **Java**
    
    - `Object.clone()` is a classic example.
        
    - `Prototype` is often used when dealing with **cached objects** (instead of reloading data from DB).
        
2. **Python**
    
    - `copy` or `deepcopy` modules implement prototype-like behavior.
        
    - Example: cloning a pre-configured `MachineLearningModel` object instead of retraining.
        
3. **Gaming**
    
    - You might have a base **Enemy prototype** (health, speed, attack style).
        
    - To create many enemies, you clone the prototype and tweak a few stats.
        
4. **Document Editors (Word, Google Docs)**
    
    - When you create a **new document from a template**, that’s Prototype in action.

### Prototype in Caching

# 🔹 Why Use Clone in Cache?

- When you keep objects in a **cache**, those objects might be reused many times.
    
- If you return the **same cached object directly**, clients might accidentally **mutate** it, affecting everyone using the cache.
    
- Instead, you keep a **prototype object in cache**, and whenever someone requests it, you return a **clone**.
    
- This way, each caller gets an **independent copy** that starts with the same pre-initialized state.
```java
import java.util.HashMap;
import java.util.Map;

// Prototype
class DbConfig implements Cloneable {
    String url;
    String user;
    String password;
    int poolSize;

    DbConfig(String url, String user, String password, int poolSize) {
        this.url = url;
        this.user = user;
        this.password = password;
        this.poolSize = poolSize;
    }

    @Override
    public DbConfig clone() {
        try {
            return (DbConfig) super.clone();
        } catch (CloneNotSupportedException e) {
            throw new RuntimeException(e);
        }
    }

    void show() {
        System.out.println("DBConfig: " + url + " user=" + user + " pool=" + poolSize);
    }
}

// Cache Registry
class ConfigCache {
    private static final Map<String, DbConfig> cache = new HashMap<>();

    static {
        cache.put("mysql", new DbConfig("jdbc:mysql://localhost:3306/test", "root", "pass", 10));
        cache.put("postgres", new DbConfig("jdbc:postgresql://localhost:5432/test", "postgres", "pass", 5));
    }

    public static DbConfig getConfig(String key) {
        return cache.get(key).clone(); // return a CLONE
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        DbConfig cfg1 = ConfigCache.getConfig("mysql");
        DbConfig cfg2 = ConfigCache.getConfig("mysql");

        cfg1.poolSize = 20; // modifying my copy only

        cfg1.show(); // DBConfig: jdbc:mysql://localhost:3306/test user=root pool=20
        cfg2.show(); // DBConfig: jdbc:mysql://localhost:3306/test user=root pool=10
    }
}

```

👉 Here:

- The **cache keeps prototypes** (`mysql`, `postgres`).
    
- Each client gets a **fresh clone** when requesting.
    
- No accidental shared-state pollution.

## 🔹 Real World Uses

1. **ORM Entities** (like Hibernate)
    
    - A cached entity can be cloned into a detached copy before returning to a client.
        
    - Prevents accidental modification of shared persistence context objects.
        
2. **Machine Learning Models**
    
    - A model with preloaded weights can be stored in cache.
        
    - Each request clones the model and runs inference safely in parallel.
        
3. **Game Engines**
    
    - You keep a cache of **enemy prototypes** (Zombie, Dragon, Soldier).
        
    - Cloning them is cheaper than building from scratch every time.



⚡ Key takeaway:

> Cache + Prototype ensures **speed** (reuse initialized objects) while maintaining **safety** (independent clones, no shared mutation).

## References