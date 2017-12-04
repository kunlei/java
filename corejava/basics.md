## Notations
In Java, all the functions must be inside a class and are called methods, while in C++, they are called member functions.


## Data Types
Java has eight **primitive types**: four integer types, two floating-number types, one character type **char** and one **boolean** type.

### integer types
1. int: 4 bytes - -2,147,483,648 to 2,417,483,648
2. short: 2 bytes - -32,768 to 32,767
3. long: 8 bytes - -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807
4. byte: 1 byte - -128 to 127
Note: Java does not have any unsigned versions of the int, long, short, byte types.


### floating-point types
1. float: 4 bytes - approximately +-3.40282347E+38F
2. double: 8 bytes - approximately +-1.79769313486231570E+308
Note: numbers of type float have a suffix F or f (for example, 3.14F).


### boolean type
The boolean type has two values, false and true.
Note: you cannnot convert between integers and boolean values.
Note: in C++, numbers and even pointers can be used in place of boolean values. The value 0 is equivalent to the bool value false, and a nonzero value is equivalent to true. This is **not** the case in Java.

### constants
In Java, one use the keyword **final** to denote a constant.


## Operators
The usual arithmetic operators +, -, \*, / are used in Java for addition, subtraction, multiplication, and division.

Note: the / operator denotes integer division if both arguments are integers, and floating-point division otherwise. Integer remainder (sometimes called modulus) is denoted by %. For example, 15 / 2 is 7, 15 % 2 is 1, and 15.0 / 2 is 7.5.

Note: integer devision by 0 raises an exception, whearas floating-point division by 0 yields an infinite or NaN result.

### mathematical functions and constants
Use **Math** class for mathematical functions. For example
```java
double x = 4;
x = Math.sqrt(x);
System.out.println(x);

double a = 2;
double y = Math.pow(x, a);
```
Some math functions in class **Math**:
```java
Math.sin
Math.cos
Math.tan
Math.atan
Math.atan2

Math.exp
Math.log
Math.log10

Math.PI
Math.E
```

### conversions between numeric types
When two values are combined with a binary operator, follow the below rules
1. if either of the operands is of type **double**, the other one will be converted to a **double**
2. otherwise, if either of the operands is of type **float**, the other one will be converted to a **float**
3. otherwise, if either of the operands is of type **long**, the other one will be converted to a **long**
4. otherwise, both operands will be converted to an **int**



### casts
Use **cast** to do conversions in which loss of information is possible, for example
```java
double x = 9.997;
int nx = (int) x;
```

Use **Math.round** method if wants to round a floating-point number to the nearest integer, for example
```java
double x = 9.997;
int nx = (int) Math.round(x);
```

Note: you cannot cast between **boolean** values and any numeric type.

### relational and boolean operators
Use == to test for equility, use != for inequility.
Use && for logical **and**, and || for logical **or**.


### enumerated types
```java
enum Size {SMALL, MEDIUM, LARGE, EXTRA\_LARGE};
Size s = Size.MEDIUM;
```

## Strings
Java does not have a built-in string type. Instead, the standard Java library contains a predefined class called String. Each quoted string is an instance of the String class:
```java
String e = ""; //empty string
String greeting = "Hello";
```


### substrings
A substring can be extracted from a larger string using the **substring** method of the **String** class:
```java
String greeting = "Hello";
String s = greeting.substring(0, 3); \\s = "Hel"
```



### concatenation
Java allows you to use + to join two strings:
```java
String expletive = "Expletive";
String PG13 = "deleted";
String message = expletive + PG13;
```

Note: every Java object can be converted to a string.
```java
int age = 13;
String rating = "PG" + age;
```

### strings are immutable


### testing strings for equality
Use **equals** method to test whether two strings are equal.
```java
s.equals(t);
"Hello".equals(greeting);
"Hello".equalsIgnoreCase("hello");
```
Note: do not use the == operator to test whether two strings are equal. It only determines whether or not the strings are stored in the same location. 


### empty and null strings
To test whether a string is empty: 
```java
if (str.length() == 0)
if (str.equals(""))
```

To test whether a string is null:
```java
if (str == null)
```

To test that a string is neither null nor empty, use:
```java
if (str != null && str.length() != 0)
```
Note: you need to test that str is not null first.



### building strings
To build a string from many small pieces, use **StringBuilder**:
```java
StringBuilder builder = new StringBuilder();
builder.append(ch); //append a single character
builder.append(str); //append a string
String completedSTring = builder.toString();
```












































































