# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)

## Terminal based Hangman

```
/*
 * Amrita Vishwa Vidyapeetham
 * TIFAC-CORE in Cyber Security
 * 20CYS181 - Computer Programming Lab Project
 * Terminal based Hangman
 * Authors: Adhithya N S, Anaswara Suresh M K, C S Amritha, R Sruthi
 * Created Date: 28-June-2023
 * Updated Date: 05-July-2023  
 */

#include<stdio.h>
#include<string.h>
#include<stdlib.h>
#include<time.h>
#define MAX_LINE_LENGTH 200

struct wordandhints{
    char random_word[100];
    char hint[256];
};

void read(struct wordandhints wh[]){
    FILE *file;
    file = fopen("wordhint.txt", "r");
    char line[256];
    for(int i=0;i<20;i++){
        fgets(line, sizeof(line), file);
        strtok(line, "\n");
        strcpy(wh[i].random_word, line);
        fgets(line, sizeof(line), file);
        strtok(line, "\n");
        strcpy(wh[i].hint, line);
    }
}
void displayGame(int wrongmove){
    switch(wrongmove){
        case 0:
		printf("\033[1;33m  ___\n");
            	printf("  |   |\n");
            	printf("      |\n");
            	printf("      |\n");
            	printf("      |\n");
            	printf("      |\n");
            	printf("__|\n");
            	break;
	case 1:
            	printf("  ___\n");
            	printf("  |   |\n");
            	printf("  O   |\n");
            	printf("      |\n");
            	printf("      |\n");
            	printf("      |\n");
            	printf("__|\n");
            	break;
        case 2:
            	printf("  ___\n");
            	printf("  |   |\n");
            	printf("  O   |\n");
            	printf("  |   |\n");
            	printf("      |\n");
            	printf("      |\n");
            	printf("__|\n");
            	break;
        case 3:
		printf("  ___\n");
            	printf("  |   |\n");
            	printf("  O   |\n");
            	printf(" /|   |\n");
            	printf("      |\n");
            	printf("      |\n");
            	printf("__|\n");
            	break;
        case 4:
            	printf("  ___\n");
            	printf("  |   |\n");
            	printf("  O   |\n");
            	printf(" /|\\  |\n");
            	printf("      |\n");
            	printf("      |\n");
            	printf("__|\n");
            	break;
        case 5:
            	printf("  ___\n");
            	printf("  |   |\n");
            	printf("  O   |\n");
            	printf(" /|\\  |\n");
            	printf(" /    |\n");
            	printf("      |\n");
            	printf("__|\n");
            	break;
        case 6:
            	printf("  ___\n");
            	printf("  |   |\n");
            	printf("  O   |\n");
            	printf(" /|\\  |\n");
            	printf(" / \\  |\n");
           	printf("      |\n");
            	printf("__|\n");
		printf("\033[1;31mOHH NOO!! YOU DIED\n");
		break;

    }
}
int is_letter_in_word(char word[],char len){
    char letter;
    char uscore[len];
    int wrongmoves=0;
    for (int i=0;i<len;i++){
        uscore[i]='_';
    }
    uscore[len]='\0';
    printf("Word:%s\n", uscore);
    while(wrongmoves<7){
            if(strcmp(word,uscore)!=0){
             printf("Enter the letter:\n");
             scanf(" %c", &letter);
             int flag=0;
              for (int j=0;j<len;j++){
                if(word[j]==letter && uscore[j]=='_'){
                        uscore[j]=letter;
                        flag=1;
                }
              }
              if(flag!=1){
                        displayGame(wrongmoves);
                        wrongmoves=wrongmoves+1;
                }
             printf("Word:%s\n", uscore);
            }
            else{
		    printf("\033[1;32mHURREEYYY!! YOU WON THE GAME\n"); 
		  
                    break;
            }
    }
    printf("\n");
    printf("Correct Word:%s\n",word);
    return wrongmoves;
}

int randomindex(){
    int num;
    srand(time(NULL));
    num = rand()%20;
    return num;
}

void scorelist(int score,char name[]){
	char line[MAX_LINE_LENGTH];
	FILE *file1;
        char filename[] = "highscore.txt";
        file1=fopen(filename, "a");
        fprintf(file1, "%s:%d\n", name, score);
	printf("\n\033[1;35m< SCORE LIST >\n");
	fclose(file1);
        file1 = fopen(filename, "r");
        while (fgets(line, MAX_LINE_LENGTH, file1) != NULL) {
		line[strcspn(line, "\n")] = '\0';
                char *name = strtok(line, ":");
                char *score_str = strtok(NULL, ":");
                int score = atoi(score_str);
                printf("# %s - %d\n", name, score);
	}
	fclose(file1);
}
int main(){

    int index;
    char letter;
    int wrongmv,score;
    struct wordandhints wh[10];

    read(wh);
    printf("\033[1;33mWelcome!!!\n");
    printf("\033[1;36mLet's Play Hangman\n");
    char name[100];
    printf("Enter name: ");
    fgets(name, sizeof(name), stdin);
    name[strcspn(name, "\n")] = '\0';
    index=randomindex();
    printf("Hint:%s \n",wh[index].hint);
    int leng;
    leng=strlen(wh[index].random_word);
    wrongmv=is_letter_in_word(wh[index].random_word,leng);
    score=70-(wrongmv*10);
    printf("\033[0;34mYOUR SCORE:");
    printf("\033[1;33m%d\n",score);
    scorelist(score,name);
    return 0;
}

```
