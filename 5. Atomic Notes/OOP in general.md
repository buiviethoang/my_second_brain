2025-08-25 21:05
Status: #baby
Tags: [[computer science]] [[java]]
## Main
**Object-Oriented Programming (OOP)** is a programming paradigm that organizes software design around **objects**, which represent **real-world entities** or **abstract concepts**.  
Objects bundle together **data (attributes/fields)** and **behavior (methods/functions)** into a single unit.

## 🔹 4 Main Principles of OOP

1. **Encapsulation**
    
    - Binding data and behavior into one unit (class).
        
    - Hides implementation details from the outside world (via `private`, `protected`, `public`).
        
    - Example: You don’t know how a car engine works internally, you just call `car.start()`.
        
2. **Abstraction**
    
    - Focuses only on essential features, hides unnecessary details.
        
    - Example: You interact with a TV remote without knowing its internal wiring.
        
    - Achieved using abstract classes or interfaces.
        
3. **Inheritance**
    
    - Allows a class (child/subclass) to inherit fields and methods from another class (parent/superclass).
        
    - Promotes code reuse.
        
    - Example: `Car` and `Bike` inherit from `Vehicle`.
        
4. **Polymorphism** ("many forms")
    
    - The ability of objects to take multiple forms, usually through method overriding or overloading.
        
    - Example: `draw()` method behaves differently for `Circle`, `Square`, and `Triangle`.


## 🔹 Benefits of OOP

- **Modularity**: Code is organized into independent objects.
    
- **Reusability**: Reuse classes through inheritance and composition.
    
- **Maintainability**: Easier to update, fix, or extend.
    
- **Scalability**: Better structure for large, complex systems.
    
- **Abstraction of complexity**: Hide unnecessary details from users.

## 🔹 Real-world Analogy

Think of **OOP like modeling the real world**:

- **Class** = blueprint (like a “Car” design).
    
- **Object** = an actual instance (a specific Toyota car).
    
- **Encapsulation** = the car’s engine is hidden, you just press `start()`.
    
- **Inheritance** = “ElectricCar” extends “Car”.
    
- **Polymorphism** = `drive()` means something slightly different for a car vs. a bike.


### OOP vs Functional Programming
|Aspect|OOP 🏗️|FP 🔢|
|---|---|---|
|**Unit of code**|Object (class + data + methods)|Function (pure, reusable)|
|**Data**|Mutable (can change)|Immutable (never changes)|
|**State**|Objects hold state|Stateless, only input/output|
|**Reusability**|Inheritance, polymorphism|Function composition|
|**Flow control**|Loops, method calls|Recursion, function chaining|
|**Concurrency**|Harder (due to shared state)|Easier (stateless functions)|
|**Examples**|Java, C#, Python (OOP-style)|Haskell, Elixir, JS (FP-style)|

## 🔹 Real-World Analogy

- **OOP**: Like building a **car factory** — you design blueprints (classes) and create cars (objects). Each car has **state** (fuel, speed) and **behavior** (drive, brake).
    
- **FP**: Like a **mathematical equation** — given the same input, you always get the same output, no hidden state. Example: `f(x) = x²`.

👉 In practice: Most modern languages (Python, Java, JavaScript, C#) mix **OOP + FP** so you can pick the best tool for each problem.




## References