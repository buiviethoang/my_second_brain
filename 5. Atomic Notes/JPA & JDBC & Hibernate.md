2025-08-17 08:37
Status: #baby
Tags: [[java]]
## Main
|Feature|**JDBC**|**JDBC Template**|**Hibernate**|**JPA**|
|---|---|---|---|---|
|**Type**|Low-level API|Spring abstraction over JDBC|ORM Framework|ORM Specification|
|**Level**|Very low (manual SQL + connections)|Mid (SQL-based, less boilerplate)|High (object-oriented, ORM)|Standard API (interface for ORM)|
|**Who writes SQL?**|Developer (must write full SQL)|Developer (still writes SQL)|Hibernate (generates SQL)|ORM provider (e.g., Hibernate)|
|**Boilerplate code**|A lot (connections, statements, results)|Minimal (Spring handles resources)|Very little (just entities + mappings)|Minimal (annotations + EntityManager)|
|**Abstraction**|None (direct DB calls)|Light abstraction (Spring handles JDBC)|Full ORM (entity mapping, caching, lazy loading)|Standardized ORM abstraction|
|**Portability**|Tied to database SQL|Tied to SQL|Vendor-specific ORM (Hibernate, EclipseLink, etc.)|Portable across ORM providers|
|**Use case**|Small apps, full SQL control|Medium apps, need SQL + simplicity|Large apps, want object-based DB access|Enterprise apps needing a standard ORM API|

✅ **Quick analogy**:

- **JDBC** → Writing letters manually.
    
- **JDBC Template** → Using a secretary to write/send letters (but you still dictate).
    
- **Hibernate** → Email client that auto-formats and sends messages (you just write content).
    
- **JPA** → The official "rules" for how email clients should work.

### JDBC
- **What it is**: A **low-level Java API** for connecting to relational databases.
    
- **How it works**: You write SQL manually, create connections, prepare statements, execute queries, and handle results.
    
- **Pros**:
    
    - Full control over SQL queries.
        
    - Works with any relational database.
        
- **Cons**:
    
    - Verbose (lots of boilerplate code).
        
    - Error-prone (manual resource closing, exception handling, etc.).

```java
Connection conn = DriverManager.getConnection(url, user, pass);
PreparedStatement stmt = conn.prepareStatement("SELECT * FROM users WHERE id=?");
stmt.setInt(1, 1);
ResultSet rs = stmt.executeQuery();
```

### JDBC Template

- **What it is**: A **Spring abstraction on top of JDBC**.
    
- **How it works**: Simplifies JDBC by handling resource management (connection closing, exception translation).
    
- **Pros**:
    
    - Less boilerplate code than raw JDBC.
        
    - Exception handling is unified with Spring’s `DataAccessException`.
        
- **Cons**:
    
    - Still SQL-centric (you must write queries).
        
- **Use case**: When you want **control over SQL** but without JDBC boilerplate.

```java
String sql = "SELECT * FROM users WHERE id = ?";
User user = jdbcTemplate.queryForObject(sql, new Object[]{1}, new BeanPropertyRowMapper<>(User.class));
```

### Hibernate

- **What it is**: A **full-fledged ORM (Object Relational Mapping)** framework.
    
- **How it works**: Maps Java objects (entities) to database tables. You interact with objects; Hibernate generates SQL under the hood.
    
- **Pros**:
    
    - Reduces SQL writing (object-oriented queries with HQL/Criteria).
        
    - Caching, lazy loading, transaction management.
        
- **Cons**:
    
    - Learning curve.
        
    - Less control over raw SQL.
        
- **Use case**: Large-scale apps where you want **object-oriented DB access**.

```java
User user = session.get(User.class, 1); // No SQL written
```
### JPA
- **What it is**: A **standard specification** for ORM in Java (part of Java EE).
    
- **How it works**: Defines annotations and interfaces for ORM (like `@Entity`, `EntityManager`).  
    Hibernate is one of its most popular **implementations**.
    
