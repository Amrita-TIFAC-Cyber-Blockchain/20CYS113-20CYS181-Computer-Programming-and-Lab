# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown) ![](https://img.shields.io/badge/Additional_Coverage-Code_Review-purple)  <br/>

## Folder Parsing in C

```
#include <stdio.h>
#include <dirent.h>
#include <string.h>

int main() {
    DIR *dir;
    struct dirent *entry;
    const char *folder_name = "root"; // Change this to the folder name you want to search

    // Open the directory
    dir = opendir(".");
    if (dir == NULL) {
        printf("Error opening directory.\n");
        return 1;
    }

    // Iterate over the directory entries
    while ((entry = readdir(dir)) != NULL) {
		
        // Check if the entry is a directory and has the desired name
        if (entry->d_type == DT_DIR && strcmp(entry->d_name, folder_name) == 0) {
            printf("Folder found: %s\n", entry->d_name);
            break;
        }
    }

    // Close the directory
    closedir(dir);

    return 0;
}
```
