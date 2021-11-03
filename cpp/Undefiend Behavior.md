# Undefiend Behavior

*"Undefined behavior is the name of a list of conditions that the program must not meet."*  

</br>

### Definition

[Apple]()
> Undefined behavior describes the result of any operation with unspecified semantics, such as dividing by zero, loading memory from a misaligned pointer, or dereferencing a null pointer.

[Wikipedia](https://en.wikipedia.org/wiki/Undefined_behavior)
> Undefined behavior (UB) is the result of executing a program whose behavior is prescribed to be unpredictable, in the language specification to which the computer code adheres.

Undefined Behaviors may have benefits in a certain optimizations, but it's very less and runtime should assume that there are no undefined behaviors happening.

</br>

### C++ Examples

1. Divide by zero  
    ```cpp
    int x = 1;
    return x / 0; // undefined behavior
    ```
2. Integer overflow
    ```cpp
    int x = INT_MAX;
    x += 1; // Integer overflow here
   ```

3. Attempt to modify [string literals](https://en.wikipedia.org/wiki/String_literal)
    ```cpp
    char *p = "wikipedia"; // valid C, deprecated in C++98/C++03, ill-formed as of C++11
    p[0] = 'W'; // undefined behavior
    ```

4. Wrong pointer operations
    ```cpp
    int arr[4] = {0, 1, 2, 3};
    int *p = arr + 5;  // undefined behavior for indexing out of bounds

    p = 0;
    int a = *p;        // undefined behavior for dereferencing a null pointer
    ```

5. Access to return-value funtion without a return
    ```cpp
    int f()
    {
    }  /* undefined behavior if the value of the function call is used*/
    ```
    
[Back to Home](../README.md)
