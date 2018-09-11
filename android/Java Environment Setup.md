**Java Environment Setup**
==========================

**Try it Option Online**
------------------------

You really do not need to set up your own environment to start learning Java
programming language. Reason is very simple, we already have setup Java
Programming environment online, so that you can compile and execute all the
available examples online at the same time when you are doing your theory work.
This gives you confidence in what you are reading and to check the result with
different options. Feel free to modify any example and execute it online.

Try following example using **Try it** option available at the top right corner
of the below sample code box:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World");
    }
}
```

For most of the examples given in this tutorial, you will find **Try it**
option, so just make use of it and enjoy your learning.

**Local Environment Setup**
---------------------------

If you are still willing to set up your environment for Java programming
language, then this section guides you on how to download and set up Java on
your machine. Please follow the following steps to set up the environment.

Java SE is freely available from the link [Download
Java](http://java.sun.com/javase/downloads/index_jdk5.jsp). So you download a
version based on your operating system.

Follow the instructions to download java and run the **.exe** to install Java on
your machine. Once you installed Java on your machine, you would need to set
environment variables to point to correct installation directories:

**Setting up the path for windows 2000/XP:**
--------------------------------------------

Assuming you have installed Java in *c:\\Program Files\\java\\jdk* directory:

-   Right-click on 'My Computer' and select 'Properties'.

-   Click on the 'Environment variables' button under the 'Advanced' tab.

-   Now, alter the 'Path' variable so that it also contains the path to the Java
    executable. Example, if the path is currently set to
    'C:\\WINDOWS\\SYSTEM32', then change your path to read
    'C:\\WINDOWS\\SYSTEM32;c:\\Program Files\\java\\jdk\\bin'.

**Setting up the path for windows 95/98/ME:**
---------------------------------------------

Assuming you have installed Java in *c:\\Program Files\\java\\jdk* directory:

-   Edit the 'C:\\autoexec.bat' file and add the following line at the end:  
    'SET PATH=%PATH%;C:\\Program Files\\java\\jdk\\bin'

**Setting up the path for Linux, UNIX, Solaris, FreeBSD:**
----------------------------------------------------------

Environment variable PATH should be set to point to where the Java binaries have
been installed. Refer to your shell documentation if you have trouble doing
this.

Example, if you use *bash* as your shell, then you would add the following line
to the end of your '.bashrc: export PATH=/path/to/java:\$PATH'

**Popular Java Editors:**
-------------------------

To write your Java programs, you will need a text editor. There are even more
sophisticated IDEs available in the market. But for now, you can consider one of
the following:

-   **Notepad:** On Windows machine you can use any simple text editor like
    Notepad (Recommended for this tutorial), TextPad.

-   **Netbeans:is** a Java IDE that is open-source and free which can be
    downloaded from <http://www.netbeans.org/index.html>.

-   **Eclipse:** is also a Java IDE developed by the eclipse open-source
    community and can be downloaded from <http://www.eclipse.org/>.

 
