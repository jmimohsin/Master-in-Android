**SQLite CREATE Database**
==========================

The SQLite **sqlite3** command is used to create new SQLite database. You do not
need to have any special privilege to create a database.

### **Syntax:**

Basic syntax of sqlite3 command is as follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$sqlite3 DatabaseName.db
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Always, database name should be unique within the RDBMS.

### **Example:**

If you want to create new database \<testDB.db\>, then SQLITE3 statement would
be as follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$sqlite3 testDB.db

SQLite version 3.7.15.2 2013-01-09 11:53:05

Enter ".help" for instructions

Enter SQL statements terminated with a ";"

sqlite>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Above command will create a file **testDB.db** in the current directory. This
file will be used as database by SQLite engine. If you have noticed while
creating database, sqlite3 command will provide a **sqlite\>** prompt after
creating database file successfully.

Once a database is created, you can check it in the list of databases using
SQLite **.databases** command as follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite>.databases

seq  name             file

---  ---------------  ----------------------

0    main             /home/sqlite/testDB.db
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You will use SQLite **.quit** command to come out of the sqlite prompt as
follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite>.quit

$
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**The .dump Command**
---------------------

You can use **.dump** dot command to export complete database in a text file
using SQLite command at command prompt as follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$sqlite3 testDB.db .dump > testDB.sql
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Above command will convert the entire contents of **testDB.db** database into
SQLite statements and dump it into ASCII text file **testDB.sql**. You can do
restoration from the generated testDB.sql in simple way as follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$sqlite3 testDB.db < testDB.sql
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

At this moment your database is empty, so you can try above two procedures once
you have few tables and data in your database.
