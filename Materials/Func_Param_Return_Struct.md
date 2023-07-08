# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/CP-20CYS113-blue)  ![](https://img.shields.io/badge/CPL-20CYS181-blue)
![](https://img.shields.io/badge/-HPOJ-brown) <br/>

## Function - Param as Struct and Returns Struct

### Example 1

```
#include <stdio.h>
#include <string.h>

// Define a structure
struct Student {
    char name[50];
    int age;
    float gpa;
};

// Function that returns a structure
struct Student createStudent(const char* name, int age, float gpa) {
    struct Student s;
    strcpy(s.name, name);
    s.age = age;
    s.gpa = gpa;
    return s;
}

// Function that displays a student's information
void displayStudent(struct Student s) {
    printf("Name: %s\n", s.name);
    printf("Age: %d\n", s.age);
    printf("GPA: %.2f\n", s.gpa);
}

int main() {
    // Call the function and store the returned structure
    struct Student s1 = createStudent("Ramaguru R", 18, 8.61);

    // Display the student's information
    displayStudent(s1);

    return 0;
}
```

### Example 2

```
#include <stdio.h>

// Define a structure
struct Circle {
    float radius;
    float diameter;
    float circumference;
    float area;
};

// Function that returns a structure
struct Circle calculateCircle(float radius) {
    struct Circle c;
    c.radius = radius;
    c.diameter = 2 * radius;
    c.circumference = 2 * 3.14159 * radius;
    c.area = 3.14159 * radius * radius;
    return c;
}

// Function that displays circle information
void displayCircle(struct Circle c) {
    printf("Radius: %.2f\n", c.radius);
    printf("Diameter: %.2f\n", c.diameter);
    printf("Circumference: %.2f\n", c.circumference);
    printf("Area: %.2f\n", c.area);
}

int main() {
    // Call the function and store the returned structure
    struct Circle c1 = calculateCircle(5.0);

    // Display the circle information
    displayCircle(c1);

    return 0;
}

```
