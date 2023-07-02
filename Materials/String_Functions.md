# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown) ![](https://img.shields.io/badge/Additional_Coverage-Code_Review-purple)  <br/>

## String Functions

```
#include <stdio.h>
#include <string.h>

int main() {
    // Example string
    char str1[20] = "Hello, 22CYS!";
    char str2[20];
    char str3[20] = "Bye";

    // 1. strlen - Calculates the length of a string
    size_t len = strlen(str1);
    printf("Length of str1: %zu\n", len);

    // 2. strcpy - Copies a string from one location to another
    strcpy(str2, str1);
    printf("Copied string: %s\n", str2);

    // 3. strncpy - Copies a certain number of characters from one string to another
    strncpy(str3, str1, 5);
    printf("Copied substring: %s\n", str3);

    // 4. strcat - Concatenates two strings
    strcat(str1, " Goodbye!");
    printf("Concatenated string: %s\n", str1);

    // 5. strncat - Concatenates a certain number of characters from one string to another
    strncat(str2, " Welcome!", 8);
    printf("Concatenated substring: %s\n", str2);

    // 6. strcmp - Compares two strings lexicographically
    int cmp = strcmp(str1, "Hello, 21CYS");
    printf("Comparison result: %d\n", cmp);

    // 7. strncmp - Compares a certain number of characters of two strings lexicographically
    int ncmp = strncmp(str1, str2, 10);
    printf("Comparison result (limited): %d\n", ncmp);

    // 8. strchr - Searches for the first occurrence of a character in a string
    char *ptr = strchr(str1, 'W2');
    printf("Character found at position: %ld\n", ptr - str1);

    // 9. strstr - Searches for the first occurrence of a substring within a string
    char *sub = strstr(str1, "Good");
    printf("Substring found at position: %ld\n", sub - str1);

    return 0;
}

```
