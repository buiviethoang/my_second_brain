2025-08-23 11:50
Status: #baby
Tags: [[design pattern]]
## Main
The **Memento Pattern** is a **behavioral design pattern** that lets you **capture and externalize an object’s internal state** (without exposing its internals), so that the object can later be **restored** to this state.

It’s often described as **“undo/rollback”** support.

## 🔹 Participants

1. **Originator** → The object whose state we want to save and restore.
    
2. **Memento** → A snapshot of the Originator’s state (but usually hidden from others).
    
3. **Caretaker** → The object that asks for the state to be saved and restores it when needed.

## 🔹 Real-World Analogy

- **Text editor undo feature**: Every time you type, the editor saves a snapshot of the document (memento). If you hit "Undo," it rolls back to the last snapshot.
    
- **Game save system**: A player can save the game (memento) and later restore it to continue from that exact point.

```java
// Memento
class Memento {
    private final String state;

    public Memento(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }
}

// Originator
class TextEditor {
    private String content;

    public void setContent(String content) {
        System.out.println("Setting content: " + content);
        this.content = content;
    }

    public String getContent() {
        return content;
    }

    // Save current state into Memento
    public Memento save() {
        return new Memento(content);
    }

    // Restore state from Memento
    public void restore(Memento memento) {
        content = memento.getState();
        System.out.println("Restored content: " + content);
    }
}

// Caretaker
class History {
    private final java.util.Stack<Memento> states = new java.util.Stack<>();

    public void push(Memento memento) {
        states.push(memento);
    }

    public Memento pop() {
        return states.pop();
    }
}

// Demo
public class MementoDemo {
    public static void main(String[] args) {
        TextEditor editor = new TextEditor();
        History history = new History();

        editor.setContent("Version 1");
        history.push(editor.save());

        editor.setContent("Version 2");
        history.push(editor.save());

        editor.setContent("Version 3");

        // Undo
        editor.restore(history.pop()); // Restores "Version 2"
        editor.restore(history.pop()); // Restores "Version 1"
    }
}

```

## When to Use

- When you need **undo/redo functionality**.
    
- When you want to **preserve object encapsulation** (don’t expose internal details).
    
- In systems like **editors, games, transactions, or caching**.

## References