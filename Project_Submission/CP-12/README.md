# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)

```
/*
 * Amrita Vishwa Vidyapeetham
 * TIFAC-CORE in Cyber Security
 * 20CYS181 - Computer Programming Lab Project
 * Encryption Decryption calculator
 * Authors: Chitla Vyshali, C N Hansica, M Sanju,T Sree Chandan
 * Created Date: 28-June-2023
 * Updated Date: 28-July-2023  
 */

#include <stdio.h>
#include <string.h>
#define MAX_LENGTH 500


//Declaration of plain text and cipher text
char cipherText[100];
char plainText[100];

//Function for encryption using permutation cipher
int PermutationEncryption() {
    int n, i, j, x;
    int y = 0;
    FILE *file;
   
    printf("Permutation cipher encrypts and decrypts text based on length of plain text.\n");
    printf("PLease enter a key of length which is a factor of the text length.\n");
    printf("Enter the length of the key:\n");
    scanf("%d", &n);
    int key[n];
    char plaintext[50], ciphertext[50];
    printf("Enter the key for Encryption:\n");
    for (i = 0; i < n; i++) {
        printf("%d :", i + 1);
        scanf("%d", &key[i]);
    }
    for (i = 0; i < n; i++) {
        key[i] = key[i] - 1;
    }
    printf("Enter the plain text without spaces:\n");
    scanf("%s", plaintext);
    x = strlen(plaintext);
    if (x % n != 0) {
        printf("Error: The length of the plain text is not divisible by the key length.\n");
    } else {
        for (i = 0; i < x; i++) {
            j = i % n;
            j = key[j];
            j = j + (y * n);
            ciphertext[i] = plaintext[j];
            if (i % n == n - 1) {
                y++;
            }
        }
        ciphertext[x] = '\0';
        printf("Encrypted text: %s\n", ciphertext);
    }
    file = fopen("output.txt", "a");
        if (file == NULL) {
            printf("Error opening the file.\n");
        return 0;
        }
	
        
	// Write the plaintext, ciphertext, and key to the file
        fprintf(file, "Plaintext: %s\n", plaintext);
        fprintf(file, "Ciphertext: %s\n", ciphertext);
        fprintf(file, "Key: ");
        
	for (i = 0; i < n; i++) {
            fprintf(file, "%d ", key[i]+1);
        }
        fprintf(file, "\n");

        // Close the file
        fclose(file);

        printf("Data written to the file successfully.\n");
    }

//Function for decryption using permutation cipher
int PermutationDecryption() {
    int n, i, j, x;
    int y = 0;
   
            printf("Permutation cipher encrypts and decrypts text based on length of plain text.\n");
            printf("PLease enter a key of length which is a factor of the text length.\n");
    printf("Enter the length of the key:\n");
    scanf("%d", &n);
    int key[n];
    char plaintext[50], ciphertext[50];
    printf("Enter the key for Decryption:\n");
    for (i = 0; i < n; i++) {
        printf("%d :", i + 1);
        scanf("%d", &key[i]);
    }
    for (i = 0; i < n; i++) {
        key[i] = key[i] - 1;
    }
    printf("Enter the cipher text without spaces:\n");
    scanf("%s",&ciphertext);
    x = strlen(ciphertext);
    if (x % n != 0) {
        printf("Error: The length of the cipher text is not divisible by the key length.\n");
    } else {
        for (i = 0; i < x; i++) {
            j = i % n;
            j = key[j];
            j = j + (n * y);
            plaintext[j] = ciphertext[i];
            if (i % n == n - 1) {
                y++;
            }
        }
        plaintext[x] = '\0';
        printf("Decrypted text: %s\n", plaintext);
}
 FILE *file;
 file = fopen("output.txt", "a");
        if (file == NULL) {
            printf("Error opening the file.\n");
        return 0;
        }
 // Write the plaintext, ciphertext, and key to the file
        fprintf(file, "Plaintext: %s\n", plaintext);
        fprintf(file, "Ciphertext: %s\n", ciphertext);
        fprintf(file, "Key: ");
        for (i = 0; i < n; i++) {
            fprintf(file, "%d ", key[i]+1);
        }
        fprintf(file, "\n");

        // Close the file
        fclose(file);

        printf("Data written to the file successfully.\n");
    }

//Function for encryption using caesar cipher
int caesarencryptmessage(char message[100], int key) {
    int i;
    char c, k,ct[100];
    for (i = 0; i < strlen(message); i++) {
        c = message[i];
        if (c >= 'A' && c <= 'Z') {
            k = ((c - 'A' + key) % 26 + 'A');
        } else if (c >= 'a' && c <= 'z') {
            k = ((c - 'a' + key) % 26 + 'a');
        } else {
            k = c;
        }

	  ct[i]=k;
    }
    
	ct[i]='\0';
        printf("%s",ct);
    
    printf("\n");
 FILE *file;
 file = fopen("output.txt", "a");
        if (file == NULL) {
            printf("Error opening the file.\n");
        return 0;
        }
 // Write the plaintext, ciphertext, and key to the file
        fprintf(file, "Plaintext: %s\n", message);
        fprintf(file, "Ciphertext: %c\n",ct);
        fprintf(file, "Key:%d\n",key);
        
        fprintf(file, "\n");

        // Close the file
        fclose(file);

        printf("Data written to the file successfully.\n");
    }

//Function for decryption using caesar cipher
int caesardecryptmessage(char message[100], int key) {
    char c, k;
    printf("Decrypted message: ");
    for (int i = 0; i < strlen(message); i++) {
        c = message[i];
        if (c >= 'A' && c <= 'Z') {
            k = ((c - 'A' - key + 26) % 26 + 'A');
        } else if (c >= 'a' && c <= 'z') {
            k = ((c - 'a' - key + 26) % 26 + 'a');
        } else {
            k = c;
        }
        printf("%c", k);
    }
    printf("\n");
    FILE *file;
    file = fopen("output.txt", "a");
    if (file == NULL) {
        printf("Error opening the file.\n");
        return 0;
    }
    
    // Write the plaintext, ciphertext, and key to the file
    fprintf(file, "Plaintext: %s\n", message);
    fprintf(file, "Ciphertext: %s\n", message);
    fprintf(file, "Key: %d\n", key);

    // Close the file
    fclose(file);

    printf("Data written to the file successfully.\n");
    return 1;
}
		    
//Function for decryption using Substitution cipher
int Subencrypt() {
     char plaintext[100], ciphertext[100];
    char key[27] = "QWERTYUIOPASDFGHJKLZXCVBNM"; // substitution key
    int i, j;

    printf("Enter plaintext message: ");
    scanf("%s", plaintext);

    // encryption
    for (i = 0; plaintext[i] != '\0'; i++) {
        if ((plaintext[i] >= 'A' && plaintext[i] <= 'Z') || (plaintext[i] >= 'a' && plaintext[i] <= 'z')) {
            if (plaintext[i] >= 'A' && plaintext[i] <= 'Z') {
                j = plaintext[i] - 'A';
                ciphertext[i] = key[j];
            } else {
                j = plaintext[i] - 'a';
                ciphertext[i] = key[j];
                ciphertext[i] += 32; // convert to lowercase
            }
        } else {
            ciphertext[i] = plaintext[i];
        }
    }
    ciphertext[i] = '\0';

    printf("Encrypted message: %s\n", ciphertext);

 FILE *file;
 file = fopen("output.txt", "a");
        if (file == NULL) {
            printf("Error opening the file.\n");
        return 0;
        }
 // Write the plaintext, ciphertext, and key to the file
        fprintf(file, "Plaintext: %s\n", plaintext);
        fprintf(file, "Ciphertext: %s\n", ciphertext);
        fprintf(file, "Key: ");
        
            fprintf(file, "%s ", key);
        
        fprintf(file, "\n");

        // Close the file
        fclose(file);

        printf("Data written to the file successfully.\n");
    }


//Function for decryption using Substitution cipher
int Subdecrypt() {
    char ciphertext[100], plaintext[100];
    char key[27] = "QWERTYUIOPASDFGHJKLZXCVBNM"; // substitution key
    int i, j;

    printf("Enter ciphertext message: ");
    scanf("%s", ciphertext);

    // decryption
    for (i = 0; ciphertext[i] != '\0'; i++) {
        if ((ciphertext[i] >= 'A' && ciphertext[i] <= 'Z') || (ciphertext[i] >= 'a' && ciphertext[i] <= 'z')) {
            if (ciphertext[i] >= 'A' && ciphertext[i] <= 'Z') {
                j = 0;
                while (key[j] != ciphertext[i])
                    j++;
                plaintext[i] = 'A' + j;
            } else {
                j = 0;
                while (key[j] != (ciphertext[i] - 32))
                    j++;
                plaintext[i] = 'a' + j;
            }
        } else {
            plaintext[i] = ciphertext[i];
        }
    }
    plaintext[i] = '\0';

    printf("Decrypted message: %s\n", plaintext);

 FILE *file;
 file = fopen("output.txt", "a");
        if (file == NULL) {
            printf("Error opening the file.\n");
        return 0;
        }
 // Write the plaintext, ciphertext, and key to the file
        fprintf(file, "Plaintext: %s\n", plaintext);
        fprintf(file, "Ciphertext: %s\n", ciphertext);
        fprintf(file, "Key: ");
        
            fprintf(file, "%d ", key);
        
        fprintf(file, "\n");

        // Close the file
        fclose(file);

        printf("Data written to the file successfully.\n");
    }


//Function for encryption using Affine cipher
int Affineencrypt() {
    char text[100], textn[100];
    int a, b,i,count=0;
    printf("Enter the text to be encrypted: ");
    scanf("%s", text);
    printf("Enter the value of a: ");
    scanf("%d", &a);
    printf("Enter the value of b: ");
    scanf("%d", &b);
    for (int i = 0; text[i] != '\0'; i++) {
        count=count+1;
        if (text[i] >= 'A' && text[i] <= 'Z') {
            textn[i] = ((a * (text[i] - 'A') + b) % 26) + 'A';
        } else if (text[i] >= 'a' && text[i] <= 'z') {
            textn[i] = ((a * (text[i] - 'a') + b) % 26) + 'a';
        }
    }
   

printf("Encrypted text: ");
for (i = 0;i<count; i++) {
    printf("%c", textn[i]);}

    
 
}




int modInverse(int a, int m) {
    a = a % m;
    for (int x = 1; x < m; x++) {
        if ((a * x) % m == 1) {
            return x;
        }
    }
    return -1;
}

//Function for decryption using Affine cipher
void AffineDecrypt() {
    char text[100], textn[100];
    int i,a, b,count=0;
    printf("Enter the text to be decrypted: ");
    scanf("%s", text);
    printf("Enter the value of a: ");
    scanf("%d", &a);
    printf("Enter the value of b: ");
    scanf("%d", &b);

    int m = 26; // For English alphabets, m = 26 (number of letters in the alphabet)

    int a_inverse = modInverse(a, m);
    if (a_inverse == -1) {
        printf("Error: 'a' does not have an inverse modulo 26.\n");
        return;
    }

    for (i = 0; text[i] != '\0'; i++) {
        count=count+1;
        if (text[i] >= 'A' && text[i] <= 'Z') {
            textn[i] = (a_inverse * (text[i] - 'A' - b + 26) % 26) + 'A';
        } else if (text[i] >= 'a' && text[i] <= 'z') {
            textn[i] = (a_inverse * (text[i] - 'a' - b + 26) % 26) + 'a';
        }
    }
   printf("Decrypted text: \n");
for (i = 0;i<count; i++) {
    printf("%c", textn[i]);}

 
    printf("\n");
}





int main() {
    int option;
    int mode;
    char message[100];
    int key;
    printf("Welcome to the encryption and decryption calculator.\n");
    printf("Please select one of the following ciphers:\n");
    printf("1 - Caesar Cipher\n");
    printf("2 - Substitution Cipher\n");
    printf("3 - Permutation Cipher\n");
    printf("4 - Affine Cipher\n");
    scanf("%d", &option);

    // Option represents the method chosen for utilization
    switch (option) {
        case 1:
            printf("1 - For Encryption\n");
            printf("2 - For Decryption\n");
            scanf("%d", &mode);

            switch (mode){
                case 1:
                    printf("Enter the message to be encrypted:\n");
                    scanf("%s", message);

                    printf("Enter the key or shift value:\n");
                    scanf("%d", &key);
                    key = key %26;

                    caesarencryptmessage(message, key);
                    break;
                case 2:
                    printf("Enter the message to be decrypted:\n");
                    scanf("%s", message);

                    printf("Enter the key or shift value:\n");
                    scanf("%d", &key);
                    key=key%26; 
		    caesardecryptmessage(message,key);
		    
                    break;
                default:
                    printf("Invalid mode selection.\n");
                    break;
            }
            break;
        case 2:
            printf("1 - For Encryption\n");
            printf("2 - For Decryption\n");
            scanf("%d", &mode);

            switch (mode) {
                case 1:
                    Subencrypt();
                    break;
                case 2:
                    Subdecrypt();
                    break;
                default:
                    printf("Invalid mode selection.\n");
                    break;
            }
            break;
        case 3:
            
	    
	    printf("1 - For Encryption\n");
            printf("2 - For Decryption\n");
            scanf("%d", &mode);

            switch (mode) {
                case 1:
                    PermutationEncryption();
                    break;
                case 2:
                    PermutationDecryption();
                    break;
                default:
                    printf("Invalid mode selection.\n");
                    break;
            }
            break;
        
        case 4:
            printf("1 - For Encryption\n");
            printf("2 - For Decryption\n");
            scanf("%d", &mode);
            switch(mode){
            case 1:
    
		 Affineencrypt();

                    break;
            case 2:
            AffineDecrypt();
		break;

	    
        default:
            printf("Please select a valid option.\n");
            	break;
    }
    break;
    }
    return 0;
    }

```
