2025-08-23 11:01
Status: #baby
Tags: [[design pattern]]
## Main
## Factory method
👉 **Intent**:  
Define an interface for creating an object, but let subclasses decide which class to instantiate. The Factory Method lets a class defer instantiation to subclasses.

👉 **When to use**:

- When you have a **general contract/interface** for an object, but the **exact implementation** is determined at runtime.
    
- You want to **delegate object creation logic** to subclasses.


### Example (Analogy):

Think of a **logistics company**.

- You want to transport goods, but you don’t know if you’ll use **Truck** (for land) or **Ship** (for sea).
    
- The base class **Logistics** defines a factory method `createTransport()`.
    
- Subclasses like **RoadLogistics** or **SeaLogistics** decide whether to return a `Truck` or `Ship`.

```java
// Product
interface Transport {
    void deliver();
}

// Concrete Products
class Truck implements Transport {
    public void deliver() {
        System.out.println("Deliver by land in a truck.");
    }
}

class Ship implements Transport {
    public void deliver() {
        System.out.println("Deliver by sea in a ship.");
    }
}

// Creator
abstract class Logistics {
    abstract Transport createTransport();  // Factory Method
    void planDelivery() {
        Transport t = createTransport();
        t.deliver();
    }
}

// Concrete Creators
class RoadLogistics extends Logistics {
    Transport createTransport() {
        return new Truck();
    }
}

class SeaLogistics extends Logistics {
    Transport createTransport() {
        return new Ship();
    }
}
```


👉 Here, `Logistics` doesn’t know about `Truck` or `Ship`. Each subclass decides which transport to use.



## Abstract Factory Pattern
👉 **Intent**:  
Provide an interface for creating **families of related or dependent objects** without specifying their concrete classes.

👉 **When to use**:

- When you need to create **multiple related objects** (like a whole "theme" of UI elements).
    
- You want to enforce that objects from the same family are **used together**.


### Example (Analogy):

Think of a **GUI toolkit**.

- You want to support **multiple operating systems**: Windows, macOS.
    
- Each OS has its **own family of UI components**: `Button`, `Checkbox`.
    
- Abstract Factory ensures you get a matching set of components.

```java
// Abstract Products
interface Button {
    void paint();
}

interface Checkbox {
    void paint();
}

// Concrete Products
class WinButton implements Button {
    public void paint() { System.out.println("Windows Button"); }
}

class MacButton implements Button {
    public void paint() { System.out.println("MacOS Button"); }
}

class WinCheckbox implements Checkbox {
    public void paint() { System.out.println("Windows Checkbox"); }
}

class MacCheckbox implements Checkbox {
    public void paint() { System.out.println("MacOS Checkbox"); }
}

// Abstract Factory
interface GUIFactory {
    Button createButton();
    Checkbox createCheckbox();
}

// Concrete Factories
class WinFactory implements GUIFactory {
    public Button createButton() { return new WinButton(); }
    public Checkbox createCheckbox() { return new WinCheckbox(); }
}

class MacFactory implements GUIFactory {
    public Button createButton() { return new MacButton(); }
    public Checkbox createCheckbox() { return new MacCheckbox(); }
}

```


👉 Client code can now request a **factory** depending on OS, and always get matching components.


|Aspect|Factory Method|Abstract Factory|
|---|---|---|
|Creates|**One product** (object)|**Families of related products**|
|Focus|A single method that subclasses override|A whole factory object with multiple creation methods|
|Example|Choosing between Truck or Ship|Choosing between Windows UI vs Mac UI components|
|Pattern Level|**Class level** (inheritance decides what to create)|**Object level** (composition: pass a factory object)|


✅ **Analogy**:

- **Factory Method**: "I’ll call a method, and the subclass decides whether I get a Truck or a Ship."
    
- **Abstract Factory**: "I’ll choose a factory (Windows Factory or Mac Factory), and it’ll give me a consistent set of UI components."


## Real-world Example

**Example: Database Drivers**

Imagine you’re building an app that needs to connect to different databases: MySQL, PostgreSQL, Oracle.

- You don’t want your code full of `if (dbType == "mysql") ... else if (dbType == "postgres") ...`
    
- Instead, you use a **factory method** that lets subclasses decide which connection to return.

```java
// Product
interface DatabaseConnection {
    void connect();
}

// Concrete Products
class MySQLConnection implements DatabaseConnection {
    public void connect() {
        System.out.println("Connecting to MySQL...");
    }
}

class PostgresConnection implements DatabaseConnection {
    public void connect() {
        System.out.println("Connecting to PostgreSQL...");
    }
}

// Creator
abstract class ConnectionFactory {
    abstract DatabaseConnection createConnection();
}

// Concrete Creators
class MySQLConnectionFactory extends ConnectionFactory {
    DatabaseConnection createConnection() {
        return new MySQLConnection();
    }
}

class PostgresConnectionFactory extends ConnectionFactory {
    DatabaseConnection createConnection() {
        return new PostgresConnection();
    }
}

// Client code
public class Main {
    public static void main(String[] args) {
        ConnectionFactory factory = new MySQLConnectionFactory(); // could be chosen by config
        DatabaseConnection conn = factory.createConnection();
        conn.connect();
    }
}

```

👉 Here, the **Factory Method** avoids hardcoding the DB type. You can swap factories based on configuration, without changing client logic.

**Example: Cross-Platform UI Frameworks**

Suppose you’re building a **cross-platform desktop application** (like Slack, Spotify, or VSCode).

- The app must render UI elements differently depending on the OS (Windows, macOS, Linux).
    
- Each OS has **its own look & feel family** (buttons, checkboxes, menus).
    

Instead of mixing conditional logic everywhere, you use **Abstract Factory**


```java
// Abstract Products
interface Button {
    void render();
}
interface Menu {
    void show();
}

// Windows Products
class WindowsButton implements Button {
    public void render() { System.out.println("Render Windows Button"); }
}
class WindowsMenu implements Menu {
    public void show() { System.out.println("Show Windows Menu"); }
}

// Mac Products
class MacButton implements Button {
    public void render() { System.out.println("Render Mac Button"); }
}
class MacMenu implements Menu {
    public void show() { System.out.println("Show Mac Menu"); }
}

// Abstract Factory
interface UIFactory {
    Button createButton();
    Menu createMenu();
}

// Concrete Factories
class WindowsUIFactory implements UIFactory {
    public Button createButton() { return new WindowsButton(); }
    public Menu createMenu() { return new WindowsMenu(); }
}
class MacUIFactory implements UIFactory {
    public Button createButton() { return new MacButton(); }
    public Menu createMenu() { return new MacMenu(); }
}

// Client Code
public class Application {
    private Button button;
    private Menu menu;

    public Application(UIFactory factory) {
        button = factory.createButton();
        menu = factory.createMenu();
    }

    public void renderUI() {
        button.render();
        menu.show();
    }

    public static void main(String[] args) {
        UIFactory factory = new MacUIFactory(); // chosen at runtime
        Application app = new Application(factory);
        app.renderUI();
    }
}

```

The client doesn’t care _which_ OS it’s running on. It just uses the factory to get consistent UI elements.


## References