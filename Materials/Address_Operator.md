# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown) ![](https://img.shields.io/badge/Additional_Coverage-Code_Review-purple)  <br/>

## Address (&) Operator 

```
#include <stdio.h>
#include<string.h>

// Structure definition
struct Person {
    char name[50];
    int age;
};

// Union definition
union Data {
    int iValue;
    float fValue;
    char cValue;
};

// Enum definition
enum Color {
    RED,
    GREEN,
    BLUE
};

int main() {
    // Variable declarations
    int i = 24;
    float f = 3.14;
    char c = 'R';
    int arr[5] = {5, 10, 44, 18, 2};
    struct Person person;
    union Data data;
    enum Color color = BLUE;
    
    strncpy(person.name,"Ramaguru", 8);
    person.age = 33;

    // Printing variable addresses using the & operator
    printf("\nVariable Addresses using & and %%x\n");
    printf("Address of i (int): %x\n", &i);
    printf("Address of f (float): %x\n", &f);
    printf("Address of c (char): %x\n", &c);
    printf("Address of arr (array): %x\n", &arr);
    printf("Address of person (structure): %x\n", &person);
    printf("Address of data (union): %x\n", &data);
    printf("Address of color (enum): %x\n", &color);
    
     // Printing variable addresses using the & operator
    printf("Variable Addresses using & and %%p:\n");
    printf("Address of i (int): %p\n", &i);
    printf("Address of f (float): %p\n", &f);
    printf("Address of c (char): %p\n", &c);
    printf("Address of arr (array): %p\n", &arr);
    printf("Address of person (structure): %p\n", &person);
    printf("Address of data (union): %p\n", &data);
    printf("Address of color (enum): %p\n", &color);
    
    
    // Printing variable addresses
    printf("\nVariable User-defined variable Addresses\n");
    printf("Address of arr (array): %p\n", arr);
    return 0;
}
```
