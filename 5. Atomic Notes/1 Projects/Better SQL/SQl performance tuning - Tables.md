
**You can influence
physical storage when you CREATE TABLE and ALTER TABLE, and you can be influenced by
physical storage when you SELECT, INSERT, UPDATE, and DELETE**

### The Storage Hierarchy
#### Pages
Depending on the DBMS, a page is also called a data block, a block, a blocking unit, a control
interval, and a row group.
- All pages in a file have the same size. Indeed for some DBMSs, it is true that all pages in all
files have the same size, but the usual case is that you have a choice when making a new
object.
- The choice of page sizes is restricted to certain multiples of 1024 (1KB), in a range between
1024 and 65536—that is, between 1KB and 64KB.
- The optimum page size is related to the disk system's attributes. Smaller page sizes like 2KB
were once the norm, but disks' capacity tends to increase over time, so now 8KB is
reasonable, while 16KB is what we'll upgrade to soon.
- Pages contain an integral number of rows. Even for the rare DBMSs that allow large rows to
overflow into later pages, the very strong recommendation is that you should avoid overflow

*Now that we know what a page is, let's look at what a page is for:*
•
A page is a minimal unit for disk I/O.
That doesn't mean that DBMSs read and write one page at a time—in fact most DBMSs will
read several pages at once—but a page is the smallest amount that a DBMS could read, and
the smallest amount that a DBMS usually writes. There is no such thing as a disk read of a
mere row! The objective is to make a page I/O synonymous with an I/O of the minimal unit
that the disk drive uses. For example, on MS Windows NT with more than 64MB RAM, a
common sector size is 512 bytes, there is one sector per cluster, and 8KB is an optimum read
size (assuming the NT File System, NTFS). On a hand-held machine, a 1KB page is better
for footprint reasons.
•
A page is a unit for locking.
It's no longer the minimal unit for locking, because most DBMSs allow locking at the row
level too. But page locking is traditional and convenient. We'll talk more about page locks in
Chapter 15, "Locks."
•
A page is a unit for caching.
A read is a transfer from disk to memory. Once the DBMS has a page in memory, it will
want to keep it there for a while. It keeps the page in a buffer, or buffer pool—an in-memory
copy of a bunch of pages, with a fixed size. The DBMS maintains the buffer pool itself (it
does not rely on the operating system, though any caching by the operating system is a nice
bonus); it generally reads several pages at once into the buffer and throws out individual
pages according to a Least-Recently-Used (LRU) algorithm. (If the cache holds 100 pages,
and you have a 101-page table, then repeated full-table scans will defeat the LRU algorithm.
There are nonstandard ways to tweak the cache size or to lock tables in cache.)
•
A page is a unit for administration.
By that we mean that DBMSs store a significant amount of housekeeping information in a
page, outside the row data. This housekeeping information will include a header (which may
contain row offsets, overflow pointers, identifications, last modified date, NULL bits, some
indication of size, etc.), some free space, and sometimes a trailer.

#### Extents
An extent is a group of contiguous pages. Extents exist to solve the allocation problem. The allocation
problem is that, when a file gets full, the DBMS must increase its size. If the file size increases by
only one page at a time, waste occurs
Depending on the DBMS, you can usually define the initial and next extent sizes, but most people
make no specification and just use default values. Typical default values are: 16x4KB pages (IBM),
8x8KB pages (Microsoft)—or 1MB for certain tablespaces (Oracle)
##### Read groups
A read group is a group of contiguous pages. For many DBMSs, a read group is the same thing as an
extent, but there's a logical difference. A read group is the number of pages that are read together,
while an extent is the number of pages that are allocated together

#### Files
A file is a group of contiguous extents
Surprisingly, a file is not a physical representation of a table

#### Partitions
A partition is a group of contiguous extents. Often a partition is a file, but it doesn't have to be
Partitions are bad if there are few extents and few database users. Why? Because the fundamental
principle is that rows should be crammed together. That helps caching and reduces the number of page
writes.
Partitions are good if—and only if—there are many extents and many database users. Why? Two
reasons, actually. The first is that in a multiuser environment, partitioning reduces contention. The
second is that in a multidisk-drive environment, partitioning increases parallelism
#### Tablespaces
A tablespace (also called a dbspace by some DBMSs, e.g., Informix) is a file, or a group of files, that
contains data. For example, this non-standard Oracle SQL-extension statement creates and associates
a tablespace with a 10MB file
A tablespace can contain a single table, or it can be shared either between one table and its indexes or
between multiple tables. In other words, it's possible to mix extents from different objects in the same
tablespace

### Heaps
## Indexes
***Indexes make SELECTs faster, but they make UPDATEs slower.*
Thus, if your code contains many
SELECT statements with the same column in the WHERE clause, you should ensure that column is
indexed. And if your code contains massive data-change statements involving the same column, it's a
good idea to make sure it's (at least temporarily) not indexed

### B-trees
#### Insert into a B-Tree
- The DBMS scans the index pages until it finds a key value that is greater than the new key
value.
- Then it shifts forward all following data in the page to make room for the new key value.
- Then it copies the new value into the page. (The shifting should mean that it's slightly slower
to insert a key at the start of a page than at the end—which means that it's bad to INSERT in a
descending sequence. However, the difference is barely measurable.)

#### Deleting from a B-tree
- Scan the index until the key whose value equals the deleted value is found. This involves
comparing both key value and data pointer because sometimes the same value can occur in
different rows.
- Shift all following keys in the page upward over the key being deleted.
- If the key was the first in the leaf page, update the key value in the intermediate page. Some
cascading may occur, and there is an opportunity for a reverse split—that is, two logically
adjacent pages could now be merged if both are less than 50% full. Actually, though, no such
thing happens.

#### Fragmentation
So far, we've done two INSERTs and one DELETE on the example database, and the result is a
horrible mess! Look at everything that's wrong with Figure 9-6:
•The leaf pages are out of order. At this stage, if the DBMS wants to go through the pages in
logical order by key value—a common requirement for a range search, an ORDER BY, or a
GROUP BY—it must jump from leaf page #2 to page #4 and then back to page #3. The
situation won't affect searches for a single row with an equals operator, but that hides the
effect only for a while. As we learned in Chapter 8, this problem is called fragmentation.
- The leaf pages vary in fullness. Leaf pages #1 and #4 are only 50% full. Leaf page #3 is
100% full, and the next insertion will almost certainly cause a split. This problem is called
skew.
- And finally, the root looks ready for a split on the very next insertion, regardless of what gets
changed. Remember, splits in upper layers happen "in anticipation" so a split may occur even
when the leaf page won't overflow. And a split on the root is an especially bad thing, because
after a root split happens, there is one more layer—and when there is one more layer, there is
one more I/O for every index lookup. And when that happens, everything takes 50% longer.
That's unfair in this case, because the leaf pages aren't really full, or even 70% full on
average.

#### Rebuilding a B-tree
**ALTER INDEX/REBUILD**
**DROP INDEX/RECREATE**
