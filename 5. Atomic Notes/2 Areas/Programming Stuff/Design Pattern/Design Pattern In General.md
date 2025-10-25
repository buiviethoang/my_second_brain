2025-08-23 10:42
Status: #baby
Tags: [[design pattern]]
## Main
"Design Patterns" are **proven solutions to common software design problems**. They provide templates and best practices to build maintainable, reusable, and scalable code. Patterns are not code themselves, but **guidelines** for structuring classes and objects.

They are typically grouped into three main categories (from the _Gang of Four_ book):

## 🔹 1. Creational Patterns (object creation)

Help create objects in a flexible and reusable way.

- **Singleton** → Ensures only one instance of a class exists (e.g., configuration, logging).
    
- **Factory Method** → Defines an interface for creating objects, but lets subclasses decide which class to instantiate.
    
- **Abstract Factory** → Creates families of related objects without specifying their concrete classes.
    
- **Builder** → Step-by-step object construction (useful for complex objects).
    
- **Prototype** → Creates objects by cloning existing ones.
    

---

## 🔹 2. Structural Patterns (class & object composition)

Deal with how classes and objects are combined.

- **Adapter** → Converts one interface into another that clients expect (like a translator).
    
- **Bridge** → Decouples abstraction from implementation so both can vary independently.
    
- **Composite** → Composes objects into tree structures (e.g., menus, file systems).
    
- **Decorator** → Dynamically adds new behavior to objects without modifying them.
    
	- **Facade** → Provides a simplified interface to a complex system.
    
- **Flyweight** → Shares common state across many small objects to save memory.
    
- **Proxy** → Provides a placeholder or surrogate for another object (e.g., lazy loading, access control).
    

---

## 🔹 3. Behavioral Patterns (object interaction)

Define how objects communicate and share responsibilities.

- **Chain of Responsibility** → Passes a request along a chain until one handler processes it.
    
- **Command** → Encapsulates a request as an object (useful for undo/redo, task queues).
    
- **Interpreter** → Defines a grammar and interpreter for a language.
    
- **Iterator** → Provides a way to traverse a collection without exposing its structure.
    
- **Mediator** → Centralizes complex communication between objects.
    
- **Memento** → Captures and restores an object’s state (useful for undo functionality).
    
- **Observer** → Defines a subscription mechanism (publish/subscribe, event listeners).
    
- **State** → Alters an object’s behavior when its state changes.
    
- **Strategy** → Defines a family of algorithms and makes them interchangeable.
    
- **Template Method** → Defines the skeleton of an algorithm, but lets subclasses override steps.
    
- **Visitor** → Adds new operations to objects without changing their classes.


### Analogy
# 🔹 Creational Patterns (object creation)

1. **Singleton** → _President of a country_  
    → Only **one** exists at a time, everyone refers to the same one.
    
2. **Factory Method** → _Coffee Shop_  
    → You order “latte” or “espresso”, the shop decides **which class of Coffee** to serve.
    
3. **Abstract Factory** → _Furniture Factory_  
    → A factory makes **families of products** (chair, sofa, table) for a particular style (Victorian, Modern).
    
4. **Builder** → _Ordering a Burger_  
    → Step-by-step: add bun → patty → cheese → lettuce → sauce → done. (Flexible construction).
    
5. **Prototype** → _Photocopy machine_  
    → Instead of building from scratch, you **clone an existing object**.

| Pattern              | Intent                                                                                                     | Real-World Analogy                                           | Key Idea                                                                    |
| -------------------- | ---------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ | --------------------------------------------------------------------------- |
| **Singleton**        | Ensure a class has only one instance and provide a global access point                                     | Database connection pool, Logger                             | Only one instance exists; provides a global point of access                 |
| **Factory Method**   | Define an interface for creating an object, but let subclasses decide which class to instantiate           | Document editor: create `WordDocument` or `PDFDocument`      | Subclasses handle the instantiation of concrete objects                     |
| **Abstract Factory** | Provide an interface for creating families of related objects without specifying concrete classes          | UI toolkit: create a family of components for Windows or Mac | Encapsulate a group of individual factories                                 |
| **Builder**          | Separate the construction of a complex object from its representation                                      | Building a house step by step (foundation, walls, roof)      | Step-by-step construction, same process can build different representations |
| **Prototype**        | Specify the kinds of objects to create using a prototypical instance, and create new objects by copying it | Cloning documents, copy-paste objects                        | Copy existing objects to create new ones instead of creating from scratch   |


