# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown) ![](https://img.shields.io/badge/Additional_Coverage-Code_Review-purple)  <br/>

## Format Specifiers
```
#include <stdio.h>

int main() {
    // Variable declarations
    int num = 42;
    double pi = 3.14159;
    char letter = 'A';

    // Printing integer with %d placeholder
    printf("Integer: %d\n", num);

    // Printing integer in octal format with %o placeholder
    printf("Octal: %o\n", num);

    // Printing integer in hexadecimal format with %x placeholder
    printf("Hexadecimal: %x\n", num);

    // Printing double with %f placeholder
    printf("Floating-point: %f\n", pi);

    // Printing double in exponential format with %e placeholder
    printf("Exponential: %e\n", pi);

    // Printing character with %c placeholder
    printf("Character: %c\n", letter);

    // Printing string with %s placeholder
    printf("String: %s\n", "Hello World");

    // Additional variable declarations
    long int largeNum = 1234567890;
    long long int hugeNum = 987654321098765432LL;
    short int shortHex = 0x1A;
    unsigned short int ushortNum = 65535;
    unsigned long int ulongNum = 4294967295UL;
    unsigned long long int ullongNum = 18446744073709551615ULL;
    size_t sizeValue = sizeof(int);

    // Printing long int with %ld placeholder
    printf("Long int: %ld\n", largeNum);

    // Printing long long int with %lld placeholder
    printf("Long long int: %lld\n", hugeNum);

    // Printing short int in hexadecimal format with %hx placeholder
    printf("Short int in Hex: %hx\n", shortHex);

    // Printing unsigned short int with %hu placeholder
    printf("Unsigned short int: %hu\n", ushortNum);

    // Printing unsigned long int with %lu placeholder
    printf("Unsigned long int: %lu\n", ulongNum);

    // Printing unsigned long long int with %llu placeholder
    printf("Unsigned long long int: %llu\n", ullongNum);

    // Printing size_t with %zd placeholder
    printf("Size_t: %zd\n", sizeValue);

    // Additional variable declarations
    long double bigPi = 3.14159265358979323846L;
    char character = 'B';
    int asciiValue = character;

    // Printing double with %lf placeholder
    printf("Double: %lf\n", pi);

    // Printing long double with %Lf placeholder
    printf("Long Double: %Lf\n", bigPi);

    // Printing character with %c placeholder
    printf("Character: %c\n", character);

    // Printing ASCII value of character with %d placeholder
    printf("ASCII value of Character: %d\n", asciiValue);

    // Pointer declaration and initialization
    int* ptr = &num;

    // Printing pointer address with %p placeholder
    printf("Pointer Address: %p\n", (void*)ptr);
	
	// Printing pointer address in hexadecimal format with %x placeholder
    printf("Pointer Address: %x\n", (void*)ptr);

    return 0;
}
```
