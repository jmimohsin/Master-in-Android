**SQLite ATTACH Database**
==========================

Consider a case when you have multiple databases available and you want to use
any one of them at a time. SQLite **ATTACH DTABASE** statement is used to select
a particular database, and after this command, all SQLite statements will be
executed under the attached database.

### **Syntax:**

Basic syntax of SQLite ATTACH DATABASE statement is as follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
ATTACH DATABASE 'DatabaseName' As 'Alias-Name';
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Above command will also create a database in case database is already not
created, otherwise it will just attach database file name with logical database
'Alias-Name'.

### **Example:**

If you want to attach an existing database **testDB.db**, then ATTACH DATABASE
statement would be as follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite> ATTACH DATABASE 'testDB.db' as 'TEST';
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use SQLite **.database** command to display attached database.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite> .database

seq  name             file

---  ---------------  ----------------------

0    main             /home/sqlite/testDB.db

2    test             /home/sqlite/testDB.db
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The database names **main** and **temp** are reserved for the primary database
and database to hold temporary tables and other temporary data objects. Both of
these database names exist for every database connection and should not be used
for attachment, otherwise you will get a warning message something as follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite>  ATTACH DATABASE 'testDB.db' as 'TEMP';

Error: database TEMP is already in use

sqlite>  ATTACH DATABASE 'testDB.db' as 'main';

Error: database TEMP is already in use
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
