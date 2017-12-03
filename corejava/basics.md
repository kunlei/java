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


