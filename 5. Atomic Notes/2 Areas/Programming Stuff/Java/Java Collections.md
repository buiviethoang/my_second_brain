2025-07-09 22:10
Status: #baby
Tags: [[java]]
## Main

![[Pasted image 20250709221111.png]]

###  - Number -

![[Pasted image 20250709221528.png]]


The object of the wrapper class contains or wraps its respective primitive data type. Converting primitive data types into object is called **boxing**, and this is taken care by the compiler. Therefore, while using a wrapper class you just need to pass the value of the primitive data type to the constructor of the Wrapper class.

And the Wrapper object will be converted back to a primitive data type, and this process is called unboxing. The **Number** class is part of the java.lang package.

|Term|Description|Example|
|---|---|---|
|**Boxing (Autoboxing)**|Converting a **primitive type** into its corresponding **wrapper class**|`int → Integer`|
|**Unboxing**|Converting a **wrapper class** back into its corresponding **primitive type**|`Integer → int`|

Why is it Needed in Java?
- Collections Only Store Objects: Java collections (e.g., `ArrayList`, `HashMap`) **do not work with primitives** (`int`, `double`, etc.).
- Object-Oriented Design: Java is an **object-oriented** language, but primitive types are **not objects**.
- Null Support: Wrapper classes can be `null` (e.g., `Integer x = null;`) but primitives cannot (`int x = null;` is illegal). Useful in databases or APIs that return no value.
- Utility Methods: Wrapper classes provide useful **methods** (unlike primitives).
- Generics Compatibility: Java generics work with objects only.
- Performance: Boxing and unboxing can add **overhead** (temporary objects are created). In performance-critical code (like tight loops), prefer **primitives**.
## References
https://www.tutorialspoint.com/java/java_collections.htm
https://www.tutorialspoint.com/java/java_lang_number.htm