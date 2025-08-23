2025-08-23 10:59
Status: #baby
Tags: [[design pattern]]
## Main

## 📌 Definition

The **Builder Pattern** is a **creational design pattern** that lets you construct complex objects **step by step**. Instead of having a huge constructor with many parameters (some optional, some required), the Builder pattern makes object creation **flexible, readable, and controlled**.

## 📌 When to Use

- When a class has **too many constructor parameters** (a.k.a. _Telescoping Constructor problem_).
    
- When you want to make an object **immutable** but still easy to construct.
    
- When you want to build an object **step by step** and sometimes with different variations.

## 📌 UML Concept

`Client --> Builder --> Product`

- **Product** → the complex object being built.
    
- **Builder** → provides methods to set attributes step by step.
    
- **ConcreteBuilder** → implements the building steps.
    
- **Client** → uses the builder to construct the product.


## 📌 Example Problem

Suppose we want to create a `House` object with many optional fields:

- `walls` (required)
    
- `roof` (required)
    
- `garage` (optional)
    
- `swimmingPool` (optional)
    
- `garden` (optional)
    

Using normal constructors would lead to **messy overloaded constructors**.


```java
// Product
class House {
    private String walls;
    private String roof;
    private boolean garage;
    private boolean swimmingPool;
    private boolean garden;

    // Private constructor (only builder can access)
    private House(Builder builder) {
        this.walls = builder.walls;
        this.roof = builder.roof;
        this.garage = builder.garage;
        this.swimmingPool = builder.swimmingPool;
        this.garden = builder.garden;
    }

    @Override
    public String toString() {
        return "House [walls=" + walls + ", roof=" + roof +
               ", garage=" + garage + ", swimmingPool=" + swimmingPool +
               ", garden=" + garden + "]";
    }

    // Builder inner class
    public static class Builder {
        private String walls;
        private String roof;
        private boolean garage;
        private boolean swimmingPool;
        private boolean garden;

        public Builder(String walls, String roof) {  // required params
            this.walls = walls;
            this.roof = roof;
        }

        public Builder garage(boolean garage) {
            this.garage = garage;
            return this;
        }

        public Builder swimmingPool(boolean swimmingPool) {
            this.swimmingPool = swimmingPool;
            return this;
        }

        public Builder garden(boolean garden) {
            this.garden = garden;
            return this;
        }

        public House build() {
            return new House(this);
        }
    }
}


public class Main {
    public static void main(String[] args) {
        House house1 = new House.Builder("Brick Walls", "Concrete Roof")
                        .garage(true)
                        .swimmingPool(false)
                        .garden(true)
                        .build();

        House house2 = new House.Builder("Wood Walls", "Tile Roof")
                        .build(); // minimal house

        System.out.println(house1);
        System.out.println(house2);
    }
}
```

## 📌 Advantages

✅ Solves **Telescoping Constructor** problem.  
✅ Makes code **readable & maintainable** (`.garage(true).garden(false)` is clear).  
✅ Supports **immutable objects** (fields set once via builder).  
✅ Flexible for creating **different variations** of the same object.



## 📌 Real-world Examples

- **Java**:
    
    - `StringBuilder` (builds a string step by step).
        
    - `java.lang.StringBuffer`
        
    - `Stream.Builder`
        
- **Spring Framework**: `MockMvcBuilders`
    
- **Lombok**: `@Builder` annotation


## References