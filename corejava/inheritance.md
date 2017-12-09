## classes, Superclasses, and Subclasses
### defining subclasses
Use **extends** to denote inheritance:
```java
public class Manager extends Employee {
}
```
Note: All inheritance in Java is public inheritance; there is no analog to the C++ features of private and protected inehritance.

### overriding methods
Class Manager also has a getSalary() method that overrides the Employee method:
```java
public class Manager extends Employee {
    ...
    public double getSalary() {
        double baseSalary = super.getSalary();
        return baseSalary + bonus;
    }
}
```
Note: **super** is not a reference to an object. For example, you cannot assign the value **super** to another object variable. Instead, **super** is a special keyword that directs the compiler to invoke the superclass method.



### subclass constructors
A subclass constructor looks like this:
```java
public Manager(String name, double salary, int year, int month, int day) {
    super(name, salary, year, month, day);
    bonus = 0;
}
```

The fact that an object variable (such as the variable e) can refer to multiple actual types is called polymorphism. Automatically selecting the appropriate method at runtime is called **dynamic binding**.
Note: in C++, you need to declare a member function as **virtual** if you want dynamic binding. In Java, dynamic binding is the default behavior; if you do not want a method to be virtual, you tag it as **final**.

Note: In C++, a class can have multiple superclasses. Java does not support multiple inheritance.

In Java, you can assign a subclass object to a superclass variable.
```java
Employee e;
e = new Employee(...); 
e = new Manager(...);
```
In Java, object variables are polymorphic. A variable of type Employee can refer to an object of type Employee or to an object of any subclass of the Employee class. However, one cannot assign a superclass reference to a subclass variable. 

### preventing inheritance
Use **final** to prevent someone from forming a subclass.
```java
public final class Executive extends Manager {
}
```
You can also make a specific method in a class final. If you do this, then no subclass can override that method.
Note: all methods in a final class are automatically final.
```java
public class Employee {

    public final String getName() {
    }
}
```

Note: recall that fields can also be declared as final. A final field cannot be changed after the object has been constructed. However, if a class is declared as final, only the methods, not the fields, are automatically final.

