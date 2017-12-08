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












































