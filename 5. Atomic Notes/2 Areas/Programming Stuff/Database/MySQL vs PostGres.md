2025-08-14 06:43
Status: #baby
Tags: [[database]]
## Main

### Overview

| Feature             | MySQL                                                      | PostgreSQL                                                               |
| ------------------- | ---------------------------------------------------------- | ------------------------------------------------------------------------ |
| **Initial Release** | 1995                                                       | 1996                                                                     |
| **License**         | GPL (with commercial licenses from Oracle)                 | PostgreSQL License (similar to MIT/BSD)                                  |
| **Focus**           | Simplicity, speed for read-heavy workloads                 | Standards compliance, advanced features, extensibility                   |
| **Popularity**      | Very popular in web apps, especially with PHP (LAMP stack) | Popular in enterprise, analytics, GIS, and advanced application backends |

### Performance
| Scenario                          | MySQL                                                                           | PostgreSQL                                                      |
| --------------------------------- | ------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| **Read-heavy workloads**          | Often faster due to simpler execution engine (esp. with MyISAM or tuned InnoDB) | Slightly slower out-of-the-box but can be optimized             |
| **Write-heavy / complex queries** | Can slow down with lots of joins, CTEs, and transactions                        | Handles complex queries, joins, and indexing better             |
| **Concurrency**                   | Good, but historically had issues with concurrent writes                        | Strong concurrency via MVCC (Multi-Version Concurrency Control) |
### Features
| Feature                     | MySQL                                                             | PostgreSQL                                                                       |
| --------------------------- | ----------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| **SQL Standard Compliance** | More lenient, can allow non-standard syntax                       | Very strict to SQL standards                                                     |
| **Joins & Subqueries**      | Good, but sometimes optimizer struggles with very complex queries | Excellent, supports advanced joins, recursive CTEs, window functions             |
| **Stored Procedures**       | Supported, but procedural language is limited                     | Supports multiple languages for stored procedures (PL/pgSQL, Python, Perl, etc.) |
| **CTEs & Window Functions** | Limited (CTEs added in v8.0, window functions in v8.0)            | Full support for decades                                                         |
| **Full-Text Search**        | Built-in (InnoDB full-text since 5.6)                             | Advanced, with ranking, stemming, and language support                           |
| **GIS (Geospatial)**        | MySQL Spatial (less feature-rich)                                 | PostGIS — industry-leading GIS extension                                         |

### Extension & Ecosystem

- **MySQL**: Limited extensions, but huge community and easy integration with many web apps.
    
- **PostgreSQL**: Extremely extensible — you can create custom data types, operators, and index methods.

### ## **Data Types**

PostgreSQL supports a **wider range of data types**:

- JSON/JSONB (binary JSON with indexing)
    
- Arrays
    
- HSTORE (key-value store)
    
- Geometric types
    
- Range types  
    MySQL supports JSON (since 5.7) but with fewer indexing and query capabilities.

### Replication & Scaling
| Feature         | MySQL                                                   | PostgreSQL                                                       |
| --------------- | ------------------------------------------------------- | ---------------------------------------------------------------- |
| **Replication** | Master-slave (async/semisync), Group Replication for HA | Streaming replication, logical replication, BDR for multi-master |
| **Sharding**    | No built-in sharding (need external tools)              | No built-in sharding, but FDW & Citus extension help             |
| **Clustering**  | MySQL NDB Cluster, Galera Cluster                       | Patroni, Citus, and other clustering solutions                   |
|                 |                                                         |                                                                  |
### When to use
**Choose MySQL if**:

- You want a lightweight, simple, fast solution for mostly read-heavy workloads.
    
- Your application is already in the LAMP stack (e.g., WordPress, Magento).
    
- You don’t need advanced query features or complex data types.
    

**Choose PostgreSQL if**:

- You need complex queries, advanced data types, or heavy analytical workloads.
    
- You want strict data integrity and standards compliance.
    
- You work with GIS, JSONB, or need extensibility.
    
- You expect to handle complex transactions and high concurrency.

### Benchmark



## References