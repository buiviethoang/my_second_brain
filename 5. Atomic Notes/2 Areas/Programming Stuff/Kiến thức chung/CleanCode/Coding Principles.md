2025-09-11 21:48
Status: 
Topic: 
Tags: [[coding]]
## Main

When people talk about **coding principles**, they usually mean the fundamental guidelines that help write clean, maintainable, and efficient code. Here are the most important ones:

### 🔑 Core Coding Principles

1. **KISS (Keep It Simple, Stupid)**  
    → Don’t overcomplicate. Choose the simplest solution that works.

```java
❌ Overcomplicated:
public int addNumbers(int a, int b) {
    int sum = 0;
    for (int i = 0; i < 1; i++) {
        sum = a + b;
    }
    return sum;
}
✅ Simple:

public int addNumbers(int a, int b) {
    return a + b;
}
```

2. **DRY (Don’t Repeat Yourself)**  
    → Avoid duplicating code. Extract common logic into functions, methods, or reusable components.
```java
double areaCircle(double r) {
    return 3.14159 * r * r;
}
double areaCylinder(double r, double h) {
    return 3.14159 * r * r * h;
}

=> 

double circleArea(double r) {
    return Math.PI * r * r;
}
double cylinderVolume(double r, double h) {
    return circleArea(r) * h;
}
```

3. **YAGNI (You Aren’t Gonna Need It)**  
    → Don’t add features “just in case.” Build only what you need right now.


**SOLID**

4. **Single Responsibility Principle (SRP)**  
    → A class/module/function should have only **one reason to change**.

```java
❌ One class doing too much:
class UserManager {
    void saveUser(User u) { /* save to DB */ }
    void sendWelcomeEmail(User u) { /* send email */ }
}
class UserRepository {
    void saveUser(User u) { /* save to DB */ }
}
class EmailService {
    void sendWelcomeEmail(User u) { /* send email */ }
}

```

4. **Open/Closed Principle (OCP)**  
    → Code should be **open for extension** but **closed for modification** (use abstractions, not modifications).

```java

❌ Modifying existing code:

class Discount {
    double applyDiscount(String type, double price) {
        if (type.equals("student")) return price * 0.9;
        else if (type.equals("vip")) return price * 0.8;
        return price;
    }
}

interface Discount {
    double apply(double price);
}
class StudentDiscount implements Discount {
    public double apply(double price) { return price * 0.9; }
}
class VipDiscount implements Discount {
    public double apply(double price) { return price * 0.8; }
}
```

5. **Liskov Substitution Principle (LSP)**  
    → Subtypes must be replaceable with their base types without breaking behavior.
    
```java
❌ Violating substitution:
class Bird {
    void fly() {}
}
class Ostrich extends Bird {
    @Override
    void fly() { throw new UnsupportedOperationException(); }
}

✅ Fix hierarchy:

interface Bird {}
interface FlyingBird extends Bird { void fly(); }

class Sparrow implements FlyingBird {
    public void fly() { System.out.println("Flying"); }
}
class Ostrich implements Bird { }

```

5. **Interface Segregation Principle (ISP)**  
    → Don’t force classes to implement methods they don’t use. Prefer smaller, specific interfaces.

```java
❌ Fat interface:
interface Machine {
    void print();
    void scan();
    void fax();
}
class Printer implements Machine {
    public void print() {}
    public void scan() {} // not supported
    public void fax() {}  // not supported
}

=> 

interface Printer { void print(); }
interface Scanner { void scan(); }

class SimplePrinter implements Printer {
    public void print() {}
}
```

6. **Dependency Inversion Principle (DIP)**  
    → Depend on abstractions, not concrete implementations.

```java
❌ Depends on concrete:
class FileLogger {
    void log(String msg) { System.out.println("File: " + msg); }
}
class App {
    FileLogger logger = new FileLogger();
}

✅ Depends on abstraction:
interface Logger {
    void log(String msg);
}
class FileLogger implements Logger {
    public void log(String msg) { System.out.println("File: " + msg); }
}
class App {
    Logger logger;
    App(Logger logger) { this.logger = logger; }
}
```

6. **Separation of Concerns**  
    → Each part of the code should deal with a distinct aspect (UI, logic, data, etc.).
    
```java
❌ Mixed layers:
class UserController {
    void createUser(String name) {
        // DB insert + business logic + HTTP response
    }
}

✅ Separate layers:
class UserController { /* handles HTTP requests */ }
class UserService { /* business logic */ }
class UserRepository { /* database access */ }
```

6. **Fail Fast & Defensive Programming**  
    → Detect problems early and handle unexpected inputs gracefully.

```java
❌ Delayed failure:
int divide(int a, int b) {
    return a / b; // crash later if b == 0
}

int divide(int a, int b) {
    if (b == 0) throw new IllegalArgumentException("Divider cannot be zero");
    return a / b;
}
```
### 🧹 Good Practices

- Write **readable code** (use meaningful names, consistent formatting).
    
- Add **tests** (unit, integration) to ensure correctness.
    
- **Refactor often** to keep code clean.
    
- **Use version control** (Git) and commit often.
    
- Document where needed, but let **code be the documentation** as much as possible.



## References