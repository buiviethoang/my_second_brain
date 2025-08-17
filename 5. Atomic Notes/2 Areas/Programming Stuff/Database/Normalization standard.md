2025-08-14 06:52
Status: #baby
Tags: [[database]]
## Main
### What? 
Normalization is the process of **organizing data in a database** so that:

1. **Redundancy** (duplicate data) is minimized.
    
2. **Data integrity** (consistency) is preserved.
    
3. **Maintenance** is easier (less risk of anomalies during insert, update, delete).
    

It’s achieved by breaking tables into smaller, related tables and defining relationships using **primary keys** and **foreign keys**.

### Without normalization, you risk:

- **Update anomalies** – same data stored in multiple places, needs updating in all places.
    
- **Insert anomalies** – can’t add data without other unrelated data.
    
- **Delete anomalies** – deleting a record accidentally removes important information.

### The Standard Normal Forms

There are several **Normal Forms (NF)**, each with stricter rules.  
The main ones you’ll see in practice are **1NF, 2NF, 3NF**, and sometimes **BCNF**.

### **1NF – First Normal Form**

**Rule:**

- No repeating groups or arrays in a column.
    
- Each cell contains **atomic** (indivisible) values.
    
- Each record is unique (use a primary key).

**Example (Bad)**:

|OrderID|ProductIDs|
|---|---|
|1|12, 15, 18|

**Fix (Good)**:

|OrderID|ProductID|
|---|---|
|1|12|
|1|15|
|1|18|

### **2NF – Second Normal Form**

**Rule:**

- Must already be in 1NF.
    
- **No partial dependency** — every non-key column must depend on the **whole** primary key (not just part of it).
    
- Applies when you have **composite primary keys**.
    

**Example (Bad)**:  
If `(OrderID, ProductID)` is the primary key, but `CustomerName` depends only on `OrderID`, it violates 2NF.

**Fix (Good)**:  
Split into:

- Orders table: `(OrderID, CustomerName)`
    
- OrderDetails table: `(OrderID, ProductID, Quantity)`

### 3NF – Third Normal Form
**Rule:**

- Must already be in 2NF.
    
- **No transitive dependency** — non-key columns must depend **only** on the primary key, not on other non-key columns.
    

**Example (Bad)**:  
If `CustomerID → CustomerZip` and `CustomerZip → CityName`, then `CityName` depends on `CustomerID` indirectly.

**Fix (Good)**:

- Customers table: `(CustomerID, CustomerZip)`
    
- ZipCodes table: `(CustomerZip, CityName)`


### ### **BCNF – Boyce-Codd Normal Form**

**Rule:**

- A stricter version of 3NF.
    
- Every determinant (column or group of columns that determines another column) must be a **candidate key**.
    
- Helps when you have multiple overlapping candidate keys.

|Normal Form|Main Rule|Fixes Problem|
|---|---|---|
|**1NF**|No repeating groups, atomic values|Storing multiple values in a cell|
|**2NF**|No partial dependencies|Columns depending on only part of a composite key|
|**3NF**|No transitive dependencies|Columns depending on other non-key columns|
|**BCNF**|Every determinant is a candidate key|Special multi-key anomalies|

### Denormalization
Denormalization is the process of **intentionally introducing redundancy** into a database design that was previously normalized, in order to **improve read performance**.

Think of it as:

> “We break the strict normal form rules _on purpose_ to make certain queries faster.”

#### Why? 
## **Why Denormalize?**

- **Fewer joins** → Complex queries become simpler and faster.
    
- **Better reporting performance** → Especially in analytics-heavy systems.
    
- **Caching within the DB** → Avoid repeated lookups for commonly needed fields.
    

However, it **comes at a cost**:

- **Data redundancy** → Same data stored in multiple places.
    
- **Higher risk of inconsistency** → Updates must be synchronized across duplicates.
    
- **More storage usage**.

#### When

- In **data warehouses** or OLAP systems (reporting, analytics).
    
- When **read performance matters more than write performance**.
    
- In **high-latency distributed systems** where multiple joins are too slow.

####  **Example**

### Normalized (3NF)

**Customers**

|CustomerID|Name|CityID|
|---|---|---|
|1|Alice|101|
|2|Bob|102|

**Cities**

|CityID|CityName|
|---|---|
|101|Hanoi|
|102|Saigon|

**Query**: To get customer name and city → requires a **join**
### Denormalized

**Customers**

| CustomerID | Name  | CityName |
| ---------- | ----- | -------- |
| 1          | Alice | Hanoi    |
| 2          | Bob   | Saigon   |

**Query**: No join needed — city name is already stored in `Customers`.

**Rule of thumb**:

- **Transactional systems** (OLTP [[OLTP & OLAP]]) → Normalize (up to 3NF/BCNF).
    
- **Analytical systems** (OLAP [[OLTP & OLAP]]) → Often denormalize for query speed.
## References
https://www.freecodecamp.org/news/database-normalization-1nf-2nf-3nf-table-examples/