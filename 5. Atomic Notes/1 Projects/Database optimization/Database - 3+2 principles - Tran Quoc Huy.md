2024-12-14 11:25
Status: #baby
Tags: [[computer science]] [[database]]
## Main

### 1 - Page / Block
- Smallest unit of any DB
- Less page => Less time, less searching, more enjoyable :)
### 2 - Cache & Read-Write mechanism
#### Read
Step 1: the query search for which page? 
Step 2: copy page to mem 
Step 3: return value from page for user
#### Write 
S1: Copy page to mem
S2: Modify content in mem
S3: Write from mem to the targeted page

### 3 - Cost 

![[Pasted image 20241214113919.png]]

**Oracle RAC - active - active**
**Database fragmentation**
**Physical read vs logical read**

### Index order does matter
## References
https://www.youtube.com/watch?v=xC1662uBym8&list=PLEzgItGwNvPvz80JbfXcuaWyHQMAU2t9n&index=2