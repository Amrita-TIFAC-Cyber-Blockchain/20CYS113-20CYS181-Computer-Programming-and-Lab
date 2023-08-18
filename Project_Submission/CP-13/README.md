# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)

```
/*
 * Amrita Vishwa Vidyapeetham
 * TIFAC-CORE in Cyber Security
 * 20CYS181 - Computer Programming Lab Project
 * Movie Ticketing system
 * Authors: Charan K, Midhrujayan K, R M Naren Adithya, Ramraj S
 * Created Date: 28-June-2023
 * Updated Date: 27-July-2023  
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct MovieDetails{
	char name[100];
	int code;
	char strCode[8];
}movie[5];

void display(FILE *file) 
{
  	char ch;
	while ((ch = fgetc(file)) != EOF)
  	{
  		if (ch!=';')
    		printf("%c", ch);
    		else
    		printf(" ");
  	}
}


void bookTicket(int cd)
{
	char mov[100]={0};
	for (int i=0; i<5; i++)
	{
		if (movie[i].code == cd)
		{
			strncpy(mov, movie[i].strCode,8);	
		}
	}
	FILE *fp, *booking;
	int number,i,n;
	char line[27];
	char line2[20];
	char booking_id[7];
	printf("The file opened is %s\n",mov);
	// Open the file in read mode
  	fp = fopen(mov, "r+");
  	if (fp == NULL) {
    		printf("No such movie exists\n");
  	}
 	else{
     	display(fp);
		// you should move the cursor back to starting
		rewind(fp);
  		// Get the two digit number from the user
  		printf("Enter number of tickets you would like to book\n");
  		scanf("%d", &n);
  		int seats[n];
  		printf("Enter the seats you would like to book: ");
  		for (int k=0; k<n; k++)
  		{
   			scanf("%d", &seats[k]);
 		} 	
 		for (int k=0; k<n; k++)
 		{
 			while (seats[k]==00 || seats[k]==10 || seats[k]==20 || seats[k]==30 || seats[k]<0 || seats[k]>40)
 			{
 				printf("\nPlease enter a valid seat number instead of %d\n", seats[k]);
 				scanf("%d", &seats[k]);
 			}
 		}	
 		char movie[4];
 		strncpy(movie, mov, 4);
 		char abc[20], chek [20];
  		// Loop through each line in the file
  		while (fgets(line, 27, fp)) {
  		// Check if the two digit number is in the line
   			for (i = 0; i < 27; i++) {
      				for (int k=0; k<n; k++){
      					if (line[i] == seats[k] / 10 + '0' && line[i + 1] == seats[k] % 10 + '0') {
      					
        				booking = fopen("booking.txt", "r+");
        				if (booking == NULL) 
        				{
   						printf("No such movie exists\n");
  					}
        				booking_id[0]=(seats[k]/10 +'0');
    					booking_id[1]=(seats[k]%10 +'0');
					booking_id[2]= cd/1000+'0';			
        				booking_id[3]= (cd%1000)/100+'0';
        				booking_id[4]= (cd%1000)/10+'0';
        				booking_id[5]= cd%10+'0';
        				booking_id[6]= '\n';
        				char id[7];
        				strncpy(id, booking_id, 7);
    					while (fgets(line2, 13, booking))
    					{
    						for (int i=0; i<13; i++)
        					{
        					chek[i]='\0';
        					}
    						strcat(chek,"BOOKING_");
    						strcat(chek,mov);
    						for (int i=12; i<16; i++)
        					{
        					chek[i]='\0';
        					}
        					strcat(chek,":\n");
        					//line 2 and chek are the same and yet strncmp returns false
    						if (strncmp(chek,line2,13)==0)
    						{
    							printf("\nsuccess\n");
    							fputs(id, booking);
    						}
    						printf("%s", line2); 
    					
    					}
    					printf("\n%s", chek); 
    					fclose(booking);
    					
        				// Replace the number with XX
        				
        				line[i] = 'X';
        				line[i + 1] = 'X';

        				// Write the line back to the file
        				fseek(fp, -26, SEEK_CUR);
        				fputs(line, fp);
        				
      					}
       				}     
      			}
    		}
    	  
 
  		// Close the file
  		fclose(fp);
 	}
}

void cancelTicket(char booking_id[], int cd)
{
	FILE *fp = fopen("booking.txt", "r+");
	char mov[100]={0};
	for (int i=0; i<5; i++)
	{
		if (movie[i].code == cd)
		{
			strncpy(mov, movie[i].strCode,8);	
		}
	}
	FILE *fp2;
	// Open the file in read mode
  	fp2 = fopen(mov, "r+");
	char line[30], line2[30];
	char *seat, *b_id; 
	char snum[2];
	while(fgets(line, 30, fp))
	{
		snum[0]=0;
		snum[1]=0;
		fgets(line2, 30, fp2);
		seat = strtok(line, ":");
		b_id = strtok(NULL, ":");
		if (strcmp(b_id, booking_id)==0)
		{
			for (int i=4; i<10; i++)
			{
				line[i]='\0';
			}
			fseek(fp, -6, SEEK_CUR);
			fputs(line, fp);
		}
		snum[0] = *seat;
		snum[1] = *++seat;
		for (int i = 0; i < 26; i++) {
		if (snum[1]<'9')
		{
		if (line[i] == 'X' && line[i + 1] == 'X' && line[i+3]==snum[0]+1 && line[i+4]==snum[1]+1) {
		        {		line[i] = 0;
        				line[i + 1] = snum[1];
        	}}
        	else if(i>=23)
        	{
        		if (line[i] == 'X' && line[i + 1] == 'X' && line[i-3]==snum[0]-1 && line[i-2]==snum[1]-1)
        		{line[i] = 0;
        				line[i + 1] = snum[1];}
        	}
        	fseek(fp, -26, SEEK_CUR);
        	fputs(line, fp);
        				
        	
	}
	fclose(fp);
	fclose(fp2);
	printf("ticket cancelled");
}
}
}

void listMovies()
{
	printf("Screening now:\n");
	for( int i = 0; i<5; i++)
	{
		printf("%s: %d\n", movie[i].name, movie[i].code);
	}
}

int main()
{
	strncpy(movie[0].name, "The Legend", strlen("The Legend"));
	movie[0].code = 1000;
	strncpy(movie[0].strCode, "1000.txt",8);
	
	strncpy(movie[1].name, "Veera Simha Reddy", strlen("Veera Simha Reddy"));
	movie[1].code = 1001;
	strncpy(movie[1].strCode, "1001.txt",8);

	strncpy(movie[2].name, "Vivegam", strlen("Vivegam"));
	movie[2].code = 1002;
	strncpy(movie[2].strCode, "1002.txt",8);

	strncpy(movie[3].name, "Varisu", strlen("Varisu"));
	movie[3].code = 1003;
	strncpy(movie[3].strCode, "1003.txt",8);

	strncpy(movie[4].name, "Adipurush", strlen("Adipurush"));
	movie[4].code = 1004;
	strncpy(movie[4].strCode, "1004.txt",8);	

	int option;
	printf("Welcome to BookYourShow.\n");
	do{
		printf("Please choose what you would like to do.\n");
		printf("1. Book Tickets.\n");
		printf("2. Cancel Tickets.\n");
		printf("3. View list of movies.\n");
		printf("4. Exit BookYourShow.\n");
		scanf("%d", &option);

		switch (option)
		{
			case 1:
				listMovies();
				int movcode;
				printf("Choose movie that you would like to watch using movie code(4-digit number after :)\n");
				scanf("%d", &movcode);
				while (movcode<1000 || movcode>1005)
				{
					printf("Invalid movie code, please re-enter a valid movie code.\n");
					scanf("%d", &movcode);
				}
				bookTicket(movcode);
				break;
			case 2:
				char bookid[6]; 
				int code;
				cancelTicket(bookid, code);
				break;
			case 3:
				listMovies();
				break;
			case 4:
				printf("Thank you for visiting us!");
				break;
			default:
				printf("Invalid Option, please select a option from 1 to 4.");
				break;
		}
	}while (option!=4);
	return 0;
}

```
