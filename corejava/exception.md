Java allows every method an alternative exit path if it is unable to complete its task in the normal way. In this situation, the method does not return a value. Instead, it throws an object that encapsulates the error information. Note that the method exits immediately; it does not return its normal (or any) value. Moreover, execution does not resume at the code that called the method; instead, the exception-handling mechanism begins its search for an exception handler that can deal with this particular error condition.

## The classification of exceptions
In Java, an exception object is always an instance of a class derived from **Throwable**. The exception hierarchy in Java:
0. Throwable
... 1. Error
... 2. Exception
...... 2.1 IOException
...... 2.2 Runtime Exception
