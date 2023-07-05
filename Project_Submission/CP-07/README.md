# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)

## Library Management System
```
/*
 * Amrita Vishwa Vidyapeetham
 * TIFAC-CORE in Cyber Security
 * 20CYS181 - Computer Programming Lab Project
 * Library Management System
 * Authors: Asrita N L, Gunateet Dev, G Pavan Shanmukha Madhav
 * Created Date: 30-June-2023
 * Updated Date: 05-July-2023  
 */

#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#define NUMBOOKS 100 // numofbooks - maxbooks//

enum Library {
    Newsletters,
    Literature,
    Physics,
    Chemistry,
    Biology,
    Mathematics,
    General_Knowledge,
    Politics,
    Economics,
    Magazines,
    Technology
};

struct book {
    char title[100];
    char author[100];
    int publication;
    int availability;
    enum Library lib;
};

struct persdetail {
    char name[25];
    char roll_number[25];
    char department[30];
    int contactno;
    char email[30];
};

// FUNCTIONS DECLARATION //
void add_book(struct book details[], int i);
void display_all_books(struct book details[], int i);
void fine_calculation();
void add_personal_details(struct persdetail perdetails[]);
void time_info();
void status();

// Definition of functions //
void add_book(struct book details[], int i)
{
    printf("Enter details of the book:\n");
    printf("Title: ");
    scanf("%s", details[i].title);
    printf("Author: ");
    scanf("%s", details[i].author);
    printf("Publicationyear: ");
    scanf("%d", &details[i].publication);
    printf("Genre (0 for Newsletters, 1 for Literature, etc.): ");
    scanf("%u", &details[i].lib);
    details[i].availability = 1;
    printf("Book added successfully!\n");
}

void display_all_books(struct book details[], int i)
{
    printf("List of books:\n");
    for (i = 0; i < NUMBOOKS; i++) {
        if (details[i].availability == 1) {
            printf("Title: %s\n", details[i].title);
            printf("Author: %s\n", details[i].author);
            printf("Publication: %d\n", details[i].publication);
            printf("Library: %d\n", details[i].lib);
        }
    }
}

void fine_calculation()
{
    int days_borrowed, fine, fine_cost = 1;
    printf("Enter the number of days the book was borrowed: ");
    scanf("%d", &days_borrowed);
    if (days_borrowed <= 20) {
        printf("No fine.\n");
    } else {
        fine = days_borrowed - 20;
        printf("Fine is %d.\n", fine);
    }
}

void add_personal_details(struct persdetail perdetails[])
{
    printf("Enter your name: ");
    scanf("%s", perdetails[0].name);
    printf("Enter your roll number: ");
    scanf("%s", perdetails[0].roll_number);
    printf("Enter your department: ");
    scanf("%s", perdetails[0].department);
    printf("Enter your contact number: ");
    scanf("%d", &perdetails[0].contactno);
    printf("Enter your email: ");
    scanf("%s", perdetails[0].email);
}

void time_info()
{
    printf("Enter the login time of your entry (HOURS:MINUTES:SECONDS): ");
    char login[20];
    scanf("%19s", login);  
 printf("Enter the logout time of your exit (HOURS:MINUTES:SECONDS): ");
    char logout[20];
    scanf("%s", logout);  
}

int main()
{
    struct book details[NUMBOOKS];
    int choice;

    printf("LIBRARY MANAGEMENT SYSTEM\n");

    do {
        printf("Enter the appropriate choice from the following options:\n");
        printf("1 : Add a book\n");
        printf("2 : Display all books\n");
        printf("3 : Display fine\n");
        printf("4 : Login and Logout time\n");
        printf("5 : Quit\n");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Add a book\n");
                add_book(details, 0);
                break;
            case 2:
                printf("Display all books\n");
                display_all_books(details, 0);
                break;
            case 3:
                printf("Fine Calculation\n");
                fine_calculation();
                break;
            case 4:
                printf("Login and Logout time\n");
                time_info();
                break;
            case 5:
                printf("Quitting the program\n");
                break;
            default:
                printf("Invalid option selected. Choose appropriate options from above.\n");
                break;
        }
        //char ch = getchar();
        char ch;
        scanf("%s", &ch);
        system("clear");
    } while (choice != 5);

    return 0;
}
```
