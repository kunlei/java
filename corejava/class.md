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


