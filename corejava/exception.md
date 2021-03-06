Java allows every method an alternative exit path if it is unable to complete its task in the normal way. In this situation, the method does not return a value. Instead, it throws an object that encapsulates the error information. Note that the method exits immediately; it does not return its normal (or any) value. Moreover, execution does not resume at the code that called the method; instead, the exception-handling mechanism begins its search for an exception handler that can deal with this particular error condition.

## The classification of exceptions
In Java, an exception object is always an instance of a class derived from **Throwable**. The exception hierarchy in Java:
```
*. Throwable
1. Error
2. Exception
   2.1 IOException
   2.2 Runtime Exception
```

The `Error` hierarchy describes internal errors and resource exhaustion situations inside the Java runtime system. You should not throw an object of this type. There is little you can do if such an internal error occurs, beyond notifying the user and trying to terminate the program gracefully. These situation are quite rare.


When doing Java programming, focus on the `Exception` hierarchy. The `Exception` hierarchy also splits into two branches: exceptions that derive from `RuntimeException` and those that do not. The general rule is this: A `RuntimeException` happens because you made a programming error. Any other exception occurs because a bad thing, such as an I/O error, happened to your otherwise good program.


Exceptions that inherit from `RuntimeException` include such problems as
* A bad cast
* An out-of-bounds array access
* A null pointer access


Exceptions that do not inherit from `RuntimeException` include
* Trying to read past the end of a file
* Trying to open a file that doesn't exist
* Trying to find a `Class` object for a string that does not denote an existing class


The rule "If it is a `RuntimeException`, it was your fault" works pretty well.


Java calls any exception that derives from the class `Error` or the class `RuntimeException` an `unchecked` exception. All other exceptions are called `checked` exceptions. The compiler checks that you provide exception handlers for all checked exceptions.


In summary, a method must declare all the checked exceptions that it might throw. Unchecked exceptions are either beyond your control (Error) or result from conditions that you should not have allowed in the first place (RuntimeException). If your methods fails to faithfully declare all checked exceptions, the compiler will issue an error message. Of course, instead of declaring the exception, you can also catch it. Then the exception won't be thrown out of the method, and no `throws` specifications is necessary. 



### creating exception classes
To create new exception classes, just derive it from `Exception`, or from a child class of `Exception` such as `IOException`. It is customary to give both a default constructor and a constructor that contains a detailed message. For example:
```java
class FileFormatException extends IOException {
    public FileFormatException() {}
    public FileFormatException(String gripe) {
        super(gripe);
    }
}
```
Now you are ready to throw your very own exception type.
```java
String readData(BufferedReader in) throws FileFormatException {
    ...
    while (...)
        if (ch == -1) {
            if (n < len) {
                throw new FileFormatException();
            }
        }
        ...
    }
}
```


Note: if you are writing a method that overrides a superclass method which throws no exceptons, then you must catch each checked exception in the method's code. You are not allowed to add more throws specifiers to a subclass method than are present in the superclass method.




