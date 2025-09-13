2025-09-08 21:36
Status: 
Topic: 
Tags: [[design pattern]]
## Main
The **Iterator Pattern** is one of the **behavioral design patterns**. It provides a standard way to access elements of a collection (like a list, set, or custom aggregate object) sequentially without exposing the collection’s internal representation.

## 🔑 Key Points

- **Purpose:** To traverse a collection object without exposing its internal details.
    
- **Problem it solves:** You want a uniform way to iterate over different collection structures (array, list, tree, graph, etc.) without having to know their internal mechanics.
    
- **Structure:**
    
    1. **Iterator (interface):** Defines methods like `hasNext()`, `next()`.
        
    2. **ConcreteIterator:** Implements the iterator interface for a specific collection.
        
    3. **Aggregate (interface):** Defines a method `createIterator()`.
        
    4. **ConcreteAggregate:** Implements the aggregate interface and returns a `ConcreteIterator`.


```java
// Iterator interface
interface Iterator<T> {
    boolean hasNext();
    T next();
}

// Aggregate interface
interface Aggregate<T> {
    Iterator<T> createIterator();
}

// ConcreteAggregate
class NameRepository implements Aggregate<String> {
    private String[] names = {"John", "Jane", "Alice", "Bob"};

    @Override
    public Iterator<String> createIterator() {
        return new NameIterator();
    }

    private class NameIterator implements Iterator<String> {
        int index = 0;

        @Override
        public boolean hasNext() {
            return index < names.length;
        }

        @Override
        public String next() {
            if (this.hasNext()) {
                return names[index++];
            }
            return null;
        }
    }
}

// Client
public class IteratorPatternDemo {
    public static void main(String[] args) {
        NameRepository repository = new NameRepository();
        Iterator<String> iterator = repository.createIterator();

        while (iterator.hasNext()) {
            System.out.println("Name: " + iterator.next());
        }
    }
}
```

## 🎯 When to Use

- When you want to provide multiple ways to traverse a collection (forward, backward, filtered, etc.).
    
- When you want to hide the collection’s internal structure from clients.
    
- When you want a **uniform traversal interface** across different types of collections.

## References