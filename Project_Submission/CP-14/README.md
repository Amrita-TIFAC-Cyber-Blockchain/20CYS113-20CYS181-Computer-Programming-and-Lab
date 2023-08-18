# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

#define MAX_FILENAME_LEN 100
#define MAX_FILE_CONTENT_LEN 1000

void createDocument();
void openDocument();
void appendText();
void deleteText();
void encryptText();
void decryptText();
void saveDocument();
void askAndSave();

char current_filename[MAX_FILENAME_LEN];
char current_content[MAX_FILE_CONTENT_LEN];
int content_length = 0;

int main() {
    int choice;

    while (1) {
        printf("\n===== Simple Text Editor =====\n");
        printf("1. Create a new document\n");
        printf("2. Open an existing document\n");
        printf("3. Append text to the document\n");
        printf("4. Delete text from the document\n");
        printf("5. Encrypt the document\n");
        printf("6. Decrypt the document\n");
        printf("7. Save the document\n");
        printf("8. Exit\n");
        printf("==============================\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                createDocument();
                break;
            case 2:
                openDocument();
                break;
            case 3:
                appendText();
                break;
            case 4:
                deleteText();
                break;
            case 5:
                encryptText();
                break;
            case 6:
                decryptText();
                break;
            case 7:
                saveDocument();
                break;
            case 8:
                askAndSave();
                return 0;
            default:
                printf("Invalid choice! Please try again.\n");
        }
    }

    return 0;
}

void createDocument() {
    printf("Enter the filename: ");
    scanf("%s", current_filename);
    getchar(); // Clear the input buffer

    printf("Enter the content (max %d characters):\n", MAX_FILE_CONTENT_LEN);
    fgets(current_content, MAX_FILE_CONTENT_LEN, stdin);
    content_length = strlen(current_content);
    printf("Document created successfully.\n");
}

void openDocument() {
    printf("Enter the filename: ");
    scanf("%s", current_filename);
    getchar(); // Clear the input buffer

    FILE* file = fopen(current_filename, "r");
    if (file == NULL) {
        printf("File not found.\n");
        return;
    }

    content_length = 0;
    char c;
    while ((c = fgetc(file)) != EOF && content_length < MAX_FILE_CONTENT_LEN) {
        current_content[content_length++] = c;
    }
    fclose(file);

    printf("File opened successfully.\n");
}

void appendText() {
    printf("Enter the text to append:\n");
    getchar(); // Clear the input buffer

    char appended_text[MAX_FILE_CONTENT_LEN];
    fgets(appended_text, MAX_FILE_CONTENT_LEN, stdin);
    int append_length = strlen(appended_text);

    if (content_length + append_length > MAX_FILE_CONTENT_LEN) {
        printf("Cannot append. Document size will exceed the limit.\n");
        return;
    }

    strcat(current_content, appended_text);
    content_length += append_length - 1;
    printf("Text appended successfully.\n");
}

void deleteText() {
    printf("Enter the starting position of text to delete: ");
    int start;
    scanf("%d", &start);

    printf("Enter the number of characters to delete: ");
    int num_chars;
    scanf("%d", &num_chars);

    if (start < 0 || start >= content_length || num_chars <= 0 || start + num_chars > content_length) {
        printf("Invalid deletion range.\n");
        return;
    }

    memmove(&current_content[start], &current_content[start + num_chars], content_length - start - num_chars + 1);
    content_length -= num_chars;
    printf("Text deleted successfully.\n");
}

void encryptText() {
    printf("Enter the encryption key: ");
    int key;
    scanf("%d", &key);

    for (int i = 0; i < content_length; i++) {
        current_content[i] = (current_content[i] + key - 32) % 95 + 32;
    }

    printf("Text encrypted successfully.\n");
}

void decryptText() {
    printf("Enter the decryption key: ");
    int key;
    scanf("%d", &key);

    for (int i = 0; i < content_length; i++) {
        current_content[i] = (current_content[i] - key - 32 + 95) % 95 + 32;
    }

    printf("Text decrypted successfully.\n");
}

void saveDocument() {
    if (strlen(current_filename) == 0) {
        printf("No document to save.\n");
        return;
    }

    FILE* file = fopen(current_filename, "w");
    if (file == NULL) {
        printf("Error opening file for writing.\n");
        return;
    }

    fwrite(current_content, sizeof(char), content_length, file);
    fclose(file);

    printf("Document saved successfully.\n");
}

void askAndSave() {
    char choice;

    if (strlen(current_filename) == 0 || content_length == 0) {
        printf("No document to save. Exiting...\n");
        return;
    }

    printf("Do you want to save the current document? (Y/N): ");
    getchar(); // Clear the input buffer
    scanf("%c", &choice);

    if (tolower(choice) == 'y') {
        saveDocument();
    }
}
```
