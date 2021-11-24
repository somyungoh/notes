# Reading Aseembly Launguages

This is following [Jason Turner's C++ Weekly series](https://www.youtube.com/channel/UCxHAlbZQNFU2LgEtiqd2Maw).

*Note* we will use clang compiler, intel x86 assembly syntax:
```assembly
mov     dest, source
```

</br>

## Part1.
```cpp
int main()
{
}
```
`-O0` optimization enabled:
```assembly
main:                       # @main
        push    rbp
        mov     rbp, rsp
        mov     eax, 0
        pop     rbp
        ret
```
- `push/pop` - Stack management. As we have entered a new function, compiler performs a stack management
- `ret` - end and return from the function `main()`
- `mov eax 0` - store the return value 0 in the register `eax`. This is how return values are handled in intel x84 architectures.

`-O1` optimization enabled:
```
main:                       # @main
        xor     eax, eax
        ret
```
- Now that compiler knows that main is the only function in the program, it removed the stack management.
- `xor A, B` - this can be interpreted as "do `xor(A,B)` and store the result in register `A`" which in this case results in `eax` 0. Why is this faster than `mov A, 0`? It's because the instruction size of `xor` is smaller than `mov` which results in a faster computation.

</br>

## x86 General Purpose Registers (GPR)
The 8 GPRs are as follows:
- `Accumulator register (AX)`. Used in arithmetic operations
- `Counter register (CX)`. Used in shift/rotate instructions and loops.
- `Data register (DX)`. Used in arithmetic operations and I/O operations.
- `Base register (BX)`. Used as a pointer to data (located in segment register DS, when in segmented mode).
- `Stack Pointer register (SP)`. Pointer to the top of the stack.
- `Stack Base Pointer register (BP)`. Used to point to the base of the stack.
- `Source Index register (SI)`. Used as a pointer to a source in stream operations.
- `Destination Index register (DI)`. Used as a pointer to a destination in stream operations.

And the full naming convension depends on the number of bits. For example,
- 16-bit: `ax`
- 32-bit: `eax`
- 64-bit: `rax`

</br>

### References
- [Wikibooks](https://en.wikibooks.org/wiki/X86_Assembly/X86_Architecture)

</br>

[Back to Home](./../README.md)
