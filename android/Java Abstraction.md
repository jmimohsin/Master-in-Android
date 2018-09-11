# Java Abstraction
 

Abstraction refers to the ability to make a class abstract in OOP. An abstract
class is one that cannot be instantiated. All other functionality of the class
still exists, and its fields, methods, and constructors are all accessed in the
same manner. You just cannot create an instance of the abstract class.

If a class is abstract and cannot be instantiated, the class does not have much
use unless it is subclass. This is typically how abstract classes come about
during the design phase. A parent class contains the common functionality of a
collection of child classes, but the parent class itself is too abstract to be
used on its own.

 

**Abstract Class:**
-------------------

 

Use the **abstract** keyword to declare a class abstract. The keyword appears in
the class declaration somewhere before the class keyword.

```java
/* File name : Employee.java */
public abstract class Employee
{
   private String name;
   private String address;
   private int number;
   public Employee(String name, String address, int number)
   {
      System.out.println("Constructing an Employee");
      this.name = name;
      this.address = address;
      this.number = number;
   }
   public double computePay()
   {
     System.out.println("Inside Employee computePay");
     return 0.0;
   }
   public void mailCheck()
   {
      System.out.println("Mailing a check to " + this.name
       + " " + this.address);
   }
   public String toString()
   {
      return name + " " + address + " " + number;
   }
   public String getName()
   {
      return name;
   }
   public String getAddress()
   {
      return address;
   }
   public void setAddress(String newAddress)
   {
      address = newAddress;
   }
   public int getNumber()
   {
     return number;
   }
}
```

Notice that nothing is different in this Employee class. The class is now
abstract, but it still has three fields, seven methods, and one constructor.

Now if you would try as follows:

```java
/* File name : AbstractDemo.java */
public class AbstractDemo
{
   public static void main(String [] args)
   {
      /* Following is not allowed and would raise error */
      Employee e = new Employee("George W.", "Houston, TX", 43);
 
      System.out.println("\n Call mailCheck using Employee reference--");
      e.mailCheck();
    }
}
```

When you would compile above class then you would get the following error:

Employee.java:46: Employee is abstract; cannot be instantiated

      Employee e = new Employee("George W.", "Houston, TX", 43);

                   \^

1 error

 

**Extending Abstract Class:**
-----------------------------

 

We can extend Employee class in normal way as follows:

```java
/* File name : Salary.java */
public class Salary extends Employee
{
   private double salary; //Annual salary
   public Salary(String name, String address, int number, double
      salary)
   {
       super(name, address, number);
       setSalary(salary);
   }
   public void mailCheck()
   {
       System.out.println("Within mailCheck of Salary class ");
       System.out.println("Mailing check to " + getName()
       + " with salary " + salary);
   }
   public double getSalary()
   {
       return salary;
   }
   public void setSalary(double newSalary)
   {
       if(newSalary >= 0.0)
       {
          salary = newSalary;
       }
   }
   public double computePay()
   {
      System.out.println("Computing salary pay for " + getName());
      return salary/52;
   }
}
```

Here, we cannot instantiate a new Employee, but if we instantiate a new Salary
object, the Salary object will inherit the three fields and seven methods from
Employee.

```java
* File name : AbstractDemo.java */
public class AbstractDemo
{
   public static void main(String [] args)
   {
      Salary s = new Salary("Mohd Mohtashim", "Ambehta, UP", 3, 3600.00);
      Employee e = new Salary("John Adams", "Boston, MA", 2, 2400.00);
 
      System.out.println("Call mailCheck using Salary reference --");
      s.mailCheck();
 
      System.out.println("\n Call mailCheck using Employee reference--");
      e.mailCheck();
    }
}
```

This would produce the following result:

Constructing an Employee

Constructing an Employee

Call mailCheck using  Salary reference --

Within mailCheck of Salary class

Mailing check to Mohd Mohtashim with salary 3600.0

 

Call mailCheck using Employee reference--

Within mailCheck of Salary class

Mailing check to John Adams with salary 2400.

 

### **Abstract Methods:**

 

If you want a class to contain a particular method but you want the actual
implementation of that method to be determined by child classes, you can declare
the method in the parent class as abstract.

The abstract keyword is also used to declare a method as abstract. An abstract
method consists of a method signature, but no method body.

Abstract method would have no definition, and its signature is followed by a
semicolon, not curly braces as follows:

```java
public abstract class Employee
{
   private String name;
   private String address;
   private int number;
  
   public abstract double computePay();
  
   //Remainder of class definition
}
```

Declaring a method as abstract has two results:

-   The class must also be declared abstract. If a class contains an abstract
    method, the class must be abstract as well.

-   Any child class must either override the abstract method or declare itself
    abstract.

A child class that inherits an abstract method must override it. If they do not,
they must be abstract and any of their children must override it.

Eventually, a descendant class has to implement the abstract method; otherwise,
you would have a hierarchy of abstract classes that cannot be instantiated.

If Salary is extending Employee class, then it is required to implement
computePay() method as follows:

```java
/* File name : Salary.java */
public class Salary extends Employee
{
   private double salary; // Annual salary
 
   public double computePay()
   {
      System.out.println("Computing salary pay for " + getName());
      return salary/52;
   }
 
   //Remainder of class definition
}
```
