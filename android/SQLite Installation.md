**SQLite - Installation**
=========================

The SQLite is famous for its great feature zero-configuration, which means no
complex setup or administration is needed. This chapter will take you through
the process of setting up SQLite on Windows, Linux and Mac OS X.

**Install SQLite On Windows**
-----------------------------

-   Go to [SQLite download page](http://www.sqlite.org/download.html), and
    download precompiled binaries from Windows section.

-   You will need to download **sqlite-shell-win32-\*.zip** and
    **sqlite-dll-win32-\*.zip** zipped files.

-   Create a folder C:\\\>sqlite and unzip above two zipped files in this folder
    which will give you sqlite3.def, sqlite3.dll and sqlite3.exe files.

-   Add C:\\\>sqlite in your PATH environment variable and finally go to the
    command prompt and issue **sqlite3** command, which should display a result
    something as below.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
C:\>sqlite3
SQLite version 3.7.15.2 2013-01-09 11:53:05
Enter ".help" for instructions
Enter SQL statements terminated with a ";"
sqlite>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Install SQLite On Linux**
---------------------------

Today, almost all the flavours of Linux OS are being shipped with SQLite. So you
just issue the following command to check if you already have SQLite installed
on your machine or not.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$sqlite3
SQLite version 3.7.15.2 2013-01-09 11:53:05
Enter ".help" for instructions
Enter SQL statements terminated with a ";"
sqlite>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you do not see above result, then it means you do not have SQLite installed
on your Linux machine. So let's follow the following steps to install SQLite:

-   Go to [SQLite download page](http://www.sqlite.org/download.html) and
    download **sqlite-autoconf-\*.tar.gz** from source code section.

-   Follow the following steps:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$tar xvfz sqlite-autoconf-3071502.tar.gz
$cd sqlite-autoconf-3071502
$./configure --prefix=/usr/local
$make
$make install
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Above procedure will end with SQLite installation on your Linux machine which
you can verify as explained above.

**Install SQLite On Mac OS X**
------------------------------

Though latest version of Mac OS X comes pre-installed with SQLite but if you do
not have installation available then just follow the following steps:

-   Go to [SQLite download page](http://www.sqlite.org/download.html), and
    download **sqlite-autoconf-\*.tar.gz** from source code section.

-   Follow the following steps:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$tar xvfz sqlite-autoconf-3071502.tar.gz
$cd sqlite-autoconf-3071502
$./configure --prefix=/usr/local
$make
$make install
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Above procedure will end with SQLite installation on your Mac OS X machine which
you can verify by issuing following command:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
$sqlite3
SQLite version 3.7.15.2 2013-01-09 11:53:05
Enter ".help" for instructions
Enter SQL statements terminated with a ";"
sqlite>
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Finally, you have SQLite command prompt where you can issue SQLite commands to
do your excercises.
