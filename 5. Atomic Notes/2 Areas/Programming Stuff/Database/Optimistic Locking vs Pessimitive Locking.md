2025-09-16 21:28
Status: 
Topic: 
Tags: [[database]]
## Main
Optimistic locking and pessimistic locking are two concurrency control strategies used in databases to manage simultaneous data access and modifications.

**Optimistic locking** assumes conflicts are rare and allows multiple users to access and modify data concurrently without locking it initially. It only checks for conflicts when changes are committed, and if a conflict is detected, the transaction is rolled back or the user is informed, requiring a manual merge or retry. This approach is efficient and avoids locking overhead, making it suitable when concurrent updates are infrequent.

**Pessimistic locking** assumes conflicts are likely and locks the data as soon as one user begins editing, preventing others from accessing or modifying the data until the lock is released after the update is committed. It serializes updates to ensure data integrity without conflict resolution but can cause delays and reduce concurrency.

| Feature            | Optimistic Locking                               | Pessimistic Locking                              |
| ------------------ | ------------------------------------------------ | ------------------------------------------------ |
| Locking mechanism  | No locking during data access; checks at commit  | Locks data immediately upon access for update    |
| Conflict detection | Detected at commit time, may require retry/merge | Prevents conflicts by blocking concurrent access |
| Performance impact | Higher concurrency, lower overhead               | Lower concurrency, potential delays              |
| Use case           | Low conflict scenarios, web apps                 | High conflict scenarios, financial transactions  |
| Conflict handling  | Manual resolution or rollback                    | Automatic serialization of updates               |

## References