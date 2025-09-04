2025-07-08 21:55
Status: #baby
Tags: [[java]]
## Main

### What is JDK, JRE, JVM, JAR? 
### 1. **JDK (Java Development Kit)**

- **What it is:** A full-featured software development kit required to develop Java applications.
    
- **Includes:**
    
    - **JRE** (Java Runtime Environment)
        
    - **JVM** (Java Virtual Machine)
        
    - **Development tools** like `javac` (Java compiler), `javadoc`, `jar`, and debugging tools.
        
- **Used by:** Developers to **write, compile, and debug** Java applications.
    
- ✅ **You need JDK** to **build** Java programs.
    

---

### 2. **JRE (Java Runtime Environment)**

- **What it is:** The runtime portion of Java used to **run** Java applications.
    
- **Includes:**
    
    - **JVM**
        
    - **Core Java libraries** and supporting files
        
- ❌ Does **not** include the compiler or development tools.
    
- ✅ You need JRE to **run** Java programs, **not** to write or compile them.
    

---

### 3. **JVM (Java Virtual Machine)**

- **What it is:** A virtual machine that runs Java **bytecode**.
    
- **Platform-dependent implementation** of a **platform-independent** Java program.
    
- It interprets or compiles `.class` files (bytecode) and executes them.
    
- Handles:
    
    - Memory management
        
    - Garbage collection
        
    - Security and exception handling
        

---

### 4. **JAR (Java ARchive)**

- **What it is:** A file format used to bundle many Java `.class` files and resources (images, text, etc.) into a **single archive**.
    
- **Similar to a ZIP file**, but specifically for Java.
    
- Makes deployment and distribution of Java apps easier.
    
- You can create a JAR using the `jar` tool (`jar cf myapp.jar *.class`).
    
- You can run a JAR file (if it's executable) with:

| Term    | Full Form                | Purpose                    | Includes                  | Who uses it?           |
| ------- | ------------------------ | -------------------------- | ------------------------- | ---------------------- |
| **JDK** | Java Development Kit     | To develop Java apps       | JRE + dev tools           | Developers             |
| **JRE** | Java Runtime Environment | To run Java apps           | JVM + libraries           | Users & developers     |
| **JVM** | Java Virtual Machine     | To execute Java bytecode   | Part of JRE               | All Java apps run here |
| **JAR** | Java Archive             | Package compiled Java code | `.class` files, resources | Developers, deployment |

### JVM Architecture
![[Pasted image 20250708220108.png]]

#### Class loader
- **BootStrap class loader**: This class loader is on the top of the class loader hierarchy. It loads the standard JDK classes in the JRE's _lib_ directory.
- **Extension class loader**: This class loader is in the middle of the class loader hierarchy and is the immediate child of the bootstrap class loader and loads the classes in the JRE's lib\ext directory.
- **Application class loader**: This class loader is at the bottom of the class loader hierarchy and is the immediate child of the application class loader. It loads the jars and classes specified by the **CLASSPATH ENV** variable.
#### Runtime data areas
The JVM spec defines certain run-time data areas that are needed during the execution of the program. Some of them are created while the **JVM starts up**. Others are **local to threads** and are created only when a thread is created (and destroyed when the thread is destroyed)
- **PC (Program Counter) Register**: local to each thread and contains the address of the JVM instruction that the thread is currently executing
- **Stack**: local to each thread and stores parameters, local variables and return addresses during method calls
- **Heap**: common to all threads and contains objects, classes' metadata, arrays, etc., that are created during run-time. 
	- created when the JVM starts and is destroyed when the JVM shuts down
	- You can control the amount of heap your JVM demands from the OS using certain flags (more on this later)
	- GC manages this space and continually removes dead objects to free up the space
- **Method area**: 
	- common to all threads and is created when the JVM starts up
	- stores per-class structures such as the constant pool (more on this later), the code for constructors and methods, method data, etc
- **Native Method Stacks**: When a thread invokes a native method, it enters a new world in which the structures and security restrictions of the Java virtual machine no longer hamper its freedom. A native method can likely access the runtime data areas of the virtual machine (it depends upon the native method interface), but can also do anything else it wants.

#### Execution engine
responsible for executing the bytecode
##### Garbage Collection
##### Interpreter
The interpreter Interprets the bytecode. It interprets the code fast but it's slow in execution.
##### JIT Complier
The JIT compiler is a main part of the Java runtime environment and it compiles **bytecodes** to **machine code** at runtime.

## References
https://www.tutorialspoint.com/java/java_jvm.htm
https://chatgpt.com/c/686d2ffa-e368-8012-b1ff-4e1cf2c82e19