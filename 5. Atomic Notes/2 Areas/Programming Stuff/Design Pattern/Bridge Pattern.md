2025-08-23 15:14
Status: #baby
Tags: [[design pattern]]
## Main
### **Intent**

The **Bridge pattern** is used to **decouple an abstraction from its implementation**, so that the two can vary independently.

In other words, it separates **what something does** (abstraction) from **how it does it** (implementation), avoiding a proliferation of subclasses.


### **Key Components**

1. **Abstraction** – defines the **interface** for the high-level control logic.
    
2. **RefinedAbstraction** – extends the abstraction, may add extra behavior.
    
3. **Implementor** – defines the **interface for implementation**.
    
4. **ConcreteImplementor** – provides concrete implementation(s) of the Implementor interface.

Abstraction
   ^
   |
RefinedAbstraction
   |
   +----> Implementor
             ^
             |
      ConcreteImplementorA
      ConcreteImplementorB



Imagine a **remote control** system where you have different devices (TV, Radio) and different remotes (Basic, Advanced).

```java
// Implementor
interface Device {
    void turnOn();
    void turnOff();
}
// ConcreteImplementor
class TV implements Device {
    public void turnOn() { System.out.println("TV is ON"); }
    public void turnOff() { System.out.println("TV is OFF"); }
}

class Radio implements Device {
    public void turnOn() { System.out.println("Radio is ON"); }
    public void turnOff() { System.out.println("Radio is OFF"); }
}
// Abstraction
abstract class Remote {
    protected Device device;

    public Remote(Device device) {
        this.device = device;
    }

    abstract void turnOn();
    abstract void turnOff();
}
// RefinedAbstraction
class BasicRemote extends Remote {
    public BasicRemote(Device device) { super(device); }

    public void turnOn() { device.turnOn(); }
    public void turnOff() { device.turnOff(); }
}

class AdvancedRemote extends Remote {
    public AdvancedRemote(Device device) { super(device); }

    public void turnOn() {
        System.out.println("Advanced Remote: pre-checks...");
        device.turnOn();
    }

    public void turnOff() {
        System.out.println("Advanced Remote: saving settings...");
        device.turnOff();
    }
}

public class Main {
    public static void main(String[] args) {
        Device tv = new TV();
        Device radio = new Radio();

        Remote basicRemote = new BasicRemote(tv);
        basicRemote.turnOn();
        basicRemote.turnOff();

        Remote advancedRemote = new AdvancedRemote(radio);
        advancedRemote.turnOn();
        advancedRemote.turnOff();
    }
}



```

### **Key Advantages**

- **Decouples abstraction from implementation** → easy to extend independently.
    
- **Reduces subclass explosion**. For example, without Bridge, combining multiple devices and remotes would require a separate subclass for every combination.
    
- **Supports runtime switching** of implementation.


### Real-world example
```java
public interface PaymentGateway {
    void pay(double amount);
}


@Component
public class StripeGateway implements PaymentGateway {
    @Override
    public void pay(double amount) {
        System.out.println("Paying $" + amount + " using Stripe.");
    }
}

@Component
public class PayPalGateway implements PaymentGateway {
    @Override
    public void pay(double amount) {
        System.out.println("Paying $" + amount + " using PayPal.");
    }
}

public abstract class PaymentService {
    protected PaymentGateway gateway;

    public PaymentService(PaymentGateway gateway) {
        this.gateway = gateway;
    }

    public abstract void processPayment(double amount);
}


@Component
public class OnlinePaymentService extends PaymentService {
    public OnlinePaymentService(PaymentGateway gateway) {
        super(gateway);
    }

    @Override
    public void processPayment(double amount) {
        System.out.println("Processing online payment...");
        gateway.pay(amount);
    }
}

@Component
public class SubscriptionPaymentService extends PaymentService {
    public SubscriptionPaymentService(PaymentGateway gateway) {
        super(gateway);
    }

    @Override
    public void processPayment(double amount) {
        System.out.println("Processing subscription payment...");
        gateway.pay(amount);
    }
}


@Configuration
public class AppConfig {

    @Bean
    public PaymentService onlinePaymentWithStripe(StripeGateway stripeGateway) {
        return new OnlinePaymentService(stripeGateway);
    }

    @Bean
    public PaymentService subscriptionPaymentWithPayPal(PayPalGateway payPalGateway) {
        return new SubscriptionPaymentService(payPalGateway);
    }
}


@SpringBootApplication
public class DemoApplication implements CommandLineRunner {

    @Autowired
    private PaymentService onlinePaymentWithStripe;

    @Autowired
    private PaymentService subscriptionPaymentWithPayPal;

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

    @Override
    public void run(String... args) {
        onlinePaymentWithStripe.processPayment(50.0);
        subscriptionPaymentWithPayPal.processPayment(100.0);
    }
}




```


### **Key Benefits in this Example**

- **Decouples payment service from gateway implementation**.
    
- Can **easily add new gateways** (e.g., Square) or new payment types (e.g., RefundPayment) without changing existing code.
    
- Supports **runtime flexibility** for combinations of services and gateways.



## References