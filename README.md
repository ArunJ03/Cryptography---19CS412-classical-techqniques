# Cryptography---19CS412-classical-techqniques


# Caeser Cipher
Caeser Cipher using with different key values

# AIM:

To develop a simple C program to implement Caeser Cipher.

## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:

#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main() {
    char plain[10], cipher[10];
    int key, i, length;

    printf("\n Enter the plain text:");
    scanf("%s", plain);
    printf("\n Enter the key value:");
    scanf("%d", &key);

    printf("\n \n \t PLAIN TEXT: %s", plain);
    printf("\n \n \t ENCRYPTED TEXT: ");
    
    length = strlen(plain);
    
    for (i = 0; i < length; i++) {
        cipher[i] = plain[i] + key;
        
        if (isupper(plain[i]) && (cipher[i] > 'Z'))
            cipher[i] = cipher[i] - 26;
            
        if (islower(plain[i]) && (cipher[i] > 'z'))
            cipher[i] = cipher[i] - 26;
            
        printf("%c", cipher[i]);
    }
    
    printf("\n \n \t AFTER DECRYPTION : ");
    
    for (i = 0; i < length; i++) {
        plain[i] = cipher[i] - key;
        
        if (isupper(cipher[i]) && (plain[i] < 'A'))
            plain[i] = plain[i] + 26;
            
        if (islower(cipher[i]) && (plain[i] < 'a'))
            plain[i] = plain[i] + 26;
            
        printf("%c", plain[i]);
    }
    
    return 0;
}


