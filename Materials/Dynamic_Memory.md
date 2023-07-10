# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)  <br/>

## Dynamic Memory Allocation

### malloc -  memory allocation & free

#### Function Prototype

```
void* malloc(size_t size);
```

#### Example

```
#include <stdio.h>
#include <stdlib.h>

int main() {
    // Example using malloc - memory allocation
    int* ptr1 = (int*) malloc(5 * sizeof(int));
    if (ptr1 == NULL) {
        printf("Memory allocation failed.\n");
        return 1;
    }

    printf("Memory allocated using malloc:\n");
    int *tptr1 = ptr1;
    for (int i = 0; i < 5; i++) {
        //ptr1[i] = i + 1;
		printf("Value Allocated : %d\n", *tptr1);
        printf("Address Allocated : %p\n", tptr1++);
		printf("--------------\n");
    }
    printf("\n");

    // Freeing the allocated memory
    free(ptr1);

    return 0;
}

```
### calloc - contiguous allocation & free

#### Function Prototype

```
void* calloc(size_t num, size_t size);
```

#### Example

```
#include <stdio.h>
#include <stdlib.h>

int main() {

    // Example using calloc - contiguous allocation
    int* ptr2 = (int*) calloc(5, sizeof(int));
    if (ptr2 == NULL) {
        printf("Memory allocation failed.\n");
        return 1;
    }
	
    int *tptr2 = ptr2;
    printf("Memory allocated using calloc:\n");
    for (int i = 0; i < 5; i++) {
        printf("Value Allocated : %d\n", *tptr2);
        printf("Address Allocated : %p\n", tptr2++);
		printf("--------------\n");
    }
    printf("\n");

    // Freeing the allocated memory
    free(ptr2);

    return 0;
}
```

### realloc - reallocation & free

#### Function Prototype

```
void* realloc(void* ptr, size_t size);
```
#### Example

```
#include <stdio.h>
#include <stdlib.h>

int main() {
    int* ptr = (int*) malloc(5 * sizeof(int));  // Allocate memory for an array of 5 integers
    if (ptr == NULL) {
        printf("Memory allocation failed.\n");
        return 1;
    }

    printf("Address: %x\n", ptr);

    // Resize the memory block to store 10 integers
    int* resizedPtr = (int*) realloc(ptr, 10 * sizeof(int));
    if (resizedPtr == NULL) {
        printf("Memory reallocation failed.\n");
        free(ptr);
        return 1;
    }

    ptr = resizedPtr;  // Update the pointer to the resized memory block
	
    printf("Address after reallocation: %x\n", ptr);

    // Use the resized memory block as needed

    free(ptr);  // Free the allocated memory

    return 0;
}

```
