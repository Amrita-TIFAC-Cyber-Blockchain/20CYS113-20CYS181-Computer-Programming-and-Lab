# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)

## Matrix Calculator

```
/*
 * Amrita Vishwa Vidyapeetham
 * TIFAC-CORE in Cyber Security
 * 20CYS181 - Computer Programming Lab Project
 * Matrix Calculator
 * Authors: AgilPrasannaa P, Deepak Kumar S, Mothe Anurag Reddy
 * Created Date: 28-June-2023
 * Updated Date: 06-July-2023
 */

#include <stdio.h> // Includes all the print and scan functions
#include<math.h>  // For calculating the cofactor matrix
#include<ctype.h> // To use the function toupper
#include<time.h>  // Used for timestamp in time.txt


//User Defined Function Declaration
void readMatrix(int array[10][10], int rows, int columns);
void printMatrix(int array[10][10], int rows, int columns, FILE *file);
void matrixScalarMultiply(int array[10][10], int scalar, int rows, int columns, FILE *file);
void matrixMultiply(int arrayone[10][10], int arraytwo[10][10], int rowsA, int columnsA, int columnsB, FILE *file);
void cofactor(float [10][10], float, FILE *file);
float determinant(float [10][10], float);
void transpose(float [10][10], float [10][10], float, FILE *file);
int main()
{

    int i, j, k; //used in for loops

    int matrixA[10][10]; // initialized at 10 just to have it initialized
    int matrixB[10][10];
    int rowA, colA;
    int rowB, colB;
    int operation;       //Used in switch statements
    char again = 'Y';    //To Access the options(operations) again
    int scalar = 0;
    time_t currentTime;
    struct tm *timeInfo; // Structure for the file
    char buffer[80];

    // Get the current time
    time(&currentTime);
    timeInfo = localtime(&currentTime);

    // Format the time as a string
    strftime(buffer, sizeof(buffer), "%Y-%m-%d %H:%M:%S", timeInfo);

    // Open the file in append mode
    FILE *file = fopen("time.txt", "a");
    if (file == NULL) {
        printf("Unable to open the file.\n");
        return 1;
    }


    while(again=='Y')
    {

    //This is the operation menu just type A, B, C or D to calculate
        printf("\n\t\t\t\t\t\tWELCOME TO THE MATRIX CALCULATOR\n");
        printf("\t\t\t\t\t\t~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~");
        printf("\nOperation Menu\n");
        printf("==============\n");
        printf("\t1. to Scalar Multiply\n");
        printf("\t2. to Multiply two matrices (Matrix Multiplication)\n");
        printf("\t3. to find inverse of a matrix\n");
        printf("Enter your choice: ");
        scanf(" %d", &operation);


        switch (operation)
        {

        case 1:

            fprintf(file,"%s\n",buffer);   // To time stamp the scalr option results
            printf("\nEnter the scalar: ");
            scanf("%d", &scalar);
            fprintf(file,"The scalar is : %d\n",scalar);
            printf("\nThe scalar is: %d ", scalar);


            printf("\nEnter the #rows and #cols for matrix A: ");
            scanf("%d%d", &rowA, &colA);

            printf("\n\tEnter elements of Matrix A a (%d x %d) matrix.\n", rowA, colA); // With the %d we remember the user the dimensions of the array
            readMatrix(matrixA, rowA, colA);
            printf("\n\tMatrix A\n\n");
            fprintf(file, "\n\t\tMatrix A\n\n");
            printMatrix(matrixA, rowA, colA, file);

            printf("\nThe scalar multiplication between matrix A * (%d) is: \n", scalar);
            matrixScalarMultiply(matrixA, scalar, rowA, colA, file);

            break;

        case 2:
            //When Multiplying arrays of matrix-A column number has to be equal to matrix-B row number
            printf("\nEnter the #rows and #cols for matrix A: ");
            scanf("%d%d", &rowA, &colA);

            printf("Enter the #rows and #cols for matrix B: ");
            scanf("%d%d", &rowB, &colB);

            // Column of first matrix should be equal to rows of the second matrix and
            while (colA != rowB)
            {
                printf("\033[31m");
                printf("\n\nError! column of first matrix not equal to row of second.\n\n");
                printf("\033[0m");
                printf("\nEnter the #rows and #cols for matrix A: ");
                scanf("%d%d", &rowA, &colA);

                printf("Enter the #rows and #cols for matrix B: ");
                scanf("%d%d", &rowB, &colB);
            }

            // Storing elements of First matrix A.
            printf("\n\tEnter elements of Matrix A a %d x %d matrix.\n", rowA, colA); // with the %d we remember the user the dimentions of the array
            readMatrix(matrixA, rowA, colA);
            fprintf(file, "%s\n", buffer);
            printf("\n\t\tMatrix A\n\n");
            fprintf(file,"\n\t\tMatrix A\n\n");
            printMatrix(matrixA, rowA, colA, file);

            // Storing elements of Second matrix B.
            printf("\n\tEnter elements of Matrix B a %d x %d matrix.\n", rowB, colB); // with the %d we remember the user the dimentions of the array
            readMatrix(matrixB, rowB, colB);
            printf("\n\t\tMatrix B\n\n");
            fprintf(file, "\n\t\tMatrix B\n\n");
            printMatrix(matrixB, rowB, colB, file);

            //Multipling the matrix arrays.
            matrixMultiply(matrixA, matrixB, rowA, colA, colB, file);

            break;
        case 3:
            int d,i,j;
            float matrixA[10][10];
            printf("\nEnter the #rows and #cols for matrix A:\n ");
            scanf("%d%d", &rowA, &colA);
            while(rowA!=colA)
            {
                    printf("\033[31m");
                    printf("\n\tThe Input matrix should be 'n x n' matrix.\n");
                    printf("\033[0m");
                    printf("\nEnter the #rows and #cols for matrix A: ");
                    scanf("%d%d", &rowA, &colA);

            }
               printf("\n\tEnter elements of Matrix A a %d x %d matrix.\n", rowA, colA);
               for (i = 0;i < rowA; i++)

               {
                        for (j = 0;j < colA; j++)
                         {
                                scanf("%f", &matrixA[i][j]);
                         }
               }
               fprintf(file, "%s\n",buffer);
               fprintf(file, "\n\tMatrix A\t\n");
               printf("\n\tMatrix A\t\n");
               for (i = 0; i < rowA; i++)
                {
                        for (j = 0; j < colA; j++)
                                {
                                        printf("\t%f", matrixA[i][j]);
                                        fprintf(file,"\t%f",matrixA[i][j]);
                                }
                printf("\n");
                fprintf(file,"\n");
                }
               d = determinant(matrixA, rowA); // Calling the Determinant function
                if (d == 0){
                printf("\033[31m");
                printf("\n The Determinant of the input matrix is zero (0), therefore inverse does not exist.\n");
                printf("\033[0m");
                }
                else
                cofactor(matrixA, rowA, file); // If det not equal to zero , calling CoFactor function
            break;
        default:
                    printf("\033[31m");
                    printf("\nIncorrect option!. Please choose a number 1-3.");
                    printf("\033[0m");
            break;
        }

        fclose(file);
        printf("\n\nDo you want to calculate again?  ");
        printf("\033[32m");
        printf("Y");
        printf("\033[0m");
        printf(" or ");
        printf("\033[31m");
        printf("N\n");
        printf("\033[0m");
        scanf(" %c", &again);
        again = toupper(again); // Toupper is a user defined function which is used to convert lowercase alphabets to uppercase alphabets
        }
        printf("\033[32m");
        printf("\nThank You for using our matrix calculator. Have a nice day!!\n");
        printf("\033[0m");
        return 0;
        }


//User Defined Functions
void readMatrix(int array[10][10], int rows, int columns) // Function to read the matrix
{
    int i, j;
    for (i = 0; i < rows; i++) //Reads each element of the matrix
    {
        printf("\t%d Entries for row %d:\n", columns, i + 1);
        for (j = 0; j < columns; j++)
        {
            scanf("%d", &array[i][j]);
        }
    }

    return;
}

void printMatrix(int array[10][10], int rows, int columns, FILE *file)// Function to print the matrix
{
    int i, j;


    for (i = 0; i < rows; i++)  // Prints each element of the matrix
    {
        for (j = 0; j < columns; j++)
        {
            printf("\t%d", array[i][j]);
            fprintf(file,"\t%d", array[i][j]);
        }
        printf("\n");
        fprintf(file,"\n");
    }
    fprintf(file,"\n");
}



void matrixScalarMultiply(int array[10][10], int scalar, int rows, int columns, FILE *file)
{
    int i, j;
    int sca[10][10];
    fprintf(file,"\t\tScalar Matrix: \n");
    for (i = 0; i < rows; i++) // First acceses the matrix and multiplies each element of the matrix with the scalar and immediately printing.
    {
        for (j = 0; j < columns; j++)
        {
            sca[i][j] = scalar * array[i][j];
            printf("\t%d", sca[i][j]);
            fprintf(file,"\t%d",sca[i][j]);
        }
        printf("\n");
        fprintf(file,"\n");
    }
    fprintf(file,"\n");
    fprintf(file, "\n----------------------------------------------------------------------------------------------------------------------------------------------------------------------\n");

}

void matrixMultiply(int arrayone[10][10], int arraytwo[10][10], int rowsA, int columnsA,int columnsB, FILE *file) // Function used for matrix multiplication
{
    int i, j, k;
    int mul[10][10];

    // Initializing all elements of result matrix to 0
    for (i = 0; i<rowsA; i++)
    {
        for (j = 0; j<columnsB; j++)
        {
            mul[i][j] = 0;
        }
    }

    // Multiplying matrices A and B and
    // Storing the result in Resultant Matrix
    for (i = 0; i<rowsA; i++)
    {
        for (j = 0; j<columnsB; j++)
        {
            for (k = 0; k<columnsA; k++)
            {
                mul[i][j] += arrayone[i][k] * arraytwo[k][j];
            }
        }
    }
    printf("\nResultant Matrix:\n");
    fprintf(file,"\n\tResultant Matrix: \n");
    for (i = 0; i<rowsA; i++)
    {
        for (j = 0; j<columnsB; j++)
        {
            printf("\t%d ", mul[i][j]);
            fprintf(file,"\t%d",mul[i][j]);
            if (j == columnsB - 1)
            {printf("\n\n");
                fprintf(file,"\n\n");}
        }
    }
    fprintf(file,"\n");
    fprintf(file, "----------------------------------------------------------------------------------------------------------------------------------------------------------------------\n");
}
// Function for the calculation of determinant


float determinant(float arrayone[10][10], float k) // Function declaration where k is the order of the matrix
{
  float s = 1, det = 0, arraytwo[10][10];
  int i, j, m, n, c;
  if (k == 1)
    {
     return (arrayone[0][0]);
    }
  else
    {
     for (c = 0; c < k; c++)
       {
        m = 0;
        n = 0;
        for (i = 0;i < k; i++)
          {
            for (j = 0 ;j < k; j++)
              {
                arraytwo[i][j] = 0;
                if (i != 0 && j != c)
                 {
                   arraytwo[m][n] = arrayone[i][j];
                   if (n < (k - 2))
                    n++;
                   else
                    {
                     n = 0;
                     m++;
                     }
                 }
              }
           }
          det = det + s * (arrayone[0][c] * determinant(arraytwo, k - 1));
          s = -1 * s;
        }
     }

    return (det);
}

// Function for cofactor calculation

void cofactor(float num[10][10], float f, FILE *file) // Function declaration where f is order of the matrix
{
 float arraytwo[10][10], fac[10][10];
 int p, q, m, n, i, j;
 for (q = 0;q < f; q++)
 {
   for (p = 0;p < f; p++) // Assigning the elements of the array two as zero
    {
     m = 0;
     n = 0;
     for (i = 0;i < f; i++)
     {
       for (j = 0;j < f; j++)
        {
          if (i != q && j != p)
          {
            arraytwo[m][n] = num[i][j];
            if (n < (f - 2))
             n++;
            else
             {
               n = 0;
               m++;
               }
            }
        }
      }
      fac[q][p] = pow(-1, q + p) * determinant(arraytwo, f - 1); // Finding the cofactor matrix using determinant function under recurssion
    }
  }
  transpose(num, fac, f, file); // Calling transpose function
}


///function to find the transpose of a matrix and also used to print the inverse of the given matrix

void transpose(float num[10][10], float fac[10][10], float r, FILE *file)
{
  int i, j;
  float arraytwo[10][10], inverse[10][10], d; // Creating arrays for storing transpose of cofactor matrix and  inverse matrix

  for (i = 0;i < r; i++)
    {
     for (j = 0;j < r; j++)
       {
         arraytwo[i][j] = fac[j][i];
        }
    }

  d = determinant(num, r);
  for (i = 0;i < r; i++) // Inverse =( (cofactor matrix)^Transpose ) / determinant
    {
     for (j = 0;j < r; j++)
       {
        inverse[i][j] = arraytwo[i][j] / d;
        }
    }

   printf("\nThe Inverse of the matrix: \n"); // Printing the inverse of the matrix
   fprintf(file,"\nThe Inverse of the matrix: \n");
   for (i = 0;i < r; i++)
    {
     for (j = 0;j < r; j++)
       {
         printf("\t%f", inverse[i][j]);
         fprintf(file,"\t%f",inverse[i][j]);
        }
    printf("\n");
    fprintf(file,"\n");
    }
   fprintf(file,"\n");
   fprintf(file, "----------------------------------------------------------------------------------------------------------------------------------------------------------------------\n");
}


```
