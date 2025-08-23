2025-08-23 14:51
Status: #baby
Tags: [[design pattern]]
## Main

The **Visitor Pattern** allows you to **separate an algorithm from the objects on which it operates**.

- You can **add new operations** to an object structure **without modifying the objects**.
    
- It’s especially useful when you have a **complex object structure** (like a tree) and want to perform operations on nodes in different ways.

## **Real-World Analogy**

- **Shopping cart checkout system**:
    
    - Items: books, electronics, groceries (different types of objects).
        
    - Visitor: calculates total price, applies discounts, or prints receipts.
        
    - You can add a **new operation** (e.g., generate tax report) without changing the item classes.
        
- **Compiler**:
    
    - Abstract Syntax Tree nodes (expressions, statements).
        
    - Visitor: performs type checking, code generation, optimization.

## 🔹 **Structure**

1. **Visitor (interface)** → Declares visit methods for each concrete element type.
    
2. **ConcreteVisitor** → Implements operations on elements.
    
3. **Element (interface)** → Declares `accept(Visitor)` method.
    
4. **ConcreteElement** → Implements `accept()` by calling `visitor.visit(this)`.
    
5. **ObjectStructure** → Collection of elements; lets visitors traverse it.


```java
// Visitor Interface
interface ShoppingCartVisitor {
    int visit(Book book);
    int visit(Fruit fruit);
}

// Concrete Visitor
class ShoppingCartVisitorImpl implements ShoppingCartVisitor {
    public int visit(Book book) {
        int cost = book.getPrice();
        System.out.println("Book ISBN::" + book.getIsbn() + " cost =" + cost);
        return cost;
    }

    public int visit(Fruit fruit) {
        int cost = fruit.getPricePerKg() * fruit.getWeight();
        System.out.println(fruit.getName() + " cost = " + cost);
        return cost;
    }
}

// Element Interface
interface ItemElement {
    int accept(ShoppingCartVisitor visitor);
}

// Concrete Elements
class Book implements ItemElement {
    private int price;
    private String isbn;

    public Book(int price, String isbn) {
        this.price = price;
        this.isbn = isbn;
    }

    public int getPrice() { return price; }
    public String getIsbn() { return isbn; }

    public int accept(ShoppingCartVisitor visitor) {
        return visitor.visit(this);
    }
}

class Fruit implements ItemElement {
    private int pricePerKg;
    private int weight;
    private String name;

    public Fruit(int pricePerKg, int weight, String name) {
        this.pricePerKg = pricePerKg;
        this.weight = weight;
        this.name = name;
    }

    public int getPricePerKg() { return pricePerKg; }
    public int getWeight() { return weight; }
    public String getName() { return name; }

    public int accept(ShoppingCartVisitor visitor) {
        return visitor.visit(this);
    }
}

// Client
public class VisitorPatternDemo {
    public static void main(String[] args) {
        ItemElement[] items = new ItemElement[] {
            new Book(20, "1234"),
            new Book(100, "5678"),
            new Fruit(10, 2, "Banana"),
            new Fruit(5, 5, "Apple")
        };

        int total = 0;
        ShoppingCartVisitor visitor = new ShoppingCartVisitorImpl();
        for (ItemElement item : items) {
            total += item.accept(visitor);
        }

        System.out.println("Total Cost = " + total);
    }
}

```


## 🔹 **When to Use**

- When you need to **perform operations across a set of objects** of different types.
    
- When you want to **add new operations without changing the object structure**.
    
- Especially useful with **composite structures or ASTs** (Abstract Syntax Trees).


### 🔹 **Pros**

- Adds new operations **without modifying existing classes**.
    
- Separates **algorithms from objects**.
    
- Easy to extend with new visitors.
    

### 🔹 **Cons**

- Adding a new **element type** requires changing all visitors.
    
- Can be complex for simple object structures.


### Compare with Interpreter
**Purpose:**

- To **evaluate sentences in a language or expressions**.
    
- Each element in the expression implements an `interpret()` method.
    
- Focus is on **parsing and evaluating**.
    

**Key Points:**

- Works with a **grammar or language structure**.
    
- Each expression knows how to interpret itself.
    
- Useful for **small DSLs, mathematical expressions, Boolean expressions**.
    

**Example:**

- Boolean expressions: `"Adult AND License"`
    
- Math expressions: `"3 + 5 * 2"`
    

---

## **2️⃣ Visitor Pattern**

**Purpose:**

- To **add new operations to existing object structures** without modifying the classes.
    
- Each element implements an `accept(visitor)` method.
    
- Focus is on **separating algorithms from objects**.
    

**Key Points:**

- Works with **complex object structures**, often composites or trees.
    
- Visitor encapsulates operations; elements delegate to visitor.
    
- Useful for **calculations, printing, exporting, reporting**.
    

**Example:**

- Shopping cart: Calculate price, print receipt, apply discounts.
    
- AST (Abstract Syntax Tree): Type checking, code generation.



|Aspect|**Interpreter**|**Visitor**|
|---|---|---|
|**Purpose**|Evaluate expressions in a language|Add operations to object structures|
|**Focus**|Parsing and interpreting|Separating algorithms from objects|
|**Element**|Implements `interpret()`|Implements `accept(visitor)`|
|**Operation**|Encapsulated in the element itself|Encapsulated in a separate visitor|
|**Usage Example**|Boolean expressions, math parser|Shopping cart pricing, AST traversal|




## References