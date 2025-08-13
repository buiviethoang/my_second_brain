2025-08-12 21:47
Status: #baby
Tags: [[java]]
## Main
### What
Generics in Java let you write **type-safe**, **reusable** classes, interfaces, and methods that can work with different data types **without sacrificing type checking at compile time**.

They were introduced in **Java 5** to remove the need for excessive casting and to catch type-related errors earlier.

## 1️⃣ Why Generics?

Before generics:

`List list = new ArrayList(); list.add("Hello"); String s = (String) list.get(0); // Manual cast`

- You can accidentally add the wrong type (`list.add(123)` would compile!).
    
- Casting at runtime can cause **`ClassCastException`**.

With generics:

`List<String> list = new ArrayList<>(); list.add("Hello"); // list.add(123); // ❌ Compile-time error String s = list.get(0); // No cast needed`


## 2️⃣ Generic Syntax

**Basic format:**

`class ClassName<T> { ... }`

Here `T` is a **type parameter** (placeholder for a type).  
Common type parameter names:

- `T` – Type
    
- `E` – Element (collection element)
    
- `K` – Key
    
- `V` – Value
    
- `N` – Number
    

Example:

`public class Box<T> {     private T value;      public void set(T value) { this.value = value; }     public T get() { return value; } }`

Usage:

`Box<Integer> intBox = new Box<>(); intBox.set(123); System.out.println(intBox.get()); // 123`

## 3️⃣ Generic Methods

A generic method declares its type parameter **before** the return type:

`public class Utils {     public static <T> void printArray(T[] array) {         for (T element : array) {             System.out.println(element);         }     } }`

Usage:
`String[] names = {"Alice", "Bob"}; Integer[] nums = {1, 2, 3}; Utils.printArray(names); Utils.printArray(nums);`


You can **restrict** the type parameter to a certain type (or subtype).

**Upper bound (`extends`)**:

`public <T extends Number> void process(T num) {     System.out.println(num.doubleValue()); }`

- Works for `Integer`, `Double`, etc.
    
- **`extends`** means "is-a subtype of" (for classes) or "implements" (for interfaces).
    

**Lower bound (`super`)**:


`public void addNumbers(List<? super Integer> list) {     list.add(123); // Allowed }`

- `? super Integer` means "Integer or any superclass of Integer".
    

## 5️⃣ Wildcards (`?`)

Wildcards are for **unknown types**:

- `?` – unknown type
    
- `? extends T` – unknown type that is a subtype of `T`
    
- `? super T` – unknown type that is a supertype of `T`
    

Example:

`List<? extends Number> nums = List.of(1, 2.5); // Read-only List<? super Integer> ints = new ArrayList<>(); // Can add Integer`


## 6️⃣ Type Erasure

Generics are a **compile-time feature**:

- At runtime, `List<String>` and `List<Integer>` are both just `List`.
    
- This is called **type erasure**.
    
- This means **no** primitive types (`List<int>` ❌) and **no** reflection on generic types without tricks.
    

## 7️⃣ Benefits

✔ Compile-time type safety  
✔ Eliminates the need for explicit casting  
✔ Improves code reusability and readability



![[Pasted image 20250812214917.png]]

### Object Class In Java
In Java, the **`Object`** class is the **root** of the class hierarchy — every class implicitly extends `Object` (directly or indirectly).

If you don’t explicitly extend another class, your class automatically extends `Object`.
## **Why `Object` is important**

- Provides a **common API** for all objects
    
- Makes **polymorphism** possible (`Object obj = new String("Hi")`)
    
- Works as a **universal container type**
    
- Essential for **collections**, reflection, and synchronization


## References

https://viblo.asia/p/lam-chu-generics-trong-java-E1XVOjXELMz