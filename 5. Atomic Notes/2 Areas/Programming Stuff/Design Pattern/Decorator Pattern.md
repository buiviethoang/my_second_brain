2025-08-23 15:08
Status: #baby
Tags: [[design pattern]]
## Main
### **Intent**

- Attach additional responsibilities to an object **dynamically**.
- Decorators provide a flexible alternative to **subclassing**, which can lead to a proliferation of subclasses when you want to add combinations of behaviors.

### **Key Components**

1. **Component (interface/abstract class)**  
    Defines the **interface** for objects that can have responsibilities added dynamically.
    
2. **ConcreteComponent**  
    The original object that you want to enhance or decorate.
    
3. **Decorator (abstract class)**  
    Implements the Component interface and has a reference to a **Component object**. It delegates operations to the wrapped component and can add new behavior **before or after** delegating.
    
4. **ConcreteDecorator**  
    Adds new behavior to the component by extending the Decorator.

Component
   ^
   |
ConcreteComponent
   ^
   |
Decorator -------> Component (reference)
   ^
   |
ConcreteDecorator




```java
// Component
interface Coffee {
    String getDescription();
    double getCost();
}

// ConcreteComponent
class SimpleCoffee implements Coffee {
    public String getDescription() { return "Simple Coffee"; }
    public double getCost() { return 2.0; }
}

// Decorator
abstract class CoffeeDecorator implements Coffee {
    protected Coffee coffee;
    public CoffeeDecorator(Coffee coffee) { this.coffee = coffee; }
    public String getDescription() { return coffee.getDescription(); }
    public double getCost() { return coffee.getCost(); }
}

// ConcreteDecorator
class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee coffee) { super(coffee); }
    public String getDescription() { return coffee.getDescription() + ", Milk"; }
    public double getCost() { return coffee.getCost() + 0.5; }
}

class SugarDecorator extends CoffeeDecorator {
    public SugarDecorator(Coffee coffee) { super(coffee); }
    public String getDescription() { return coffee.getDescription() + ", Sugar"; }
    public double getCost() { return coffee.getCost() + 0.2; }
}

// Usage
public class Main {
    public static void main(String[] args) {
        Coffee coffee = new SimpleCoffee();
        coffee = new MilkDecorator(coffee);
        coffee = new SugarDecorator(coffee);
        System.out.println(coffee.getDescription()); // Simple Coffee, Milk, Sugar
        System.out.println(coffee.getCost());        // 2.7
    }
}

```


### **Key Advantages**

- **Flexible**: You can combine multiple decorators at runtime.
    
- **Open/Closed Principle**: You can extend behavior without modifying existing code.
    
- **Avoids subclass explosion**: No need to create a subclass for every combination of behaviors.
    

### **Disadvantages**

- Can lead to **many small classes**, which may complicate code.
    
- Debugging can be harder because of multiple layers of wrappers.
    

### Real-world scenario

A common use case is **enhancing service functionality dynamically**, e.g., logging, caching, or validation, **without modifying the original service**.

```java
public interface UserService {
    String getUserById(Long id);
}


@Service
public class UserServiceImpl implements UserService {
    @Override
    public String getUserById(Long id) {
        // Imagine fetching user from database
        return "User#" + id;
    }
}



public abstract class UserServiceDecorator implements UserService {
    protected UserService decoratedUserService;

    public UserServiceDecorator(UserService decoratedUserService) {
        this.decoratedUserService = decoratedUserService;
    }

    @Override
    public String getUserById(Long id) {
        return decoratedUserService.getUserById(id);
    }
}



@Component
public class LoggingUserService extends UserServiceDecorator {

    public LoggingUserService(UserService decoratedUserService) {
        super(decoratedUserService);
    }

    @Override
    public String getUserById(Long id) {
        System.out.println("Fetching user with id: " + id);
        String result = super.getUserById(id);
        System.out.println("Fetched result: " + result);
        return result;
    }
}



@Component
public class CachingUserService extends UserServiceDecorator {

    private final Map<Long, String> cache = new HashMap<>();

    public CachingUserService(UserService decoratedUserService) {
        super(decoratedUserService);
    }

    @Override
    public String getUserById(Long id) {
        if (cache.containsKey(id)) {
            System.out.println("Cache hit for user " + id);
            return cache.get(id);
        }
        String result = super.getUserById(id);
        cache.put(id, result);
        return result;
    }
}


@SpringBootApplication
public class DemoApplication implements CommandLineRunner {

    @Autowired
    private UserService userService;

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

    @Override
    public void run(String... args) {
        System.out.println(userService.getUserById(1L));
        System.out.println(userService.getUserById(1L)); // cache hit
    }
}

```


### ✅ **Benefits in this context**

- Original `UserServiceImpl` remains untouched.
    
- Logging and caching can be added **independently and dynamically**.
    
- Supports **multiple combinations** of behaviors (logging + caching + validation, etc.).
    
- Easy to extend: just create a new decorator.


## References