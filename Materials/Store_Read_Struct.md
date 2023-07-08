# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/CP-20CYS113-blue)  ![](https://img.shields.io/badge/CPL-20CYS181-blue)
![](https://img.shields.io/badge/-HPOJ-brown) <br/>

## Storing and Reading Structure to a file

## Store Structure to a file

```
#include <stdio.h>
#include <string.h>

// Define a structure
struct Person {
    char name[50];
    int age;
};

int main() {
    // Create a structure variable
    struct Person person;
    strcpy(person.name, "Ramaguru R");
    person.age = 33;

    // Open the file in binary mode for writing
    FILE* file = fopen("structure.bin", "wb");
    if (file != NULL) {
        // Write the structure variable to the file
        fwrite(&person, sizeof(struct Person), 1, file);
        fclose(file);
        printf("Structure variable stored in file successfully.\n");
    } else {
        printf("Failed to open the file.\n");
    }

    return 0;
}
```

### Read Structure from a file

```
#include <stdio.h>
#include <string.h>

// Define a structure
struct Person {
    char name[50];
    int age;
};

int main() {
    // Create a structure variable
    struct Person person;

    // Open the file in binary mode for reading
    FILE* file = fopen("structure.bin", "rb");
    if (file != NULL) {
        // Read the structure variable from the file
        fread(&person, sizeof(struct Person), 1, file);
        fclose(file);

        // Display the read data
        printf("Name: %s\n", person.name);
        printf("Age: %d\n", person.age);
    } else {
        printf("Failed to open the file.\n");
    }

    return 0;
}
```
