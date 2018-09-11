**SQLite DETACH Database**
==========================

SQLite **DETACH DTABASE** statement is used to detach and dissociate a named
database from a database connection which was previously attached using ATTACH
statement. If the same database file has been attached with multiple aliases,
then DETACH command will disconnect only given name and rest of the attachement
will still continue. You cannot detach the **main** or **temp** databases.

If the database is an in-memory or temporary database, the database will be
destroyed and the contents will be lost.

### **Syntax:**

Basic syntax of SQLite DETACH DATABASE 'Alias-Name' statement is as follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
DETACH DATABASE 'Alias-Name';
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Here 'Alias-Name' is the same alias, which you had used while attaching database
using ATTACH statement.

### **Example:**

Consider you have a database, which you created in previous chapter and attached
it with 'test' and 'currentDB' as we can see using .database command:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite>.databases

seq  name             file

---  ---------------  ----------------------

0    main             /home/sqlite/testDB.db

2    test             /home/sqlite/testDB.db

3    currentDB        /home/sqlite/testDB.db
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now let's try to detach 'currentDB' from testDB.db as follows:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite> DETACH DATABASE 'currentDB';
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now, if you will check current attachment, you will find that testDB.db is still
connected with 'test' and 'main'.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
sqlite>.databases

seq  name             file

---  ---------------  ----------------------

0    main             /home/sqlite/testDB.db

2    test             /home/sqlite/testDB.db
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
