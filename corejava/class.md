## Class and Object
Java comes with a cosmic superclass called **Object**. All other classes extend this class.

#### Relationships between classes
The most common relationships between classes are
1. dependence ("use-a")
2. aggregation ("has-a")
3. inheritance ("is-a")

### Object and object variables
Use **new** with constructor to construct a object:
```java
new Date()
String s = new Date().toString()
Date birthday = new Date();
```

The statement 
```java
Date deadline
```
defines an object variable that can refer to objects of type **Date**. It is important to realize that the variable deadline is not an objectt and, in fact, does not even refer to an object yet.

Note: an object variable doesn't actually contain an object. It only refers to an object. In Java, the value of any object variable is a reference to an object that is stored elsewhere. The return value of the **new** operator is also a reference.

Note: you can explicitly set an object variable to **null** to indicate that it currently refers to no object.
```java
deadline = null;
if (deadline != null) 
    System.out.println(deadline);
```

Note: One can think of Java object variables as analogous to object pointers in C++. For example,
```java
    Date birthday; //Java
```
is really the same as
```c++
Date* birthday; //C++
Date * birthday = new Date(); //C++
```
The equivalent of the Java **null** reference is the C++ **NULL** pointer.


Note:: all Java objects live on the heap. When an object contains another object variable, it contains just a pointer to yet another heap object. In Java, you must use the **clone** method to get a complete copy of an object.


### The LocalDate class of the Java Library
An instance of the **Date** class has a state, namely a particular point in time. The standard Java library contains two separate classes: the **Date** class, which represents a point in time, and the **LocalDate** class, which expresses days in the familiar calendar notation.

One do not use a constructor to construct objects of the **LocalDate** class. Instead, use static factory methods that call constructors on your behalf. The expression
```java
LocalDate.now()
```
constructs a new object that represents the date at which the object was constructed. Another example:
```java
LocalDate newYearsEve = LocalDate.of(1999, 12, 31);
int year = newYearsEve.getYear(); //1999
int month = newYearsEve.getMonthValue(); //12
int day = newYearsEve.getDayOfMonth(); //31

LocalDate aThousandDaysLater = newYearsEve.plusDays(1000);
```


## Classes
You can only have one public class in a source file, but you can't have any number of nonpublic classes.

Keep in mind that all Java objects are constructed on the heap and that a constructor must be combined with **new**. It is a common error of C++ programmers to forget the **new** operator:
```c++
Employee number007("James Bound", 10000, 1950, 1, 1); //C++, not Java
```
This works in C++, but not in Java.


## Final instance fields
One can define an instance field as **final**. Such a field must be initialized when the object is constructed. That is, one must guarantee that the field value has been set after the end of every constructor. Afterwards, the field may not be modified again.
```java
class Employee {
    private final String name;
}
```
The **final** modifier is particularly useful for fields whose type is primitive or an immutable class.
For mutable class, the **final** modifier can be confusing. For example, consider a field
```java
private final StringBuilder evaluations;
```
that is initialized in the Employee constructor as
```java
evaluations = new StringBuilder();
```
The final keyword merely means that the object reference stored in the evaluations variable will never again refer to a different StringBuilder object. But the object can be mutated:
```java
public void giveGoldStar() {
    evaluations.append(LocalDate.now() + ": Gold star!\n");
}
```


## Static fields and methods
### Static fields
If one defines a field as **static**, then there is only one such field per class. In contrast, each object has its own copy of all instance fields. For example, let's suppose we want to assign a unique identificiation number to each employee. Wee add an instance field id and a static field enxtId to the employee class:
```java
class Employee {
    private static int nextId = 1;

    private int id;
}
```

### static constants
Example:
```java
public class Math {
    public static final double PI = 3.1415;
}
```

### static methods
Static methods are methods that do not operate on objects.

### main methods
Every class can have a main method.


## Method Parameters
Java **always** uses call by value. That means that the method gets a copy of all parameter values. In particular, the methods cannot modify the contents of any paramter variables passed to it.

