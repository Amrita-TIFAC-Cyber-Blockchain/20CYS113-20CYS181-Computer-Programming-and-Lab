# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)


## Crypto Calculator
```
/*
 * Amrita Vishwa Vidyapeetham
 * TIFAC-CORE in Cyber Security
 * 20CYS181 - Computer Programming Lab Project
 * Encryption and Decryption Calculator
 * Authors: Amal Ritessh A P, Ananth R, Mukund K, Shravan Krishnan.G
 * Created Date: 28-June-2023
 * Updated Date: 09-July-2023  
 */

#include <stdio.h>
#include <string.h>
#define LENGTH 100

struct data{
    char encrypt[LENGTH];
    char decrypt[LENGTH];
}store;

void filestore(char text[LENGTH],char output[LENGTH],int menu_val){
    FILE *file;
    file=fopen("info.txt","a");
    
    //this is to add which cypher is used in file.
    switch (menu_val){
        case 1:
            fprintf(file,"Shift cypher:\n");
            break;
        case 2:
            fprintf(file,"Vigenere cypher:\n");
            break;
    }

    //this is used to add the user input value in file.
    fprintf(file,"Input : ");
    fprintf(file,text);
    fprintf(file,"\n");
    
    //this is used to add the output value in file.
    fprintf(file,"Output: ");
    fprintf(file,output);
    fprintf(file,"\n\n");

    fclose(file);
}


void shift_cypher(char text[LENGTH],int menu_val){
    int ed,key,loop=0;
    
    while(loop==0){
        printf("1 - encryption\n2 - decryption\nchoice: ");
        scanf("%d",&ed);

        switch (ed){
            case 1:
                //shift cypher encryption
                printf("enter key: ");
                scanf("%d",&key);
                for(int i=0;i<strlen(text);i++){
                    if((((int)text[i]+key)%122)<32){
                        store.encrypt[i]=(char)((((int)text[i]+key)%122)+32);    
                    }
                    else{
                        store.encrypt[i]=(char)(((int)text[i]+key)%122);
                    }
                }
                printf("encrypted text: \n");
                for(int i=0;i<strlen(text);i++){
                    printf("%c",store.encrypt[i]);
                }
                loop=1;
                filestore(text,store.encrypt,menu_val);
                break;
            case 2:
                //shift cypher decryption
                printf("enter key: ");
                scanf("%d",&key);
                for(int i=0;i<strlen(text);i++){
                    if(((int)text[i]-key)<32){
                        store.decrypt[i]=(char)((((int)text[i]-key-32+122)%122));
                    }
                    else{
                        store.decrypt[i]=(char)((((int)text[i]-key+122)%122));
                    }
                }
                printf("decrypted text: \n");
                for(int i=0;i<strlen(text);i++){
                    printf("%c",store.decrypt[i]);
                }
                loop=1;
                filestore(text,store.decrypt,menu_val);
                break;
            default:
                printf("invalid input");
                break;
        }
    }
}

void vigenere_cypher(char text[LENGTH],int menu_val){
    int ed,j=0,loop=0;
    char key[LENGTH];
    
    while(loop==0){
        printf("1 - encryption\n2 - decryption\nchoice: ");
        scanf("%d",&ed);
        
        switch (ed){
            case 1:
                //vigenere cypher encryption
                printf("enter key: ");
                scanf("%s",key);
                for(int i=0;i<strlen(text);i++){
                    if (j==strlen(key)){
                        j=0;
                    }
                    if(((int)text[i]+(int)key[j])%122<32){
                        store.encrypt[i]=(char)((((int)text[i]+(int)key[j])%122)+32);
                    }
                    else{
                        store.encrypt[i]=(char)(((int)text[i]+(int)key[j])%122);
                    }
                    j=j+1;
                }
                printf("encrypted text: \n");
                for(int i=0;i<strlen(text);i++){
                    printf("%c",store.encrypt[i]);
                }
                loop=1;
                filestore(text,store.encrypt,menu_val);
                break;

            case 2:
                //vigenere cypher decryption
                printf("enter key: ");
                scanf("%s",key);
                for(int i=0;i<strlen(text);i++){
                    if (j==strlen(key)){
                        j=0;
                    }
                    if ((((int)text[i]-(int)key[j])+122)%122<=64){
                        store.decrypt[i]=(char)((((int)text[i]-(int)key[j]+122-32)%122));    
                    }
                    else{
                        store.decrypt[i]=(char)((((int)text[i]-(int)key[j]+122)%122));
                    }
                    
                    j=j+1;
                }
                printf("decrypted text: \n");
                for(int i=0;i<strlen(text);i++){
                    printf("%c",store.decrypt[i]);
                }
                loop=1;
                filestore(text,store.decrypt,menu_val);
                break;

            default:
                printf("invalid input");
                break;
        }
    }
}

int main(){
    char text[LENGTH];
    int menu_val,key,loop=0;

    printf("\nEnter the text/sentence: \n");
    gets(text);
    
    while(loop==0){
        printf("\n1 - shift cypher\n2 - vigenere cypher\nchoice: ");
        scanf("%d",&menu_val);
        
        switch (menu_val){
            case 1:
                shift_cypher(text,menu_val);
                loop=1;
                break;
            case 2:
                vigenere_cypher(text,menu_val);
                loop=1;
                break;
            default:
                printf("invalid input");
        }
    }
}
```
