There are three possible plans to process a subquery:
- flattened. Transform the query to a join, then process as a join.
- out-to-in. For each row in the outer query, look up in the inner query.
- in-to-out. For each row in the inner query, look up in the outer query.
## Join vs subquery
The difference between nested-loops for joins and nested-loops for subqueries is that a subquery needs to find only a single match, so it might be able to break out early from the inner loop. In contrast, a join needs all matches, so it must chug through all rows. (Because the subquery loop can abort early the result is sometimes called a "semijoin," but that's a rare word.) And that's one point in favor of writing subqueries, because a subquery loop will have fewer iterations.

```sql
Query #1        /* avoid this */
SELECT column1 FROM Table1
  WHERE column1 =
     (SELECT column1 FROM Table2)

Query #2        /* use this */
SELECT column1 FROM Table1
  WHERE column1 = ANY
     (SELECT column1 FROM Table2)

Query #3        /* or use this */
SELECT column1 FROM Table1
  WHERE column1 IN
     (SELECT column1 FROM Table2)
```

```sql
Join:
SELECT MIN(Table1.column1)

   FROM Table1, Table2
   WHERE Table1.column1 = Table2.column1

Subquery:
SELECT MIN(Table1.column1)

   FROM Table1
   WHERE Table1.column1 IN

      (SELECT Table2.column1
         FROM Table2)
```

### Flattening
To flatten a query means to make everything one level. Based on our observations so far, there are clearly times when you should flatten a subquery. In this section, we'll discuss how the DBMS can flatten automatically, but first let's establish how you can do it yourself.
```sql
0. Subquery with IN:
    SELECT * FROM Table1
    
      WHERE Table1.column1 IN
         (SELECT Table2.column1
    
    FROM Table2
    
            WHERE Table2.column1 = 5)
    Flattened:
    
    SELECT Table1.*
      FROM Table1, Table2
      WHERE Table1.column1 = Table2.column1
    
        AND Table2.column1 = 5
```

This simple flattening seems like it should be equivalent to the IN query, but it has a flaw that can be seen if Table1 has these three rows: {1, 5, 5} and Table2 has these three rows: {2, 5, 5}. Notice that the subquery-based SELECT would correctly return two rows: {5, 5}, but the flattened
 
SELECT would return four rows: {5, 5, 5, 5}. Notice further that if the flattened SELECT is "corrected" by using SELECT DISTINCT instead of just SELECT, the join would return only one row: {5}. In other words, flattening can cause too many duplicate rows—and if you try to get rid of the duplicates, you can end up with too few duplicate rows. Sometimes you'll see this flaw if the DBMS flattens automatically. (By the way, DISTINCT can be expensive so don't use it if Table2.column1 is uniquely indexed.)

## Syntax choices
### In
In a slight plurality of cases, the plan for IN subqueries is in-to-out—that is, the DBMS starts on the inside and drives to the outer query.
### DISTINCT
The IBM plan for IN includes steps for sorting and eliminating duplicates. That makes sense because the best optimizations are ones that reduce the row count in the driver. In addition, a slight speedup occurs if the rows in the outer query are in order by Table1.column1, because the lookups will occur in ascending order by value
It is legal to add the word DISTINCT in the inner query, like this:
```sql
SELECT * from Table1
  WHERE Table1.column1 IN

     (SELECT DISTINCT Table2.column1 FROM Table2
        WHERE Table2.column1 = 5)

GAIN: 2/7
```

Logically, DISTINCT is 

here, but we're looking for some common side effects of DISTINCT: (a) it causes ORDER BY, and (b) it reduces the number of rows in the inner query. In our tests, Table2.column1 contained integers, most of them duplicates, and it had a high likelihood that smaller numbers would match values in Table1. The explanation for the gain is that, by eliminating duplicates and by making it more probable that "matches" (i.e., small numbers) would appear early, DISTINCT sped things up with some DBMSs. Other DBMSs just ignored DISTINCT, so no harm was done.

Another side effect of DISTINCT, but more frequently seen with GROUP BY or HAVING, is materialization—that is, to evaluate some expressions, the DBMS will create a temporary table, put the rows from the original table(s) into the temporary table, and select from the temporary copy. Scanning is faster if the inner loop happens on a materialized "view" of the table, which is smaller than the table itself. Materialization is also a factor that discourages the DBMS from flattening. As we've suggested before: If DISTINCT is a do-nothing operator because there's no duplication, then the relation is not one-to-many, and therefore a join is probably better than a subquery.

