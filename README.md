## AIM:
To encrypt and decrypt a given message using the RSA (Rivest-Shamir-Adleman) algorithm.
## ALGORITHM:
1.Design the RSA algorithm.
2.Implement the RSA algorithm using C or Python.
3.The RSA algorithm involves two keys: a public key for encryption and a private key for decryption. The keys are generated based on two large prime numbers. The encryption process uses the public key to convert plaintext into ciphertext, and decryption uses the private key to retrieve the original message.
## PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <math.h>

int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int modExp(int base, int exp, int mod) {
    int result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1) {
            result = (result * base) % mod;
        }
        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}

int modInverse(int a, int m) {
    int m0 = m, t, q;
    int x0 = 0, x1 = 1;
    
    if (m == 1)
        return 0;

    while (a > 1) {
        q = a / m;
        t = m;
        m = a % m;
        a = t;
        t = x0;
        x0 = x1 - q * x0;
        x1 = t;
    }

    if (x1 < 0)
        x1 += m0;

    return x1;
}

int main() {
    int p = 61, q = 53;  
    int n = p * q;     
    int phi = (p - 1) * (q - 1); 
    int e = 17;        
    while (gcd(e, phi) != 1) {
        e++;
    }
    
    int d = modInverse(e, phi); 
    
    char plaintext[100];
    printf("Enter the plaintext: ");
    scanf("%s", plaintext);
    
    int encryptedMessage[100];
    int decryptedMessage[100];
  
    printf("Encrypted Message: ");
    for (int i = 0; i < strlen(plaintext); i++) {
        encryptedMessage[i] = modExp(plaintext[i], e, n);
        printf("%d ", encryptedMessage[i]);
    }
    printf("\n");
  
    printf("Decrypted Message: ");
    for (int i = 0; i < strlen(plaintext); i++) {
        decryptedMessage[i] = modExp(encryptedMessage[i], d, n);
        printf("%c", (char)decryptedMessage[i]);
    }
    printf("\n");
    
    return 0;
}

```
## OUTPUT:
 ![image](https://github.com/user-attachments/assets/49ac02ec-1562-4524-a8f8-966d8634b943)


## RESULT:
The program for the RSA algorithm is executed successfully.


