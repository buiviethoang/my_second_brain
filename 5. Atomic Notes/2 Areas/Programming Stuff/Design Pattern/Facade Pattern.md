2025-08-23 15:20
Status: #baby
Tags: [[design pattern]]
## Main
The **Facade pattern** provides a **simplified interface** to a **complex subsystem**.

It **hides the complexity** of the subsystem and exposes only the necessary operations to the client, making it easier to use.

### **Key Components**

1. **Subsystem classes** – the complex set of classes or modules that do the actual work.
    
2. **Facade** – provides a **high-level interface** that wraps the subsystem and simplifies client interaction.
    
3. **Client** – uses the Facade instead of interacting with the subsystem directly.


Client
   |
  Facade
  / | \
Sub1 Sub2 Sub3



```java
// Subsystem
class TV {
    public void on() { System.out.println("TV is ON"); }
    public void off() { System.out.println("TV is OFF"); }
}

class SoundSystem {
    public void on() { System.out.println("Sound System is ON"); }
    public void off() { System.out.println("Sound System is OFF"); }
}

class DVDPlayer {
    public void on() { System.out.println("DVD Player is ON"); }
    public void off() { System.out.println("DVD Player is OFF"); }
    public void play(String movie) { System.out.println("Playing " + movie); }
}

// Facade 
class HomeTheaterFacade {
    private TV tv;
    private SoundSystem sound;
    private DVDPlayer dvd;

    public HomeTheaterFacade(TV tv, SoundSystem sound, DVDPlayer dvd) {
        this.tv = tv;
        this.sound = sound;
        this.dvd = dvd;
    }

    public void watchMovie(String movie) {
        System.out.println("Get ready to watch a movie...");
        tv.on();
        sound.on();
        dvd.on();
        dvd.play(movie);
    }

    public void endMovie() {
        System.out.println("Shutting down movie theater...");
        dvd.off();
        sound.off();
        tv.off();
    }
}


public class Main {
    public static void main(String[] args) {
        TV tv = new TV();
        SoundSystem sound = new SoundSystem();
        DVDPlayer dvd = new DVDPlayer();

        HomeTheaterFacade homeTheater = new HomeTheaterFacade(tv, sound, dvd);
        homeTheater.watchMovie("Inception");
        homeTheater.endMovie();
    }
}



```

### **Key Advantages**

- Simplifies client code by hiding subsystem complexity.
    
- Reduces dependencies between client and subsystem.
    
- Makes the system easier to use and understand.

### **Disadvantages**

- Can become a **god object** if it handles too many responsibilities.


### Real-world Example
### **Scenario:** Unified Customer Service API

Imagine a system with multiple services:

- **CustomerRepository** – fetches customer info from the database
    
- **OrderService** – fetches customer orders
    
- **LoyaltyService** – calculates loyalty points
    

Instead of having the client call all services separately, we provide a **Facade** to simplify access.

```java
@Service
public class CustomerRepository {
    public String getCustomerInfo(Long customerId) {
        return "Customer#" + customerId;
    }
}

@Service
public class OrderService {
    public List<String> getOrders(Long customerId) {
        return List.of("Order1", "Order2", "Order3");
    }
}

@Service
public class LoyaltyService {
    public int getLoyaltyPoints(Long customerId) {
        return 120;
    }
}



@Component
public class CustomerFacade {

    private final CustomerRepository customerRepo;
    private final OrderService orderService;
    private final LoyaltyService loyaltyService;

    public CustomerFacade(CustomerRepository customerRepo, OrderService orderService, LoyaltyService loyaltyService) {
        this.customerRepo = customerRepo;
        this.orderService = orderService;
        this.loyaltyService = loyaltyService;
    }

    public Map<String, Object> getCustomerDashboard(Long customerId) {
        Map<String, Object> dashboard = new HashMap<>();
        dashboard.put("info", customerRepo.getCustomerInfo(customerId));
        dashboard.put("orders", orderService.getOrders(customerId));
        dashboard.put("loyaltyPoints", loyaltyService.getLoyaltyPoints(customerId));
        return dashboard;
    }
}


@SpringBootApplication
public class DemoApplication implements CommandLineRunner {

    @Autowired
    private CustomerFacade customerFacade;

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

    @Override
    public void run(String... args) {
        Map<String, Object> dashboard = customerFacade.getCustomerDashboard(1L);
        System.out.println(dashboard);
    }
}

```

### **Key Benefits**

- **Simplifies client access**: The client calls **only one method** instead of three services.
    
- **Reduces coupling**: Client doesn’t need to know about the subsystem details.
    
- **Flexible**: If subsystem logic changes, the client code remains untouched.


## References