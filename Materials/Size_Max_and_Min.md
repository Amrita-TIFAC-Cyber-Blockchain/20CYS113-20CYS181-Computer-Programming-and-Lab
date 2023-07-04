# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown) ![](https://img.shields.io/badge/Additional_Coverage-Code_Review-purple)  <br/>

## Limits 

<limits.h>
- INT_MAX: Maximum value for int
- INT_MIN: Minimum value for int
- UINT_MAX: Maximum value for unsigned int
- LONG_MAX: Maximum value for long
- LONG_MIN: Minimum value for long
- ULONG_MAX: Maximum value for unsigned long
- LLONG_MAX: Maximum value for long long
- LLONG_MIN: Minimum value for long long
- ULLONG_MAX: Maximum value for unsigned long long

<float.h>
- DBL_MAX: Maximum finite value representable by a double.
- DBL_MIN: Smallest positive normalized value representable by a double.

## Example 

```
#include <stdio.h>
#include <limits.h>
#include <float.h>

int main() {
    printf("Size of int: %zu bytes\n", sizeof(int));
    printf("Range of int: %d to %d\n", INT_MIN, INT_MAX);

    printf("Size of unsigned int: %zu bytes\n", sizeof(unsigned int));
    printf("Range of unsigned int: 0 to %u\n", UINT_MAX);

    printf("Size of long: %zu bytes\n", sizeof(long));
    printf("Range of long: %ld to %ld\n", LONG_MIN, LONG_MAX);

    printf("Size of unsigned long: %zu bytes\n", sizeof(unsigned long));
    printf("Range of unsigned long: 0 to %lu\n", ULONG_MAX);

    printf("Size of long long: %zu bytes\n", sizeof(long long));
    printf("Range of long long: %lld to %lld\n", LLONG_MIN, LLONG_MAX);

    printf("Size of unsigned long long: %zu bytes\n", sizeof(unsigned long long));
    printf("Range of unsigned long long: 0 to %llu\n", ULLONG_MAX);

    printf("Size of double: %zu bytes\n", sizeof(double));
    printf("Range of double: %e to %e\n", DBL_MIN, DBL_MAX);

    return 0;
}

```
