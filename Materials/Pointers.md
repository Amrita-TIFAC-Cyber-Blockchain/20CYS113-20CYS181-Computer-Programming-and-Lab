# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown) ![](https://img.shields.io/badge/Additional_Coverage-Code_Review-purple)  <br/>

## Pointers

```
#include <stdio.h>
#include <string.h>

// Structure definition
struct Person {
    char name[10];
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
    
    strcpy(person.name, "Ramaguru");
    person.age = 33;
    
    data.iValue = 72;

    // Printing variable addresses using the & operator and %p
    printf("\nVariable Addresses using & and %%p:\n");
    printf("Address of i (int): %p\n", &i);
    printf("Address of f (float): %p\n", &f);
    printf("Address of c (char): %p\n", &c);
    printf("Address of arr (array): %p\n", arr);
    printf("Address of person (structure): %p\n", &person);
    printf("Address of data (union): %p\n", &data);
    printf("Address of color (enum): %p\n", &color);

    // Printing variable values using pointers
    printf("\nVariable Values using pointers:\n");
    printf("Value of i (int): %d\n", *(&i));
    printf("Value of f (float): %.2f\n", *(&f));
    printf("Value of c (char): %c\n", *(&c));
    printf("Value of arr[0] (array): %d\n", *(arr));
    printf("Value of person.name (structure): %s\n", person.name);
    printf("Value of person.age (structure): %d\n", person.age);
    printf("Value of data.iValue (union): %d\n", data.iValue);
    printf("Value of color (enum): %d\n", color);

    return 0;
}
```
