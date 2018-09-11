**SQLite DELETE Query**
=======================

The SQLite **DELETE** Query is used to delete the existing records from a table.
You can use WHERE clause with DELETE query to delete selected rows, otherwise
all the records would be deleted.

### **Syntax:**

The basic syntax of DELETE query with WHERE clause is as follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DELETE FROM table_name

WHERE [condition];
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can combine N number of conditions using AND or OR operators.

### **Example:**

Consider COMPANY table is having the following records:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
ID          NAME        AGE         ADDRESS     SALARY

----------  ----------  ----------  ----------  ----------

1           Paul        32          California  20000.0

2           Allen       25          Texas       15000.0

3           Teddy       23          Norway      20000.0

4           Mark        25          Rich-Mond   65000.0

5           David       27          Texas       85000.0

6           Kim         22          South-Hall  45000.0

7           James       24          Houston     10000.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Following is an example, which would DELETE a customer whose ID is 7:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite> DELETE FROM COMPANY WHERE ID = 7;
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now COMPANY table will have following records:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
ID          NAME        AGE         ADDRESS     SALARY

----------  ----------  ----------  ----------  ----------

1           Paul        32          California  20000.0

2           Allen       25          Texas       15000.0

3           Teddy       23          Norway      20000.0

4           Mark        25          Rich-Mond   65000.0

5           David       27          Texas       85000.0

6           Kim         22          South-Hall  45000.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you want to DELETE all the records from COMPANY table, you do not need to use
WHERE clause with DELETE query, which would be as follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite> DELETE FROM COMPANY;
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now, COMPANY table does not have any record because all the records have been
deleted by DELETE statement.
