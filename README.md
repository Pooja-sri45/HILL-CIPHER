# HILL CIPHER
# NAME:POOJASRI L
# REG.NO:212223220076
 
## To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <ctype.h>
#define SIZE 2
int keyMatrix[SIZE][SIZE] = {{3, 3}, {2, 5}};
int modInverse(int a, int m) {
a = a % m;
for (int x = 1; x < m; x++)
if ((a * x) % m == 1)
return x;
return -1;
}
int determinant(int matrix[SIZE][SIZE]) {
return (matrix[0][0] * matrix[1][1] - matrix[0][1] * matrix[1][0]) % 26;
}
void inverseMatrix(int matrix[SIZE][SIZE], int invMatrix[SIZE][SIZE]) {
int det = determinant(matrix);
if (det < 0) det += 26;
int detInv = modInverse(det, 26);
if (detInv == -1) {
printf("Inverse does not exist!\n");
exit(0);
}
invMatrix[0][0] = matrix[1][1] * detInv % 26;
invMatrix[0][1] = -matrix[0][1] * detInv % 26;
invMatrix[1][0] = -matrix[1][0] * detInv % 26;
invMatrix[1][1] = matrix[0][0] * detInv % 26;
for (int i = 0; i < SIZE; i++)
for (int j = 0; j < SIZE; j++)
if (invMatrix[i][j] < 0)
invMatrix[i][j] += 26;
}
void matrixMultiply(int matrix[SIZE][SIZE], int message[], int result[]) {
for (int i = 0; i < SIZE; i++) {
result[i] = 0;
for (int j = 0; j < SIZE; j++)
result[i] += matrix[i][j] * message[j];
result[i] %= 26;
}
}
void encryptMessage(char message[], char encrypted[]) {
int messageVector[SIZE], cipherVector[SIZE];
int len = strlen(message);
if (len % SIZE != 0) {
strcat(message, "X");
len++;
}
for (int i = 0; i < len; i += SIZE) {
for (int j = 0; j < SIZE; j++)
messageVector[j] = toupper(message[i + j]) - 'A';
matrixMultiply(keyMatrix, messageVector, cipherVector);
for (int j = 0; j < SIZE; j++)
encrypted[i + j] = cipherVector[j] + 'A';
}
encrypted[len] = '\0';
}
void decryptMessage(char encrypted[], char decrypted[]) {
int invKeyMatrix[SIZE][SIZE];
inverseMatrix(keyMatrix, invKeyMatrix);
int cipherVector[SIZE], messageVector[SIZE];
int len = strlen(encrypted);
for (int i = 0; i < len; i += SIZE) {
for (int j = 0; j < SIZE; j++)
cipherVector[j] = encrypted[i + j] - 'A';
matrixMultiply(invKeyMatrix, cipherVector, messageVector);
for (int j = 0; j < SIZE; j++)
decrypted[i + j] = messageVector[j] + 'A';
}
decrypted[len] = '\0';
}
int main() {
char message[100] = "POOJASRI";
char encrypted[100], decrypted[100];
encryptMessage(message, encrypted);
printf("Encrypted Message: %s\n", encrypted);
decryptMessage(encrypted, decrypted);
printf("Decrypted Message: %s\n", decrypted);
return 0;

```

## OUTPUT
![image](https://github.com/user-attachments/assets/bf9ebeae-7da7-462d-aeb3-a9a8920bd8bf)


## RESULT
The program is executed successfully
