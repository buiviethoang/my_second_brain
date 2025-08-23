2025-08-23 11:39
Status: #baby
Tags: [[design pattern]]
## Main

### Template Method
👉 **Intent**:  
Define the **skeleton of an algorithm** in a base class, but let **subclasses redefine certain steps** without changing the overall algorithm structure.

## 🏠 Real World Analogy

Think of making **tea vs coffee**:

- Steps are always the same:
    
    1. Boil water
        
    2. Brew drink (tea leaves / coffee powder)
        
    3. Pour in cup
        
    4. Add condiments (lemon for tea / milk & sugar for coffee)
        

👉 The **algorithm (skeleton)** is fixed, but **specific steps differ**.



```java
// Abstract class defines the template
abstract class CaffeineBeverage {
    // Template Method
    public final void prepareRecipe() {
        boilWater();
        brew();
        pourInCup();
        addCondiments();
    }

    void boilWater() {
        System.out.println("Boiling water");
    }

    void pourInCup() {
        System.out.println("Pouring into cup");
    }

    // Steps that subclasses must implement
    abstract void brew();
    abstract void addCondiments();
}

// Subclass 1
class Tea extends CaffeineBeverage {
    void brew() {
        System.out.println("Steeping the tea");
    }
    void addCondiments() {
        System.out.println("Adding lemon");
    }
}

// Subclass 2
class Coffee extends CaffeineBeverage {
    void brew() {
        System.out.println("Dripping coffee through filter");
    }
    void addCondiments() {
        System.out.println("Adding sugar and milk");
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        CaffeineBeverage tea = new Tea();
        tea.prepareRecipe();

        System.out.println("----");

        CaffeineBeverage coffee = new Coffee();
        coffee.prepareRecipe();
    }
}

```


## 🔹 Real-World Examples in Software

1. **Frameworks & Libraries**
    
    - In **Spring Framework**, methods like `JdbcTemplate.query()` define a **template** for DB access (open connection → execute query → close connection). You just supply the custom **RowMapper**.
        
2. **Game Engines**
    
    - The **game loop** structure is defined once (initialize → update → render → shutdown). Each game overrides the details of `update()` and `render()`.
        
3. **Web Servers**
    
    - HTTP request handling: a framework (like Django or Spring MVC) defines the flow → parse request, run handler, build response. You only implement the handler step.


## 🔑 Key Points

- **Base class** defines the **template method** (fixed steps of algorithm).
    
- **Subclasses** override specific steps.
    
- Ensures consistency while allowing customization.


### Strategy
👉 **Intent**:  
Define a **family of algorithms**, encapsulate each one, and make them **interchangeable at runtime**.

👉 **Why**:

- You want to choose an algorithm **dynamically**, without hardcoding logic with `if/else` or `switch`.

## 🏠 Real World Analogy

Think of a **navigation app (Google Maps)**:

- You want to get from **A → B**.
    
- Strategies: **Driving, Walking, Cycling, Public Transit**.
    
- The app has a **common interface**: `calculateRoute(start, end)` but each strategy implements it differently.
    
- You can switch the strategy at runtime.

```java
// Strategy Interface
interface RouteStrategy {
    void buildRoute(String from, String to);
}

// Concrete Strategies
class RoadStrategy implements RouteStrategy {
    public void buildRoute(String from, String to) {
        System.out.println("Route from " + from + " to " + to + " by road");
    }
}

class WalkingStrategy implements RouteStrategy {
    public void buildRoute(String from, String to) {
        System.out.println("Route from " + from + " to " + to + " by walking");
    }
}

class PublicTransportStrategy implements RouteStrategy {
    public void buildRoute(String from, String to) {
        System.out.println("Route from " + from + " to " + to + " by public transport");
    }
}

// Context
class Navigator {
    private RouteStrategy strategy;

    public void setStrategy(RouteStrategy strategy) {
        this.strategy = strategy;
    }

    public void buildRoute(String from, String to) {
        strategy.buildRoute(from, to);
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        Navigator navigator = new Navigator();

        navigator.setStrategy(new RoadStrategy());
        navigator.buildRoute("Hanoi", "Haiphong");

        navigator.setStrategy(new WalkingStrategy());
        navigator.buildRoute("Hanoi", "Old Quarter");

        navigator.setStrategy(new PublicTransportStrategy());
        navigator.buildRoute("Hanoi", "Noi Bai Airport");
    }
}

```

