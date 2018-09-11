**SQLite DISTINCT Keyword**
===========================

The SQLite **DISTINCT** keyword is used in conjunction with SELECT statement to
eliminate all the duplicate records and fetching only unique records.

There may be a situation when you have multiple duplicate records in a table.
While fetching such records, it makes more sense to fetch only unique records
instead of fetching duplicate records.

### **Syntax:**

The basic syntax of DISTINCT keyword to eliminate duplicate records is as
follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
SELECT DISTINCT column1, column2,.....columnN 

FROM table_name

WHERE [condition]
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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

8           Paul        24          Houston     20000.0

9           James       44          Norway      5000.0

10          James       45          Texas       5000.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

First, let us see how the following SELECT query returns duplicate salary
records:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite> SELECT name FROM COMPANY;
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This would produce the following result:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
NAME

----------

Paul

Allen

Teddy

Mark

David

Kim

James

Paul

James

James
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now, let us use **DISTINCT** keyword with the above SELECT query and see the
result:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite> SELECT DISTINCT name FROM COMPANY;
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This would produce the following result, where we do not have any duplicate
entry:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
NAME

----------

Paul

Allen

Teddy

Mark

David

Kim

James
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
