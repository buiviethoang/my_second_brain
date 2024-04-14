## General Tuning
### Code for points
![[Screenshot 2023-09-14 at 10.15.27.png]]›››![[Screenshot 2023-09-14 at 10.15.48.png]]
```sql
... WHERE smallint_column = 12345
```
This example gets a total of 27 points, calculated as follows:

- Five points for the column (smallint_column) alone on the left
- Two points for the exact numeric (smallint_column) operand data type
- Ten points for the equals operator
- Ten points for the literal (12345) alone on the right
```sql
... WHERE char_column >= varchar_column || 'x'
```

- Five points for the column (char_column) alone on the left
- Zero points for the CHAR (char_column) operand data type
- Five points for the greater than or equal to operator
- Three points for the multioperand expression (varchar_column || 'x') on the right
- Zero points for the VARCHAR (varchar_column) operand data type

### Constant Propagation
***Law of Transitivity***

```
IF
(A <comparison operator> B) IS TRUE AND (B <comparison
operator> C) IS TRUE
THEN
(A <comparison operator> C) IS TRUE AND NOT (A <comparison
operator> C) IS FALSE
```

```sql
WHERE column1 < column2
      AND column2 = column3
      AND column1 = 5
```
=> 
```sql
WHERE 5 < column2
      AND column2 = column3
      AND column1 = 5
```

Most good DBMSs do this sort of thing automatically. But some DBMSs won't try transforms when the expression contains multiple parentheses and NOTs. For example, this SELECT statement can be slow:
```sql
SELECT * FROM Table1
  WHERE column1 = 5 AND
    NOT (column3 = 7 OR column1 = column2)
```
=> 
```sql
SELECT * FROM Table1
  WHERE column1 = 5
    AND column3 <> 7
    AND column2 <> 5
```

Sometimes constant propagation won't work with floats, because it's possible to be both "greater than" and "equal to" at the same time when approximate numeric comparisons happen. When it does work, though, expect a GAIN: 5/8. And sometimes, constant propagation won't work for CHAR expressions. But when it does, expect a GAIN: 4/8.

```sql
Query #1:
SELECT * FROM Table1

  WHERE date_column = CURRENT_DATE
    AND amount * 5 > 100.00

Query #2:
SELECT * FROM Table1

  WHERE date_column = DATE '2002-01-01'
    AND amount * 5 > 100.00

GAIN: 5/8
```

### Dead Code Elimination
In some old SQL programs, you'll encounter literals on both sides of the comparison operator, as in this example
```sql
SELECT * FROM Table1
  WHERE 0 = 1
    AND column1 = 'I hope we never execute this'
```

In the days before C-style /* comments */ were legal in an SQL statement, this was a way to add an inline comment string. Because the expression 0 = 1 is always false, this query will

always return zero rows, and therefore DBMSs can skip the whole WHERE clause. But some of them don't. We tested this by removing the WHERE clause and got a gain
```
SELECT * FROM Table1
GAIN: 5/8
```
of course, obvious that these two queries aren't equivalent—the point is merely that it should take less time to retrieve zero rows due to an always-false condition than it should to do a full table scan-provided the DBMS doesn't evaluate the always-false condition. This example shows that DBMSs don't always throw out always-false conditions and all their dependents in the PREPARE stage. But they're pretty reliable at throwing out always-true conditions

So you can use always- true conditions for an SQL equivalent of conditional compilation. For example, if you worry that a DBMS won't give high precision for division results, add a separate condition that comes into play only when necessary—as in this example:

```sql
... WHERE (77 / 10 = 7.7 AND column1 / 10 = 7.7)
       OR (77 / 10 = 7 AND column1 * 10 = 77)
       GAIN: 5/8
``` 

