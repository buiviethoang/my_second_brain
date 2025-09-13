2025-08-23 11:57
Status: #baby
Tags: [[design pattern]]
## Main
The **Mediator Pattern** defines an object (**Mediator**) that **encapsulates how a set of objects interact**. Instead of objects communicating directly with each other (which leads to a complex web of dependencies), they interact **only through the mediator**.

This reduces coupling between objects and centralizes communication logic.

## 🔹 Problem It Solves

Imagine you have a system like an **air traffic control tower**:

- Planes must talk to each other to avoid collisions.
    
- If each plane communicates directly with every other plane, the system becomes messy (lots of connections, difficult to manage).
    
- Instead, all planes talk to the **control tower** (Mediator), which manages communication.
    

This avoids chaos and reduces dependencies between objects.


## 🔹 Structure

- **Mediator (Interface/Abstract Class)** → Defines communication methods.
    
- **ConcreteMediator** → Implements coordination logic between Colleagues.
    
- **Colleague** → Objects that communicate via the Mediator, not directly with each other.



```java
// Mediator
interface ChatMediator {
    void sendMessage(String message, User user);
    void addUser(User user);
}

// Concrete Mediator
class ChatRoom implements ChatMediator {
    private List<User> users = new ArrayList<>();

    @Override
    public void addUser(User user) {
        users.add(user);
    }

    @Override
    public void sendMessage(String message, User sender) {
        for (User u : users) {
            if (u != sender) {
                u.receive(message);
            }
        }
    }
}

// Colleague
abstract class User {
    protected ChatMediator mediator;
    protected String name;

    public User(ChatMediator mediator, String name) {
        this.mediator = mediator;
        this.name = name;
    }

    public abstract void send(String message);
    public abstract void receive(String message);
}

// Concrete Colleague
class ChatUser extends User {
    public ChatUser(ChatMediator mediator, String name) {
        super(mediator, name);
    }

    @Override
    public void send(String message) {
        System.out.println(name + " sends: " + message);
        mediator.sendMessage(message, this);
    }

    @Override
    public void receive(String message) {
        System.out.println(name + " receives: " + message);
    }
}

// Client
public class MediatorPatternDemo {
    public static void main(String[] args) {
        ChatMediator chatRoom = new ChatRoom();

        User user1 = new ChatUser(chatRoom, "Alice");
        User user2 = new ChatUser(chatRoom, "Bob");
        User user3 = new ChatUser(chatRoom, "Charlie");

        chatRoom.addUser(user1);
        chatRoom.addUser(user2);
        chatRoom.addUser(user3);

        user1.send("Hello everyone!");
        user2.send("Hi Alice!");
    }
}

```


## 🔹 When to Use

- When many objects interact in complex but **well-defined ways**.
    
- To avoid **tight coupling** between components.
    
- Common in **UI frameworks, chat systems, workflow engines, and event-driven systems**.


👉 Quick analogy:

- **Without Mediator:** Every class is directly connected (spaghetti).
    
- **With Mediator:** One central hub coordinates communication (clean + manageable).


### Mediator vs Observer [[Observer Pattern]]

| Aspect            | **Observer**                               | **Mediator**                             |
| ----------------- | ------------------------------------------ | ---------------------------------------- |
| **Purpose**       | Notify multiple objects about state change | Centralize complex communication         |
| **Coupling**      | Subject → observers (loosely coupled)      | Colleagues → mediator (loosely coupled)  |
| **Control**       | Observers decide how to react              | Mediator decides how messages are routed |
| **Communication** | One-to-many                                | Many-to-many (centralized)               |
| **Example**       | Stock price updates → traders              | Chat room / Air traffic control          |

### **Analogy**

- **Observer:** Newspaper publisher sends updates to all subscribers. Subscribers read and react on their own.
    
- **Mediator:** Airport control tower coordinates all airplanes. Planes do nothing on their own; they follow the mediator’s instructions.


✅ **Summary**

- Use **Observer** when you want **automatic notifications** about changes.
    
- Use **Mediator** when you want to **control complex interactions** between objects.

## References