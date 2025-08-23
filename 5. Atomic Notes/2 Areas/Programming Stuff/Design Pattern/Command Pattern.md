2025-08-23 12:04
Status: #baby
Tags: [[design pattern]]
## Main

The **Command Pattern** encapsulates a request as an object, allowing you to:

- Parameterize clients with queues, requests, and operations.
    
- Support **undo/redo** operations.
    
- Decouple the **object that invokes the operation** from the **object that knows how to perform it**.


## 🔹 **Real-World Analogy**

- **Remote control for home appliances:**
    
    - Each button press (command) is encapsulated as an object.
        
    - The remote doesn’t need to know how the device works; it just invokes the command.
        
    - You can store commands to implement **undo/redo**.
        
- **Text editor:** each action (cut, copy, paste) can be a command that supports undo.


## 🔹 **Structure**

1. **Command interface** → Declares `execute()` (and optionally `undo()`).
    
2. **ConcreteCommand** → Implements the command by invoking actions on the receiver.
    
3. **Receiver** → Knows how to perform the operation.
    
4. **Invoker** → Calls the command.
    
5. **Client** → Creates and configures commands.


```java
// Command Interface
interface Command {
    void execute();
    void undo();
}

// Receiver
class Light {
    public void on() { System.out.println("Light is ON"); }
    public void off() { System.out.println("Light is OFF"); }
}

// Concrete Commands
class LightOnCommand implements Command {
    private Light light;
    public LightOnCommand(Light light) { this.light = light; }
    public void execute() { light.on(); }
    public void undo() { light.off(); }
}

class LightOffCommand implements Command {
    private Light light;
    public LightOffCommand(Light light) { this.light = light; }
    public void execute() { light.off(); }
    public void undo() { light.on(); }
}

// Invoker
class RemoteControl {
    private Command slot;

    public void setCommand(Command command) { slot = command; }
    public void pressButton() { slot.execute(); }
    public void pressUndo() { slot.undo(); }
}

// Client
public class CommandPatternDemo {
    public static void main(String[] args) {
        Light livingRoomLight = new Light();
        
        Command lightOn = new LightOnCommand(livingRoomLight);
        Command lightOff = new LightOffCommand(livingRoomLight);
        
        RemoteControl remote = new RemoteControl();
        
        remote.setCommand(lightOn);
        remote.pressButton();   // Light is ON
        remote.pressUndo();     // Light is OFF
        
        remote.setCommand(lightOff);
        remote.pressButton();   // Light is OFF
        remote.pressUndo();     // Light is ON
    }
}

```

## 🔹 **When to Use**

- To **decouple request sender and receiver**.
    
- When you want **undo/redo functionality**.
    
- To **queue, log, or schedule operations**.
    
- For **macro commands** (execute multiple commands in sequence).


### Compare with [[Chain of Responsibility]]
|Aspect|**Command**|**Chain of Responsibility**|
|---|---|---|
|**Purpose**|Encapsulate a request/action|Pass a request along a chain of handlers|
|**Behavior**|Executes a specific action|Each handler decides to process or forward|
|**Invoker**|Executes commands|Sends request to first handler|
|**Undo support**|Built-in possibility|Not typical|


## References