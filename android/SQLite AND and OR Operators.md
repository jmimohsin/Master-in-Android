**SQLite AND and OR Operators**
===============================

The SQLite **AND** and **OR** operators are used to compile multiple conditions
to narrow down selected data in an SQLite statement. These two operators are
called conjunctive operators.

These operators provide a means to make multiple comparisons with different
operators in the same SQLite statement.

**The AND Operator:**
---------------------

The **AND** operator allows the existence of multiple conditions in an SQLite
statement's WHERE clause. While using AND operator, complete condition will be
assumed true when all the conditions are true. For example, [condition1] AND
[condition2] will be true only when both condition1 and condition2 are true.

### **Syntax:**

The basic syntax of AND operator with WHERE clause is as follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
SELECT column1, column2, columnN 

FROM table_name

WHERE [condition1] AND [condition2]...AND [conditionN];
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can combine N number of conditions using AND operator. For an action to be
taken by the SQLite statement, whether it be a transaction or query, all
conditions separated by the AND must be TRUE.

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

Following SELECT statement lists down all the records where AGE is greater than
or equal to 25 **AND** salary is greater than or equal to 65000.00:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite> SELECT * FROM COMPANY WHERE AGE >= 25 AND SALARY >= 65000;

 

ID          NAME        AGE         ADDRESS     SALARY

----------  ----------  ----------  ----------  ----------

4           Mark        25          Rich-Mond   65000.0

5           David       27          Texas       85000.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**The OR Operator:**
--------------------

The OR operator is also used to combine multiple conditions in an SQLite
statement's WHERE clause. While using OR operator, complete condition will be
assumed true when at least any of the the conditions is true. For example,
[condition1] OR [condition2] will be true if either condition1 or condition2 is
true.

### **Syntax:**

The basic syntax of OR operator with WHERE clause is as follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
SELECT column1, column2, columnN 

FROM table_name

WHERE [condition1] OR [condition2]...OR [conditionN]
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can combine N number of conditions using OR operator. For an action to be
taken by the SQLite statement, whether it be a transaction or query, only any
ONE of the conditions separated by the OR must be TRUE.

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

Following SELECT statement lists down all the records where AGE is greater than
or equal to 25 **OR** salary is greater than or equal to 65000.00:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite> SELECT * FROM COMPANY WHERE AGE >= 25 OR SALARY >= 65000;

 

ID          NAME        AGE         ADDRESS     SALARY

----------  ----------  ----------  ----------  ----------

1           Paul        32          California  20000.0

2           Allen       25          Texas       15000.0

4           Mark        25          Rich-Mond   65000.0

5           David       27          Texas       85000.0
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
