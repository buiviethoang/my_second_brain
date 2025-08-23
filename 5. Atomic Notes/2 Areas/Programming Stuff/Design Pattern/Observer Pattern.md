2025-08-23 11:47
Status: #baby
Tags: [[design pattern]]
## Main
👉 **Intent**:  
Define a **one-to-many dependency** between objects so that when **one object (Subject)** changes state, all its **dependents (Observers)** are automatically notified and updated.

## 🏠 Real World Analogy

Think of a **YouTube Channel**:

- The **channel** = **Subject**.
    
- The **subscribers** = **Observers**.
    
- When the channel uploads a new video, all subscribers get notified.


```java
import java.util.ArrayList;
import java.util.List;

// Observer
interface Observer {
    void update(String message);
}

// Concrete Observers
class User implements Observer {
    private String name;

    public User(String name) {
        this.name = name;
    }

    public void update(String message) {
        System.out.println(name + " received notification: " + message);
    }
}

// Subject
class Channel {
    private List<Observer> observers = new ArrayList<>();

    public void subscribe(Observer observer) {
        observers.add(observer);
    }

    public void unsubscribe(Observer observer) {
        observers.remove(observer);
    }

    public void notifyObservers(String message) {
        for (Observer o : observers) {
            o.update(message);
        }
    }
}

// Client
public class Main {
    public static void main(String[] args) {
        Channel channel = new Channel();

        Observer u1 = new User("Alice");
        Observer u2 = new User("Bob");

        channel.subscribe(u1);
        channel.subscribe(u2);

        channel.notifyObservers("New video uploaded!");

        channel.unsubscribe(u1);

        channel.notifyObservers("Live stream starting now!");
    }
}

```


## 🔹 Real-World Examples in Software

1. **GUI Frameworks**
    
    - Button click → notifies all registered listeners.
        
    - Java Swing, JavaFX, and Android use Observer heavily.
        
2. **Event Systems / Pub-Sub**
    
    - Kafka, RabbitMQ, or even Java’s `PropertyChangeListener`.
        
    - Publisher (subject) → notifies subscribers (observers).
        
3. **Model-View-Controller (MVC)**
    
    - Model = Subject.
        
    - Views = Observers.
        
    - When Model changes, all Views get updated.
        
4. **Realtime Applications**
    
    - Chat apps (WhatsApp, Slack): new message notifies all connected clients.
        
    - Stock price updates in trading platforms.


## 🔑 Characteristics

✔ **Loose coupling** — Subject doesn’t need to know details of Observers.  
✔ **Scalability** — many observers can listen to one subject.  
✔ **Dynamic** — observers can be added/removed at runtime.


## References