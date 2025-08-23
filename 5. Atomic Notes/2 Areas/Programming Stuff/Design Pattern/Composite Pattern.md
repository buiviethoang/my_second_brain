2025-08-23 15:34
Status: #baby
Tags: [[design pattern]]
## Main
### **Intent**

The **Composite pattern** lets you **treat individual objects and compositions of objects uniformly**.

It’s useful when you have a **tree-like structure** of objects, where **leaf nodes** and **containers** (composites) should be handled the same way by the client.

### **Key Components**

1. **Component** – declares the interface for objects in the composition.
    
2. **Leaf** – represents individual objects (cannot have children).
    
3. **Composite** – represents a group of components and implements the same interface.


Component
   ^
   |
+---------+
|         |
Leaf    Composite
           |
        [Component children...]



```java
// Component
interface FileSystemComponent {
    void showDetails();
}

// Leaf (File)
class FileLeaf implements FileSystemComponent {
    private String name;

    public FileLeaf(String name) {
        this.name = name;
    }

    @Override
    public void showDetails() {
        System.out.println("File: " + name);
    }
}


// Composite (Folder)
class FolderComposite implements FileSystemComponent {
    private String name;
    private List<FileSystemComponent> children = new ArrayList<>();

    public FolderComposite(String name) {
        this.name = name;
    }

    public void add(FileSystemComponent component) {
        children.add(component);
    }

    public void remove(FileSystemComponent component) {
        children.remove(component);
    }

    @Override
    public void showDetails() {
        System.out.println("Folder: " + name);
        for (FileSystemComponent component : children) {
            component.showDetails();
        }
    }
}

// Client Usage
public class Main {
    public static void main(String[] args) {
        FileSystemComponent file1 = new FileLeaf("file1.txt");
        FileSystemComponent file2 = new FileLeaf("file2.txt");

        FolderComposite folder1 = new FolderComposite("Folder1");
        folder1.add(file1);
        folder1.add(file2);

        FileSystemComponent file3 = new FileLeaf("file3.txt");
        FolderComposite rootFolder = new FolderComposite("RootFolder");
        rootFolder.add(folder1);
        rootFolder.add(file3);

        rootFolder.showDetails();
    }
}




```

- The client interacts with **FileLeaf** and **FolderComposite** through the same interface.

### **Key Advantages**

- **Simplifies client code**: Treats individual objects and compositions the same way.
    
- **Makes adding new components easier**.
    
- **Supports recursive structures** naturally.
    

### **Disadvantages**

- Can make design **too general**, possibly allowing invalid operations on leaf nodes.

## References