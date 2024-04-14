### NOT NULL 

NOT NULL affects storage because it is impossible to store a NULL value in the column itself. For instance, if a column is defined as SMALLINT, then it may contain any negative or positive number that fits in 16 bits—but there is no room for a reserved 16-bit value that could mean NULL. Therefore the DBMS must have a flag outside the column itself that says either "this is NULL" or "this is not NULL." In Microsoft, this flag is part of a bit list at the start of the row. In IBM and most other DBMSs, the flag is a byte at the start of the column. Either way, a column that can contain NULL takes more space to store than does a NOT NULL column

0. A column that can contain NULL also takes slightly longer to retrieve, because you must always add a check for a NULL indicator to your program before processing the value itself
1. The severest effect is seen with Sybase, because Sybase silently changes fixed-size columns (such as CHAR) into variable-
length columns (such as VARCHAR) if they can contain NULL. The result is that with unindexed columns, most DBMSs handle columns that can contain NULL slower than NOT NULL columns. On the other hand, with indexed columns, Oracle handles nullable columns faster
#### Bottom line
To speed things up, define columns and domains with NOT NULL as often as possible.

Even if your definitions always include NOT NULL, make sure your program allows for the possibility of retrieved NULLs. Add NULL indicator checks for every OUTER JOIN retrieval and wherever it's possible that a query might be searching an empty table.

### CHECK
A CHECK constraint is used to enforce a rule that a column may contain only data that falls within some specific criteria
### FOREIGN KEY
A foreign key is a column, or group of columns, that may contain only those values found in a similar set of unique (usually primary key) columns belonging to (usually) another table. The rule enforces data integrity: The rationale is that you can't have an order if there is no customer, you can't have an employee working in department "A" if there is no such department, you can't have a factory that makes widgets if you don't have widgets as a product, and so on.

Define all foreign-key columns to match their primary-key column exactly in data type, column size, and column name.

Save time by eliminating redundant CHECK constraints on foreign-key columns where the same constraint already exists on the matching primary-key column.

Avoid the use of NATURAL JOIN when two tables have columns with the same name that are not linked with a primary-key/foreign-key relationship.

Don't use the same column for multiple FOREIGN KEY constraints or your DBMS will have a hard time prejoining with a join index.