## 🔹 **Creational Pattern Highlights**

1. **Encapsulate object creation**: Decouple the client code from concrete classes.
    
2. **Support flexibility and reuse**: Easily change which objects are created without changing the client.
    
3. **Reduce complexity**: Especially for complex objects with many parameters (**Builder**).
    
4. **Control instance management**: **Singleton** ensures only one instance exists.


# 🔹 Structural Patterns (class/object composition)

6. **Adapter** → _Travel plug adapter_  
    → Converts **EU plug → US socket**, so incompatible systems can work.
    
7. **Bridge** → _Remote control and TV_  
    → Remote = abstraction, TV = implementation. You can change either independently.
    
8. **Composite** → _Tree / File system_  
    → A folder can contain files **and** subfolders. Treat them uniformly.
    
9. **Decorator** → _Pizza toppings_  
    → Start with plain pizza, then dynamically **wrap it** with cheese, olives, mushrooms.
    
10. **Facade** → _Universal remote control_  
    → Instead of using 5 remotes (TV, AC, Speakers), you use **one simplified interface**.
    
11. **Flyweight** → _Chess pieces_  
    → You don’t create 32 separate “white pawn” objects; you share **one pawn object** with different positions.
    
12. **Proxy** → _Credit card_  
    → A card acts as a **proxy** for money in the bank. You don’t directly handle cash.

| Pattern       | Intent                                                                  | Real-World Analogy                                    | Key Idea                                                       |
| ------------- | ----------------------------------------------------------------------- | ----------------------------------------------------- | -------------------------------------------------------------- |
| **Adapter**   | Convert one interface into another expected by clients                  | Power plug adapter: US plug → EU socket               | Wraps an incompatible object to match expected interface       |
| **Bridge**    | Separate abstraction from implementation so they can vary independently | TV remote (abstraction) vs TV model (implementation)  | Decouple interface and implementation                          |
| **Composite** | Treat individual objects and compositions uniformly                     | Folder structure: folders contain files or subfolders | Build tree structures of objects that are handled the same way |
| **Decorator** | Add responsibilities to objects dynamically                             | Coffee with milk and sugar                            | Wrap objects to extend behavior without subclassing            |
| **Facade**    | Provide a simplified interface to a complex subsystem                   | Home theater remote controlling TV, DVD, sound system | Hide subsystem complexity behind a single interface            |
| **Flyweight** | Share common parts of objects to save memory                            | Text editor: letters share font objects               | Minimize memory usage by sharing state between objects         |
| **Proxy**     | Provide a surrogate or placeholder for another object                   | Virtual proxy for loading large images                | Control access to an object or add extra functionality         |

## 🔹 **Structural Pattern Highlights**

1. **Composition over inheritance**: Most structural patterns favor **object composition** to assemble structures dynamically.
    
2. **Simplify complex systems**: Patterns like **Facade** and **Proxy** hide or control complexity.
    
3. **Memory optimization**: **Flyweight** reduces memory usage when you have many similar objects.
    
4. **Flexible behavior extension**: **Decorator** allows behavior to be added at runtime.
    
5. **Uniformity in hierarchies**: **Composite** allows clients to treat single and composite objects the same way.



# 🔹 Behavioral Patterns (object interaction)

13. **Chain of Responsibility** → _Customer support hotline_  
    → Call goes → Level 1 → Level 2 → Manager, until someone handles it.
    
