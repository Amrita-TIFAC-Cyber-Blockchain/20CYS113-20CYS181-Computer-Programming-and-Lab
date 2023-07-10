# 20CYS113 - Computer-Programming and 20CYS181 - Computer Programming Lab 
![](https://img.shields.io/badge/Batch-22CYS-lightgreen) ![](https://img.shields.io/badge/UG-blue) ![](https://img.shields.io/badge/Subject-CP-blue)
![](https://img.shields.io/badge/-HPOJ-brown)  <br/>

## Escape Sequences in C

Escape sequences in C are particular character combinations used to represent specific characters or control characters within a string or character constant. 
They are denoted by a backslash (\) followed by a specific character or sequence.

Some commonly used escape sequences in C:

 - \n - *Newline:* Moves the cursor to the beginning of the next line. 
 - \r - *Carriage Return:* Moves the cursor to the beginning of the current line. 
 - \t - *Horizontal Tab:* Moves the cursor to the next horizontal tab stop. 
 - \\ - *Backslash:* Represents a literal backslash character.
 - \" - *Double Quote:* Represents a literal double quote character. 
 - \' - *Single Quote:* Represents a literal single quote character. 
 - \b - *Backspace*: Moves the cursor back one position within the same line.
 - \f - *Form Feed:* Moves the cursor to the next logical page. 
 - \v - *Vertical Tab:* Moves the cursor to the next vertical tab stop. 
 - \a - *Alert (Bell):* Produces an audible or visible alert.

Additionally, there are a few numeric escape sequences that represent characters using their ASCII or Unicode values:

 - \xHH - *Hexadecimal Escape Sequence:* Represents a character using its hexadecimal ASCII or Unicode value.
 - \ooo - *Octal Escape Sequence:* Represents a character using its octal ASCII value.

It's important to note that the behavior of escape sequences may vary depending on the context in which they are used, such as in strings, character constants, or output functions like printf().

Escape sequences are useful for representing special characters, controlling formatting, and inserting non-printable characters within C strings or character constants.


## Example Code

```
#include <stdio.h>

int main() {
    
    // Using \x (Hexa) and \"
    char ch = '\x41'; // ASCII value for 'A'
    printf("English Alphabet starts at: \"%c\"\n", ch);
    
    // Using \t and \n 
    printf("\nName \tAge \nRama \t33 \nAmmu \t29 \n");

    // Using \0
    printf("\nWhen I am visible \0, he wont be visble \n");
    
    // Using \yyy (Octal)
    printf("\nOur Class Strength in Octal is: \110\n");
    
    //Using \b 
    printf("\nRama\b");
    return 0;

}
```

Posted on: 15th June, 2023 in [HPOJ](https://hpoj.cb.amrita.edu:8000/problem/20cys181pract7).
