# EX-NO-12-ELGAMAL-ALGORITHM

## AIM:
To Implement ELGAMAL ALGORITHM

## ALGORITHM:

1. ElGamal Algorithm is a public-key cryptosystem based on the Diffie-Hellman key exchange and relies on the difficulty of solving the discrete logarithm problem.

2. Initialization:
   - Select a large prime \( p \) and a primitive root \( g \) modulo \( p \) (these are public values).
   - The receiver chooses a private key \( x \) (a random integer), and computes the corresponding public key \( y = g^x \mod p \).

3. Key Generation:
   - The public key is \( (p, g, y) \), and the private key is \( x \).

4. Encryption:
   - The sender picks a random integer \( k \), computes \( c_1 = g^k \mod p \), and \( c_2 = m \times y^k \mod p \), where \( m \) is the message.
   - The ciphertext is the pair \( (c_1, c_2) \).

5. Decryption:
   - The receiver computes \( s = c_1^x \mod p \), and then calculates the plaintext message \( m = c_2 \times s^{-1} \mod p \), where \( s^{-1} \) is the modular inverse of \( s \).

6. Security: The security of the ElGamal algorithm relies on the difficulty of solving the discrete logarithm problem in a large prime field, making it secure for encryption.

## Program:
```
#include <stdio.h>
#include <math.h>

// Function to compute (base^exp) % mod
long long power(long long base, long long exp, long long mod)
{
    long long result = 1;
    base = base % mod;

    while (exp > 0)
    {
        if (exp % 2 == 1)
            result = (result * base) % mod;

        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}

// Function to find modular inverse using brute force
long long modInverse(long long a, long long m)
{
    for (long long x = 1; x < m; x++)
    {
        if ((a * x) % m == 1)
            return x;
    }
    return -1;
}

int main()
{
    long long p, g, x, y, k, m;
    long long c1, c2, s, s_inv, decrypted;

    printf("Enter prime number (p): ");
    scanf("%lld", &p);

    printf("Enter primitive root (g): ");
    scanf("%lld", &g);

    printf("Enter private key (x): ");
    scanf("%lld", &x);

    // Public key generation
    y = power(g, x, p);

    printf("\nPublic Key (p, g, y) = (%lld, %lld, %lld)\n", p, g, y);

    printf("\nEnter message to encrypt (m): ");
    scanf("%lld", &m);

    printf("Enter random integer (k): ");
    scanf("%lld", &k);

    // Encryption
    c1 = power(g, k, p);
    c2 = (m * power(y, k, p)) % p;

    printf("\nEncrypted message:");
    printf("\nc1 = %lld", c1);
    printf("\nc2 = %lld\n", c2);

    // Decryption
    s = power(c1, x, p);
    s_inv = modInverse(s, p);

    decrypted = (c2 * s_inv) % p;

    printf("\nDecrypted message = %lld\n", decrypted);

    return 0;
}
```

## Output:


## Result:
The program is executed successfully.
