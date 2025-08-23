2025-08-23 11:55
Status: #baby
Tags: [[design pattern]]
## Main
The **State Pattern** is a **behavioral design pattern** that allows an object to change its **behavior** when its **internal state changes**.  
It looks like the object is **changing its class** at runtime.

👉 Instead of writing long `if-else` or `switch` statements, the behavior is **delegated to state-specific classes**.
## 🏦 **Analogy**

Think about a **Vending Machine**:

- If it’s in **"No Coin Inserted"** state → pressing the button does nothing.
    
- If it’s in **"Coin Inserted"** state → pressing the button dispenses a product.
    
- If it’s in **"Out of Stock"** state → pressing the button shows "Sold Out".
    

The vending machine’s behavior changes based on its **state**, not because we wrote a giant `if-else` block.


```java
// State interface
interface State {
    void pressPlay(MediaPlayer player);
}

// Concrete States
class PlayingState implements State {
    @Override
    public void pressPlay(MediaPlayer player) {
        System.out.println("Pausing the media...");
        player.setState(new PausedState());
    }
}

class PausedState implements State {
    @Override
    public void pressPlay(MediaPlayer player) {
        System.out.println("Resuming the media...");
        player.setState(new PlayingState());
    }
}

class StoppedState implements State {
    @Override
    public void pressPlay(MediaPlayer player) {
        System.out.println("Starting the media...");
        player.setState(new PlayingState());
    }
}

// Context
class MediaPlayer {
    private State state;

    public MediaPlayer() {
        state = new StoppedState(); // initial state
    }

    public void setState(State state) {
        this.state = state;
    }

    public void pressPlay() {
        state.pressPlay(this);
    }
}

// Client
public class StatePatternDemo {
    public static void main(String[] args) {
        MediaPlayer player = new MediaPlayer();

        player.pressPlay(); // Starting the media...
        player.pressPlay(); // Pausing the media...
        player.pressPlay(); // Resuming the media...
    }
}

```


## ✅ **When to Use State Pattern**

- When an object’s behavior depends on its **state**, and it must change its behavior at runtime.
    
- To **eliminate long conditional statements** (`if`/`switch`).
    
- Example:
    
    - Vending Machines
        
    - ATMs (Card Inserted / No Card / Authenticated)
        
    - Media Players (Playing / Paused / Stopped)



### Compare to Strategy

## 🔑 **State Pattern**

- **Intent**:  
    Allows an object to alter its **behavior** when its **internal state changes**.  
    → The object appears to change its class.
    
- **Key Idea**:  
    The **context** has different _states_ (e.g., Draft → Moderation → Published for a Document). Each state knows what the next behavior should be.
    
- **When to Use**:
    
    - Object behavior depends on its **current state**.
        
    - You want to avoid big `if/else` or `switch` statements for states.
        
- **Example**:  
    A `VendingMachine` in **NoCoinState**, **HasCoinState**, **SoldState**. The machine changes state internally after each operation.
    

---

## 🔑 **Strategy Pattern**

- **Intent**:  
    Defines a **family of algorithms**, encapsulates each one, and makes them **interchangeable** at runtime.
    
- **Key Idea**:  
    The **context** delegates to a chosen _strategy_ (e.g., `BubbleSort`, `QuickSort`, `MergeSort`).  
    Strategies don’t change the context’s internal state, they just provide different ways to do a job.
    
- **When to Use**:
    
    - You need to choose from **multiple algorithms** (or policies).
        
    - You want to avoid hardcoding algorithm choices inside a context.
        
- **Example**:  
    A `PaymentService` where you can plug in `CreditCardPayment`, `PayPalPayment`, `CryptoPayment`.


|Aspect|**State** 🏛️|**Strategy** 🛠️|
|---|---|---|
|**Purpose**|Change object behavior when its **state** changes|Allow selecting an **algorithm/policy** at runtime|
|**Who decides?**|The **object itself** (state transitions inside)|The **client or context** (chooses strategy)|
|**Transitions**|States usually know what the next state is|Strategies are independent, no transition logic|
|**Behavior**|Context behavior **evolves dynamically**|Context behavior is **consistent, just different flavors**|
|**Example**|Vending machine states, TCP connection states|Sorting algorithms, payment methods|


👉 **Analogy**:

- **State**: Think of a **traffic light** 🚦. It changes from Green → Yellow → Red automatically based on its state machine. The light decides itself what comes next.
    
- **Strategy**: Think of a **driver choosing a route** 🚗. The GPS lets you pick "fastest route," "shortest route," or "no tolls." The driver (client) decides.


## References