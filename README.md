# C960 WGU C960 Discrete Math II
## RSA Encryption
### Step 1: Key Generation

1. **Choose two distinct prime numbers**: 
   - Let $p$ and $q$ be two large prime numbers. These primes are kept secret.
   
2. **Compute their product**:
   - $n = p \cdot q$
   - $n$ is the modulus for both the public and private keys.

3. **Calculate the totient (Euler's totient function)**:
   - $\phi(n) = (p - 1)(q - 1)$
   - This value, $\phi(n)$, is used to determine the public and private keys.

4. **Choose an encryption exponent**:
   - Select an integer $e$ such that $1 < e < \phi(n)$ and $\gcd(e, \phi(n)) = 1$.
   - $e$ is the public key exponent. It is chosen such that it is relatively prime to $\phi(n)$.

5. **Determine the decryption exponent**:
   - Compute $d$ as the modular multiplicative inverse of $e$ modulo $\phi(n)$.
   - $d$ satisfies the equation: $d \cdot e \equiv 1 \pmod{\phi(n)}$
   - The value $d$ is the private key exponent.

6. **Public and Private Keys**:
   - The **public key** is $(e, n)$.
   - The **private key** is $(d, n)$.

### Step 2: Encryption

1. **Convert the plaintext message into an integer**:
   - Let the plaintext be represented as an integer $m$ such that $0 \leq m < n$.

2. **Compute the ciphertext**:
   - The ciphertext $c$ is computed using the public key $(e, n)$:
   - $c \equiv m^e \pmod{n}$

### Step 3: Decryption

1. **Compute the plaintext from the ciphertext**:
   - Using the private key $(d, n)$, the plaintext $m$ is recovered from the ciphertext $c$:
   - $m \equiv c^d \pmod{n}$

### Example

Let's go through a small numerical example with small primes (in practice, much larger primes are used).

1. **Choose primes**:
   - $p = 61$, $q = 53$

2. **Compute $n$**:
   - $n = p \cdot q = 61 \cdot 53 = 3233$

3. **Calculate $\phi(n)$**:
   - $\phi(n) = (p-1)(q-1) = 60 \cdot 52 = 3120$

4. **Choose $e$**:
   - Let $e = 17$ (17 is a common choice; it is relatively prime to 3120)

5. **Compute $d$**:
   - We need $d$ such that $d \cdot e \equiv 1 \pmod{3120}$
   - The modular inverse of $17$ modulo $3120$ is $d = 2753$

6. **Public and private keys**:
   - Public key: $(e, n) = (17, 3233)$
   - Private key: $(d, n) = (2753, 3233)$

7. **Encryption**:
   - Suppose we want to encrypt the message $m = 65$.
   - Compute the ciphertext: $c \equiv 65^{17} \pmod{3233} = 2790$

8. **Decryption**:
   - To decrypt the ciphertext $c = 2790$, compute: $m \equiv 2790^{2753} \pmod{3233} = 65$

Thus, the original message $m = 65$ is recovered.

### Summary

RSA encryption involves choosing two large prime numbers, computing a modulus, and generating a public/private key pair. Encryption is performed using the public key, and decryption is done with the private key. The security of RSA relies on the difficulty of factoring the product of two large prime numbers.
