# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown) ![](https://img.shields.io/badge/Additional_Coverage-Code_Review-purple)  <br/>

## Overflow and Underflow

### char 
```
char overflow = 127;   // Maximum value for a char
char underflow = -128;  // Minimum value for a char

overflow++;  // Overflow: Value wraps around to -128
underflow--; // Underflow: Value wraps around to 127
```

### unsigned char
```
unsigned char overflow = 255; // Maximum value for an unsigned char
unsigned char underflow = 0;  // Minimum value for an unsigned char

overflow++;  // Overflow: Value wraps around to 0
underflow--; // Underflow: Value wraps around to 255
```

### short
```
short overflow = 32767;     // Maximum value for a short
short underflow = -32768;   // Minimum value for a short

overflow++;  // Overflow: Value wraps around to -32768
underflow--; // Underflow: Value wraps around to 32767
```

### unsigned short
```
unsigned short overflow = 65535; // Maximum value for an unsigned short
unsigned short underflow = 0;    // Minimum value for an unsigned short

overflow++;  // Overflow: Value wraps around to 0
underflow--; // Underflow: Value wraps around to 65535
```

### int
```
int overflow = 2147483647;   // Maximum value for an int
int underflow = -2147483648; // Minimum value for an int

overflow++;  // Overflow: Value wraps around to -2147483648
underflow--; // Underflow: Value wraps around to 2147483647
```

#### unsigned int
```
unsigned int overflow = 4294967295; // Maximum value for an unsigned int
unsigned int underflow = 0;         // Minimum value for an unsigned int

overflow++;  // Overflow: Value wraps around to 0
underflow--; // Underflow: Value wraps around to 4294967295
```

### long 
```
long overflow = 9223372036854775807;     // Maximum value for a long
long underflow = -9223372036854775808;   // Minimum value for a long

overflow++;  // Overflow: Value wraps around to -9223372036854775808
underflow--; // Underflow: Value wraps around to 9223372036854775807
```

### unsigned long
```
unsigned long overflow = 18446744073709551615; // Maximum value for an unsigned long
unsigned long underflow = 0;                    // Minimum value for an unsigned long

overflow++;  // Overflow: Value wraps around to 0
underflow--; // Underflow: Value wraps around to 18446744073709551615
```

### float
```
float overflow = FLT_MAX;      // Maximum value for a float
float underflow = FLT_MIN;     // Minimum normalized value for a float

overflow *= 2;  // Overflow: Value becomes infinity
underflow /= 2;  // Underflow: Value becomes denormalized or rounded to zero
```

### double 
```
double overflow = DBL_MAX;    // Maximum value for a double
double underflow = DBL_MIN;   // Minimum normalized value for a double

overflow *= 2;   // Overflow: Value becomes infinity
underflow /= 2;  // Underflow: Value becomes denormalized or rounded to zero
```

### long double 
```
long double overflow = LDBL_MAX;    // Maximum value for a long double
long double underflow = LDBL_MIN;   // Minimum normalized value for a long double

overflow *= 2;   // Overflow: Value becomes infinity
underflow /= 2;  // Underflow: Value becomes denormalized or rounded to zero
```
