## classes, Superclasses, and Subclasses


### defining subclasses
The example below shows how one defines a `Manager` class that inherits from the `Employee` class. Use **extends** to denote inheritance:
```java
public class Manager extends Employee {
    private double bonus;
    ...
    public void setBonus(double bonus) {
        this.bonus = bonus;
    }
}


Manager boss = ...;
boss.setBonus(5000);
```
Note: All inheritance in Java is public inheritance; there is no analog to the C++ features of private and protected inehritance.





### overriding methods
Some of the superclass methods are not appropriate for the `Manager` subclass. In particular, the `getSalary` method should return the sum of the base salary and the bonus. One need to supply a new method to override the superclass method:
```java
public class Manager extends Employee {
    ...
    public double getSalary() {
        return salary + bonus; //won't work
    }

    public double getSalary() {
        double baseSalary = super.getSalary();
        return baseSalary + bonus;
    }
}
```
Note: the subclass cannot directly call the `salary` field since it is declared as `private` in the superclass and only the `Employee` methods have direct access to the private fields of the `Employee` class. This means that the `getSalary` method of the `Manager` class cannot directly access the `salary` field.
Note: **super** is not a reference to an object. For example, you cannot assign the value **super** to another object variable. Instead, **super** is a special keyword that directs the compiler to invoke the superclass method.







### subclass constructors
A subclass constructor looks like this:
```java
public Manager(String name, double salary, int year, int month, int day) {
    super(name, salary, year, month, day);
    bonus = 0;
}
```
Since the `Manager` constructor cannot access the private fields of the `Employee` class, it must initialize them through a constructor. The call using `super` must be the first statement in the constructor for the subclass.

Note: if the subclass constructor does not call a superclass constructor explicitly, the no-argument constructor of the superclass is invoked. If the superclass does not have a no-argument constructor and the subclass constructor does not call another superclass constructor explicitly, the Java compiler reports an error.


An example:
```java
Manager boss = new Manager("Carl Cracker", 80000, 1987, 12, 15);
boss.setBonus(5000);

Employee[] staff = new Employee[3];
staff[0] = boss;
staff[1] = new Employee("Harry Hacker", 50000, 1989, 10, 1);
staff[2] = new Employee("Tony Tester", 40000, 1990, 3, 15);

for (Employee e : staff) {
    System.out.println(e.getName() + " " + e.getSalary());
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




### Abstract class
A class with one or more abstract methods must iteself be declared abstract.
```java
public abstract class Person {A
    private String name;
    
    public Person (String name) {
        this.name = name;
    }

    public abstract String getDescription();

    public String getName() {
        return name;
    }
}
```
In addition to abstract methods, abstract classes can have fields and concrete methods. See above example.

When one extends an abstract class, there are two choices: one can leave some or all of the abstract methods undefined, then one must tag the subclass as abstract as well. Or one can define all methods, and the subclass is no longer abstract.

A class can even be declared as `abstract` though it has no abstract methods.

Abstract classes cannot be instantiated.

Note that one can still create object variables of an abstract class, but such a varaible must refer to an object of a nonabstract subclass. For example
```java
Person p = new Student("Vince Wu", "Economics");
```
Here `p` is a variable of the abstract type `Person` that refers to an instance of the nonabstract subclass `Student`.


### Protected classes
Summary of the four access modifiers in Java that controls visibility:
1. Visible to the class only (private).
2. Visible to the world (public).
3. Visible to the package and all subclasses (protected).
4. Visible to the package - the (unfortunate) default. No modifiers are needed.







## Object: the cosmic superclass
The `Object` class is the ultimate ancestor - every class in Java extends `Object`. You can use a variable of type `Object` to refer to objects of any type:
```java
Object obj = new Employee("Harry Hacker", 35000);
```
Of course, a variable of `Object` is only useful as a generic holder for arbitrary values. To do anything specific with the value, you need to have some knowledge about the original type and apply a cast:
```java
Employee e = (Employee) obj;
```
In Java, only the values of primitive types (numbers, characters, and boolean values) are not objects.

All array types, no matter whether they are arrays of objects or arrays of primitive types, are class types that extend the `Object` class.
```java
Employee[] staff = new Employee[10];
obj = staff; //ok
obj = new int[10]; //ok
```
### The `equals` method
The `equals` method in the `Object` class tests whether one object is considered equal to another.
```java
public class Employee {
    ...
    public boolean equals (Object otherObject) {

        //a quick test to see if the objects are idential
        if (this == otherObject) return true;

        //must return false if the explicit parameter is null
        if (otherObject == null) return false;

        //if the classes don't match, they can't be equal
        if (getClass() != otherObject.getClass())  return false;

        //test whether the fields have identical values
        return name.equals(other.name) && 
            salary == other.salary &&
            hireDay.equals(other.hireDay);
    }
}
```





