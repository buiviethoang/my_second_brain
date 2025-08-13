2025-08-11 21:28
Status: #baby
Tags: [[computer science]] [[database]]
## Main

### Creating indexes
#### Single field index
- **Structure**: Indexes on one field, e.g. `{ name: 1 }`
    
- **When to use**:
    
    - You frequently query on a single field (`find({ name: "John" })`)
        
    - You use `sort()` on a single field
        
    - Field has **high selectivity** (many unique values)
        
- **Avoid**:
    
    - If the field has very few distinct values (e.g., gender `"M"`/`"F"`) → poor filtering power
#### Compound index
- **Structure**: Multiple fields, e.g. `{ age: 1, name: -1 }`
    
- **When to use**:
    
    - You query on multiple fields in the **same query** (`find({ age: 30, name: "John" })`)
        
    - You filter on the **first field** and optionally sort/filter on the rest
        
    - You want to optimize both filtering and sorting
        
- **Rule**:
    
    - **Prefix rule** → Queries must use the index from the leftmost field onward  
        `{ age: 1, name: -1 }` works for:
        
        - `find({ age: 30 })`
            
        - `find({ age: 30, name: "John" })`  
            but **not** `find({ name: "John" })` alone


#### Multikey index
- **Structure**: Automatically used for arrays
    
- **When to use**:
    
    - You store arrays and query inside them (`tags: ["sports", "news"]`)
        
    - Index is built on each array element
#### Text Index
- **When to use**:
    
    - You need full-text search on string fields
        
    - Good for keywords, but **not** for prefix search (`"Jo"` won’t match `"John"`)
        
- **Limitations**:
    
    - Only one text index per collection
        
    - Case-insensitive by default

#### Geospatial Index
- **Types**:
    
    - `2d` for planar coordinates
        
    - `2dsphere` for Earth-like sphere
        
- **When to use**:
    
    - Queries with `$near`, `$geoWithin`, etc.
        
    - Location-based search

## **Choosing Strategy**

- **Read-heavy app** → More indexes to speed queries
    
- **Write-heavy app** → Minimize indexes (every index slows inserts/updates)
    
- Always:
    
    - Use `explain()` to see if index is used
        
    - Index only what you query/sort often
        
    - Avoid redundant indexes (`{ name: 1 }` and `{ name: 1, age: 1 }` where `{ name: 1 }` is already covered by the second)



### Optimization
https://learn.mongodb.com/learn/course/query-optimization/query-optimization/optimize-query-performance?page=1
## References