2025-08-13 07:06
Status: #baby
Tags: [[java]]
## Main
Dependency Injection (DI) is a **design pattern** and a key principle of software engineering, especially in frameworks like **Spring**.

At its core, **Dependency Injection** is about **decoupling** objects from their dependencies, so that instead of a class creating its own dependencies, they are **"injected"** from the outside.

### 🔹 Types of Dependency Injection

1. **Constructor Injection** – dependencies are provided via constructor (most common, recommended).

```java
@Component
public class Car {
    private final Engine engine;

    // Dependency is injected via constructor
    @Autowired  // (Optional since Spring 4.3 if only one constructor)
    public Car(Engine engine) {
        this.engine = engine;
    }

    public void drive() {
        engine.start();
        System.out.println("Car is driving...");
    }
}

```
    
2. **Setter Injection** – dependencies are provided via setter methods.
```java
@Component
public class Car {
    private Engine engine;

    // Dependency injected via setter
    @Autowired
    public void setEngine(Engine engine) {
        this.engine = engine;
    }

    public void drive() {
        engine.start();
        System.out.println("Car is driving...");
    }
}

```

    
3. **Field Injection** – dependencies are injected directly into fields (e.g., with annotations like `@Autowired` in Spring).

```java
@Component
public class Car {
    @Autowired
    private Engine engine;  // injected directly

    public void drive() {
        engine.start();
        System.out.println("Car is driving...");
    }
}

```



| Feature                   | Constructor Injection                        | Setter Injection                   | Field Injection                    |
| ------------------------- | -------------------------------------------- | ---------------------------------- | ---------------------------------- |
| **Visibility**            | Dependencies are explicit in constructor.    | Dependencies visible via setters.  | Dependencies hidden (fields only). |
| **Immutability**          | ✅ Supports `final` fields (safe, immutable). | ❌ No immutability.                 | ❌ No immutability.                 |
| **Best For**              | Mandatory dependencies.                      | Optional/replaceable dependencies. | Quick prototyping.                 |
| **Spring Recommendation** | ✅ Strongly recommended.                      | Good for optional.                 | ❌ Avoid in production.             |
| **Testing**               | Easy to inject mocks.                        | Easy to inject mocks.              | Harder to inject mocks.            |

✅ **Rule of Thumb in Spring:**

- Use **Constructor Injection** for mandatory dependencies.
    
- Use **Setter Injection** for optional dependencies.
    
- Avoid **Field Injection** except for quick demos/tests.

### 🔹 Benefits

- **Loose Coupling** – classes depend on abstractions (interfaces), not implementations.
    
- **Easier Testing** – you can inject mock objects in unit tests.
    
- **Better Maintainability** – changes in one part of the system don’t cascade everywhere.
    
- **Flexibility & Reusability** – easier to swap implementations.

### Inversion of Control vs DI
- **General principle** in software design.
    
- Means: instead of your code controlling _how_ dependencies are created and managed, you **hand over that control** to a framework/container.
    
- In Spring, the **IoC Container** is responsible for creating objects (beans), wiring them together, managing their lifecycle, etc.
    

👉 IoC is the _bigger concept_. It says: _"Don’t call us, we’ll call you."_ (Hollywood Principle)


**DI**
- **One way to achieve IoC**.
    
- DI specifically means: instead of a class instantiating its own dependencies, they are **injected from outside** (by a framework or manually).
    
- Spring achieves IoC **via DI**.

#### Simple Analogy

Imagine you’re a **chef** in a restaurant:

- **Without IoC/DI**:  
    You (chef) must go to the market, buy vegetables, meat, spices, etc., before cooking. You handle everything yourself.
    
- **With IoC + DI**:  
    The **restaurant manager (IoC container)** supplies everything you need.  
    You (chef/class) just say: "I need chicken and vegetables" → the manager provides them (DI).  
    Now you only focus on cooking (business logic), not sourcing ingredients (dependency management).


#### Relationship

- **IoC** = principle ("Let framework control object creation and lifecycle")
    
- **DI** = technique ("Inject dependencies instead of creating them")
	    

📌 In Spring:

- The **IoC container** is `ApplicationContext` (or `BeanFactory`).
    
- The **mechanism it uses** to implement IoC is **Dependency Injection** (via constructor, setter, or field).

✅ So you can say:  
👉 _"All DI is IoC, but not all IoC is DI."_

| Aspect                | IoC (Inversion of Control)                                                                                      | DI (Dependency Injection)                                                                                |
| --------------------- | --------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **Definition**        | A **principle**: shifting control of object creation & lifecycle to a container/framework.                      | A **design pattern/technique**: injecting dependencies into a class instead of creating them internally. |
| **Scope**             | Broad concept; many ways to implement (Factory, Service Locator, Events, DI, etc.).                             | A specific way to achieve IoC.                                                                           |
| **Who controls?**     | Framework/IoC Container (e.g., Spring’s `ApplicationContext`) manages object creation and wiring.               | Dependencies are **injected** (via constructor, setter, or field) by the IoC container.                  |
| **Example (General)** | "Don’t call us, we’ll call you" (Hollywood principle). The framework calls your code, not the other way around. | A class just declares what it needs, and the framework supplies it.                                      |
| **Spring Role**       | Spring IoC Container manages beans.                                                                             | DI is how Spring injects dependencies into those beans.                                                  |
| **Analogy**           | Restaurant manager ensures chefs have all resources.                                                            | Ingredients (dependencies) are handed to the chef instead of chef buying them.                           |
|                       |                                                                                                                 |                                                                                                          |


## References