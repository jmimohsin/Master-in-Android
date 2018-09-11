**Java Character Class**
========================

Normally, when we work with characters, we use primitive data types char.

### **Example:**

```java
char ch = 'a';
 
// Unicode for uppercase Greek omega character
char uniChar = '\u039A';
 
// an array of chars
char[] charArray ={ 'a', 'b', 'c', 'd', 'e' };
```

However in development, we come across situations where we need to use objects
instead of primitive data types. In order to achieve this, Java provides wrapper
class **Character** for primitive data type char.

The Character class offers a number of useful class (i.e., static) methods for
manipulating characters. You can create a Character object with the Character
constructor:

Character ch = new Character('a');

The Java compiler will also create a Character object for you under some
circumstances. For example, if you pass a primitive char into a method that
expects an object, the compiler automatically converts the char to a Character
for you. This feature is called autoboxing or unboxing, if the conversion goes
the other way.

### **Example:**

```java
// Here following primitive char 'a'
// is boxed into the Character object ch
Character ch = 'a';
 
// Here primitive 'x' is boxed for method test,
// return is unboxed to char 'c'
char c = test('x');
```

A character preceded by a backslash (\\) is an escape sequence and has special
meaning to the compiler.

The newline character (\\n) has been used frequently in this tutorial in
System.out.println() statements to advance to the next line after the string is
printed.

Following table shows the Java escape sequences:

 

| **Escape Sequence** | **Description**                                              |
|---------------------|--------------------------------------------------------------|
| \\t                 | Inserts a tab in the text at this point.                     |
| \\b                 | Inserts a backspace in the text at this point.               |
| \\n                 | Inserts a newline in the text at this point.                 |
| \\r                 | Inserts a carriage return in the text at this point.         |
| \\f                 | Inserts a form feed in the text at this point.               |
| \\'                 | Inserts a single quote character in the text at this point.  |
| \\"                 | Inserts a double quote character in the text at this point.  |
| \\\\                | Inserts a backslash character in the text at this point.     |

 

When an escape sequence is encountered in a print statement, the compiler
interprets it accordingly.

### **Example:**

If you want to put quotes within quotes you must use the escape sequence, \\",
on the interior quotes:

```java
public class Test {
 
   public static void main(String args[]) {
      System.out.println("She said \"Hello!\" to me.");
   }
}
```

This would produce the following result:

She said "Hello!" to me.

**Character Methods:**
----------------------

Here is the list of the important instance methods that all the subclasses of
the Character class implement:

 

| **SN** | **Methods with Description**                                                                                                                                                                                        |
|--------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1      | [isLetter()](file:///My%20Web%20Sites/www.tutorialspoint.com/www.tutorialspoint.com/java/character_isletter.html)                                                                                                   |
|        | Determines whether the specified char value is a letter.                                                                                                                                                            |
| 2      | [isDigit()](file:///My%20Web%20Sites/www.tutorialspoint.com/www.tutorialspoint.com/java/character_isdigit.html)                                                                                                     |
|        | Determines whether the specified char value is a digit.                                                                                                                                                             |
| 3      | [isWhitespace()](file:///My%20Web%20Sites/www.tutorialspoint.com/www.tutorialspoint.com/java/character_iswhitespace.html)                                                                                           |
|        | Determines whether the specified char value is white space.                                                                                                                                                         |
| 4      | [isUpperCase()](file:///My%20Web%20Sites/www.tutorialspoint.com/www.tutorialspoint.com/java/character_isuppercase.html)                                                                                             |
|        | Determines whether the specified char value is uppercase.                                                                                                                                                           |
| 5      | [isLowerCase()](file:///My%20Web%20Sites/www.tutorialspoint.com/www.tutorialspoint.com/java/character_islowercase.html)                                                                                             |
|        | Determines whether the specified char value is lowercase.                                                                                                                                                           |
| 6      | [toUpperCase()](file:///My%20Web%20Sites/www.tutorialspoint.com/www.tutorialspoint.com/java/character_touppercase.html)                                                                                             |
|        | Returns the uppercase form of the specified char value.                                                                                                                                                             |
| 7      | [toLowerCase()](file:///My%20Web%20Sites/www.tutorialspoint.com/www.tutorialspoint.com/java/character_tolowercase.html)                                                                                             |
|        | Returns the lowercase form of the specified char value.                                                                                                                                                             |
| 8      | [toString()](file:///My%20Web%20Sites/www.tutorialspoint.com/www.tutorialspoint.com/java/character_tostring.html)                                                                                                   |
|        | Returns a String object representing the specified character valuethat is, a one-character string.                                                                                                                  |

 

For a complete list of methods, please refer to the java.lang.Character API
specification.
