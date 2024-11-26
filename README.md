# EX-NO-9-RSA-Algorithm

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:


Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Convert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: **Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:
```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int gcd(int a, int b) { return b == 0 ? a : gcd(b, a % b); }

long long mod_exp(long long base, long long exp, long long mod) {
    long long result = 1;
    while (exp) {
        if (exp % 2) result = (result * base) % mod;
        base = (base * base) % mod;
        exp /= 2;
    }
    return result;
}

int mod_inverse(int e, int phi) {
    int t = 0, newt = 1, r = phi, newr = e;
    while (newr) {
        int q = r / newr;
        int temp = t;
        t = newt;
        newt = temp - q * newt;
        temp = r;
        r = newr;
        newr = temp - q * newr;
    }
    return r > 1 ? -1 : (t < 0 ? t + phi : t);
}

int main() {
    int p = 61, q = 53, n = p * q, phi = (p - 1) * (q - 1), e = 17, d;
    if (gcd(e, phi) != 1 || (d = mod_inverse(e, phi)) == -1) return -1;

    printf("Public Key: (e = %d, n = %d)\nPrivate Key: (d = %d, n = %d)\n", e, n, d, n);

    char message[100];
    printf("Enter a message: ");
    fgets(message, sizeof(message), stdin);
    int len = strlen(message);
    if (message[len - 1] == '\n') message[--len] = '\0';

    long long encrypted[100];
    printf("Encrypted Message:\n");
    for (int i = 0; i < len; i++) {
        encrypted[i] = mod_exp((int)message[i], e, n);
        printf("%lld ", encrypted[i]);
    }
    printf("\nDecrypted Message:\n");
    for (int i = 0; i < len; i++) 
        printf("%c", (char)mod_exp(encrypted[i], d, n));
    printf("\n");
    return 0;
}

```



## Output:



## Result:
 The program is executed successfully.
