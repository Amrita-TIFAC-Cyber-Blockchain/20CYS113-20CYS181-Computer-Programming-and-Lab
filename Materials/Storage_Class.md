# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/CP-20CYS113-blue)  ![](https://img.shields.io/badge/CPL-20CYS181-blue)
![](https://img.shields.io/badge/-HPOJ-brown) <br/>

## Storage Class

- auto (default)
- register
- static
- extern
- typedef

```
#include <stdio.h>

// Example using auto storage class
void autoExample() {
    auto int num = 10; // Same as int num = 10;
    printf("Auto variable: %d\n", num);
}

// Example using static storage class
void staticExample() {
    static int count = 0;
    count++;
    printf("Static variable: %d\n", count);
}

// Example using register storage class
void registerExample() {
    register int x = 5;
    printf("Register variable: %d\n", x);
}

// Example using extern storage class
extern int externVar; // Declaration of an external variable

void externExample() {
    printf("Extern variable: %d\n", externVar);
}

// Example using typedef storage class
typedef int ram; // Alias for int
typedef char guru; // Alias for int

void typedefExample() {
    ram number = 100;
	guru enter = 'y';
    printf("Typedef variable: %d\n", number);
	printf("Typedef variable: %c\n", enter);
}

// Definition of the external variable
int externVar = 50;

int main() {
    autoExample();
    staticExample();
	  staticExample();
	  staticExample();
    registerExample();
    externExample();
    typedefExample();

    return 0;
}
```
