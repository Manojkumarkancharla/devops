# devops
programme
#include <stdio.h>
#include <stdlib.h>

#define SIZE 2

// Function to find the modular inverse of a number
int modInverse(int a, int m) {
    a = a % m;
    for (int x = 1; x < m; x++) {
        if ((a * x) % m == 1) return x;
    }
    return -1; // If no modular inverse exists
}

// Function to find the determinant of the matrix
int determinant(int matrix[SIZE][SIZE]) {
    return (matrix[0][0] * matrix[1][1] - matrix[0][1] * matrix[1][0]) % 26;
}

// Function to encrypt the plaintext
void encrypt(char *plaintext, int key[SIZE][SIZE]) {
    int len = strlen(plaintext);
    for (int i = 0; i < len; i += SIZE) {
        int vector[SIZE] = {0};
        for (int j = 0; j < SIZE; j++) {
            if (i + j < len) {
                vector[j] = plaintext[i + j] - 'A';
            }
        }
        int cipher[SIZE] = {0};
        for (int j = 0; j < SIZE; j++) {
            for (int k = 0; k < SIZE; k++) {
                cipher[j] += key[j][k] * vector[k];
            }
            cipher[j] = (cipher[j] % 26 + 26) % 26; // Ensures positive value
            printf("%c", cipher[j] + 'A');
        }
    }
    printf("\n");
}

int main() {
    int key[SIZE][SIZE] = {{6, 24}, {1, 13}}; // Example key matrix
    char plaintext[] = "HELLO";

    printf("Ciphertext: ");
    encrypt(plaintext, key);

    return 0;
}