### Ensure You Use the Right DBMS
### Constant Folding
Anyone who has used C will know that the expression x=1+1-1-1 is folded to x=0 at compile time. So it may surprise you that many SQL DBMSs do not fold these five obvious-looking transform candidates
```sql
... WHERE column1 + 0
... WHERE 5 + 0.0
... WHERE column1 IN (1, 3, 3)
... CAST(1 AS INTEGER)
... WHERE 'a' || 'b'
```

If you find expressions like these in old code though, our tip is—Leave them alone. They are there for historical reasons, such as forcing the DBMS to ignore indexes, changing the result data type, allowing for the difference between SMALLINT and INTEGER, or evading a limit on line size.

The obvious-looking cases are precisely the cases where you should stop and wonder whether the original programmer had some reason for the weird syntax choice. We read a Java optimization article once that sums it up nicely: "Rule #1: Understand the code." Nevertheless, we do recommend that you transform this search condition:
```sql
... WHERE a - 3 = 5

to:

... WHERE a = 8         /* a - 3 = 5 */
GAIN: 6/8
```

### Case-Insensitive Searches
We've seen many programmers try to ensure case insensitivity by using the fold function UPPER, as in:

```
... WHERE UPPER(column1) = 'SMITH'
```
That can be a mistake if you're dealing with strings that contain anything other than strictly Latin letters. With some DBMSs, when you translate certain French or German strings to uppercase, you lose information. For example, the function:
```
... UPPER('résumé')
```

An even better way is to eliminate the fold function entirely if that's possible, because—we appeal to authority here—both the Microsoft and Oracle manuals say: "Avoid functions on columns." We're sure they mean "avoid functions on columns when there's another way to get the result needed"—for example, to ensure case insensitivity, the best method is to use a case-insensitive collation rather than a fold function.

```sql
... WHERE column1 = 'SMITH'
       OR column1 = 'Smith'

GAIN: 8/8
```

which is still slow

Our tip here is—Take advantage of dead code elimination so that the 'Smith'
search happens only when the DBMS is case sensitive. Here's how:

```sql
... WHERE column1 = 'SMITH'
      OR  ('SMITH' <> 'Smith' AND column1 = 'Smith')

GAIN: 3/8
```

If you can't avoid functions, don't use UPPER to ensure case insensitivity. Use LOWER instead.
### Sargability

The left side of a search condition should be a **simple column name**; the right side should be an **easy- to-look-up value**

```
5 = column1
=> 
column1 = 5
```
When there's arithmetic involved, though, only some DBMSs will transpose. For example, we tested this transform:
```
... WHERE column1 - 3 = -column2

transforms to:

... WHERE column1 = -column2 + 3
GAIN: 4/8
```

On a 32-bit computer, arithmetic is fastest if all operands are INTEGERs (because INTEGERs are 32- bit signed numbers) rather than SMALLINTs, DECIMALs, or FLOATs. Thus this condition:

```
.. WHERE decimal_column * float_column

is slower than:

... WHERE integer_column * integer_column
GAIN: 5/8
```


## Specific Tuning
### AND

**When everything else is equal, DBMSs will evaluate a series of ANDed expressions from left to right (except Oracle, which evaluates from right to left when the cost-based optimizer is operating)**

**You can take advantage of this behavior by putting the *least likely expression* first or—if both expressions are equally likely—putting the least complex expression first**

Then, if the first expression is false, the DBMS won't bother to evaluate the second expression. So, for example (unless you're using Oracle), you should transform:
```sql
... WHERE column1 = 'A' AND column2 = 'B'

to:

... WHERE column2 = 'B' AND column1 = 'A'
GAIN: 6/7 assuming column2 = 'B' is less likely
```

*Oracle with the rule-based optimizer shows a gain, but don't do this for Oracle running the cost-based optimizer. The gain shown is for only seven DBMSs.*

### OR

**When you're writing expressions with OR, put the *most likely expression* at the left.**
So do transform
```sql
Expression #1:
... WHERE column2 = 'B' OR column1 = 'A'

Expression #2:
... WHERE column1 = 'A' OR column2 = 'B'
GAIN: 4/7 assuming column1 = 'A' is most likely
```

