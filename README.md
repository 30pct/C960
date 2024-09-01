# C960 WGU C960 Discrete Math II
# 2.Number Theory & Cryptography
## RSA Encryption

**Step 1: Key Generation**
1. **Choose two distinct prime numbers**:  
   - Let $p = 61$ and $q = 53$. These are two large prime numbers.
   - **Example**: We select $p = 61$ and $q = 53$.

2. **Compute their product**:  
   - $n = p \cdot q$
   - **Example**: $n = 61 \cdot 53 = 3233$

3. **Calculate the totient (Euler's totient function)**:  
   - $\phi(n) = (p - 1)(q - 1)$
   - **Example**: $\phi(n) = (61 - 1)(53 - 1) = 60 \cdot 52 = 3120$

4. **Choose an encryption exponent**:  
   - Select an integer $e$ such that $1 < e < \phi(n)$ and $\gcd(e, \phi(n)) = 1$.
   - **Example**: Choose $e = 17$ (17 is a common choice as it is relatively prime to $3120$).

5. **Determine the decryption exponent**:  
   - Compute $d$ as the modular multiplicative inverse of $e$ modulo $\phi(n)$.
   - $d \cdot e \equiv 1 \pmod{\phi(n)}$
   - **Example**: Calculate $d$ such that $d \cdot 17 \equiv 1 \pmod{3120}$. The result is $d = 2753$.

6. **Public and Private Keys**:  
   - The **public key** is $(e, n)$.
   - The **private key** is $(d, n)$.
   - **Example**: Public key is $(17, 3233)$, and private key is $(2753, 3233)$.

**Step 2: Encryption**

1. **Convert the plaintext message into an integer**:  
   - Let the plaintext be represented as an integer $m$ such that $0 \leq m < n$.
   - **Example**: Suppose we want to encrypt the message $m = 65$.

2. **Compute the ciphertext**:  
   - The ciphertext $c$ is computed using the public key $(e, n)$:
   - $c \equiv m^e \pmod{n}$
   - **Example**: Compute $c \equiv 65^{17} \pmod{3233}$.  
     To simplify:  
     $65^{17} \pmod{3233} = 2790$  
   - So, the ciphertext $c = 2790$.

**Step 3: Decryption**

1. **Compute the plaintext from the ciphertext**:  
   - Using the private key $(d, n)$, the plaintext $m$ is recovered from the ciphertext $c$:
   - $m \equiv c^d \pmod{n}$
   - **Example**: Compute $m \equiv 2790^{2753} \pmod{3233}$.  
     To simplify:  
     $2790^{2753} \pmod{3233} = 65$  
   - The original message $m = 65$ is recovered.
