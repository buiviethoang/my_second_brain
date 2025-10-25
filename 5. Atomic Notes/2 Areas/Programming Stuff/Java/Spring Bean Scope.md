2025-08-21 21:36
Status: #baby
Tags: [[java]]
## Main
**Bean Scope** defines the **lifecycle and visibility** of a bean (i.e., how many instances of a bean are created and how they are shared).
By default, Spring beans are **singleton**, but there are other scopes too.

## **Common Bean Scopes in Spring**

### 1. **Singleton (default)**
- **One instance per Spring container**.
- Every request for this bean returns the same instance.
- Good for **stateless services**.

### 2. **Prototype**
- **A new instance every time** the bean is requested.
- Useful for **stateful beans** or beans with changing data.

⚠️ In `prototype`, Spring creates the bean but does **not manage its full lifecycle** (e.g., no `@PreDestroy` callback).

### 3. **Request** (Web-aware scope)
- One bean instance **per HTTP request**.
- Only works in a **web application** context.

### 4. **Session**
- One bean instance **per HTTP session**.
- Different users get different instances.

### 5. **Application**
- One bean instance **per ServletContext (web app)**.
- Shared across all sessions and requests.

### 6. **WebSocket**
- One bean instance per **WebSocket session**.
- Useful for messaging/websocket applications.

| Scope           | Lifecycle                          | Usage                               |
| --------------- | ---------------------------------- | ----------------------------------- |
| **singleton**   | One per Spring container (default) | Stateless service beans             |
| **prototype**   | New instance each time requested   | Stateful beans, short-lived objects |
| **request**     | One per HTTP request               | Request-scoped data in web apps     |
| **session**     | One per HTTP session               | User-specific data across requests  |
| **application** | One per ServletContext             | Shared app-wide data                |
| **websocket**   | One per WebSocket session          | WebSocket messaging apps            |
```java
@Configuration
public class AppConfig {

    @Bean
    @Scope("prototype")
    public MyPrototypeBean myPrototypeBean() {
        return new MyPrototypeBean();
    }
}

```

## References