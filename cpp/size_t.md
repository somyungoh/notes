# size_t

### Definition
from [GeeksForGeeks](https://www.geeksforgeeks.org/size_t-data-type-c-language/):
> `size_t` is an `unsigned integral data type` which is defined in various header files such as:  
<stddef.h>, <stdio.h>, <stdlib.h>, <string.h>, <time.h>, <wchar.h>  
It’s a type which is used to *represent the size of objects in bytes* and is therefore used as the return type by the `sizeof` operator.

</br>

Okay, then why `size_t` instead of `unsigned int` (or any unsigned integral)?

> It is guaranteed to be big enough to contain the size of the biggest object the host system can handle.

This means that maximum size that compiler can represent can vary. More precisely, it will exactly map like this:
```cpp
#ifdef (X32_COMPILER)
    typedef size_t unsigned int         // 32-bit
#elif (X64_COMPILER)
    typedef size_t unsigned long long   // 64-bit
#enif
```

</br>

### `size_t` in the for loop?:
I've seen many codes using size_t in the for loop without knowing why:
```cpp
for (size_t i = SIZE_MAX; i >= 0; i--)
...
```
In turns out to be that simply being able to handle more non-negitive integers so the range of loop is safe enough. HOWEVER, [this](https://www.quora.com/Why-do-some-C-programs-use-size_t-instead-of-int-What-are-the-advantages) Q&A warns about simply thinking `unsinged` as "non-negative" and use it in the corresponding context. It can easily violate the intention of the implementation, already can see in the example above. Can you spot the issue?

[Back to Home](./../README.md)
