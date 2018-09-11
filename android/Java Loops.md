**Java Loops - for, while and do...while**
==========================================

There may be a situation when we need to execute a block of code several number
of times, and is often referred to as a loop.

Java has very flexible three looping mechanisms. You can use one of the
following three loops:

-   while Loop

-   do...while Loop

-   for Loop

As of Java 5, the *enhanced for loop* was introduced. This is mainly used for
Arrays.

**The while Loop:**
-------------------

A while loop is a control structure that allows you to repeat a task a certain
number of times.

### **Syntax:**

The syntax of a while loop is:

```java
while(Boolean_expression)
{
   //Statements
}
```

When executing, if the *boolean_expression* result is true, then the actions
inside the loop will be executed. This will continue as long as the expression
result is true.

Here, key point of the *while* loop is that the loop might not ever run. When
the expression is tested and the result is false, the loop body will be skipped
and the first statement after the while loop will be executed.

### **Example:**

```java
public class Test {
 
   public static void main(String args[]) {
      int x = 10;
 
      while( x < 20 ) {
         System.out.print("value of x : " + x );
         x++;
         System.out.print("\n");
      }
   }
}
```

This would produce the following result:

value of x : 10

value of x : 11

value of x : 12

value of x : 13

value of x : 14

value of x : 15

value of x : 16

value of x : 17

value of x : 18

value of x : 19

**The do...while Loop:**
------------------------

A do...while loop is similar to a while loop, except that a do...while loop is
guaranteed to execute at least one time.

### **Syntax:**

The syntax of a do...while loop is:

```java
do
{
   //Statements
}while(Boolean_expression);
```

Notice that the Boolean expression appears at the end of the loop, so the
statements in the loop execute once before the Boolean is tested.

If the Boolean expression is true, the flow of control jumps back up to do, and
the statements in the loop execute again. This process repeats until the Boolean
expression is false.

### **Example:**

```java
public class Test {
 
   public static void main(String args[]){
      int x = 10;
 
      do{
         System.out.print("value of x : " + x );
         x++;
         System.out.print("\n");
      }while( x < 20 );
   }
}
```

This would produce the following result:

value of x : 10

value of x : 11

value of x : 12

value of x : 13

value of x : 14

value of x : 15

value of x : 16

value of x : 17

value of x : 18

value of x : 19

**The for Loop:**
-----------------

A for loop is a repetition control structure that allows you to efficiently
write a loop that needs to execute a specific number of times.

A for loop is useful when you know how many times a task is to be repeated.

### **Syntax:**

The syntax of a for loop is:

```java
for(initialization; Boolean_expression; update)
{
   //Statements
}
```

Here is the flow of control in and for loop:

-   The initialization step is executed first, and only once. This step allows
    you to declare and initialize any loop control variables. You are not
    required to put a statement here, as long as a semicolon appears.

-   Next, the Boolean expression is evaluated. If it is true, the body of the
    loop is executed. If it is false, the body of the loop does not execute and
    flow of control jumps to the next statement past the for loop.

-   After the body of the for loop executes, the flow of control jumps back up
    to the update statement. This statement allows you to update any loop
    control variables. This statement can be left blank, as long as a semicolon
    appears after the Boolean expression.

-   The Boolean expression is now evaluated again. If it is true, the loop
    executes and the process repeats itself (body of loop, then update step,
    then Boolean expression). After the Boolean expression is false, the for
    loop terminates.

### **Example:**

```java
public class Test {
 
   public static void main(String args[]) {
 
      for(int x = 10; x < 20; x = x+1) {
         System.out.print("value of x : " + x );
         System.out.print("\n");
      }
   }
}
```

This would produce the following result:

value of x : 10

value of x : 11

value of x : 12

value of x : 13

value of x : 14

value of x : 15

value of x : 16

value of x : 17

value of x : 18

value of x : 19

**Enhanced for loop in Java:**
------------------------------

As of Java 5, the enhanced for loop was introduced. This is mainly used for
Arrays.

### **Syntax:**

The syntax of enhanced for loop is:

```java
for(declaration : expression)
{
   //Statements
}
```

-   **Declaration:** The newly declared block variable, which is of a type
    compatible with the elements of the array you are accessing. The variable
    will be available within the for block and its value would be the same as
    the current array element.

-   **Expression:** This evaluates to the array you need to loop through. The
    expression can be an array variable or method call that returns an array.

### **Example:**

```java
public class Test {
 
   public static void main(String args[]){
      int [] numbers = {10, 20, 30, 40, 50};
 
      for(int x : numbers ){
         System.out.print( x );
         System.out.print(",");
      }
      System.out.print("\n");
      String [] names ={"James", "Larry", "Tom", "Lacy"};
      for( String name : names ) {
         System.out.print( name );
         System.out.print(",");
      }
   }
}
```

This would produce the following result:

10,20,30,40,50,

James,Larry,Tom,Lacy,

**The break Keyword:**
----------------------

The *break* keyword is used to stop the entire loop. The break keyword must be
used inside any loop or a switch statement.

The break keyword will stop the execution of the innermost loop and start
executing the next line of code after the block.

### **Syntax:**

The syntax of a break is a single statement inside any loop:

```java
break;
```

### **Example:**

```java
public class Test {
 
   public static void main(String args[]) {
      int [] numbers = {10, 20, 30, 40, 50};
 
      for(int x : numbers ) {
         if( x == 30 ) {
              break;
         }
         System.out.print( x );
         System.out.print("\n");
      }
   }
}
```

This would produce the following result:

10

20

**The continue Keyword:**
-------------------------

The *continue* keyword can be used in any of the loop control structures. It
causes the loop to immediately jump to the next iteration of the loop.

-   In a for loop, the continue keyword causes flow of control to immediately
    jump to the update statement.

-   In a while loop or do/while loop, flow of control immediately jumps to the
    Boolean expression.

### **Syntax:**

The syntax of a continue is a single statement inside any loop:

```java
continue;
```

### **Example:**

```java
public class Test {
 
   public static void main(String args[]) {
      int [] numbers = {10, 20, 30, 40, 50};
 
      for(int x : numbers ) {
         if( x == 30 ) {
              continue;
         }
         System.out.print( x );
         System.out.print("\n");
      }
   }
}
```

This would produce the following result:

10

20

40

50
