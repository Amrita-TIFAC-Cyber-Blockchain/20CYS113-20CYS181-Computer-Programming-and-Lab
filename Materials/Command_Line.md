# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)

## Command Line Arguments

### General Logic

The main function should have parameters argc - argument count and argv - argument list as a string array.

```
int main(int argc, char *argv[])
{
    // Program logic goes here
    return 0;
}
```

To execute, assume the program expects three arguments from the user.

```
$ gcc program.c -o program
$ ./program arg1 arg2 arg3
```

### Example 1 - Simple Addition

```
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    if (argc != 3) {
        printf("Usage: ./sum <num1> <num2>\n");
        return 1;
    }

    int num1 = atoi(argv[1]);
    int num2 = atoi(argv[2]);
    int sum = num1 + num2;

    printf("Sum: %d\n", sum);

    return 0;
}
```

To execute, assume the file name is _sum.c_
```
$ gcc sum.c -o sum
$ ./sum 30 50
```

### Example 2 - File Reading

```
#include <stdio.h>

int main(int argc, char *argv[]) {
    if (argc != 2) {
        printf("Usage: ./file_reader <filename>\n");
        return 1;
    }

    char *filename = argv[1];
    FILE *file = fopen(filename, "r");

    if (file == NULL) {
        printf("Error opening file.\n");
        return 1;
    }

    char line[256];

    while (fgets(line, sizeof(line), file) != NULL) {
        printf("%s", line);
    }

    fclose(file);

    return 0;
}
```

To execute, assume the file name is _file_reader.c_

```
$ gcc file_reader.c -o file_reader
$ ./file_reader sample.txt
```