- **Pros**:
    
    - Standardized API (can switch providers like Hibernate, EclipseLink).
        
    - Cleaner code with annotations (`@Entity`, `@OneToMany`, etc.).
        
- **Cons**:
    
    - Abstract layer → sometimes you need native SQL for performance tuning.
        
- **Use case**: Enterprise applications needing a **portable ORM standard**.

```java
@Entity
public class User {
   @Id
   private Long id;
   private String name;
}
User user = entityManager.find(User.class, 1L);

```

## 🧩 **How they relate**

- **JDBC** → Low-level DB access.
    
- **JDBC Template** → Simplifies JDBC (still SQL-based).
    
- **Hibernate** → ORM framework (object-based, hides SQL).
    
- **JPA** → Standard API for ORM, Hibernate is a provider of JPA.

JDBC  → Base API
JDBC Template → Spring helper on JDBC
Hibernate → ORM framework (implements JPA)
JPA → ORM specification (Hibernate, EclipseLink, etc. implement it)

### ORM

**ORM (Object Relational Mapping)** is a programming technique that maps **Java objects (classes)** to **relational database tables**.

- **Objects → Tables**
    
- **Fields → Columns**
    
- **Relationships → Foreign keys/joins**
    

So instead of writing raw SQL, you work with **Java objects**, and the ORM framework translates those operations into SQL queries.

Without ORM (JDBC)
```java
// Fetch user with id = 1
PreparedStatement stmt = conn.prepareStatement("SELECT * FROM users WHERE id=?");
stmt.setInt(1, 1);
ResultSet rs = stmt.executeQuery();
User user = new User();
if(rs.next()) {
    user.setId(rs.getInt("id"));
    user.setName(rs.getString("name"));
}

```

=> You do everything: SQL, mapping, closing connections.

With ORM (Hibernate/JPA)

```java
// Fetch user with id = 1
User user = entityManager.find(User.class, 1L);

```

=> ORM handles SQL, mapping, and object lifecycle.

#### Key Features of ORM

1. **Entity Mapping**  
    Use annotations like:
    
```java
@Entity
@Table(name = "users")
public class User {
    @Id
    private Long id;
    private String name;
}

```
    
    This tells ORM: `User` → `users` table.
    
2. **Relationships**
    
    `@OneToMany(mappedBy = "user") private List<Order> orders;`
    
    ORM automatically joins tables (`users` ↔ `orders`).
    
3. **Queries**
    
    - **HQL/JPQL** (object-oriented queries, e.g., `FROM User WHERE name = :name`)
        
    - **Criteria API** (type-safe query building)
        
    - **Native SQL** (if you need full SQL control)
        
4. **Advanced Features**
    
    - Lazy/eager loading of relationships.
        
    - Caching for performance.
        
    - Transaction management.
        
    - Database-agnostic (switch DBs with minimal code changes).\

## Benefits of ORM

✅ Less boilerplate code (no manual SQL + mapping).  
✅ Object-oriented (work with Java objects).  
✅ Database independence (JPA/Hibernate can work with MySQL, Postgres, Oracle, etc.).  
✅ Built-in support for caching, transactions, batch operations.

## Downsides of ORM

❌ Learning curve (annotations, entity lifecycle, caching).  
❌ Performance overhead if misused (e.g., N+1 query problem).  
❌ Less control compared to raw SQL (sometimes you must drop down to native queries).

## 🔹 Popular ORM Frameworks

- **Hibernate** (most popular in Java, implements JPA).
    
- **EclipseLink** (reference implementation of JPA).
    
- **TopLink** (Oracle).
    
- **MyBatis** (not full ORM, more like SQL mapper).

👉 In short:

- **ORM = technique**.
    
- **JPA = standard for ORM in Java**.
    
- **Hibernate = ORM framework that implements JPA**.
## References