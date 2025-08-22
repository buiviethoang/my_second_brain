2025-08-21 21:20
Status: #baby
Tags: [[java]]
## Main
- **Aspect-Oriented Programming (AOP)** is a programming paradigm that allows you to separate **cross-cutting concerns** (logic that spans multiple modules) from the main business logic.

- Examples of cross-cutting concerns:
    - Logging
    - Security
    - Transaction management
    - Caching
    - Performance monitoring

Instead of duplicating these concerns inside many service methods, you extract them into **aspects**.

## AOP Key Concepts in Spring

- **Aspect** → A module that encapsulates a cross-cutting concern (e.g., LoggingAspect).
    
- **Join Point** → A point in program execution (like method execution or exception handling).
    
- **Advice** → The action taken at a join point (before, after, around, etc.).
    
- **Pointcut** → Expression that selects join points (e.g., all methods in a package).
    
- **Weaving** → Linking aspects with application code (done at runtime in Spring using proxies).


## Types of Advice in Spring AOP

- `@Before` → Runs before a method executes.
    
- `@AfterReturning` → Runs after a method successfully returns.
    
- `@AfterThrowing` → Runs if a method throws an exception.
    
- `@After` → Runs after method execution (regardless of outcome).
    
- `@Around` → Runs before and after method execution (most powerful, can control execution).


## Common Use Cases

- **Logging**: Track method calls, parameters, and execution time.
    
- **Security**: Check authentication/authorization before method calls.
    
- **Transactions**: Declarative transaction handling (`@Transactional` is AOP under the hood).
    
- **Monitoring**: Measure performance, collect metrics.
    
- **Error handling**: Centralized exception logging.


```java
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.aspectj.lang.annotation.AfterReturning;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.ProceedingJoinPoint;
			import org.springframework.stereotype.Component;

@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.service.*.*(..))")
    public void logBefore() {
        System.out.println("Before method execution");
    }

    @AfterReturning(
      pointcut = "execution(* com.example.service.*.*(..))",
      returning = "result")
    public void logAfterReturning(Object result) {
        System.out.println("Method returned: " + result);
    }

    @Around("execution(* com.example.service.*.*(..))")
    public Object logAround(ProceedingJoinPoint joinPoint) throws Throwable {
        System.out.println("Before method: " + joinPoint.getSignature());
        Object proceed = joinPoint.proceed(); // execute target method
        System.out.println("After method: " + joinPoint.getSignature());
        return proceed;
    }
}

```



## References

https://howtodoinjava.com/spring-aop-tutorial/