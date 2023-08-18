# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)

```
/*
 * Amrita Vishwa Vidyapeetham
 * TIFAC-CORE in Cyber Security
 * 20CYS181 - Computer Programming Lab Project
 * Airline Ticketing System
 * Authors: B Rushyendra , P Vamsi , V Satya Siddardha , Y Kishan Sai
 * Created Date: 01-July-2023
 * Updated Date: 08-July-2023
 */


#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#define MAX_FLIGHTS 5
#define MAX_TICKETS_PER_FLIGHT 80
#define MAX_DESTINATIONS 6
#define PNR_LENGTH 10

// Structure to represent a ticket
typedef struct {
    char passengerName[50];
    int age;
    char gender[10];
    int seatNumber;
    char fromDestination[50];
    char toDestination[50];
    char flightName[10];
    char pnrNumber[PNR_LENGTH + 1];
    char class[15];
    int ticketStatus; // 0 - Not reserved, 1 - Reserved
} Ticket;

// Structure to represent ticket prices between destinations
typedef struct {
    char fromDestination[50];
    char toDestination[50];
    double economyPrice;
    double businessPrice;
} TicketPrice;

// Function to generate a random PNR number
void generatePNR(char *pnr) {
    const char charset[] = "0123456789";
    for (int i = 0; i < PNR_LENGTH; ++i) {
        pnr[i] = charset[rand() % (sizeof(charset) - 1)];
    }
    pnr[PNR_LENGTH] = '\0';
}

// Function to reserve a ticket
void reserveTicket(Ticket tickets[], int *totalTickets, const char flightNames[][50], int totalFlights, const char destinations[][50], int totalDestinations) {
    // Check if maximum ticket limit per flight has been reached
    if (*totalTickets >= MAX_FLIGHTS * MAX_TICKETS_PER_FLIGHT) {
        printf("Ticket reservation limit reached.\n");
        return;
    }

    printf("Enter passenger name: ");
    scanf("%s", tickets[*totalTickets].passengerName);
    printf("Enter passenger age: ");
    scanf("%d", &tickets[*totalTickets].age);
    printf("Enter passenger gender: ");
    scanf("%s", tickets[*totalTickets].gender);

    // Select flight
    int flightChoice;
    printf("Select a flight:\n");
    for (int i = 0; i < totalFlights; ++i) {
        printf("%d. %s\n", i + 1, flightNames[i]);
    }
    printf("Enter your choice: ");
    scanf("%d", &flightChoice);

    if (flightChoice < 1 || flightChoice > totalFlights) {
        printf("Invalid flight choice.\n");
        return;
    }

    strcpy(tickets[*totalTickets].flightName, flightNames[flightChoice - 1]);

    // Select from destination
    int fromDestChoice;
    printf("Select from destination:\n");
    for (int i = 0; i < totalDestinations; ++i) {
        printf("%d. %s\n", i + 1, destinations[i]);
    }
    printf("Enter your choice: ");
    scanf("%d", &fromDestChoice);

    if (fromDestChoice < 1 || fromDestChoice > totalDestinations) {
        printf("Invalid from destination choice.\n");
        return;
    }

    strcpy(tickets[*totalTickets].fromDestination, destinations[fromDestChoice - 1]);

    // Select to destination
    int toDestChoice;
    printf("Select to destination:\n");
    for (int i = 0; i < totalDestinations; ++i) {
        printf("%d. %s\n", i + 1, destinations[i]);
    }
    printf("Enter your choice: ");
    scanf("%d", &toDestChoice);

    if (toDestChoice < 1 || toDestChoice > totalDestinations) {
        printf("Invalid to destination choice.\n");
        return;
    }

    strcpy(tickets[*totalTickets].toDestination, destinations[toDestChoice - 1]);

    // Check if the from destination and to destination are the same
    if (strcmp(tickets[*totalTickets].fromDestination, tickets[*totalTickets].toDestination) == 0) {
        printf("Invalid destination selection. From and to destinations cannot be the same.\n");
        return;
    }

    // Select ticket class
    int classChoice;
    printf("Select ticket class:\n");
    printf("1. Economy Class\n");
    printf("2. Business Class\n");
    printf("Enter your choice: ");
    scanf("%d", &classChoice);

    if (classChoice == 1) {
        // Economy Class
        printf("Economy Class selected.\n");
        strcpy(tickets[*totalTickets].pnrNumber, "E");
        strcpy(tickets[*totalTickets].class, "Economy Class");
    } else if (classChoice == 2) {
        // Business Class
        printf("Business Class selected.\n");
        strcpy(tickets[*totalTickets].pnrNumber, "B");
        strcpy(tickets[*totalTickets].class, "Business Class");
    } else {
        printf("Invalid class choice.\n");
        return;
    }

    int price = loadTicketprice(tickets[*totalTickets].fromDestination,tickets[*totalTickets].toDestination,tickets[*totalTickets].class);
    if(price > 0){
        int payment;
        printf("Ticket price from %s to %s: %d\n",tickets[*totalTickets].fromDestination,tickets[*totalTickets].toDestination,price);
        printf("Enter the payable amount: ");
        scanf("%d", &payment);
        if(payment == price){
            printf("Payment Successful.\n");
        }
        else{
        printf("Payment failed.\n");
        return;
        }
    }
    else{return;}
    // Check if there are available seats on the flight
    int availableSeat = -1;
    for (int i = 0; i < MAX_TICKETS_PER_FLIGHT; ++i) {
        if (tickets[i].ticketStatus == 0 && strcmp(tickets[i].flightName, tickets[*totalTickets].flightName) == 0) {
            availableSeat = i + 1;
            break;
        }
    }

    if (availableSeat != -1) {
        tickets[*totalTickets].seatNumber = rand() % MAX_TICKETS_PER_FLIGHT;
        tickets[*totalTickets].ticketStatus = 1;
        generatePNR(tickets[*totalTickets].pnrNumber);
        ++(*totalTickets);
        printf("Ticket reserved successfully.\n");
        printf("PNR Number: %s\n", tickets[*totalTickets - 1].pnrNumber);

        // Save passenger details to file
        savePassengerDetails(tickets[*totalTickets - 1]);
    } else {
        printf("No available seats on the selected flight.\n");
    }
}

// Function to cancel a ticket
void cancelTicket(Ticket tickets[], int totalTickets){
    char pnr[PNR_LENGTH + 1];
    printf("Enter PNR number: ");
    scanf("%s", pnr);

    const char* file = "passengers.txt";
    char startString[100] = "PNR Number: ";
    strcat(startString, pnr);

    removeContents(file, startString);
}
//Function to remove the ticket details from the passengers file
void removeContents(const char* filename, const char* startStr){
    FILE *inputFile = fopen(filename, "r");
    if (inputFile == NULL) {
        printf("Failed to open the input file.\n");
        return;
    }

    FILE *tempFile = fopen("temp.txt", "w");
    if (tempFile == NULL) {
        printf("Failed to create the temporary file.\n");
        fclose(inputFile);
        return;
    }

    char line[100];
    const char* endStr = "---------------------------------------------\n";
    int skipMode = 0;
    int foundStartString = 0;

    while (fgets(line, sizeof(line), inputFile) != NULL) {
        if (strncmp(line, startStr, strlen(startStr)) == 0) {
            skipMode = 1;
            foundStartString = 1;
        }

        if (skipMode == 0) {
            fputs(line, tempFile);
        }

        if (strncmp(line, endStr, strlen(endStr)) == 0) {
            skipMode = 0;
        }
    }

    fclose(inputFile);
    fclose(tempFile);

    if (!foundStartString) {
        printf("No ticket with this PNR number or this ticket is already canceled.\n");
        remove("temp.txt");
    }
    else {
        remove(filename);
        rename("temp.txt", filename);
        const char* knownSubStr = "PNR Number: ";
        const char* remainingStr = strstr(startStr, knownSubStr);

    if (remainingStr != NULL){
        remainingStr += strlen(knownSubStr);
    }
        printf("Ticket with PNR number %s is canceled",remainingStr);
    }
}

// Function to display a ticket
void displayTicket(Ticket tickets[], int totalTickets) {
    char pnr[PNR_LENGTH + 1];
    printf("Enter PNR number: ");
    scanf("%s", pnr);

    const char* file = "passengers.txt";
    char startString[100] = "PNR Number: ";
    strcat(startString, pnr);

    printContentBetweenStrings(file, startString);

}
//Function to load ticket prices from the file
int loadTicketprice(const char* fromDest, const char* toDest, const char* ticket_class){
    // Open the file
    FILE* file = fopen("ticket_prices.txt", "r");
    if (file == NULL) {
        // Handle file open error
        printf("Failed to open the file.\n");
        return -1;
    }

    char line[100];
    while (fgets(line, sizeof(line), file)) {
        // Split the line into destination, class, economy price, and business price
        char fdestination[50];
        char tdestination[50];
        char economy_price[20];
        char business_price[20];

        sscanf(line, "%s %s %s %s", fdestination, tdestination, economy_price, business_price);

        // Check if the destination and class match the arguments
        if(strcmp(fdestination, fromDest) == 0 && strcmp(tdestination, toDest) == 0 && strcmp(ticket_class, "Economy Class") == 0){
            fclose(file);
            return atof(economy_price);
        } 
        else if(strcmp(fdestination, fromDest) == 0 && strcmp(tdestination, toDest) == 0 && strcmp(ticket_class, "Business Class") == 0){
            fclose(file);
            return atof(business_price);
           }
        
    }

}
//Function to get contents of the passenger from the passenger file
void printContentBetweenStrings(const char* filename, const char* startString) {

    FILE* file = fopen(filename, "r");
    if (file == NULL) {
        printf("Failed to open the file.\n");
        return;
    }

    const char* endString = "---------------------------------------------\n";

    
    char line[100];
    int insideContent = 0;
    int found = 0;
    while (fgets(line, sizeof(line), file)) {
        
        if (strstr(line, startString) != NULL) {
            insideContent = 1;
            found = 1;
            printf("=============================================\n");
        }
        
        
        if (insideContent) {
            if (strcmp(line, endString) == 0){
                    insideContent = 0;
                    printf("=============================================");
                    fclose(file);
                    break;
            }
            printf("%s", line);
        }

    }
    if(found){
        fclose(file);
    }
    else{
        const char* knownSubStr = "PNR Number: ";
        const char* remainingStr = strstr(startString, knownSubStr);

    if (remainingStr != NULL){
        remainingStr += strlen(knownSubStr);
    }
    
    printf("Ticket with PNR number %s is canceled or not reserved",remainingStr);
    }

}



// Function to save passenger details to a file
void savePassengerDetails(Ticket ticket) {
    FILE *file = fopen("passengers.txt", "a");
    if (file == NULL) {
        printf("Failed to open passengers.txt file.\n");
        return;
    }

    fprintf(file, "PNR Number: %s\n", ticket.pnrNumber);
    fprintf(file, "Passenger Name: %s\n", ticket.passengerName);
    fprintf(file, "Age: %d\n", ticket.age);
    fprintf(file, "Gender: %s\n", ticket.gender);
    fprintf(file, "Seat Number: %d\n", ticket.seatNumber);
    fprintf(file, "From Destination: %s\n", ticket.fromDestination);
    fprintf(file, "To Destination: %s\n", ticket.toDestination);
    fprintf(file, "Flight Name: %s\n", ticket.flightName);
    fprintf(file,"Seat class: %s\n",ticket.class);
    fprintf(file, "---------------------------------------------\n");

    fclose(file);
}

int main() {
    Ticket tickets[MAX_FLIGHTS * MAX_TICKETS_PER_FLIGHT];
    int totalTickets = 0;
    const char flightNames[MAX_FLIGHTS][50] = {
        "Indigo",
        "SpiceJet",
        "AirIndia",
        "DeccanAir",
        "Jet Airways"   // We can add more flights if needed
    };
    int totalFlights = sizeof(flightNames) / sizeof(flightNames[0]);

    const char destinations[MAX_DESTINATIONS][50] = {
        "Hyderabad(HYD)",
        "Chennai(CHE)",
        "Coimbatore(CBE)",
        "Bengaluru(BLR)",
        "Mumbai(BOM)",
        "Delhi(DEL)"
        // We can add more destinations if needed
    };
    int totalDestinations = sizeof(destinations) / sizeof(destinations[0]);

    srand(time(0));

    int choice;
    do {
        printf("\n========== Ticket Reservation System ==========\n");
        printf("1. Reserve a ticket\n");
        printf("2. Cancel a ticket\n");
        printf("3. Display a ticket\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                reserveTicket(tickets, &totalTickets, flightNames, totalFlights, destinations, totalDestinations);
                break;
            case 2:
                cancelTicket(tickets, totalTickets);
                break;
            case 3:
                displayTicket(tickets, totalTickets);
                break;
            case 4:
                printf("Exiting program.\n");
                printf("Please visit again!!!\n");
                break;
            default:
                printf("Invalid choice. Please try again.\n");
                break;
        }
    } while (choice != 4);

    return 0;
}
```