14. **Command** → _Restaurant order slip_  
    → The waiter writes an order (command), the chef executes it. Supports queue & undo (cancel order).
    
15. **Interpreter** → _Google Translate_  
    → Converts sentences into another language based on grammar rules.
    
16. **Iterator** → _TV remote channel surfing_  
    → Go through channels (collection) **without knowing how TV stores them internally**.
    
17. **Mediator** → _Air Traffic Control tower_  
    → Pilots don’t talk directly to each other; they communicate through the **mediator (ATC)**.
    
18. **Memento** → _Save game checkpoint_  
    → Stores state, so you can restore later (Undo / Load Game).
    
19. **Observer** → _YouTube subscribers_  
    → When a channel uploads, all subscribers get notified.
    
20. **State** → _Traffic light_  
    → Behavior changes depending on state (Red → Stop, Green → Go).
    
21. **Strategy** → _Navigation app routes_  
    → You can switch strategies: fastest route, shortest distance, avoid tolls.
    
22. **Template Method** → _Making tea vs coffee_  
    → Boil water (same step), then subclass decides → add tea leaves / add coffee powder.
    
23. **Visitor** → _Insurance agent visiting houses_  
    → You add new operations (**evaluate car**, **evaluate house**) without changing the classes themselves.


| Pattern                     | Intent                                                                    | Real-World Analogy                                            | Key Idea                                                        |
| --------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------- | --------------------------------------------------------------- |
| **Template Method**         | Define the skeleton of an algorithm, letting subclasses fill in the steps | Cooking a recipe: steps are fixed, ingredients can vary       | Base class controls the algorithm, subclasses customize steps   |
| **Strategy**                | Encapsulate interchangeable algorithms and make them pluggable            | GPS choosing "fastest route", "shortest route", "no tolls"    | Context delegates to a strategy object                          |
| **Observer**                | Notify multiple objects automatically when a subject changes              | YouTube channel sends notifications to subscribers            | One-to-many dependency, loose coupling                          |
| **Memento**                 | Capture and restore an object’s internal state                            | Undo/redo in a text editor                                    | Encapsulates state, separates it from external objects          |
| **State**                   | Change object behavior when internal state changes                        | Vending machine states: NoCoin → HasCoin → Sold               | Context behavior evolves dynamically based on state             |
| **Mediator**                | Centralize communication between objects                                  | Air traffic control tower coordinating planes                 | Colleagues interact only via mediator                           |
| **Chain of Responsibility** | Pass requests along a chain until someone handles it                      | Technical support levels: L1 → L2 → L3                        | Decouples sender and receiver, multiple possible handlers       |
| **Command**                 | Encapsulate a request as an object                                        | Remote control buttons for lights, undo/redo                  | Decouples invoker from receiver, supports undo, queuing, macros |
| **Interpreter**             | Evaluate sentences or expressions in a language                           | Boolean expressions: `"Adult AND License"`                    | Each element interprets itself according to a grammar           |
| **Visitor**                 | Add new operations to objects without changing their classes              | Shopping cart: calculate price, apply discount, print receipt | Separate algorithms from object structure                       |


### 🔑 **Behavioral Pattern Highlights**

1. **Delegation & Decoupling**: Most behavioral patterns aim to **reduce tight coupling** and **delegate responsibilities**.
    
    - Examples: **Strategy, State, Command, Mediator, Observer**
        
2. **Encapsulating Varying Behavior**: When behavior changes at runtime, encapsulate it.
    
    - Examples: **Strategy, State**
        
3. **Managing Communication**: When multiple objects interact, centralize or structure communication.
    
    - Examples: **Mediator, Observer, Chain of Responsibility**
        
4. **Separating Algorithms**: Separate the logic from the object structure.
    
    - Examples: **Visitor, Interpreter, Template Method**
        
5. **Undo/Redo / History**: Capture and restore object state cleanly.
    
    - Examples: **Memento, Command**


![[Pasted image 20250823104744.png]]


![[Pasted image 20250823104751.png]]


## References