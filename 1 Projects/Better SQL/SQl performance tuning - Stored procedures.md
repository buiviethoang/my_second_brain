### Determinism
Nondeterministic functions are bad.
•They are bad in CHECK clauses because you cannot be sure that you can rerun the same
data-change statements and get the same results each time.
- They are bad in select lists because DBMSs like to say "if the query has the same syntax then
use the same plan."
- They are bad in WHERE clauses because they cannot be indexed. There's no point in
indexing a function that is subject to unpredictable change. The DBMS has to reevaluate the
function every time

Nondeterminism is a long name but a fairly simple idea. Clearly, you want to make sure your
functions are deterministic, and you want to declare to the DBMS that they are deterministic. The
problem area is external functions. They often depend on hidden factors (like the existence of a file)
that the DBMS cannot detect.

### Advantages of Stored Procedures
- Procedures are on the server so messages don't need to go back and forth to the client during
the time the procedure is executed.
- Procedures are parsed once, and the result of the parsing is stored persistently, so there's no
need to reparse for every execution.
- Procedures are in the catalog so they are retrievable, and procedures are subject to security
provisions, in the same way as other SQL data.
- Procedures are in one place so code sharing is easy, and when changes happen there's no need
to send code changes to clients.

#### Less Traffic
Stored procedures mean less message traffic between clients and servers. The client must send some
sort of message to initiate the procedure, and the procedure must return some sort of result when the
procedure is over, but that's all—no message passing occurs within the procedure.
So a stored
procedure that contains [n] statements will need only two messages, while an ODBC application
that contains [n] statements will need (2 * n) messages
#### Semiprecompilation
The second advantage of stored procedures is that they're precompiled. This means that the DBMS
only has to prepare a statement once, instead of preparing a statement every time it executes. To avoid
building false hopes, we should emphasize that the precompilation is only partial, is only temporary,
and is not a free lunch.
#### Parameters
We've already noted that the DBMS rechecks the parameter values every time it executes a stored
procedure, and that the DBMS takes parameter values into account for its query plan when it executes
a procedure for the first time. The same cannot be said for local-variable values. Therefore if a
procedure has a condition like this somewhere:
... WHERE column1 = num1
it's better if num1 is a parameter, not a variable.
##
