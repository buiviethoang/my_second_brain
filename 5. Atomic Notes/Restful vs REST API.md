2025-09-24 07:18
Tags: [[api]]
## Main
### **1. REST**

- **REST** stands for **Representational State Transfer**.
    
- It’s an **architectural style** for building web services, introduced by Roy Fielding in his PhD dissertation (2000).
    
- REST is **not a protocol or a standard** — it’s a set of **constraints** and principles for designing networked applications.
    

Core **REST constraints**:

1. **Client-Server**: Separation of client and server concerns.
    
2. **Stateless**: Each request from client to server must contain all the info needed (no session state stored on server).
    
3. **Cacheable**: Responses must define themselves as cacheable or not.
    
4. **Uniform Interface**: A standard way of interacting with resources (e.g., URIs, HTTP methods).
    
5. **Layered System**: Architecture can be composed of hierarchical layers.
    
6. **Code on Demand (optional)**: Servers can send executable code to clients (e.g., JavaScript).

### **2. RESTful API**

- A **RESTful API** is an **implementation** of the REST principles.
    
- It is an API that **follows (strictly or mostly) the REST constraints**.
    
- Example:

```java
GET /users/123
```


### **3. REST API**

- The term **REST API** is broader and looser.
    
- It usually just means **an API that uses HTTP methods and looks REST-like**, but **it may not fully adhere to all REST constraints**.
    
- Many so-called REST APIs are actually **“REST-ish”** or **“HTTP APIs”** because they violate some REST rules (e.g., they keep session state on the server, or use RPC-style endpoints like `/getUserData`).

✅ **Summary**:

- **REST** → the theory (architectural style).
    
- **RESTful API** → a web service that correctly implements REST principles.
    
- **REST API** → a looser term, often any HTTP-based API that claims to use REST, but may not be fully RESTful.


| Aspect                 | REST API                                           | RESTful API                                                                                    |
| ---------------------- | -------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **Definition**         | Any API that uses HTTP methods and looks like REST | An API that _fully_ follows REST architectural principles                                      |
| **Strictness**         | Loose (may or may not follow all REST rules)       | Strict (adheres to REST constraints)                                                           |
| **Resource Handling**  | Might use RPC-style endpoints (`/getUserData`)     | Uses **resource-based URIs** (`/users/123`)                                                    |
| **HTTP Methods**       | Sometimes misused (e.g., `POST /getUser`)          | Correctly maps methods: `GET` = read, `POST` = create, `PUT/PATCH` = update, `DELETE` = remove |
| **Statelessness**      | May keep session state on server                   | **Stateless**: each request contains all necessary info                                        |
| **Caching**            | Not always considered                              | Responses explicitly define cacheability                                                       |
| **Uniform Interface**  | Often inconsistent                                 | Consistent design for all resources                                                            |
| **Common in Practice** | Very common (most APIs are like this)              | Less common (harder to fully implement)                                                        |


## References