2025-07-09 22:19
Status: #baby
Tags: [[java]]
## Main
### Category
- Checked exceptions:  an exception that is checked (notified) by the compiler at compilation-time. These exceptions cannot simply be ignored, the programmer should take care of (handle) these exceptions.
- Unchecked exceptions: an exception that occurs at the time of execution. These are also called as Runtime Exceptions, ignored at the time of compilation.
- Errors: These are not exceptions at all, but problems that arise beyond the control of the user or the programmer. Errors are typically ignored in your code because you can rarely do anything about an error. For example, if a stack overflow occurs, an error will arise. They are also ignored at the time of compilation.

![[Pasted image 20250709222211.png]]

	All exception classes are subtypes of the java.lang.Exception class

## References
https://www.tutorialspoint.com/java/java_exceptions.htm