## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER

 

## AIM:
 

 

To write a C program to implement the Playfair Substitution technique.

## DESCRIPTION:

The Playfair cipher starts with creating a key table. The key table is a 5×5 grid of letters that will act as the key for encrypting your plaintext. Each of the 25 letters must be unique and one letter of the alphabet is omitted from the table (as there are 25 spots and 26 letters in the alphabet).

To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. The two letters of the diagram are considered as the opposite corners of a rectangle in the key table. Note the relative position of the corners of this rectangle. Then apply the following 4 rules, in order, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair.
## EXAMPLE:
![image](https://github.com/Hemamanigandan/EX-NO-2-/assets/149653568/e6858d4f-b122-42ba-acdb-db18ec2e9675)

 

## ALGORITHM:

STEP-1: Read the plain text from the user.<br>
STEP-2: Read the keyword from the user.<br>
STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.<br>
STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.<br>
STEP-5: Display the obtained cipher text.<br>




## Program:
```

#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main()
{
    char key[100], text[100], table[25];
    int i, j, k = 0, a, b, r1, c1, r2, c2;
    int used[26] = {0};

    printf("Enter the key: ");
    scanf("%s", key);

    printf("Enter the plaintext: ");
    scanf("%s", text);

    used['J' - 'A'] = 1;

    for(i = 0; key[i] != '\0'; i++)
    {
        char ch = toupper(key[i]);

        if(ch == 'J')
            ch = 'I';

        if(ch >= 'A' && ch <= 'Z' && !used[ch - 'A'])
        {
            table[k++] = ch;
            used[ch - 'A'] = 1;
        }
    }

    for(i = 0; i < 26; i++)
    {
        if(!used[i])
            table[k++] = 'A' + i;
    }

    printf("\nKey Matrix:\n");

    for(i = 0; i < 25; i++)
    {
        printf("%c ", table[i]);

        if(i % 5 == 4)
            printf("\n");
    }

    for(i = 0; text[i] != '\0'; i++)
        text[i] = toupper(text[i]);

    printf("\nCipher Text: ");

    for(i = 0; text[i] != '\0'; i += 2)
    {
        a = text[i] - 'A';

        if(text[i + 1] == '\0')
            b = 'X' - 'A';
        else
            b = toupper(text[i + 1]) - 'A';

        if(text[i] == 'J')
            a = 'I' - 'A';

        if(text[i + 1] == 'J')
            b = 'I' - 'A';

        for(j = 0; j < 25; j++)
        {
            if(table[j] == 'A' + a)
            {
                r1 = j / 5;
                c1 = j % 5;
            }

            if(table[j] == 'A' + b)
            {
                r2 = j / 5;
                c2 = j % 5;
            }
        }

        if(r1 == r2)
        {
            printf("%c%c",
                   table[r1 * 5 + (c1 + 1) % 5],
                   table[r2 * 5 + (c2 + 1) % 5]);
        }
        else if(c1 == c2)
        {
            printf("%c%c",
                   table[((r1 + 1) % 5) * 5 + c1],
                   table[((r2 + 1) % 5) * 5 + c2]);
        }
        else
        {
            printf("%c%c",table[r1 * 5 + c2],table[r2 * 5 + c1]);
        }
    }

    return 0;
}


```


## Output:

<img width="627" height="377" alt="Screenshot 2026-10-29 110859" src="https://github.com/user-attachments/assets/a6a142e5-6f1a-4126-8312-75fe2da078e6" />

## Result:  
Thus the implementation of  Playfair Cipher had been executed successfully.