Though DISTINCT takes time, the rows are short if you're just retrieving one column in the subquery. But DISTINCT does involve a sort, so do consider the sort tips provided in Chapter 3, "ORDER BY."

### Exists
The sort of subquery that [NOT] EXISTS introduces has a notable characteristic: It contains correlations.
```sql
Query #1:
SELECT * FROM Table1

  WHERE EXISTS
     (SELECT * FROM Table2

        WHERE Table1.column1 = Table2.column1)
    Query #2:
SELECT * FROM Table1

  WHERE 0 <
     (SELECT COUNT(*) FROM Table2

        WHERE Table1.column1 = Table2.column1)
GAIN: -4/7
```

The reason the COUNT(*) alternative (Query #2) is slower than Query #1 is that a subquery's nested- loop breaks out as soon as there's a match. That's like stopping the count when you reach the number one. Not that anybody would really consider the COUNT(*) alternative, but it illustrates nicely the maxim—Don't ask for more precision than is needed to answer the question. The condition > 0 (or 0 <) is often a hint of an underlying "Yes/No" question.

We want to dispose of a popular superstition that says—Instead of using SELECT * in an EXISTS subquery, you should use a short and specific select list. To test this "tip," we tried these three variants on some large tables:

SELECT * FROM Table1
  WHERE EXISTS

     (SELECT * FROM Table2)

SELECT * FROM Table1
  WHERE EXISTS

     (SELECT column1 FROM Table2)

SELECT * FROM Table1
  WHERE EXISTS

     (SELECT 5 FROM Table2)

All three queries took the same amount of time.

### IN or EXISTS?
SELECT * FROM Table1
  WHERE Table1.column1 IN

     (SELECT Table2.column1 FROM Table2)

SELECT * FROM Table1
  WHERE EXISTS

     (SELECT * FROM Table2
        WHERE Table1.column1 = Table2.column1)


• If Table1 has many rows and Table2 has few rows, use IN (GAIN: 2/7).
• If the outer query has an additional restrictive expression (e.g., WHERE
Table1.column2 = 5), use EXISTS (GAIN: 2/7).
• If the outer query is WHERE NOT ..., use NOT EXISTS (GAIN: 3/7).

### Double INs
```sql

SELECT * FROM Table1
  WHERE EXISTS
     (SELECT * FROM Table2
        WHERE Table1.column1 = Table2.column1
      UNION
      SELECT * FROM Table3
        WHERE Table1.column2 = Table3.column1)

```

There are two problems with this example. First, many DBMSs don't support UNION in a subquery. Second, it's slow! It's better to transform queries like this one to a SELECT with an outer query that contains two IN subqueries. Here's how:

```sql
SELECT * FROM Table1
  WHERE Table1.column1 IN
    (SELECT Table2.column1 FROM Table2)
    OR Table1.column2 IN
       (SELECT Table3.column1 FROM Table3)
```

Here's another example. Query #1 could be transformed to Query #2:

Query #1
SELECT * FROM Table1

  WHERE Table1.column1 IN
    (SELECT Table2.column1 FROM Table2)
    AND Table1.column2 IN

        (SELECT Table2.column2 FROM Table2)

Query #2
SELECT * FROM Table1

  WHERE (Table1.column1, Table1.column2) IN
     (SELECT Table2.column1, Table2.column2 FROM Table2)

But this transform works only if the DBMS supports row subqueries—a rare feature. If your DBMS doesn't support row subqueries, you can still get the effect of the transform by using arithmetic or concatenation, like this:

SELECT * FROM Table1
  WHERE Table1.column1 || ',' || Table1.column2 IN

     (SELECT Table2.column1 || ',' || Table2.column2
        FROM Table2)

GAIN: 4/6

Query #1:
SELECT * FROM Table1

  WHERE Table1.column1 IN
     (SELECT Table2.column1 FROM Table2

        WHERE Table2.column1 IN

           (SELECT Table3.column1 FROM Table3))
=> 
Query #2:
SELECT * FROM Table1

  WHERE Table1.column1 IN
    (SELECT Table2.column1 FROM Table2)
    AND Table1.column1 IN

        (SELECT Table3.column1 FROM Table3)
GAIN: 7/7

It's better to merge two subqueries into one.