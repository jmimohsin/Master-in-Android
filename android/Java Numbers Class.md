**Java - Numbers Class**
========================

Normally, when we work with Numbers, we use primitive data types such as byte,
int, long, double, etc.

### **Example:**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
int i = 5000;
float gpa = 13.65;
byte mask = 0xaf;
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

However, in development, we come across situations where we need to use objects
instead of primitive data types. In-order to achieve this Java provides wrapper
classes for each primitive data type.

All the wrapper classes (Integer, Long, Byte, Double, Float, Short) are
subclasses of the abstract class Number.

![Number Subclasses](file:///D:/Mohsin/assets/assets/img/Numbers_class.jpg)

This wrapping is taken care of by the compiler, the process is called boxing. So
when a primitive is used when an object is required, the compiler boxes the
primitive type in its wrapper class. Similarly, the compiler unboxes the object
to a primitive as well. The **Number** is part of the java.lang package.

Here is an example of boxing and unboxing:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
public class Test{
 
   public static void main(String args[]){
      Integer x = 5; // boxes int to an Integer object
      x =  x + 10;   // unboxes the Integer to a int
      System.out.println(x);
   }
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This would produce the following result:

15

When x is assigned integer values, the compiler boxes the integer because x is
integer objects. Later, x is unboxed so that they can be added as integers.

**Number Methods:**
-------------------

Here is the list of the instance methods that all the subclasses of the Number
class implement:

 

| **SN** | **Methods with Description**                                                                            |
|--------|---------------------------------------------------------------------------------------------------------|
| 1      | xxxValue()                                                                                              |
|        | Converts the value of *this* Number object to the xxx data type and returned it.                        |
| 2      | compareTo()                                                                                             |
|        | Compares *this* Number object to the argument.                                                          |
| 3      | equals()                                                                                                |
|        | Determines whether *this* number object is equal to the argument.                                       |
| 4      | valueOf()                                                                                               |
|        | Returns an Integer object holding the value of the specified primitive.                                 |
| 5      | toString()                                                                                              |
|        | Returns a String object representing the value of specified int or Integer.                             |
| 6      | parseInt()                                                                                              |
|        | This method is used to get the primitive data type of a certain String.                                 |
| 7      | abs()                                                                                                   |
|        | Returns the absolute value of the argument.                                                             |
| 8      | ceil()                                                                                                  |
|        | Returns the smallest integer that is greater than or equal to the argument. Returned as a double.       |
| 9      | floor()                                                                                                 |
|        | Returns the largest integer that is less than or equal to the argument. Returned as a double.           |
| 10     | rint()                                                                                                  |
|        | Returns the integer that is closest in value to the argument. Returned as a double.                     |
| 11     | round()                                                                                                 |
|        | Returns the closest long or int, as indicated by the method's return type, to the argument.             |
| 12     | min()                                                                                                   |
|        | Returns the smaller of the two arguments.                                                               |
| 13     | max()                                                                                                   |
|        | Returns the larger of the two arguments.                                                                |
| 14     | exp()                                                                                                   |
|        | Returns the base of the natural logarithms, e, to the power of the argument.                            |
| 15     | log()                                                                                                   |
|        | Returns the natural logarithm of the argument.                                                          |
| 16     | pow()                                                                                                   |
|        | Returns the value of the first argument raised to the power of the second argument.                     |
| 17     | sqrt()                                                                                                  |
|        | Returns the square root of the argument.                                                                |
| 18     | sin()                                                                                                   |
|        | Returns the sine of the specified double value.                                                         |
| 19     | cos()                                                                                                   |
|        | Returns the cosine of the specified double value.                                                       |
| 20     | tan()                                                                                                   |
|        | Returns the tangent of the specified double value.                                                      |
| 21     | asin()                                                                                                  |
|        | Returns the arcsine of the specified double value.                                                      |
| 22     | acos()                                                                                                  |
|        | Returns the arccosine of the specified double value.                                                    |
| 23     | atan()                                                                                                  |
|        | Returns the arctangent of the specified double value.                                                   |
| 24     | atan2()                                                                                                 |
|        | Converts rectangular coordinates (x, y) to polar coordinate (r, theta) and returns theta.               |
| 25     | toDegrees()                                                                                             |
|        | Converts the argument to degrees                                                                        |
| 26     | toRadians()                                                                                             |
|        | Converts the argument to radians.                                                                       |
| 27     | random()                                                                                                |
|        | Returns a random number.                                                                                |
