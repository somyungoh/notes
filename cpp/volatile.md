# volatile.md

*"`volatile` instructs compiler that status is special variable so that no such optimization are allowed on this variable"*

</br>

### What's up with the compiler optimization then?
If we disassembly the following code (used [Compiler Explorer](https://godbolt.org/)):
```cpp
#define SUCCESS 1

int main()
{
    unsigned int status = 1;
    while (status == SUCCESS) {
        // loop loop
    }
    return 0;
}
```
`-O0` optimization enabled:
```assembly
main:                                   # @main
        push    rbp
        mov     rbp, rsp
        mov     dword ptr [rbp - 4], 0
        mov     dword ptr [rbp - 8], 1
.LBB0_1:                                # =>This Inner Loop Header: Depth=1
        jmp     .LBB0_1
```
`-O1` optimization enabled:
```assembly
main:                                   # @main
.LBB0_1:                                # =>This Inner Loop Header: Depth=1
        jmp     .LBB0_1
```
Here, as the variable `status` will never be used or modified other than the loop condition, the compiler can drop the data from the memory and store it in the temporary location. HOWEVER, imagine a code that is outside the scope of the compiler attempts to access the memory location of `status`, it will fail to access it since it is cleaned up by the compiler and no longer exists in the memory.

This is where we need the `volatile` qualifier so that compiler does not perform any optimization and keep it in the memory:
```cpp
volatile unsigned int status = 1;
```
Now when we go back to the assembly, even with `-O2` optimization enabled:
```assembly
main:                                   # @main
        mov     dword ptr [rsp - 4], 1
.LBB0_1:                                # =>This Inner Loop Header: Depth=1
        mov     eax, dword ptr [rsp - 4]
        cmp     eax, 1
        je      .LBB0_1
        xor     eax, eax
        ret
```
It's nicely protected from being eliminated by the compiler :)

</br>


### References:
- [GG: Volatile qualifier C Part 1: Introduction](https://www.geeksforgeeks.org/understanding-volatile-qualifier-c-set-1-introduction/)
- [GG: Volatile qualifier C Part 2: Examples](https://www.geeksforgeeks.org/understanding-volatile-qualifier-in-c/)

</br>
[Back to Home](./../README.md)
