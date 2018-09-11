**SQLite CREATE Table**
=======================

The SQLite **CREATE TABLE** statement is used to create a new table in any of
the given database. Creating a basic table involves naming the table and
defining its columns and each column's data type.

### **Syntax:**

Basic syntax of CREATE TABLE statement is as follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
CREATE TABLE database_name.table_name(

   column1 datatype  PRIMARY KEY(one or more columns),

   column2 datatype,

   column3 datatype,

   .....

   columnN datatype,

);
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

CREATE TABLE is the keyword telling the database system to create a new table.
The unique name or identifier for the table follows the CREATE TABLE statement.
Optionally you can specify *database_name* along with *table_name*.

### **Example:**

Following is an example which creates a COMPANY table with ID as primary key and
NOT NULL are the constraints showing that these fields can not be NULL while
creating records in this table:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite> CREATE TABLE COMPANY(

   ID INT PRIMARY KEY     NOT NULL,

   NAME           TEXT    NOT NULL,

   AGE            INT     NOT NULL,

   ADDRESS        CHAR(50),

   SALARY         REAL

);
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Let us create one more table, which we will use in our exercises in subsequent
chapters:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite> CREATE TABLE DEPARTMENT(

   ID INT PRIMARY KEY      NOT NULL,

   DEPT           CHAR(50) NOT NULL,

   EMP_ID         INT      NOT NULL

);
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can verify if your table has been created successfully using SQLIte command
**.tables** command, which will be used to list down all the tables in an
attached database.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite>.tables

COMPANY     DEPARTMENT
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Here, you can see COMPANY table twice because its showing COMPANY table for main
database and test.COMPANY table for 'test' alias created for your testDB.db. You
can get complete information about a table using SQLite **.schema** command as
follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite>.schema COMPANY

CREATE TABLE COMPANY(

   ID INT PRIMARY KEY     NOT NULL,

   NAME           TEXT    NOT NULL,

   AGE            INT     NOT NULL,

   ADDRESS        CHAR(50),

   SALARY         REAL

);
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
