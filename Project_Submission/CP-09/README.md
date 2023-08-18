# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)

```
#include <stdio.h>
#include <string.h>
#include <ctype.h>
#include <stdbool.h>
#include <stdlib.h>
#include <unistd.h>
#include <openssl/evp.h>

void calculate_md5(const char* message, unsigned char* digest) {
    EVP_MD_CTX* context = EVP_MD_CTX_new();
    EVP_DigestInit(context, EVP_md5());
    EVP_DigestUpdate(context, message, strlen(message));
    EVP_DigestFinal(context, digest, NULL);
    EVP_MD_CTX_free(context);
}

	enum type{
		website=1,
		app,
		mail
	}typechoice;

	union Account_Type{
		char website[20];
		char app[20];
		char mail[20];
	}type;

	struct Credentials{
		char username[20];
		char password[20];
	}credential;


	bool check_upper(char password[],int p_length)
	{
	    for (int i = 0;i<p_length; i++)
	    {
	        if (isupper(password[i]))
	        {return true;}
	   }
	    return false;
	}

	bool check_lower(char password[],int p_length)
	{
	    for (int i = 0;i<p_length; i++)
	    {
	        if (islower(password[i]))
	        {return true;}
	    }
	    return false;
	}

	bool check_digit(char password[],int p_length)
	{
	    for (int i = 0;i<p_length; i++)
	    {
	        if (isdigit(password[i]))
	        {return true;}
	    }
	    return false;
	}

	bool check_special(char password[],int p_length)
	{
	    for (int i = 0;i<p_length; i++)
	    {
	        if (ispunct(password[i]))
	        {return true;}
	    }
	    return false;
	}

	bool check_length(char password[])
	{
	    if (strlen(password) >= 8)
	    {return true;}
	    return false;
	}


	void decryption(char cipher[],char key[], char decrypted[])
	{
		int c_length=strlen(cipher);
		int k_length=strlen(key);
		char plain[c_length];
		int j=0;

		for(int i=0;i<c_length;i++)
		{
			plain[i]=(cipher[i]-key[j]+128)%128;
			j=(j+1)%k_length;
		}

		plain[c_length]= '\0';
		strcpy(decrypted,plain);

	}

	void encryption(char plain[], char key[], char encrypted[])
	{
	    int p_length = strlen(plain);
	    int k_length = strlen(key);
	    char cipher[p_length];
	    int j = 0;

	    for (int i = 0; i < p_length; i++)
	    {
	        cipher[i] = (plain[i] + key[j]) % 128;
	        j = (j + 1) % k_length;
	    }

	    cipher[p_length] = '\0';
	    strcpy(encrypted,cipher);
	}


	void Add_Password(char m_user[], char m_key[])
	{
		int p_length,u_length;

		FILE* userinfo;
		userinfo=fopen("userinfo.txt","a");
		
		printf("\t\t\t\t\t\t        1.Website\n\t\t\t\t\t\t        2.App\n\t\t\t\t\t\t        3.Mail\n\n");
		printf("\nEnter Your Choice : ");
		
		scanf("%d",&typechoice);
		
		switch(typechoice)
		{
			case 1:{
				system("clear");
					printf("\t\t\t\t\t\t\t\033[1;33mSecurePass");printf("\033[0m\n");
	    			printf("\t\t\t\t\t\t\033[1;37mPassword Managment System\n");
	    			printf("\n");

	    			printf("\t\t\t\t\t             \033[1;31mStore Password\n");printf("\033[0m");
	    			printf("\n\n\n");
	            printf("Enter Website : ");
			    scanf("%s",type.website);
			    fputs(type.website,userinfo);
				fputs(" ",userinfo);
			    break;
			       }
			case 2:{
				system("clear");
					printf("\t\t\t\t\t\t\t\033[1;33mSecurePass");printf("\033[0m\n");
	    			printf("\t\t\t\t\t\t\033[1;37mPassword Managment System\n");
	    			printf("\n");

	    			printf("\t\t\t\t\t             \033[1;31mStore Password\n");printf("\033[0m");
	    			printf("\n\n\n");

			   	printf("Enter App : ");
			   	scanf("%s",type.app);
			   	fputs(type.app,userinfo);
			 	fputs(" ",userinfo);
			   	break;
				    }
			case 3:{
				system("clear");
					printf("\t\t\t\t\t\t\t\033[1;33mSecurePass");printf("\033[0m\n");
	    			printf("\t\t\t\t\t\t\033[1;37mPassword Managment System\n");
	    			printf("\n");

	    			printf("\t\t\t\t\t             \033[1;31mStore Password\n");printf("\033[0m");
	    			printf("\n\n\n");

		        printf("Enter Mail : ");
			   	scanf("%s",type.mail);
			   	fputs(type.mail,userinfo);
				fputs(" ",userinfo);
			   	}		   
		}		

		printf("\nEnter Username : ");
		scanf("%s",credential.username);
		
		fputs(credential.username,userinfo);
		fputs(" ",userinfo);
		fputs(m_user,userinfo);
		fputs(" ",userinfo);
		
		printf("\nEnter Password : ");
		
		system("stty -echo");
		scanf("%s",credential.password);
		system("stty echo");

		printf("\n\n");

		p_length=strlen(credential.password);

		password_check(credential.password,p_length);

		fputs(m_key,userinfo);
		fputs(" ",userinfo);
		
		char encrypted[strlen(credential.password)];
		
		encryption(credential.password,m_key,encrypted);

		fputs(encrypted,userinfo);
		fputs("\n",userinfo);
		
		fclose(userinfo);
	}


int Display(char userusername[], char m_user[])
	{	FILE *disp;
		
		char ch,decryptedpass[30],userinfo[30][5][50],username[30],password[30];
		int i=0,k=0,display=0;

		disp=fopen("userinfo.txt","r");

		if (disp == NULL) {
        printf("\033[0;31mStore Passwords before trying to view\033[0m");
        return -1;
    }


		while((ch = getc(disp)) != EOF){
			fseek(disp, -1, SEEK_CUR);
			
			//type
			while((ch=getc(disp))!=' '){
				userinfo[i][0][k]=ch;
				k++;
			}
			userinfo[i][0][k] = '\0';
			k=0;

			//username
			while((ch=getc(disp))!=' '){
				userinfo[i][1][k]=ch;
				k++;
			}
			userinfo[i][1][k] = '\0';
			k=0;

			//m_user
			while((ch=getc(disp))!=' '){
				userinfo[i][2][k]=ch;
				k++;
			}
			userinfo[i][2][k] = '\0';
			k=0;

			//m_key
			while((ch=getc(disp))!=' '){
				userinfo[i][3][k]=ch;
				k++;
			}
			userinfo[i][3][k] = '\0';
			k=0;

			//password
			while((ch=getc(disp))!='\n'){
				userinfo[i][4][k]=ch;
				k++;
			}
			userinfo[i][4][k] = '\0';
			k=0;
		i++;
		}
		int m=0;
		for(int p=0;p<i;p++){
			if((strcmp(userinfo[p][1],userusername)==0)&&(strcmp(m_user,userinfo[p][2])==0)){

			printf("\033[0;32mWebsite/App/Mail\033[0m : %s\n",userinfo[p][m]);m+=3;
			printf("\033[0;32mKey\033[0m : %s\n",userinfo[p][m]);m++;

			decryption(userinfo[p][4],userinfo[p][3],decryptedpass);
			
			printf("\033[0;32mPassword\033[0m : %s\n",decryptedpass);

			m=0;

			printf("\n");

			display=1;
			}
		}

		return display;
	}


	void password_check(char password[],int length){
			int digit=1;

			while(!check_upper(password,length)||!check_lower(password,length)||!check_digit(password,length)||!check_special(password,length)||!check_length(password))
			{
			if(!check_upper(password,length)){
				printf("%d : Minimum One \033[0;31mUppercase\033[0m Character\n\n",digit);
				digit++;
			}
			if(!check_lower(password,length)){
				printf("%d : Minimum One \033[0;31mLowercase\033[0m Character\n\n",digit);
				digit++;
			}
			if(!check_digit(password,length)){
				printf("%d : Minimum One \033[0;31mDigit\033[0m\n\n",digit);
				digit++;
			}
			if(!check_special(password,length)){
				printf("%d : Minimum One \033[0;31mSpecial Character\033[0m\n\n",digit);
				digit++;
			}
			if(!check_length(password)){
				printf("%d : Minimum \033[0;31mLength 8\033[0m\n\n",digit);
				digit++;
			}
			digit=1;

			printf("\nEnter Password Again : ");

			system("stty -echo");
			scanf("%s",password);
			printf("\n");
			system("stty echo");
			printf("\n");
			
			length=strlen(password);
			}

		}

	bool isMasterUsernameExists(char username[], char userinfo[30][3][50], int count) {
	    for (int i = 0; i < count; i++) {
	        if (strcmp(username, userinfo[i][0]) == 0) {
	            return true;
	        }
	    }
	    return false;
	}

	bool isMasterUsernameMasterPasswordExists(char username[], char password[], char m_key[], char userinfo[30][3][50], int count) {
	    for (int i = 0; i < count; i++) {
	        if ((strcmp(username, userinfo[i][0]) == 0)&&(strcmp(password,userinfo[i][2])==0)) {
	            printf("\n\033[0;32mMaster\033[0m Key : %s\n",userinfo[i][1]);
	            //for (int i = 0; i < EVP_MD_size(EVP_md5()); i++) {
     			  // printf("%02x", password[i]);
    			//}
	            strcpy(m_key,userinfo[i][1]);
	            return true;
	        }
	    }
	    return false;
	}


	int data_from_master(char userinfo[30][3][50]){
		
		FILE* disp;
		disp=fopen("master.txt","r");

		int i=0,k=0;
		char ch;

		while((ch=getc(disp))!=EOF){
			fseek(disp,-1,SEEK_CUR);

		while((ch = getc(disp)) != EOF){
			fseek(disp, -1, SEEK_CUR);
		
		//username
			while((ch=getc(disp))!=' '){
				userinfo[i][0][k]=ch;
				k++;
			}
			userinfo[i][0][k] = '\0';
			k=0;

		//key
			while((ch=getc(disp))!=' '){
				userinfo[i][1][k]=ch;
				k++;
			}
			userinfo[i][1][k] = '\0';
			k=0;

		//password
			while((ch=getc(disp))!='\n'){
				userinfo[i][2][k]=ch;
				k++;
			}
			userinfo[i][2][k] = '\0';
			k=0;
		i++;
			}
		}
		return i;
	}


	int main(){
		
		FILE* master;
		master=fopen("master.txt","a");

		char m_password[20];

		int m_choice,no_of_records,m_length;

		char m_user[20],m_key[20],encrypted_signup_pass[m_length],userusername[30];

		char ch,masterinfo[30][3][50];
		
		char encrypted_login_pass[strlen(m_password)];	

		system("clear");
		printf("\t\t\t\t\t\t\t\033[1;33mWelcome to SecurePass ");printf("\033[0m\n");
	    printf("\t\t\t\t\t\t\033[1;37mA Place to Store you passwords securly \n");printf("\033[0m\n");
	    printf("\n\n\n\n");
	    printf("20CYS181 - Computer Programming Lab\n");
		printf("Project : Password Manager With Strength Analyser\n");
		printf("Authors : Mukesh R, Krishna Moorthi, JP Hemanth Kumar, BM Sai Sathvik\n");
		printf("Start Date : 24-06-2023\n");
	    sleep(2);

	    system("clear");
	    printf("\t\t\t\t\t\t\t\033[1;33mSecurePass");printf("\033[0m\n");
	    printf("\t\t\t\t\t\t\033[1;37mPassword Managment System\n");
	    printf("\n");
		
		
		printf("\t\t\t\t\t\t\t \033[1;31mChoices\n");printf("\033[0m");
		printf("\t\t\t\t\t\t\t1.Sign-In\n");
		printf("\t\t\t\t\t\t\t2.Log-In\n");
		printf("Enter Your Choice : ");
		scanf("%d",&m_choice);

		system("clear");
	    printf("\t\t\t\t\t\t\t\033[1;33mSecurePass");printf("\033[0m\n");
	    printf("\t\t\t\t\t\t\033[1;37mPassword Managment System\n");
	    printf("\n");
		
		if(m_choice==1){
			//Sign-In
			printf("\t\t\t\t\t\t\t \033[1;31mSign-In\n\n");printf("\033[0m");
			//m_user should be unique. m_user should be stored in userinfo file so that for that particular m_user only those particular data can be recovered
			printf("Enter \033[0;32mMaster\033[0m Username: ");
			scanf("%s",m_user);
			printf("\n");
			no_of_records=data_from_master(masterinfo);
			while(isMasterUsernameExists(m_user,masterinfo,no_of_records)){
				printf("\033[0;31mUsername already exists\033[0m\n\n");
				printf("Enter \033[0;32mMaster\033[0m Username again : ");
				scanf("%s",m_user);
				printf("\n");
			}

		fputs(m_user,master);
		fputs(" ",master);

		printf("Enter \033[0;32mMaster\033[0m Key: ");
		scanf("%s",m_key);
		printf("\n");

		fputs(m_key,master);
		fputs(" ",master);

		printf("Enter \033[0;32mMaster\033[0m Password : ");
		system("stty -echo");
		scanf("%s",m_password);
		system("stty echo");
		printf("\n\n");

		m_length=strlen(m_password);	
		
		password_check(m_password,m_length);
		
		calculate_md5(m_password,encrypted_signup_pass);
		//encryption(m_password,m_password,encrypted_signup_pass);

		fputs(encrypted_signup_pass,master);
		fputs("\n",master);

		fclose(master);

		no_of_records=data_from_master(masterinfo);

		system("clear");
	    printf("\t\t\t\t\t\t\t\033[1;33mSecurePass");printf("\033[0m\n");
	    printf("\t\t\t\t\t\t\033[1;37mPassword Managment System\n");
	    printf("\n");

	    printf("\t\t\t\t\t\t\t \033[1;31mLog-In\n\n");printf("\033[0m");
			
			printf("Enter \033[0;32mMaster\033[0m Username : ");
			scanf("%s",m_user);
			
			printf("\nEnter \033[0;32mMaster\033[0m Password : ");
			
			system("stty -echo");
			scanf("%s",m_password);
			system("stty echo");
			printf("\n");
			
			calculate_md5(m_password,encrypted_login_pass);
			
			if(isMasterUsernameMasterPasswordExists(m_user,encrypted_login_pass,m_key,masterinfo,no_of_records)){
				printf("\n\033[0;32mCorrect Credentials\033[0m\n\n");
				sleep(1);
				}
			
			else{printf("\n\033[0;31mWrong Credentials\033[0m\n");
				return 0;
				}
		}

		else if(m_choice==2){
			no_of_records=data_from_master(masterinfo);

			printf("\t\t\t\t\t\t\t \033[1;31mLog-In\n\n");printf("\033[0m");
			
			printf("Enter \033[0;32mMaster\033[0m Username : ");
			scanf("%s",m_user);
			
			printf("\nEnter \033[0;32mMaster\033[0m Password : ");
			
			system("stty -echo");
			scanf("%s",m_password);
			system("stty echo");
			printf("\n");
			
			calculate_md5(m_password,encrypted_login_pass);
			
			if(isMasterUsernameMasterPasswordExists(m_user,encrypted_login_pass,m_key,masterinfo,no_of_records)){
				printf("\n\033[0;32mCorrect Credentials\033[0m\n\n");
				sleep(1);
				}
			
			else{printf("\n\033[0;31mWrong Credentials\033[0m\n");
				return 0;
				}
			}
		
		else{printf("Try Again\n");return 0;}

		system("clear");
		printf("\t\t\t\t\t\t\t\033[1;33mSecurePass");printf("\033[0m\n");
	    printf("\t\t\t\t\t\t\033[1;37mPassword Managment System\n");
	    printf("\n");

		printf("\t\t\t\t\t\t\t \033[1;31mOptions\n");printf("\033[0m");
	    printf("\t\t\t\t\t\t   1.Store Password\n");
	    printf("\t\t\t\t\t\t   2.Display Password\n");
	    printf("\t\t\t\t\t\t   3.Exit\n\n");

	    int choice;
	    int c;
	    fclose(master);
	    
	    do{
	    	system("clear");
			printf("\t\t\t\t\t\t\t\033[1;33mSecurePass");printf("\033[0m\n");
			printf("\t\t\t\t\t\t\033[1;37mPassword Managment System\n");
			printf("\n");

			printf("\t\t\t\t\t\t\t \033[1;31mOptions\n");printf("\033[0m");
			printf("\t\t\t\t\t\t   1.Store Password\n");
			printf("\t\t\t\t\t\t   2.Display Password\n");
			printf("\t\t\t\t\t\t   3.Exit\n\n");

			choice=1;
			if(choice>3 || choice<1){printf("\nInvalid Choice, Try again...\n");}

		    printf("\nEnter Your Choice : ");
		    scanf("%d",&choice);
		    printf("\n");
		    
		    switch(choice)
		    {
			    case 1:{
			    	system("clear");
					printf("\t\t\t\t\t\t\t\033[1;33mSecurePass");printf("\033[0m\n");
	    			printf("\t\t\t\t\t\t\033[1;37mPassword Managment System\n");
	    			printf("\n");

	    			printf("\t\t\t\t\t             \033[1;31mStore Password\n");printf("\033[0m");
		    		printf("\t\t\t\t\t\t    \033[1;31mType of Password\n");printf("\033[0m");
					Add_Password(m_user, m_key);
					break;
		            }
			    case 2:
			    {
		    		printf("Enter username you want to display for : ");
		    		scanf("%s",userusername);
		    		printf("\n");
					if(Display(userusername,m_user)==0){printf("\033[0;31mNo such records found\033[0m");}  
		    		fflush(stdout);	
					sleep(5);
			    }
		    }	    
	    }
	    while(choice!=3);
	    printf("\033[1;33mExiting...");printf("\033[0m\n");
	}

```
