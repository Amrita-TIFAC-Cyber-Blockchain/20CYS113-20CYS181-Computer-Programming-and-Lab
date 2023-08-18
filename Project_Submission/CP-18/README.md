# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)

```
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
#include <string.h>

char filename[100];

void errormsg(){
printf("\nOh no! Since you didn't enter a valid digit, our chance to go up the stairs was lost..\n(You have lost this game, but this is not the end.Try again, but don't forget to enter correct options.)\nThankyou for playing!");
}

void sep(){
printf("\n\n*****************************************************\n\n");
}


void conv( char filename[100];){
 FILE *file;             
   char ch;           
 file = fopen(filename, "r");
  while ((ch = fgetc(file)) != EOF) {
        printf("%c", ch); }
  fclose(file);
}

// this function used to get the user's answer
char getanswer() {
    char answer;
    printf("Your answer: ");
    scanf(" %c", &answer);
    return answer;
}
//this function is used to check the user's answer and count the score
int checkanswer(char answer, char correctanswer) {
    if (answer == correctanswer) {
        printf("Correct.\n");
        return 1;  // Return 1 if the answer is correct
    } else {
        printf("Incorrect. The correct answer is %c.\n", correctanswer);
        return 0;  // Return 0 f the answer is incorrect
    }
}

void main(){
        int opt;
for(int i=0;i<15;i++){
            for(int s=0; s<15-i ;s++){
                 printf(" "); }
          for(int j=0;j<=i;j++){
                  printf("* ");

         if(i==14&&j==14){printf("                                           Welcome to Castle Xcape");}



          }       printf("\n");}

                for(int x=0; x<15; x++){
                        printf("     xxxxxxxxxxxxxxxxxxxxx\n");}
char c;
char name[15];

printf("Hello there..I'm Ada Lovegood, the rightful heir to the throne..\nMy evil uncle has claimed the throne as his, after the passing of my father, King Richard.\nInorder to reclaim my right, I must find my father's legacy will- which is hidden \nsomewhere in the third storey of the castle.\nCan you help me on my journey of reclaiming my birthright?(y/n)\n");
scanf("%c",&c);
if (c=='n'||c=='N'){printf("Too bad! Hope you can help another time..\n"); return;}
else if (c=='Y'||c=='y'){printf("Thankyou kind person..before we start, can I know your name?\n");}
else if (c!='n'||c!='N'||c!='Y'||c!='y'){printf("Oh no! It seems like you've selected a wrong option, please enter a valid choice from next time..\n(reminder: please enter either the letter y or n)\n");return;}
scanf("%s",name);
printf("Nice to meet you %s! Come on, lets start our expedition..\n\n",name);

sep();


strcpy(filename,"c1.txt");
conv("%s",filename);

        scanf("%d",&opt);
        printf("\n");
        switch (opt){
                case 1: strcpy(filename,"c1_1.txt");
                        conv("%s",filename);
                      
                        break;
		case 2: strcpy(filename,"c1_2.txt");
                        conv("%s",filename);
                      
                        break;
                default: errormsg();
                         break;
	                 return;}
printf("\n");
strcpy(filename,"c@.txt");
conv("%s",filename);
//game
 int score;
  score=0;
char answer;
 printf("Welcome to Maths challenge\n");
printf("Guard:You will have three questions to answer.\nYou will be given three chances for each question.\nIf you go wrong in all the three chances then sorry you won't get the will\n");

//question1
printf("Question 1: The town is in danger.Warrior Franklin is the knight\n in shining armour.Everyone is sick and only a special\nherb can cure the sickness.Franklin needs to travel\na certain distance to get to the herb.He has to \ntravel for months to reach the destination.In the month \nof january,he travelled 50 km.By the month of february,\n he covered 100km.By march,he covered 150km.How much total \ndistance he covered till month of may? \n");
    printf("option a:400\n");
    printf("option b:350\n");
    printf("option c:250\n");
    printf("option d:200\n");
 do {
        answer = getanswer();
        if (answer == 'a' || answer == 'b' || answer == 'c' || answer == 'd') {
            break;  // if user selects Valid option ,exits the loop
        } else {
            printf("Invalid option. Please choose a valid option!!\n");
        }
    } while (1);

    score += checkanswer(answer, 'c');

//question2
printf("Question 2:If 2+2=6,3+3=11,4+4=18,then find 6+6=?\n");
    printf("option a:38\n");
    printf("option b:36\n");
    printf("option c:34\n");
    printf("option d:15\n");
 do {
        answer = getanswer();
        if (answer == 'a' || answer == 'b' || answer == 'c' || answer == 'd') {
            break;  // if user selects Valid option ,exits the loop
        } else {
            printf("Invalid option. Please choose a valid option!!\n");
        }
    } while (1);

    score += checkanswer(answer, 'a');

//question3
printf("Question 3: Evaluate the expression 8+10/5-3\n");
    printf("option a:4\n");
    printf("option b:5\n");
    printf("option c:6\n");
    printf("option d:7\n");
 do {
        answer = getanswer();
        if (answer == 'a' || answer == 'b' || answer == 'c' || answer == 'd') {
            break;  // if user selects Valid option ,exits the loop
        } else {
            printf("Invalid option. Please choose a valid option!!\n");
        }
    } while (1);

    score += checkanswer(answer, 'd');
    

 if (score==0){
     printf(" You scored 0 out of 3 questions.\n");
     printf("Oh! No You have lost this game.");
     
 }
 else{
     printf(" You scored %d out of 3 questions.\n", score);
 }

sep();

strcpy(filename,"c2.txt");
conv("%s",filename);


scanf("%d",&opt);
        if (opt==1){
strcpy(filename,"c2_1.txt");
conv("%s",filename); 
}
	if (opt==2){
strcpy(filename,"c2_2.txt");
conv("%s",filename); 
}
	if (opt!=1&&opt!=2){
errormsg(); 
}
       // rock paper scissors
    char options[] = {'r', 'p', 's'};
    char player, boy;
    int rounds;
    srand(time(NULL));
    printf("Andrew: Hello there new visitor.Your task for today will be to enter into a tremendous game of rock, paper, and scissors with me.\n");
    printf("Let's start the game.\n");
    printf("The rules of the game my friend are quite simple.\n");
    printf("Enter 'r' for ROCK, 'p' for PAPER, and 's' for SCISSORS: ");
    printf("\nTick-tock, the time is running out.\n");
    for (rounds = 1; rounds <= 3; rounds++)
    {
        printf("Your Round %d begins now.\n", rounds);
        scanf(" %c", &player);
        if (player != 'r' && player != 'p' && player != 's')
        {
            printf("Oh man, the entered option is invalid. Please enter a correct option. Come on, let's try again.\n");
            rounds--;
        }
        else
        {
            boy = options[rand() % 3];
            if (player == boy)
            {
                printf("It's a draw!\n");
            }
            else if ((player == 'r' && boy == 'p') ||
                     (player == 'p' && boy == 's') ||
                     (player == 's' && boy == 'r'))
            {
                printf("Oh no! You have lost the game!You wont get the will\n");
		
            }
            else
            {
                printf("Congratulations! You have won the game!\n");
            }
        }
        
        printf("Ada: %c, Cousin brother: %c\n", player, boy);
    }
    printf("Oh your chances for this game have ended my friend!!Hope I never see you again!!\n\n");	

sep();

strcpy(filename,"c3.txt");
conv("%s",filename); 

scanf("%d",&opt);
        switch (opt){
		case 1:
strcpy(filename,"c3_1.txt");
conv("%s",filename); 
break;
                case 2: 
strcpy(filename,"c3_2.txt");
conv("%s",filename); 
break;
                default: errormsg();
                         break;}

printf("Grandmother: I heard from Andrew that you guys are searching for the legacy will..\nI'll help you find it if you can solve my riddles..\n");
//riddle
char ans1[50];
    int cmp, count = 0;

    printf("Grandmother: You will have three questions to answer.\nYou will be given three chances for question 1.\nIf you go wrong in all three chances, then sorry you won't get the will.\nFor the other two questions, you will get one chance.\n");
    printf("Question 1: A guy got an anonymous letter with a clue below it which when decoded will reveal her name. The clue is 'Third of august;Fourth of February;Second of May;Third of December;Sixth of October'. Find her name.\n");
    printf("Enter the name in all capital letters\n");
    for (int i = 0; i < 3; i++) {
        printf("This is your chance %d: ", i + 1);
        scanf("%s", ans1);
        cmp = strcmp(ans1, "GRACE");
        if (cmp == 0) {
            printf("The answer is correct!!\n");
            break;
        } else {
            count = count + 1;
            continue;
        }
    }

    if (count == 3) {
        printf("Sorry! You answered wrong in all attempts.\nYou won't get the will.\n");
        return -1;
    } else {
        printf("Question 2: One of the three colored buttons (Yellow;Blue;Purple) will set you free, the other two will lock you forever. The clue given is [nte rbu lup otp]. Which button should he press to escape?\n");
        printf("Option 1: Blue\nOption 2: Purple\nOption 3: Yellow\n");
        printf("Choose (1/2/3): ");
        int opt;
        scanf("%d", &opt);
        if (opt == 1) {
            printf("Wrong answer.\n");
        } else if (opt == 2) {
	printf("The answer is correct!!\n");}}
            
			printf("Question 3: Maya lives with her parents in India. Maya went missing on a Saturday when his parents went out for dinner. The police were called and the helpers were questioned.\nHelper 1 said 'I was packing Maya's bag for school the next day'.\nHelper 2 said 'I spent the whole evening cleaning the kitchen'.\nHelper 3 said 'I was cooking and listening to music'.\nWho kidnapped Maya?\n");
    printf("Option 1: Helper 2\nOption 2: Helper 3\nOption 3: Helper 1\n");
    printf("Choose (1/2/3): ");
    scanf("%d", &opt);

    if (opt == 1) {
        printf("Your answer is wrong.\n");
    } else if (opt == 2) {
        printf("Your answer is wrong.\n");
    } else if (opt == 3) {
        printf("Your answer is right..\n\n\n* Grandma:Well then, good luck my dears...Oh, and   *\n* don't forget to open the left room..              *\n");
    }

sep();

printf("(With help from grandmother, you and Ada reach the 3rd storey and open the left door, and succeed in finding the legacy will..With your help, Ada became the ruler she was born to be..\n\n\nThankyou for playing!\nCredits:\nAmita\nMeera\nParvathi\nSri Lakshmi ");
}
```
