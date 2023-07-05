# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)

## Bank Management System

```
 
/*
 * Amrita Vishwa Vidyapeetham
 * TIFAC-CORE in Cyber Security
 * 20CYS181 - Computer Programming Lab Project
 * Bank Management System 
 * Authors: Rahul Shankar V, R Thanuj, Nandana Mahesh, Navarang C D
 * Created Date: 29-June-2023
 * Updated Date: 05-July-2023  
 */



#include <stdio.h>
#include <stdlib.h>
#include <string.h>
struct Customer {
   int id;
   char name[20];
   char account_number[20];
   int pin,age,phone;
   int Balance;
};

int reset(){
    FILE *of;        //write part
   of= fopen ("usps.txt", "w");
   if (of == NULL) {
      fprintf(stderr,"Error to open the file");
      return 1;
   }
   struct Customer inp1 = {1, "Admin", "000000", 1234,100,1234568, 5000};
   if(fwrite != 0)
      printf("Contents to file written successfully !\n");
   else
      printf("Error writing file !");
   fclose (of);
}
int display(){
    FILE *inf;       // read part
   struct Customer inp;
   inf = fopen ("usps.txt", "r");
   if (inf == NULL) {
      fprintf(stderr, "Error to open the file");
      return 2;
   }
   while(fread(&inp, sizeof(struct Customer), 1, inf))
      printf ("id = %d name = %s Account=%s pin=%d age=%d", inp.id, inp.name,inp.account_number,inp.pin,inp.age);
      printf ("Phone number: %d,Balance=%d\n",inp.phone,inp.Balance);
   fclose (inf);
   return 0;
}
int add_account(){
    FILE *ind;        //append part
   ind= fopen ("usps.txt", "a");
   if (ind == NULL) {
      fprintf(stderr,"Error to open the file");
      return 1;
   }
   struct Customer cus;
   printf("\n ACCOUNT CREATION ");
   printf("\nEnter the account number:");
   scanf("%s",cus.account_number);
    printf("\nEnter the name:");
    scanf("%s",cus.name);
    printf("\nEnter the age:");
    scanf("%d",&cus.age);
    printf("\nEnter the phone number:");
    scanf("%lf",&cus.phone);
    printf("\nEnter the minimum balance: ");
    scanf("%d",&cus.Balance);
    printf("\nEnter the pin:");
    scanf("%d",&cus.pin);
    printf("\nAccount created successfully!");

   fwrite (&cus, sizeof(struct Customer), 1, ind);
   if(fwrite != 0)
      printf("Contents to file written successfully !\n");
   else
      printf("Error writing file !");
   fclose (ind);
}
int count(){
   struct Customer cus;
   FILE *fc;
   fc=fopen("usps.txt","r");
   fseek(fc,0,SEEK_END);
   int n=ftell(fc)/sizeof(struct Customer);
   printf("\nNo: of records:%d",n);
   fclose(fc);
}
int search(){
   FILE *inf;       // read part
   char ac_no[20];
   struct Customer inp;
   int found=0;
   inf = fopen ("usps.txt", "r");
   if (inf == NULL) {
      fprintf(stderr, "Error to open the file");
      return 2;
   }
   printf("Enter the Account number to be searched:");
   scanf("%s",ac_no);
   while(fread(&inp, sizeof(struct Customer), 1, inf)){
      if(!strcmp(inp.account_number,ac_no)){
         found=1;
         printf ("id = %d name = %s Account=%s pin=%d Balance=%d\n", inp.id, inp.name,inp.account_number,inp.pin,inp.Balance);
      }
   }
   if(found!=1){
      printf("\nnot found");
   }
   fclose (inf);
   return 0;
}
/*int remove(){
   FILE *inf,*inu;       // read part
   char ac_no[20];
   struct Customer inp;
   int found=0;
   inf = fopen("usps.txt", "r");
   inu = fopen("temp.txt","w");
   if (inf == NULL) {
      fprintf(stderr, "Error to open the file");
      return 2;
   }
   printf("Enter the Account number to be deleted:");
   scanf("%s",ac_no);
   while(fread(&inp, sizeof(struct Customer), 1, inf)){
      if(!strcmp(inp.account_number,ac_no)){
         found=1;
      }
      else
         fwrite(&inp,sizeof(struct Customer),1,inu);
   }
   fclose(inu); fclose (inf);
   if(found!=1){
      printf("\nnot found");
   }
   else{
      inu = fopen("usps.txt", "w");
      inf = fopen("temp.txt","r");
      while(fread(&inp, sizeof(struct Customer), 1, inf)){
         fwrite(&inp, sizeof(struct Customer), 1, inu);
      }

      fclose(inu); fclose (inf);
   }
   return 0;
}*/
int sortdis(){
   struct Customer *cus,c1;
   FILE *fs;
   int i,j;
   fs=fopen("usps.txt","r");
   fseek(fs,0,SEEK_END);
   int n=ftell(fs)/sizeof(struct Customer);
   cus=(struct Customer*)calloc(n,sizeof(struct Customer));
   rewind(fs);
   for(i=0;i<n;i++){
      fread(&cus[i],sizeof(struct Customer),1,fs);
   }
   for(i=0;i<n;i++){
      for(j=i+1;j<n;j++){
      if(cus[i].Balance>cus[j].Balance){
         c1=cus[i];
         cus[i]=cus[j];
         cus[j]=c1;
      }
   }
   }
   for(i=0;i<n;i++){
      printf ("id = %d name = %s Account=%s pin=%d Balance=%d\n", cus[i].id, cus[i].name,cus[i].account_number,cus[i].pin,cus[i].Balance);
   }
   fclose(fs);
}
int sortfile(){
   struct Customer *cus,c1;
   FILE *fs;
   int i,j;
   fs=fopen("usps.txt","r");
   fseek(fs,0,SEEK_END);
   int n=ftell(fs)/sizeof(struct Customer);
   cus=(struct Customer*)calloc(n,sizeof(struct Customer));
   rewind(fs);
   for(i=0;i<n;i++){
      fread(&cus[i],sizeof(struct Customer),1,fs);
   }
   fclose(fs);
   for(i=0;i<n;i++){
      for(j=i+1;j<n;j++){
      if(cus[i].Balance>cus[j].Balance){
         c1=cus[i];
         cus[i]=cus[j];
         cus[j]=c1;
      }
   }
   fs=fopen("usps.txt","w");

   }
   for(i=0;i<n;i++){
      printf ("id = %d name = %s Account=%s pin=%d Balance=%d\n", cus[i].id, cus[i].name,cus[i].account_number,cus[i].pin,cus[i].Balance);
      fwrite(&cus[i],sizeof(struct Customer),1,fs);
   }
   fclose(fs);
}
int sortdisn(){
   struct Customer *cus,c1;
   FILE *fs;
   int i,j;
   fs=fopen("usps.txt","r");
   fseek(fs,0,SEEK_END);
   int n=ftell(fs)/sizeof(struct Customer);
   cus=(struct Customer*)calloc(n,sizeof(struct Customer));
   rewind(fs);
   for(i=0;i<n;i++){
      fread(&cus[i],sizeof(struct Customer),1,fs);
   }
   for(i=0;i<n;i++){
      for(j=i+1;j<n;j++){
      if(strcmp(cus[i].account_number,cus[j].account_number)>0){
         c1=cus[i];
         cus[i]=cus[j];
         cus[j]=c1;
      }
   }
   }
   for(i=0;i<n;i++){
      printf ("id = %d name = %s Account=%s pin=%d Balance=%d\n", cus[i].id, cus[i].name,cus[i].account_number,cus[i].pin,cus[i].Balance);
   }
   fclose(fs);
}
int sortfilen(){
   struct Customer *cus,c1;
   FILE *fs;
   int i,j;
   fs=fopen("usps.txt","r");
   fseek(fs,0,SEEK_END);
   int n=ftell(fs)/sizeof(struct Customer);
   cus=(struct Customer*)calloc(n,sizeof(struct Customer));
   rewind(fs);
   for(i=0;i<n;i++){
      fread(&cus[i],sizeof(struct Customer),1,fs);
   }
   fclose(fs);
   for(i=0;i<n;i++){
      for(j=i+1;j<n;j++){
      if(strcmp(cus[i].account_number,cus[j].account_number)<0){
         c1=cus[i];
         cus[i]=cus[j];
         cus[j]=c1;
      }
   }
   fs=fopen("usps.txt","w");

   }
   for(i=0;i<n;i++){
      printf ("id = %d name = %s Account=%s pin=%d Balance=%d\n", cus[i].id, cus[i].name,cus[i].account_number,cus[i].pin,cus[i].Balance);
      fwrite(&cus[i],sizeof(struct Customer),1,fs);
   }
   fclose(fs);
}
int login(){
   FILE *inf;       // read part
   char ac_no[20];
   struct Customer inp;
   int found=0,pin;
   inf = fopen ("usps.txt", "r");
   if (inf == NULL) {
      fprintf(stderr, "Error to open the file");
      return 2;
   }
   printf("Enter the Account number:");
   scanf("%s",ac_no);
   printf("Enter the pin:");
   scanf("%d",&pin);

   while(fread(&inp, sizeof(struct Customer), 1, inf)){
      if(!strcmp(inp.account_number,ac_no)){
         found=1;
         if(inp.pin==pin){
         printf ("id = %d name = %s Account=%s pin=%d Balance=%d\n", inp.id, inp.name,inp.account_number,inp.pin,inp.Balance);
         break;
         }
         else{
            printf("Incorrect credentials");
            break;
         }
      }
   }
   if(found!=1){
      printf("\nnot found");
   }
   fclose (inf);
   return 0;
}
int user(){
   int ch,withrwal,balance;
   printf("\n Enter the required number:");
   printf("\n1.See Balance");
   printf("\n2. Withdraw");
   printf("\n3. Deposit\n");
   scanf("%d",&ch);
   switch(ch){
      case 1 : seeBalance(); break;
      case 2 : withdraw(); break;
      case 3 : deposit(); break;
      default: return 0;}
}
int seeBalance(){
   FILE *inf;       // read part
   char ac_no[20];
   struct Customer inp;
   int found=0,pin;
   inf = fopen ("usps.txt", "r");
   if (inf == NULL) {
      fprintf(stderr, "Error to open the file");
      return 2;
   }
   printf("Enter the Account number:");
   scanf("%s",ac_no);
   printf("Enter the pin:");
   scanf("%d",&pin);

   while(fread(&inp, sizeof(struct Customer), 1, inf)){
      if(!strcmp(inp.account_number,ac_no)){
         found=1;
         if(inp.pin==pin){
         printf ("Balance remaining:%d",inp.Balance);
         break;
         }
         else{
            printf("Incorrect credentials");
            break;
         }
      }
   }
   if(found!=1){
      printf("\nnot found");
   }
   fclose (inf);
   return 0;
}
int withdraw(int balance){
   FILE *inf,*inu;       // read part
   char ac_no[20];
   struct Customer inp;
   int found=0,amount,pin;
   inf = fopen("usps.txt", "r");
   inu = fopen("temp.txt","w");
   if (inf == NULL) {
      fprintf(stderr, "Error to open the file");
      return 2;
   }
   printf("Enter the Account number to be updated:");
   scanf("%s",ac_no);
   printf("Enter the pin:");
   scanf("%d",&pin);

   while(fread(&inp, sizeof(struct Customer), 1, inf)){
      if(!strcmp(inp.account_number,ac_no)){
         found=1;
         if(inp.pin==pin){
         printf("Enter the amount to be deducted:");
         scanf("%d",&amount);
         inp.Balance-=amount;
         }
      }
      fwrite(&inp,sizeof(struct Customer),1,inu);
   }
   fclose(inu); fclose (inf);
   if(found!=1){
      printf("\nnot found");
   }
   else{
      inu = fopen("usps.txt", "w");
      inf = fopen("temp.txt","r");
      while(fread(&inp, sizeof(struct Customer), 1, inf)){
         fwrite(&inp, sizeof(struct Customer), 1, inu);
      }

      fclose(inu); fclose (inf);
   }
   return 0;
}
int deposit(int balance){
   FILE *inf,*inu;       // read part
   char ac_no[20];
   struct Customer inp;
   int found=0,amount,pin;
   inf = fopen("usps.txt", "r");
   inu = fopen("temp.txt","w");
   if (inf == NULL) {
      fprintf(stderr, "Error to open the file");
      return 2;
   }
   printf("Enter the Account number to be updated:");
   scanf("%s",ac_no);
   printf("Enter the pin:");
   scanf("%d",&pin);
   while(fread(&inp, sizeof(struct Customer), 1, inf)){
      if(!strcmp(inp.account_number,ac_no)){
         found=1;
         if(inp.pin==pin){
         printf("Enter the amount to be deposited:");
         scanf("%d",&amount);
         inp.Balance+=amount;
         }
      }
      fwrite(&inp,sizeof(struct Customer),1,inu);
   }
   fclose(inu); fclose (inf);
   if(found!=1){
      printf("\nnot found");
   }
   else{
      inu = fopen("usps.txt", "w");
      inf = fopen("temp.txt","r");
      while(fread(&inp, sizeof(struct Customer), 1, inf)){
         fwrite(&inp, sizeof(struct Customer), 1, inu);
      }

      fclose(inu); fclose (inf);
   }
   return 0;
}
int main () {
    int ch;
    printf("\n1.add an account:\n");
    printf("2.reset\n");
    printf("3.Display\n");
    printf("4.User\n");
    printf("5.Remove record\n");
    printf("6.sort by account in display\n");
    printf("7.sort by account in file\n");
    printf("8.sort by balance in display\n");
    printf("9.sort by balance in file\n");
    printf("10.Search\n");
    printf("11. Number of entries");
    printf("Enter your choice:");
    scanf("%d",&ch);
    switch(ch){
      case 1: add_account();break;
      case 2: reset();break;
      case 3: display();break;
      case 4: user(); break;
      //case 5: remove();break;
      case 6: sortdisn();break;
      case 7: sortfilen();break;
      case 8: sortdis();break;
      case 9: sortfile();break;
      case 10: search();break;
      case 11: count();break;
      default: 
    }
   return 0;
}
```
