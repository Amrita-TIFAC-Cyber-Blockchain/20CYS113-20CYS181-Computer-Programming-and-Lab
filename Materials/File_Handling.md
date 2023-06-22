# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown) ![](https://img.shields.io/badge/Additional_Coverage-Code_Review-purple)  <br/>

## File Handling in C

File handling in general involves operations related to reading, writing, and manipulating existing files in the filesystem. It allows the program to perform tasks such as creating files, opening files, reading contents from files, writing contents to files, and closing files.

### Opening a File:

- Use the *fopen()* function to open a file.
- Example:

```
FILE *file = fopen("example.txt", "r");
```

### Closing a File:

- Use the *fclose()* function to close a file that was previously opened.
- Example: 

```
fclose(file);
```

### Reading from a File:

- Use functions like *fgetc()*, *fgets()*, or *fread()* to read contents from a file.
- Example using *fgets()*:

```
char buffer[100];
fgets(buffer, sizeof(buffer), file);
```

### Writing to a File:

- Use functions like *fputc()*, *fputs()*, or *fwrite()* to write contents to a file.
Example using *fputs()*:

```
fputs("Hello, world!", file);
```

#### Reading/Writing through the file - Checking End of File (EOF)

```
while (!feof(file)) {
    // read or write contents
}
```

### File Modes

- "r": Opens a file for reading. The file must exist.
- "w": Opens a file for writing. If the file exists, its previous contents are truncated. If the file does not exist, a new file is created.
- "a": Opens a file for appending. Data is written at the end of the file. If the file does not exist, a new file is created.
- "r+": Opens a file for both reading and writing. The file must exist.
- "w+": Opens a file for both reading and writing. If the file exists, its previous contents are truncated. If the file does not exist, a new file is created.
- "a+": Opens a file for both reading and appending. Data can be read or written at any position in the file. If the file does not exist, a new file is created.

## Reading contents from a file

```
#include <stdio.h>

int main() {
    FILE *file;         // Declare a pointer to a FILE structure
    char filename[100]; // Store the filename
    char ch;            // Store each character read from the file

    printf("Enter the filename: ");
    scanf("%s", filename);  // Read the filename from the user

    // Open the file in "r" mode (read mode)
    file = fopen(filename, "r");

    // Check if the file was opened successfully
    if (file == NULL) {
        printf("Error opening the file.\n");
        return 1;
    }

    // Read and print the file contents
    printf("File contents:\n");
    while ((ch = fgetc(file)) != EOF) {
        printf("%c", ch);  // Print each character read from the file
    }

    // Close the file
    fclose(file);

    return 0;
}
```

### Output

<img src="https://i.ibb.co/w0G12G8/fileread-op.png" alt="fileread-op" border="0">

## Writing contents to the file

```
#include <stdio.h>

int main() {
    FILE *file;                     // Declare a pointer to a FILE structure
    char filename[100];             // Store the filename
    char content[1000];             // Store the content to be written to the file

    printf("Enter the filename: ");
    scanf("%99s", filename);        // Read the filename from the user

    // Open the file in "w" mode (write mode)
    file = fopen(filename, "w");

    // Check if the file was opened successfully
    if (file == NULL) {
        printf("Error opening the file.\n");
        return 1;
    }

    printf("Enter content to write to the file (max 1000 characters):\n");

    // Clear the input buffer
    int c;
    while ((c = getchar()) != '\n' && c != EOF);

    // Read content from the user using fgets()
    fgets(content, sizeof(content), stdin);

    // Write the content to the file using fputs()
    fputs(content, file);

    // Close the file
    fclose(file);

    printf("Content written to the file successfully.\n");

    return 0;
}
```

### Output

<img src="https://i.ibb.co/q7HXnDk/filewrite-op.png" alt="filewrite-op" border="0">

Posted on: 14th June, 2023 in [HPOJ](https://hpoj.cb.amrita.edu:8000/problem/20cys113ramfile01).

