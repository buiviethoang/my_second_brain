2025-08-23 12:01
Status: #baby
Tags: [[design pattern]]
## Main
The **Chain of Responsibility Pattern** lets you **pass a request along a chain of handlers**.

- Each handler decides **either to handle the request or pass it to the next handler**.
    
- This decouples the sender of the request from its receivers.

## 🔹 **Real-World Analogy**

- **Technical support system:**
    
    - Level 1 support → Level 2 support → Level 3 support.
        
    - A customer request moves up the chain until someone can handle it.
        
- **Document approval workflow:**
    
    - Team lead → Manager → Director → CEO.
        
    - Each level approves or forwards the document.


## **Structure**

1. **Handler (interface/abstract class)** → Defines a method to handle requests and a reference to the next handler.
    
2. **ConcreteHandlers** → Implement request handling and optionally pass to the next handler.
    
3. **Client** → Sends a request to the first handler in the chain.


```java
// Handler
abstract class Logger {
    public static int INFO = 1;
    public static int DEBUG = 2;
    public static int ERROR = 3;

    protected int level;
    protected Logger nextLogger;

    public void setNextLogger(Logger nextLogger) {
        this.nextLogger = nextLogger;
    }

    public void logMessage(int level, String message) {
        if (this.level <= level) {
            write(message);
        }
        if (nextLogger != null) {
            nextLogger.logMessage(level, message);
        }
    }

    abstract protected void write(String message);
}

// Concrete Handlers
class InfoLogger extends Logger {
    public InfoLogger(int level) { this.level = level; }
    @Override
    protected void write(String message) { System.out.println("INFO: " + message); }
}

class DebugLogger extends Logger {
    public DebugLogger(int level) { this.level = level; }
    @Override
    protected void write(String message) { System.out.println("DEBUG: " + message); }
}

class ErrorLogger extends Logger {
    public ErrorLogger(int level) { this.level = level; }
    @Override
    protected void write(String message) { System.out.println("ERROR: " + message); }
}

// Client
public class ChainPatternDemo {
    private static Logger getChainOfLoggers() {
        Logger errorLogger = new ErrorLogger(Logger.ERROR);
        Logger debugLogger = new DebugLogger(Logger.DEBUG);
        Logger infoLogger = new InfoLogger(Logger.INFO);

        infoLogger.setNextLogger(debugLogger);
        debugLogger.setNextLogger(errorLogger);

        return infoLogger; // head of the chain
    }

    public static void main(String[] args) {
        Logger loggerChain = getChainOfLoggers();

        loggerChain.logMessage(Logger.INFO, "This is an info message");
        loggerChain.logMessage(Logger.DEBUG, "This is a debug message");
        loggerChain.logMessage(Logger.ERROR, "This is an error message");
    }
}

```

## 🔹 **When to Use**

- When multiple objects can handle a request, but the **handler isn’t known in advance**.
    
- To **decouple sender and receiver**.
    
- For **workflow or pipeline-style processing**.

### 🔑 **Benefits**

- Reduces coupling between sender and receiver.
    
- Flexible: you can add or remove handlers dynamically.
    
- Easy to extend: add new handlers without changing existing ones.

### 🔹 **Comparison with Mediator** [[Mediator Pattern]]

- **Mediator:** central hub controls interaction between objects.
    
- **Chain of Responsibility:** request moves along a chain of objects; no central control.


## References