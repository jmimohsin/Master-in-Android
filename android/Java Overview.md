**Java - Overview**
===================

Java programming language was originally developed by Sun Microsystems which was
initiated by James Gosling and released in 1995 as core component of Sun
Microsystems' Java platform (Java 1.0 [J2SE]).

As of December 2008, the latest release of the Java Standard Edition is 6
(J2SE). With the advancement of Java and its widespread popularity, multiple
configurations were built to suite various types of platforms. Ex: J2EE for
Enterprise Applications, J2ME for Mobile Applications.

Sun Microsystems has renamed the new J2 versions as Java SE, Java EE and Java ME
respectively. Java is guaranteed to be **Write Once, Run Anywhere.**

Java is:

-   **Object Oriented:** In Java, everything is an Object. Java can be easily
    extended since it is based on the Object model.

-   **Platform independent:** Unlike many other programming languages including
    C and C++, when Java is compiled, it is not compiled into platform specific
    machine, rather into platform independent byte code. This byte code is
    distributed over the web and interpreted by virtual Machine (JVM) on
    whichever platform it is being run.

-   **Simple:Java** is designed to be easy to learn. If you understand the basic
    concept of OOP Java would be easy to master.

-   **Secure:** With Java's secure feature it enables to develop virus-free,
    tamper-free systems. Authentication techniques are based on public-key
    encryption.

-   **Architectural-neutral :Java** compiler generates an architecture-neutral
    object file format which makes the compiled code to be executable on many
    processors, with the presence of Java runtime system.

-   **Portable:Being** architectural-neutral and having no implementation
    dependent aspects of the specification makes Java portable. Compiler in Java
    is written in ANSI C with a clean portability boundary which is a POSIX
    subset.

-   **Robust:Java** makes an effort to eliminate error prone situations by
    emphasizing mainly on compile time error checking and runtime checking.

-   **Multithreaded:** With Java's multithreaded feature it is possible to write
    programs that can do many tasks simultaneously. This design feature allows
    developers to construct smoothly running interactive applications.

-   **Interpreted:Java** byte code is translated on the fly to native machine
    instructions and is not stored anywhere. The development process is more
    rapid and analytical since the linking is an incremental and light weight
    process.

-   **High Performance:** With the use of Just-In-Time compilers, Java enables
    high performance.

-   **Distributed:Java** is designed for the distributed environment of the
    internet.

-   **Dynamic:** Java is considered to be more dynamic than C or C++ since it is
    designed to adapt to an evolving environment. Java programs can carry
    extensive amount of run-time information that can be used to verify and
    resolve accesses to objects on run-time.

**History of Java:**
--------------------

James Gosling initiated the Java language project in June 1991 for use in one of
his many set-top box projects. The language, initially called Oak after an oak
tree that stood outside Gosling's office, also went by the name Green and ended
up later being renamed as Java, from a list of random words.

Sun released the first public implementation as Java 1.0 in 1995. It promised
**Write Once, Run Anywhere** (WORA), providing no-cost run-times on popular
platforms.

On 13 November 2006, Sun released much of Java as free and open source software
under the terms of the GNU General Public License (GPL).

On 8 May 2007, Sun finished the process, making all of Java's core code free and
open-source, aside from a small portion of code to which Sun did not hold the
copyright.

**Tools you will need:**
------------------------

For performing the examples discussed in this tutorial, you will need a Pentium
200-MHz computer with a minimum of 64 MB of RAM (128 MB of RAM recommended).

You also will need the following softwares:

-   Linux 7.1 or Windows 95/98/2000/XP operating system.

-   Java JDK 5

-   Microsoft Notepad or any other text editor

This tutorial will provide the necessary skills to create GUI, networking, and
Web applications using Java.

**Try It Option:**
------------------

We have provided you an option to compile and execute available code online.
Just click on **Try it** button avaiable at top-right corner of the code window
to compile and execute available code. There are certain examples which can not
be executed online, so we have skipped those examples.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World");
    }
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There may be a case that you do not see the result of the compiled/executed
code, in such case you can re-try to compile and execute the code using
**execute** button available in compliation pop-up window.

 