*Oracle with the rule-based optimizer shows no change, but don't do this for Oracle running the cost- based optimizer. The gain shown is for only seven DBMSs.*

Oracle users should ignore this advice because Oracle evaluates from right to left when the cost-based optimizer is operating.

ORs are also faster if all columns are the same, because that reduces the number of columns and indexes that the DBMS has to read. Therefore, in a long series of ORs, expressions for the same column should be together

```sql
Expression #1:
... WHERE column1 = 1
       OR column2 = 3
       OR column1 = 2

Expression #2:
... WHERE column1 = 1
	   OR column1 = 2
       OR column2 = 3
GAIN: 1/8
```

### AND Plus OR

The Distributive Law states that:

```
A AND (B OR C)
is the same thing as
(A AND B) OR (A AND C)
```

Suppose you have the table shown in Table 2-3, on which you must execute a query where the ANDs come first:
![[Screenshot 2023-09-14 at 11.28.17.png]]

```sql
SELECT * FROM Table1

WHERE (column1 = 1 AND column2 = 'A')
     OR (column1 = 1 AND column2 = 'B')
```
Step: 
- Index lookup: column1=1. Result set = {row 3}
- Index lookup: column2='A'. Result set = {row 1}
- AND to merge the result sets. Result set = {}
- Index lookup: column1=1. Result set = {row 3}
- Index lookup: column2='B. Result set = {row 2}
- AND to merge the result sets. Result set = {}
- OR to merge the result sets. Result set = {}
=> 
```sql
SELECT * FROM Table1
      WHERE column1 = 1
    
        AND (column2 = 'A' OR column2 = 'B')
    GAIN: 2/8
```
Step: 
- Index lookup: column2='A'. Result set = {row 1}
- Index lookup: column2='B'. Result set = {row 2}
- OR to merge the result sets. Result set = {row 1, 2}
- Index lookup: column1=1. Result set = {row 3}
- AND to merge the result sets. Result set = {}

This test gave us a gain for only two of the Big Eight. The other DBMSs tend to apply the Distributive Law themselves, so that they will always be working with the same, canonical query. Nevertheless, the evidence shows that, for simple search conditions, you're better off with this construct:
    
    A AND (B OR C)
    
    than with this one:
    
    (A AND B) OR (A AND C)


### NOT
```sql
... WHERE NOT (column1 > 5)

transforms to:

... WHERE column1 <= 5
```

**De morgan**

```sql
... WHERE NOT (column1 > 5 OR column2 = 7)

transforms to:

... WHERE column1 <= 5
      AND column2 <> 7
```

If, after transforming, you end up with a not equals operator, expect slowness. After all, in any evenly distributed set of values, when there are more than two rows, the unequal values always outnumber the equal values. Because of this, some DBMSs won't use an index for not equals comparisons. But they will use an index for greater than and for less than—so you can transform this type of condition

```sql
... WHERE NOT (bloodtype = 'O')

to:

... WHERE bloodtype < 'O'
       OR bloodtype > 'O'

GAIN: 3/8
```

### IN
```sql
Condition #1:
... WHERE column1 = 5

OR column1 = 6

Condition #2:
... WHERE column1 IN (5, 6)
GAIN: 2/8
```

With two of the Big Eight, IN is faster than OR. So transform OR to IN when you can. All the other DBMSs will just translate IN back to OR, so you won't lose anything.

When an IN operator has a dense series of integers, it's better to ask "what is out" rather than "what is in." Thus, this condition

```sql
... WHERE column1 IN (1, 3, 4, 5)

should be transformed to:

... WHERE column1 BETWEEN 1 AND 5
      AND column1 <> 2

GAIN: 7/8
```

Similar gains can happen when a series can be represented by an arithmetic expression.

### LIKE

Most DBMSs will use an index for a LIKE pattern if it starts with a real character but will avoid an index for a LIKE pattern that starts with a wildcard (either % or _).