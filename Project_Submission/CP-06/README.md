# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)

```
/*
 * Amrita Vishwa Vidyapeetham
 * TIFAC-CORE in Cyber Security
 * 20CYS181 - Computer Programming Lab Project
 * Student Management System
 * Authors: Arul Sujith S, Hemadhri P C, Jose Rohit S, Aadhithya Sivakumar 
 * Created Date: 29-June-2023
 * Updated Date: 02-August-2023  
 */

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <openssl/evp.h>

#define USERNAME 50
#define PASSWORD 50
#define NAME 50
#define EMAIL 50
#define PHONE 50
#define SUBJECTS 6

#define YELLOW  "\x1b[33m"
#define RESET   "\x1b[0m"

typedef struct {
    char username[USERNAME];
    char passwordHash[EVP_MAX_MD_SIZE * 2 + 1];
    char firstName[NAME];
    char lastName[NAME];
    char email[EMAIL];
    char phoneNumber[PHONE];
    float subjectMarks[SUBJECTS];
    float attendancePercentage;
} UserData;

void displayWelcomeMessage() {
    printf(YELLOW "                                            Welcome to student portal\n" RESET);
}

void displayMainMenu() {
    printf("\n1. Login\n");
    printf("2. Signup\n");
    printf("3. Exit\n");
}

int fileExists(const char* filename) {
    FILE* file = fopen(filename, "r");
    if (file) {
        fclose(file);
        return 1;
    }
    return 0;
}

void calculate_md5(const char* message, unsigned char* digest) {
    EVP_MD_CTX* context = EVP_MD_CTX_new();
    EVP_DigestInit(context, EVP_md5());
    EVP_DigestUpdate(context, message, strlen(message));
    EVP_DigestFinal(context, digest, NULL);
    EVP_MD_CTX_free(context);
}

void digest_to_string(const unsigned char* digest, char* md5string) {
    for (int i = 0; i < EVP_MD_size(EVP_md5()); i++) {
        sprintf(&md5string[i * 2], "%02x", digest[i]);
    }
    md5string[EVP_MD_size(EVP_md5()) * 2] = '\0';
}

int readUserDataFromFile(const char* filename, UserData* user) {
    FILE* file = fopen(filename, "r");
    if (!file) {
        printf("Error opening file for reading.\n");
        return 0;
    }

    int itemsRead = fscanf(file, "%s", user->passwordHash);
    itemsRead += fscanf(file, "%s %s", user->firstName, user->lastName);
    itemsRead += fscanf(file, "%s", user->email);
    itemsRead += fscanf(file, "%s", user->phoneNumber);
    for (int i = 0; i < SUBJECTS; i++) {
        itemsRead += fscanf(file, "%f", &user->subjectMarks[i]);
    }
    itemsRead += fscanf(file, "%f", &user->attendancePercentage);

    fclose(file);

    if (itemsRead != 10) {
        printf("Error reading data from file.\n");
        return 0;
    }

    return 1;
}

void writeUserDataToFile(const char* filename, const UserData* user) {
    FILE* file = fopen(filename, "w");
    if (!file) {
        printf("Error opening file for writing.\n");
        return;
    }

    // Calculate MD5 hash for the password and write it to the file
    unsigned char passwordHash[EVP_MAX_MD_SIZE];
    calculate_md5(user->passwordHash, passwordHash);
    char passwordHashString[EVP_MAX_MD_SIZE * 2 + 1];
    digest_to_string(passwordHash, passwordHashString);
    fprintf(file, "%s\n", passwordHashString);

    // Write the rest of the data to the file as-is
    fprintf(file, "%s\n", user->username);
    fprintf(file, "%s %s\n", user->firstName, user->lastName);
    fprintf(file, "%s\n", user->email);
    fprintf(file, "%s\n", user->phoneNumber);
    for (int i = 0; i < SUBJECTS; i++) {
        fprintf(file, "%.2f ", user->subjectMarks[i]);
    }
    fprintf(file, "\n");
    fprintf(file, "%.2f\n", user->attendancePercentage);

    fclose(file);
}

// Function to authenticate the user using MD5 hashed password
int authenticateUser(const char* username, const char* password, UserData* user) {
    char filename[50];
    sprintf(filename, "%s.txt", username);

    if (!fileExists(filename)) {
        printf("\nNo such username.\n");
        return 0;
    }

    FILE* file = fopen(filename, "r");
    char storedPasswordHash[EVP_MAX_MD_SIZE * 2 + 1];
    fscanf(file, "%s", storedPasswordHash);
    fclose(file);

    // Get the MD5 hash of the entered password
    unsigned char passwordHash[EVP_MAX_MD_SIZE];
    calculate_md5(password, passwordHash);

    // Convert the MD5 hash to a string for comparison
    char enteredPasswordHash[EVP_MAX_MD_SIZE * 2 + 1];
    digest_to_string(passwordHash, enteredPasswordHash);

    if (strcmp(storedPasswordHash, enteredPasswordHash) != 0) {
        printf("Incorrect password.\n");
        return 0;
    }

    return 1;
}


void signup() {
    char username[50], password[50];
    char filename[50];

    printf("Enter username: ");
    scanf("%s", username);
    sprintf(filename, "%s.txt", username);

    if (fileExists(filename)) {
        printf("Username already exists.\n");
        return;
    }

    printf("Enter password: ");
    system("stty -echo");
    scanf("%s", password);
    system("stty echo");

    // Get the MD5 hash of the password
    unsigned char passwordHash[EVP_MAX_MD_SIZE];
    calculate_md5(password, passwordHash);

    // Convert the MD5 hash to a string
    char passwordHashString[EVP_MAX_MD_SIZE * 2 + 1];
    digest_to_string(passwordHash, passwordHashString);

    FILE* file = fopen(filename, "w");
    fprintf(file, "%s\n", passwordHashString);

    char firstName[50], lastName[50], email[50], phoneNumber[50];
    float subjectMarks[6], attendancePercentage;
    char subjects[6][50] = {"Subject 1","Subject 2","Subject 3","Subject 4","Subject 5","Subject 6"};

    printf("\nEnter first name: ");
    scanf("%s", firstName);
    printf("Enter last name: ");
    scanf("%s", lastName);
    printf("Enter email: ");
    scanf("%s", email);
    printf("Enter phone number: ");
    scanf("%s", phoneNumber);
    printf("Enter marks : \n");

    for (int i = 0; i < 6; i++) {
        printf("%s - ", subjects[i]);
        scanf("%f", &subjectMarks[i]);
    }
    printf("Enter attendance percentage: ");
    scanf("%f", &attendancePercentage);

    fprintf(file, "%s %s\n", firstName, lastName);
    fprintf(file, "%s\n", email);
    fprintf(file, "%s\n", phoneNumber);
    fprintf(file, "%.2f %.2f %.2f %.2f %.2f %.2f\n", subjectMarks[0], subjectMarks[1], subjectMarks[2], subjectMarks[3], subjectMarks[4], subjectMarks[5]);
    fprintf(file, "%.2f\n", attendancePercentage);

    fclose(file);

    printf("\nSignup successful.\n");

}

void displayUserDetails(const char* username, const UserData* user) {
    char filename[50];
    sprintf(filename, "%s.txt", username);

    if (!fileExists(filename)) {
        printf("No such username.\n");
        return;
    }

    FILE* file = fopen(filename, "r");

    char password[50], firstName[50], lastName[50], email[50], phoneNumber[50];
    float subjectMarks[6], attendancePercentage;

    fscanf(file, "%s", password);
    fscanf(file, "%s %s", firstName, lastName);
    fscanf(file, "%s", email);
    fscanf(file, "%s", phoneNumber);
    fscanf(file, "%f %f %f %f %f %f", &subjectMarks[0], &subjectMarks[1], &subjectMarks[2], &subjectMarks[3], &subjectMarks[4], &subjectMarks[5]);
    fscanf(file, "%f", &attendancePercentage);

    fclose(file);

    float cgpa = ((subjectMarks[0] + subjectMarks[1] + subjectMarks[2] + subjectMarks[3] + subjectMarks[4] + subjectMarks[5]) / 6.0)/10;

    printf("\nUsername: %s\n", username);
    printf("Name: %s %s\n", firstName, lastName);
    printf("Email: %s\n", email);
    printf("Phone Number: %s\n", phoneNumber);
    printf("Subject Marks: %.2f %.2f %.2f %.2f %.2f %.2f\n", subjectMarks[0], subjectMarks[1], subjectMarks[2], subjectMarks[3], subjectMarks[4], subjectMarks[5]);
    printf("Attendance Percentage: %.2f%%\n", attendancePercentage);
    printf("CGPA: %.2f\n", cgpa);

}

void editProfile(const char* username, UserData* user) {
    char filename[50];
    sprintf(filename, "%s.txt", username);

    if (!fileExists(filename)) {
        printf("No such username.\n");
        return;
    }

    FILE* file = fopen(filename, "r");
    char password[50];
    fscanf(file, "%s", password);
    fclose(file);

    file = fopen(filename, "w");
    fprintf(file, "%s\n", password);

    char firstName[50], lastName[50], email[50], phoneNumber[50];
    float subjectMarks[6], attendancePercentage;
    char subjects[6][50] = {"Subject 1","Subject 2","Subject 3","Subject 4","Subject 5","Subject 6"};

    printf("Enter first name: ");
    scanf("%s", firstName);
    printf("Enter last name: ");
    scanf("%s", lastName);
    printf("Enter email: ");
    scanf("%s", email);
    printf("Enter phone number: ");
    scanf("%s", phoneNumber);
    printf("Enter marks : ");
    
    for (int i = 0; i < 6; i++) {
        printf("%s - ", subjects[i]);
        scanf("%f", &subjectMarks[i]);
    }
    printf("Enter attendance percentage: ");
    scanf("%f", &attendancePercentage);

    fprintf(file, "%s %s\n", firstName, lastName);
    fprintf(file, "%s\n", email);
    fprintf(file, "%s\n", phoneNumber);
    fprintf(file, "%.2f %.2f %.2f %.2f %.2f %.2f\n", subjectMarks[0], subjectMarks[1], subjectMarks[2], subjectMarks[3], subjectMarks[4], subjectMarks[5]);
    fprintf(file, "%.2f\n", attendancePercentage);

    fclose(file);

    printf("Profile updated successfully.\n");

}

int main() {
    system("clear");
    displayWelcomeMessage();

    int choice;
    int loggedIn = 0;
    UserData user;
    char username[USERNAME], password[PASSWORD];

    while (1) {
        displayMainMenu();

        printf("\nEnter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:  // Login
                if (loggedIn) {
                    printf("You are already logged in.\n");
                    break;
                }

                printf("Enter username: ");
                scanf("%s", username);
                system("stty -echo");
                printf("Enter password: ");
                scanf("%s", password);
                system("stty echo");

                if (authenticateUser(username, password, &user)) {
                    printf("Login successful.\n");
                    loggedIn = 1;
                } else {
                    printf("Login failed. Please try again.\n");
                }
                break;

            case 2:  // Signup
                if (loggedIn) {
                    printf("You are already logged in.\n");
                    break;
                }

                signup();
                break;

            case 3:  // Exit
                printf("Exiting the program.\n");
                exit(0);

            default:
                printf("Invalid choice.\n");
                break;
        }

        if (loggedIn) {
            displayUserDetails(username, &user);

            int option;
            printf("\n1. Logout\n");
            printf("2. Edit Profile\n");
            printf("Enter your option: ");
            scanf("%d", &option);

            switch (option) {
                case 1:  // Logout
                    loggedIn = 0;
                    break;

                case 2:  // Edit Profile
                    editProfile(username, &user);
                    break;

                default:
                    printf("Invalid option.\n");
                    break;
            }
        }
    }

    return 0;
}
```
