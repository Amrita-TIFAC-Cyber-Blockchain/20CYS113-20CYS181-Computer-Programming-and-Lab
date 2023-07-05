# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown) ![](https://img.shields.io/badge/Additional_Coverage-Code_Review-purple)  <br/>

## Bubble Sort with Tracing Table

```
#include <stdio.h>

// Bubble Sort algorithm
void bubbleSort(int arr[], int size) {
    int i, j;
    for (i = 0; i < size - 1; i++) {
        for (j = 0; j < size - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j+1]
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

// Function to print the elements of an array
void printArray(int arr[], int size) {
    int i;
    for (i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int arr[] = {23, 10, 05, 44, 18, 02}; // Array to be sorted
    int size = sizeof(arr) / sizeof(arr[0]); // Size of the array

    printf("Original array: ");
    printArray(arr, size);
    printf("-----------------\n");

    printf("Pass | Comparison | Swapped | Array          \n");
    printf("-----|------------|---------|----------------\n");

    for (int i = 0; i < size - 1; i++) { // Outer loop for passes
        for (int j = 0; j < size - i - 1; j++) { // Inner loop for comparisons and swapping
            printf("%4d | %4d > %4d  | ", i, arr[j], arr[j + 1]); // Print pass and comparison
            if (arr[j] > arr[j + 1]) { // Compare elements
                printf(" Yes    | "); // Elements are swapped
                // Swap arr[j] and arr[j+1]
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            } else {
                printf(" No     | "); // Elements are not swapped
            }
            printArray(arr, size); // Print the current state of the array
        }
        printf("-----|------------|---------|----------------\n");
    }

    printf("Sorted array: ");
    printArray(arr, size); // Print the sorted array

    return 0;
}
```

### Trace Table

Pass | Comparison | Swapped | Array
-----|------------|---------|----------------
   0 |   23 >   10  |  Yes    | 10 23 5 44 18 2
   0 |   23 >    5  |  Yes    | 10 5 23 44 18 2
   0 |   23 >   44  |  No     | 10 5 23 44 18 2
   0 |   44 >   18  |  Yes    | 10 5 23 18 44 2
   0 |   44 >    2  |  Yes    | 10 5 23 18 2 44
   1 |   10 >    5  |  Yes    | 5 10 23 18 2 44
   1 |   10 >   23  |  No     | 5 10 23 18 2 44
   1 |   23 >   18  |  Yes    | 5 10 18 23 2 44
   1 |   23 >    2  |  Yes    | 5 10 18 2 23 44
   2 |    5 >   10  |  No     | 5 10 18 2 23 44
   2 |   10 >   18  |  No     | 5 10 18 2 23 44
   2 |   18 >    2  |  Yes    | 5 10 2 18 23 44
   3 |    5 >   10  |  No     | 5 10 2 18 23 44
   3 |   10 >    2  |  Yes    | 5 2 10 18 23 44
   4 |    5 >    2  |  Yes    | 2 5 10 18 23 44
