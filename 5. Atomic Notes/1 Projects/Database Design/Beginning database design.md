## Database Modeling Past and Present
### The Evolution of Database Modeling
#### File Systems
Using a file system database model implies that no modeling techniques are applied and that the
database is stored in flat files in a file system, utilizing the structure of the operating system alone
For a file system database, data can be stored in individual files or multiple files
#### Hierarchical Database Model
The hierarchical database model is an inverted tree-like structure. 
![[Pasted image 20230907214943.png]]
#### Network Database Model
The network database model is essentially a refinement of the hierarchical database model. The network
model allows child tables to have more than one parent, thus creating a networked-like table structure
Multiple parent tables for each child allows for many-to-many relationships, in addition to one-to-many
relationships
![[Pasted image 20230907215015.png]]

#### Relational Database Model
The relational database model improves on the restriction of a hierarchical structure, not completely
abandoning the hierarchy of data
![[Pasted image 20230907215225.png]]

![[Pasted image 20230907215406.png]]
Another benefit of the relational database model is that any tables can be linked together, regardless of
their hierarchical position. Obviously, there should be a sensible link between the two tables, but you are
not restricted by a strict hierarchical structure; therefore, a table can be linked to both any number of
parent tables and any number of child tables.

#### Object Database Model

An object database model provides a three-dimensional structure to data where any item in a database
can be retrieved from any point very rapidly. Whereas the relational database model lends itself to
retrieval of groups of records in two dimensions, the object database model is efficient for finding unique
items. Consequently, the object database model performs poorly when retrieving more than a single item,
at which the relational database model is proficient.

The object database model does resolve some of the more obscure complexities of the relational database
model, such as removal of the need for types and many-to-many relationship replacement tables
One
of the biggest sticking points between object programmed applications and relational databases is the
performance of the mapping process between the two structural types: object and relational. Object and
relational structure is completely different. It is, therefore, essential to have some understanding of object
database modeling techniques to allow development of efficient use of relational databases by object-
built applications

#### Object-Relational Database Model
The object database model is somewhat spherical in nature, allowing access to unique elements anywhere
within a database structure, with extremely high performance. The object database model performs
extremely poorly when retrieving more than a single data item. The relational database model, on the
other hand, contains records of data in tables across two dimensions. The relational database model is best
suited for retrieval of groups of data, but can also be used to access unique data items fairly efficiently.
The object-relational database model was created in answer to conflicting capabilities of relational and
object database models

### Examining the Types of Databases
#### Transactional Databases
A transactional database is a database based on small changes to the database (that is, small transactions).
The database is transaction-driven. In other words, the primary function of the database is to add new
data, change existing data, delete existing data, all done in usually very small chunks, such as individual
records.
- Client-Server database
- OLTP database
#### Decision Support Databases
Decision support systems are commonly known as DSS databases, and they do just that — they support
decisions, generally more management-level and even executive-level decision-type of objectives.
Following are some DSS examples:
- Data warehouse database: A data warehouse database can use the same data modeling approach as a
transactional database model. However, data warehouses often contain many years of historical
data to provide effective forecasting capabilities. The result is that data warehouses can become
excessively large, perhaps even millions of times larger than their counterpart OLTP source. The OLTP database is the source database because the OLTP database is the database
where all the transactional information in the data warehouse originates
- Data mart — A data mart is essentially a small subset of a larger data warehouse. Data marts are
typically extracted as small sections of data warehouses, or created as small section data chunks
during the process of creating a much larger data warehouse database. There is no reason why
a data mart should use a different database modeling technique than that of its parent data
warehouse.
- Reporting database — A reporting database is often a data warehouse type database, but containing
only active (and not historical or archived) data. A simple reporting database is of small size
compared to a data warehouse database, and likely to be much more manageable and flexible

#### Hybrid Databases
A hybrid database is simply a mixture containing both OLTP type concurrency requirements and data
warehouse type throughput requirements. In less-demanding environments (or in companies running
smaller operations), a smaller hybrid database is often a more cost-effective option, simply because there
is one rather than two databases — fewer machines, fewer software licenses, fewer people, the list goes on