## OUTPUT:

 ![Screenshot 2024-03-16 200207](https://github.com/ArunJ03/Cryptography---19CS412-classical-techqniques/assets/131673036/2d694abd-b5ab-44e9-a6e3-473ed4dcbeba)


## RESULT:
The program is executed successfully

---------------------------------

# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To develop a simple C program to implement PlayFair Cipher.

## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:

#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define MX 5

void playfair(char ch1, char ch2, char key[MX][MX]) {
    int i, j, w, x, y, z;
    FILE *out;

    if ((out = fopen("cipher.txt", "a+")) == NULL) {
        printf("Error: Unable to open file.\n");
        return;
    }

    for (i = 0; i < MX; i++) {
        for (j = 0; j < MX; j++) {
            if (ch1 == key[i][j]) {
                w = i;
                x = j;
            } else if (ch2 == key[i][j]) {
                y = i;
                z = j;
            }
        }
    }

    if (w == y) {
        x = (x + 1) % MX;
        z = (z + 1) % MX;
        printf("%c%c ", key[w][x], key[y][z]);
        fprintf(out, "%c%c ", key[w][x], key[y][z]);
    } else if (x == z) {
        w = (w + 1) % MX;
        y = (y + 1) % MX;
        printf("%c%c ", key[w][x], key[y][z]);
        fprintf(out, "%c%c ", key[w][x], key[y][z]);
    } else {
        printf("%c%c ", key[w][z], key[y][x]);
        fprintf(out, "%c%c ", key[w][z], key[y][x]);
    }

    fclose(out);
}

int main() {
    int i, j, k = 0, l, m = 0, n;
    char key[MX][MX], keyminus[25], keystr[10], str[25] = {0};
    char alpa[26] = "ABCDEFGHIKLMNOPQRSTUVWXYZ"; // 'J' is omitted as per Playfair cipher
    printf("\nEnter key: ");
    fgets(keystr, sizeof(keystr), stdin);
    keystr[strcspn(keystr, "\n")] = '\0'; // Removing newline character
    printf("\nEnter the plain text: ");
    fgets(str, sizeof(str), stdin);
    str[strcspn(str, "\n")] = '\0'; // Removing newline character
    n = strlen(keystr);

    for (i = 0; i < n; i++) {
        if (keystr[i] == 'j' || keystr[i] == 'J') {
            keystr[i] = 'I';
        }
        keystr[i] = toupper(keystr[i]);
    }

    for (i = 0; i < strlen(str); i++) {
        if (str[i] == 'j' || str[i] == 'J') {
            str[i] = 'I';
        }
        str[i] = toupper(str[i]);
    }

    j = 0;

    for (i = 0; i < 26; i++) {
        for (k = 0; k < n; k++) {
            if (keystr[k] == alpa[i]) {
                break;
            } else if (alpa[i] == 'J') {
                break;
            }
        }
        if (k == n) {
            keyminus[j] = alpa[i];
            j++;
        }
    }

    k = 0;

    for (i = 0; i < MX; i++) {
        for (j = 0; j < MX; j++) {
            if (k < n) {
                key[i][j] = keystr[k];
                k++;
            } else {
                key[i][j] = keyminus[m];
                m++;
            }
            printf("%c ", key[i][j]);
        }
        printf("\n");
    }

    printf("\n\nEntered text: %s\nCipher Text: ", str);

    for (i = 0; i < strlen(str); i++) {
        if (str[i + 1] == '\0') {
            playfair(str[i], 'X', key);
        } else {
            if (str[i] == str[i + 1]) {
                playfair(str[i], 'X', key);
                i++;
            } else {
                playfair(str[i], str[i + 1], key);
                i++;
            }
        }
    }
    return 0;
}

## OUTPUT:
![Screenshot 2024-03-16 200532](https://github.com/ArunJ03/Cryptography---19CS412-classical-techqniques/assets/131673036/1aa357a4-4091-4568-9b8f-a166a86f5383)


## RESULT:
The program is executed successfully


---------------------------

# Hill Cipher
Hill Cipher using with different key values

# AIM:

To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

### Step 1:

Design of Hill Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
#include<stdio.h>
#include<math.h>
 
float encrypt[3][1], decrypt[3][1], a[3][3], b[3][3], mes[3][1], c[3][3];
 
void encryption();	//encrypts the message
void decryption();	//decrypts the message
void getKeyMessage();	//gets key and message from user
void inverse();		//finds inverse of key matrix
 
void main() {
	getKeyMessage();
	encryption();
	decryption();
}
 
void encryption() {
	int i, j, k;
	
	for(i = 0; i < 3; i++)
		for(j = 0; j < 1; j++)
			for(k = 0; k < 3; k++)
				encrypt[i][j] = encrypt[i][j] + a[i][k] * mes[k][j];
	
	printf("\nEncrypted string is: ");
	for(i = 0; i < 3; i++)
		printf("%c", (char)(fmod(encrypt[i][0], 26) + 97));
 
}
 
void decryption() {
	int i, j, k;
	
	inverse();
	
	for(i = 0; i < 3; i++)
		for(j = 0; j < 1; j++)
			for(k = 0; k < 3; k++)
				decrypt[i][j] = decrypt[i][j] + b[i][k] * encrypt[k][j];
	
	printf("\nDecrypted string is: ");
	for(i = 0; i < 3; i++)
		printf("%c", (char)(fmod(decrypt[i][0], 26) + 97));
	
	printf("\n");
}
 
void getKeyMessage() {
	int i, j;
	char msg[3];
 
	printf("Enter 3x3 matrix for key (It should be inversible):\n");
	
	for(i = 0; i < 3; i++)
		for(j = 0; j < 3; j++) {
			scanf("%f", &a[i][j]);
			c[i][j] = a[i][j];
		}
	
	printf("\nEnter a 3 letter string: ");
	scanf("%s", msg);
	
	for(i = 0; i < 3; i++)
		mes[i][0] = msg[i] - 97;
}
 
void inverse() {
	int i, j, k;
	float p, q;
	
	for(i = 0; i < 3; i++)
		for(j = 0; j < 3; j++) {
			if(i == j)
				b[i][j]=1;
			else
				b[i][j]=0;
		}
		
	for(k = 0; k < 3; k++) {
		for(i = 0; i < 3; i++) {
			p = c[i][k];
			q = c[k][k];
				
			for(j = 0; j < 3; j++) {
				if(i != k) {
					c[i][j] = c[i][j]*q - p*c[k][j];
					b[i][j] = b[i][j]*q - p*b[k][j];
				}
			}
		}
	}
	
	for(i = 0; i < 3; i++)
		for(j = 0; j < 3; j++)
			b[i][j] = b[i][j] / c[i][i];
	
	printf("\n\nInverse Matrix is:\n");
	for(i = 0; i < 3; i++) {
		for(j = 0; j < 3; j++)
			printf("%d ", b[i][j]);
		
		printf("\n");
	}
}

## OUTPUT:

![Screenshot 2024-03-16 204718](https://github.com/ArunJ03/Cryptography---19CS412-classical-techqniques/assets/131673036/ae3f81f2-843b-4f62-bcf5-4c64caf40d33)



## RESULT:
The program is executed successfully

-------------------------------------------------

# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:

To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:

### Step 1:

Design of Vigenere Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:

#include <stdio.h>  
#include <ctype.h>  
#include <string.h>  
#include <stdlib.h>  
  
void encrypt() {  
    char plaintext[128];  
    char key[16];  
    printf("\nEnter the plaintext (up to 128 characters): ");  
    scanf(" %[^\n]", plaintext); // Read input with spaces  
    printf("Enter the key (up to 16 characters): ");  
    scanf(" %[^\n]", key);  
  
    printf("Cipher Text: ");  
    for (int i = 0, j = 0; i < strlen(plaintext); i++, j++) {  
        if (j >= strlen(key)) {  
            j = 0;  
        }  
        int shift = toupper(key[j]) - 'A';  
        char encryptedChar = ((toupper(plaintext[i]) - 'A' + shift) % 26) + 'A';  
        printf("%c", encryptedChar);  
    }  
    printf("\n");  
}  
  
void decrypt() {  
    char ciphertext[128];  
    char key[16];  
    printf("\nEnter the ciphertext: ");  
    scanf(" %[^\n]", ciphertext);  
    printf("Enter the key: ");  
    scanf(" %[^\n]", key);  
  
    printf("Deciphered Text: ");  
    for (int i = 0, j = 0; i < strlen(ciphertext); i++, j++) {  
        if (j >= strlen(key)) {  
            j = 0;  
        }  
        int shift = toupper(key[j]) - 'A';  
        char decryptedChar = ((toupper(ciphertext[i]) - 'A' - shift + 26) % 26) + 'A';  
        printf("%c", decryptedChar);  
    }  
    printf("\n");  
}  
  
int main() {  
    int option;  
    while (1) {  
        printf("\n1. Encrypt");  
        printf("\n2. Decrypt");  
        printf("\n3. Exit\n");  
        printf("\nEnter your option: ");  
        scanf("%d", &option);  
  
        switch (option) {  
            case 1:  
                encrypt();  
                break;  
            case 2:  
                decrypt();  
                break;  
            case 3:  
                exit(0);  
            default:  
                printf("\nInvalid selection! Try again.\n");  
                break;  
        }  
    }  
    return 0;  
}  

## OUTPUT:

![Screenshot 2024-03-16 201413](https://github.com/ArunJ03/Cryptography---19CS412-classical-techqniques/assets/131673036/fafc9d0e-3a6b-460e-8bf7-4a67b9af26e4)


## RESULT:
The program is executed successfully

-----------------------------------------------------------------------

# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
#include<stdio.h>
#incl#include<stdio.h>
#include<conio.h>
#include<string.h>

int main() {
    int i, j, k, l;
    char a[20], c[20], d[20];
    
    printf("\n\t\t RAIL FENCE TECHNIQUE");
    printf("\n\nEnter the input string : ");
    scanf("%[^\n]%*c", a);
    l = strlen(a);
    
    /* Ciphering */
    for(i = 0, j = 0; i < l; i++) {
        if(i % 2 == 0)
            c[j++] = a[i];
    }
    for(i = 0; i < l; i++) {
        if(i % 2 == 1)
            c[j++] = a[i];
    }
    c[j] = '\0';
    
    printf("\nCipher text after applying rail fence :");
    printf("\n%s", c);
    
    /* Deciphering */
    if(l % 2 == 0)
        k = l / 2;
    else
        k = (l / 2) + 1;
    for(i = 0, j = 0; i < k; i++) {
        d[j] = c[i];
        j = j + 2;
    }
    for(i = k, j = 1; i < l; i++) {
        d[j] = c[i];
        j = j + 2;
    }
    d[l] = '\0';
    
    printf("\nText after decryption : ");
    printf("%s", d);
    
    return 0;
}



## OUTPUT:

![Screenshot 2024-03-16 201505](https://github.com/ArunJ03/Cryptography---19CS412-classical-techqniques/assets/131673036/fe46723d-3936-4c98-a87a-e2075c99e811)


## RESULT:
The program is executed successfully
