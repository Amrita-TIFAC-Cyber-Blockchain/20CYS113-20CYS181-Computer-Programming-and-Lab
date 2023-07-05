# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)

## Hospital Management System 

```
/*
 * Amrita Vishwa Vidyapeetham
 * TIFAC-CORE in Cyber Security
 * 20CYS181 - Computer Programming Lab Project
 * Hospital Managment System
 * Authors: Aishwarya S, Dharshika S, Joshua Anto A, Shree Harini T
 * Created Date: 28-June-2023
 * Updated Date: 05-July-2023  
 */



#include <stdio.h>
#include <time.h>
#include <string.h>

struct Patient {
    int id;
    char name[50];
    int age;
    char gender[10];
    char contact[20];
    char medical_history[100];
};

char usrname[50]= "admin";
char passwd[50]= "admin";

struct doctors{
        int doc_id;
        char doc_name[20];
        char doc_password[14];
        char doc_spec[15];
};

struct doctors doc[10]={
                {1,"RUDHRAN", "siv1", "Cardiology"},
                {2,"PREETHI","sak2"," Dermatology"},
                {3,"HAMSINI","ran3","Endocrinology"},
                {4,"KARTHIK","kav4","Pediatrics"},
                {5,"KEERTHI","kee5","General Doctor"},
                {6,"SARANYA","sar6","Neurology"},
                {7,"DHARANI","sub7","Gynecology"}
};

void ledger(char name[101]) {
    FILE *file = fopen("Admin_ledger", "a");

    if (file == NULL) {
        printf("Unable to open the file.\n");
        return 1;
    }

    char data[101];
    strcpy(data,name);  

    time_t currentTime = time(NULL);
    char* timeString = ctime(&currentTime);
    strcat(data," ");
    strcat(data,timeString);    
    fprintf(file, "%s", data);

    fclose(file);

}

void display_doc_rec(){
      printf("HERE ARE THE DETAILS OF DOCTORS\n");
        printf("DOC_ID|   DOC_NAME | DOC_SPECIALIZATION\n");
        for(int i=0;i<7;i++){
                printf("%d    | %s       | %s \n",doc[i].doc_id,doc[i].doc_name,doc[i].doc_spec);}
}


void addPatientRecord() {
    struct Patient patient;

    printf("Enter patient ID: ");
    scanf("%d", &patient.id);

    printf("Enter patient name: ");
    scanf(" %[^\n]", patient.name);

    printf("Enter patient age: ");
    scanf("%d", &patient.age);

    printf("Enter patient gender: ");
    scanf(" %[^\n]", patient.gender);

    printf("Enter patient contact: ");
    scanf(" %[^\n]", patient.contact);

    printf("Enter patient medical history: ");
    scanf(" %[^\n]", patient.medical_history);

    FILE* file = fopen("patient_records.txt", "a");
    if (file == NULL) {
        printf("Error opening the file.\n");
        return;
    }

   fprintf(file, "ID: %d\nName: %s\nAge: %d\nGender: %s\nContact: %s\nMedical History: %s\n",
            patient.id, patient.name, patient.age, patient.gender, patient.contact, patient.medical_history);
   fprintf(file,"---------------------------\n");
    fclose(file);

    printf("Patient record saved successfully.\n");
}

void display_all_Patient_Rec() {
    FILE* file = fopen("patient_records.txt", "r");
    if (file == NULL) {
        printf("Error opening the file.\n");
        return;
    }

    printf("List of Patient's Record:\n");

    char ch;
    while ((ch = fgetc(file)) != EOF) {
        printf("%c", ch);
    }

    fclose(file);
}

void searchPatient() {
    printf("Enter the patient id: \n");
    char id[7];
    char sub[20]="ID: ";

    scanf("%s",id);
    strcat(sub,id);
    const char *substring = sub;

    const char *filename = "patient_records.txt";
    FILE *file = fopen(filename, "r");
    if (file == NULL) {
        printf("Failed to open the file.\n");
        return;
    }

    char line[256];
    int lineNum = 1;
    int fline;
    int found =0;
    while (fgets(line, sizeof(line), file)) {
        if (strstr(line, substring) != NULL) {
          fline = lineNum;
          found = 1;
            break;
        }
        lineNum++;

    }
    if (found ==0){
      printf("patient not found\n");
    }

    fclose(file);
    printLines(fline,fline+5);
}

void printLines(int startLine, int endLine) {
    const char *filename = "patient_records.txt";
    FILE *file = fopen(filename, "r");
    if (file == NULL) {
        printf("Failed to open the file.\n");
        return;
    }

    char line[256];
    int lineNum = 1;
    printf("-----------------------------------\n");
    while (fgets(line, sizeof(line), file)) {
        if (lineNum >= startLine && lineNum <= endLine) {
            printf("%s", line);
        }
        lineNum++;
    }
    printf("-----------------------------------\n");
    fclose(file);
}

int main() {
    printf("Welcome to JHAD Hospital!!\n");
    printf("Enter your credentials: \n");
    char username[50];
    char password[50];
    printf("Username: ");
    scanf("%s",username);
     printf("\nPassword: ");
    scanf("%s",password);

    if (strcmp(username,usrname)==0 && strcmp(password,passwd)==0){
          printf("login succesful\n");
          ledger(username);
          int operation;
          do{
          printf("what operation would you like to perform?\n");
          printf("1. add a patient's record \n2. view available doctor\n3. view all the patient records\n4. view an patient's record.\n5. logout\n");           
          scanf("%d",&operation);
          switch (operation)
            {
            case 1:
                  addPatientRecord();
                  break;

            case 2:
                  display_doc_rec();
                  break;
            case 3:
                  display_all_Patient_Rec();
                  break;
            case 4:
                  searchPatient();
                  break;
            case 5:
                   break;     
            default:
                   printf("enter a valid operation\n");
                   break;
          }     
          }while(operation !=5);
      }
    else{
          printf("invalid username or password");
    }


    return 0;
}

```
