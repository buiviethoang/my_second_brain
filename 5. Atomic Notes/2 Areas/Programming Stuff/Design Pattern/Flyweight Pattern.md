2025-08-23 15:22
Status: #baby
Tags: [[design pattern]]
## Main
### **Intent**

The **Flyweight pattern** is used to **minimize memory usage** by **sharing as much data as possible** between similar objects.

It is especially useful when you have **many objects with repeating data**.


### **Key Concepts**

1. **Intrinsic State** – the part of the object’s state that **can be shared** (does not change across contexts).
    
2. **Extrinsic State** – the part of the object’s state that **varies depending on context** (passed in externally).
    
3. **Flyweight Factory** – ensures that **shared objects are reused**, rather than creating new ones every time.\


Flyweight
   ^
   |
ConcreteFlyweight
       \
        FlyweightFactory
Client




- Clients request Flyweight objects from the **factory**.
    
- **Intrinsic state** is stored in the Flyweight.
    
- **Extrinsic state** is passed from the client when using the Flyweight.


```java

// Flyweight interface
interface Character {
    void display(int fontSize);
}

// ConcreteFlyweight
class ConcreteCharacter implements Character {
    private char symbol; // intrinsic state

    public ConcreteCharacter(char symbol) {
        this.symbol = symbol;
    }

    @Override
    public void display(int fontSize) { // extrinsic state
        System.out.println("Character: " + symbol + " with font size " + fontSize);
    }
}

// FlyweightFactory
class CharacterFactory {
    private Map<Character, ConcreteCharacter> characters = new HashMap<>();

    public Character getCharacter(char symbol) {
        characters.putIfAbsent(symbol, new ConcreteCharacter(symbol));
        return characters.get(symbol);
    }
}


public class Main {
    public static void main(String[] args) {
        CharacterFactory factory = new CharacterFactory();

        Character a1 = factory.getCharacter('A');
        Character a2 = factory.getCharacter('A');
        Character b1 = factory.getCharacter('B');

        a1.display(12);
        a2.display(14);
        b1.display(12);

        System.out.println(a1 == a2); // true, shared object
    }
}


```

`a1` and `a2` are the **same object**. Only one `A` character exists in memory.

### **Key Advantages**

- **Reduces memory usage** when you have many similar objects.
    
- **Improves performance** by reusing shared objects.
    
- Supports **large numbers of objects** efficiently.
    

### **Disadvantages**

- Extra complexity for managing **intrinsic and extrinsic states**.
    
- Can make code **harder to understand** if overused.

### Real-world example
### **Scenario:** Reusing Report Templates in a Reporting System

Imagine a system that generates reports. Each report has a **template** (shared, intrinsic state) and **parameters** (extrinsic state).

Instead of creating a new template object for each report, we **reuse templates**.


```java
public interface ReportTemplate {
    void generateReport(Map<String, Object> parameters);
}


public class ConcreteReportTemplate implements ReportTemplate {
    private final String templateName; // intrinsic state

    public ConcreteReportTemplate(String templateName) {
        this.templateName = templateName;
    }

    @Override
    public void generateReport(Map<String, Object> parameters) { // extrinsic state
        System.out.println("Generating report using template: " + templateName);
        System.out.println("Parameters: " + parameters);
    }
}


@Component
public class ReportTemplateFactory {
    private final Map<String, ReportTemplate> templates = new HashMap<>();

    public ReportTemplate getTemplate(String templateName) {
        templates.putIfAbsent(templateName, new ConcreteReportTemplate(templateName));
        return templates.get(templateName);
    }
}



@SpringBootApplication
public class DemoApplication implements CommandLineRunner {

    @Autowired
    private ReportTemplateFactory factory;

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

    @Override
    public void run(String... args) {
        Map<String, Object> params1 = Map.of("userId", 1, "date", "2025-08-23");
        Map<String, Object> params2 = Map.of("userId", 2, "date", "2025-08-23");

        ReportTemplate templateA1 = factory.getTemplate("SalesReport");
        ReportTemplate templateA2 = factory.getTemplate("SalesReport");
        ReportTemplate templateB = factory.getTemplate("InventoryReport");

        templateA1.generateReport(params1);
        templateA2.generateReport(params2);
        templateB.generateReport(Map.of("warehouseId", 10));

        System.out.println(templateA1 == templateA2); // true, shared object
    }
}

```

### **Key Benefits in this Example**

- **Memory efficiency**: Only one instance of each template exists.
    
- **Performance improvement**: Avoids repeatedly loading/creating templates.
    
- **Separation of intrinsic/extrinsic state**: Template is intrinsic; report parameters are extrinsic.
## References