There are, however, two kinds of method parameters:
1. Primitive types (numbers, boolean values)
2. Object references
It is impossible for a method to change a primitive type parameter. The situation is different for object parameters. One can easily implement a method that triples the salary of an employee:
```java
public static void tripleSalary(Employee x) {
    x.raiseSalary(200);
}
```
Object references are passed by value.

Summary of what you can and cannot do with method parameters in Java:
1. A method cannot modify a parameter of a primitive type (that is, numbers of boolean values)
2. A method can change the state of an object parameter
3. A method cannot make an object parameter refer to a new object



## Overloading
The method name and its parameters are called the signature of the method.
Note: the return type is not part of the method signature. That is, you cannot have two methods with the same names and parameter types but different return types.


## Default field initialization
If you don't set a field explicitly in a constructor, it is automatically set to a default value: numbers to 0, boolean values to false, and object references to null.
Note: there is an important difference between fields and local variables. You must always explicitly initialize local variables in a method. But in a class, if you don't initialize a field, it is automatically initialized to a default (0, false or null).



## The constructor with no arguments
If you write a class with no constructors whatsoever, then a non-argument constructor is provided for you. This constructor sets all the instance fields to their default values. So, all numeric data contained in the instance fields would be 0, all boolean values would be false, and all object variables would be set to null.

If a class supplies at least one constructor but does not supply a no-argument constructor, it is illegal to construct objects without supplying arguments. 

Note: keep in mind that you get a free no-argument constructor **only** when your class has no other constructors. If you write your class with even a single constructor of your own and you want the users of your class to have the ability to create an instance by a call to
```java
new ClassName()
```
then you must provide a no-argument constructor. Of course, if you are happy with the default values for all fields, you can simply supply
```java
public ClassName {

}
```

## Explicit field initialization
One can simply assign a value to any field in the class definition. For example,
```java
class Employee {
    private String name = "";
}
```
This assignment is carried out before the constructor executes. The initialization value doesn't have to be a constant value. For example:
```java
class Employee {
    private static int nextId;
    private int id = assignId();

    private static int assignId() {
        int r = nextId;
        nextId++;
        return r;
    }
}
```


## Calling another constructor
The keyword **this** refers to the implicit parameter of a method. However, this keyword has a second meaning.
If the first statement of a constructor has the form this(...), then the constructor calls another constructor of the same class. Here is a typical example:
```java
pulic Employee(double s) {
    this("Employee #" + nextId, s);
    nextId;
}
```
Note: in C++, it is not possible for one constructor to call another.

## Initialization blocks
There are three ways to initialize a data field:
1. by setting a value in a constructor
2. by assigning a value in the declaration
3. by using an initialization block.

In the thrid method, class declarations can contain arbitrary blocks of code. These blocks are executed whenever an object of that class is constructed. For example:
```java
class Employee {
    private static int nextId;

    private int id;
    private String name;
    private double salary;

    //object initialization block
    {
        id = nextId;
        nextId++;
    }

    public Employee(String n, double s) {
        name = n;
        salary = s;
    }

    pulic Employee() {
        name = "";
        salary = 0;
    }
}
```
In this example, the id field is initialized in the object initialization block, no matter which constructor is used to construct an object. The initialization block runs first, and then the body of the constructor is executed.


Detailed steps when a constructor is called:
1. All data fields are initialized to their default values (0, false, or null).
2. All field initializers and initliazaiton blocks are executed, in the order in which they occur in the class declaration.
3. If the first line of the constructor calls a second constructor, then the body of the second constructor is executed.
4. The body of the constructor is executed.


To initialize a static field, either supply an initial value or use a static initialization block. In the first mechanism:
```java
private static int nextId = 1;
```
If the static fields of your class require complex initialization code, use a static initialization block. Place the code inside a block and tag it with the keyword static. For example
```java
static {
    Random generator = new Random();
    nextId = generator.nextInt(10000);
}
```
Static initialization occurs when the class is first loaded. Like instance fields, static fields are 0, false, or null unless you explicitly set them to another value.












































