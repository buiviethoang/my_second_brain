2025-08-23 15:27
Status: #baby
Tags: [[design pattern]]
## Main
The **Proxy pattern** provides a **surrogate or placeholder** for another object to control access to it.

It’s often used for:

- **Lazy loading** (load object only when needed)
    
- **Access control / security**
    
- **Logging or monitoring**
    
- **Remote proxies** (access objects across network)

### **Key Components**

1. **Subject** – defines the common interface for the real object and the proxy.
    
2. **RealSubject** – the actual object that does the work.
    
3. **Proxy** – implements the same interface and controls access to the RealSubject.

Client
   |
  Proxy ----> RealSubject
   |
Subject (interface)


```java
// Subject
interface Document {
    void display();
}
// RealSubject
class RealDocument implements Document {
    private String filename;

    public RealDocument(String filename) {
        this.filename = filename;
        loadFromDisk();
    }

    private void loadFromDisk() {
        System.out.println("Loading " + filename + " from disk...");
    }

    @Override
    public void display() {
        System.out.println("Displaying " + filename);
    }
}
// Proxy 
class DocumentProxy implements Document {
    private String filename;
    private RealDocument realDocument;

    public DocumentProxy(String filename) {
        this.filename = filename;
    }

    @Override
    public void display() {
        if (realDocument == null) { // lazy loading
            realDocument = new RealDocument(filename);
        }
        realDocument.display();
    }
}


public class Main {
    public static void main(String[] args) {
        Document doc = new DocumentProxy("MyFile.pdf");
        // Document is not loaded yet

        doc.display(); // loads and displays
        doc.display(); // displays without loading again
    }
}



```

The **proxy controls access** and loads the document only once.

### **Key Advantages**

- **Lazy initialization**: Save resources by creating objects only when needed.
    
- **Access control**: Can enforce security rules before forwarding requests.
    
- **Logging/monitoring**: Add functionality without changing the RealSubject.
    

### **Disadvantages**

- Adds a level of indirection (slight performance overhead).
    
- Can increase system complexity if overused.


### Real-world example
### **Scenario:** Logging Proxy for a User Service

We have a `UserService` that fetches user data. We want to **log method calls** without changing the original service.

```java
public interface UserService {
    String getUserById(Long id);
}

@Service
public class UserServiceImpl implements UserService {
    @Override
    public String getUserById(Long id) {
        return "User#" + id;
    }
}


@Component
public class UserServiceProxy implements UserService {

    private final UserService realUserService;

    public UserServiceProxy(UserService realUserService) {
        this.realUserService = realUserService;
    }

    @Override
    public String getUserById(Long id) {
        System.out.println("Logging: fetching user with id " + id);
        String result = realUserService.getUserById(id);
        System.out.println("Logging: fetched user: " + result);
        return result;
    }
}


@Configuration
public class AppConfig {

    @Bean
    @Primary
    public UserService userService(UserServiceImpl realService) {
        return new UserServiceProxy(realService);
    }
}


@SpringBootApplication
public class DemoApplication implements CommandLineRunner {

    @Autowired
    private UserService userService; // this will be the proxy

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

    @Override
    public void run(String... args) {
        System.out.println(userService.getUserById(1L));
    }
}



```

### **Key Benefits in this Example**

- **Separation of concerns**: Logging is handled by the proxy, not the real service.
    
- **No changes to existing service**: Original `UserServiceImpl` remains untouched.
    
- **Flexible**: Can add other proxies (e.g., security, caching) dynamically.


### Proxy vs AOP

| Feature                    | Manual Proxy                       | Spring AOP                                     |
| -------------------------- | ---------------------------------- | ---------------------------------------------- |
| **Purpose**                | Control access, add extra behavior | Same, but declarative and reusable             |
| **Implementation**         | Wrap service in another class      | Use annotations or XML to define aspects       |
| **Cross-Cutting Concerns** | One proxy per service              | One aspect can apply to multiple services      |
| **Maintenance**            | More boilerplate                   | Much cleaner, less code                        |
| **Flexibility**            | Fixed at runtime                   | Dynamic, can intercept multiple methods easily |
```java
@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.demo.UserService.*(..))")
    public void logBefore(JoinPoint joinPoint) {
        System.out.println("Logging BEFORE method: " + joinPoint.getSignature().getName());
    }

    @AfterReturning(value = "execution(* com.example.demo.UserService.*(..))", 
                    returning = "result")
    public void logAfter(JoinPoint joinPoint, Object result) {
        System.out.println("Logging AFTER method: " + joinPoint.getSignature().getName() 
                           + ", result: " + result);
    }
}


@Service
public class UserServiceImpl implements UserService {
    @Override
    public String getUserById(Long id) {
        return "User#" + id;
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
        userService.getUserById(1L);
    }
}



```

### **5. Benefits of AOP**

- No need to manually write proxy classes.
    
- One aspect can handle multiple services and methods.
    
- Easy to add/remove cross-cutting concerns like logging, security, caching, transactions.
    
- Fully integrated into Spring, supports **runtime weaving**.
## References