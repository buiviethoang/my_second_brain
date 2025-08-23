2025-08-23 14:49
Status: #baby
Tags: [[design pattern]]
## Main
The **Interpreter Pattern** defines a **grammar for a language** and uses **an interpreter to evaluate sentences in that language**.

- It’s typically used for **simple languages or expressions**, like mathematical formulas, scripting languages, or configuration expressions.
    
- Each symbol or rule in the language is represented by a class implementing a common interface.

## 🔹 **Real-World Analogy**

- **Math expression parser**: `3 + 5 * 2`
    
    - Each number, operator, and expression is a node.
        
    - Interpreter evaluates the expression tree to get the result.
        
- **Regular expressions**: Pattern defines grammar, matcher interprets it against text.
    
- **SQL or scripting language interpreters** in small apps.


## 🔹 **Structure**

1. **AbstractExpression** → Interface for all expressions (`interpret(context)`).
    
2. **TerminalExpression** → Represents leaf nodes (e.g., numbers, variables).
    
3. **NonTerminalExpression** → Combines other expressions (e.g., operators like +, *, AND, OR).
    
4. **Context** → Contains global information needed for interpretation.
    
5. **Client** → Builds expressions and invokes interpretation.



```java
// AbstractExpression
interface Expression {
    boolean interpret(String context);
}

// TerminalExpression
class TerminalExpression implements Expression {
    private String data;

    public TerminalExpression(String data) {
        this.data = data;
    }

    public boolean interpret(String context) {
        return context.contains(data);
    }
}

// NonTerminalExpression
class OrExpression implements Expression {
    private Expression expr1;
    private Expression expr2;

    public OrExpression(Expression expr1, Expression expr2) {
        this.expr1 = expr1;
        this.expr2 = expr2;
    }

    public boolean interpret(String context) {
        return expr1.interpret(context) || expr2.interpret(context);
    }
}

class AndExpression implements Expression {
    private Expression expr1;
    private Expression expr2;

    public AndExpression(Expression expr1, Expression expr2) {
        this.expr1 = expr1;
        this.expr2 = expr2;
    }

    public boolean interpret(String context) {
        return expr1.interpret(context) && expr2.interpret(context);
    }
}

// Client
public class InterpreterDemo {
    public static void main(String[] args) {
        Expression isAdult = new TerminalExpression("Adult");
        Expression hasLicense = new TerminalExpression("License");

        Expression canDrive = new AndExpression(isAdult, hasLicense);

        System.out.println(canDrive.interpret("Adult License")); // true
        System.out.println(canDrive.interpret("Adult"));         // false
    }
}

```


## 🔹 **When to Use**

- You have a **simple language or grammar** to interpret.
    
- You want to **represent expressions as objects**.
    
- You need a **flexible and extensible way to parse or evaluate commands**.


### 🔹 **Pros**

- Easy to extend with new expressions.
    
- Decouples grammar from interpretation logic.
    

### 🔹 **Cons**

- Can become **complex for large grammars**.
    
- Usually suitable for **small DSLs (Domain-Specific Languages)**, not full programming languages.



## References