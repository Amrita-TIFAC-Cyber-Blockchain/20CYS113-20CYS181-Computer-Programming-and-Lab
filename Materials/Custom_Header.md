# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/CP-20CYS113-blue)  ![](https://img.shields.io/badge/CPL-20CYS181-blue)
![](https://img.shields.io/badge/-HPOJ-brown) <br/>

## Own Header File

Download ```rebind.h``` from [here](Materials/rebind.zip)

```
#include<stdio.h>
#include"rebind.h"

int main() {
	
	ram clsstrngth = CLASS_STRENGTH; // ram is integer here
	guru classname[10] = "re-bin-d"; // guru is character here
	printf("Our Class Strength: %d\n", clsstrngth);
	printf("The example for typedef is %d\n", clsstrngth);
	
	printf("Roll Number of Class Representatives are: %d, %d, %d, %d\n", KOLLURU_SAI_SUPRAJ, N_MEERA, RAMRAJ_S, LALITHA_K);
	
	printf("Average Grade for Computer Programming should be %c\n", GRADE(85));
	
	ram sem;
	printf("Enter the Semester to know the representatives:");
	scanf("%d",&sem);
	get_representatives(sem);
	return 0;
	
}
```