## Real-World Examples in Software

1. **Sorting Algorithms**
    
    - Java’s `Collections.sort()` uses a **Comparator Strategy**.
        
    - You can pass different comparators (ascending, descending, custom rules).
        
2. **Payment Systems**
    
    - E-commerce apps let you choose **Credit Card, PayPal, Apple Pay** → each is a payment strategy.
        
3. **Compression Algorithms**
    
    - File archivers (e.g., WinRAR, 7zip) let you choose compression algorithm: ZIP, RAR, GZIP → all are strategies.
        
4. **Authentication**
    
    - Web frameworks often support multiple strategies: **JWT, OAuth, SAML, LDAP**.


### Difference 

| Aspect              | Strategy                                                    | Template Method                                  |
| ------------------- | ----------------------------------------------------------- | ------------------------------------------------ |
| Variation           | Encapsulates interchangeable algorithms                     | Subclasses override steps of a fixed algorithm   |
| Technique           | Uses **composition** (delegate behavior to strategy object) | Uses **inheritance** (override abstract methods) |
| Runtime Flexibility | Can switch strategies **at runtime**                        | Algorithm structure is fixed at compile time     |

- **Strategy** = "I can swap out **how** I do it (e.g., different navigation modes)."
    
- **Template Method** = "I always follow the same steps, but subclasses fill in the details."


### Strategy with Factory
# 🔹 Why Combine Strategy + Factory?

- **Strategy**: defines a family of interchangeable algorithms.
    
- **Factory**: encapsulates the logic of _which strategy to create_.
    
- Combined: client code doesn’t need to worry about instantiation or selection — just provide some input (like a config or user choice).

## 🏠 Real World Analogy: Payments

Imagine an **E-commerce platform**:

- Payment strategies: **Credit Card, PayPal, Bitcoin**.
    
- You don’t want to hardcode `if/else` everywhere.
    
- Instead:
    
    - A **PaymentFactory** decides which strategy to create (based on user input).
        
    - The **CheckoutService** uses the chosen strategy to process payment.

```java
// Strategy Interface
interface PaymentStrategy {
    void pay(double amount);
}

// Concrete Strategies
class CreditCardPayment implements PaymentStrategy {
    public void pay(double amount) {
        System.out.println("Paid $" + amount + " using Credit Card");
    }
}

class PayPalPayment implements PaymentStrategy {
    public void pay(double amount) {
        System.out.println("Paid $" + amount + " using PayPal");
    }
}

class BitcoinPayment implements PaymentStrategy {
    public void pay(double amount) {
        System.out.println("Paid $" + amount + " using Bitcoin");
    }
}

// Factory to choose strategy
class PaymentFactory {
    public static PaymentStrategy getPaymentStrategy(String type) {
        switch (type.toLowerCase()) {
            case "creditcard": return new CreditCardPayment();
            case "paypal": return new PayPalPayment();
            case "bitcoin": return new BitcoinPayment();
            default: throw new IllegalArgumentException("Unknown payment type: " + type);
        }
    }
}

// Context
class CheckoutService {
    private PaymentStrategy paymentStrategy;

    public CheckoutService(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void checkout(double amount) {
        paymentStrategy.pay(amount);
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        String userChoice = "paypal"; // this could come from user input or config

        PaymentStrategy strategy = PaymentFactory.getPaymentStrategy(userChoice);
        CheckoutService checkout = new CheckoutService(strategy);

        checkout.checkout(99.99);
    }
}

```


## 🔹 Where You See This in Real Software

1. **Spring Security**
    
    - Authentication strategies (JWT, OAuth2, LDAP).
        
    - Strategy = actual authentication mechanism.
        
    - Factory = decides which authentication provider to use.
        
2. **Logging Frameworks**
    
    - Strategy = logging backend (Console, File, Database, Cloud).
        
    - Factory = reads config and picks the right strategy.
        
3. **Payment Gateways**
    
    - Exactly like above: strategy = gateway (Stripe, PayPal, Apple Pay).
        
    - Factory = choose based on config / user selection.


## 🔑 Benefits of Combining

✔ **Open/Closed**: new strategies can be added without modifying existing code.  
✔ **Encapsulation**: selection logic stays inside Factory.  
✔ **Runtime flexibility**: swap strategies based on config or input.


## References